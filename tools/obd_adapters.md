# OBD Adapters and Bus Access

Which adapter you use determines which half of the car you can talk to. See [the module overview](/systems/modules/ford_module_overview.md) for why: the modules are split across HS-CAN (pins 6/14) and MS-CAN (pins 3/11).

## Adapter Capabilities

| Adapter type                     | HS-CAN | MS-CAN | Notes                                             |
| -------------------------------- | ------ | ------ | ------------------------------------------------- |
| Cheap ELM327 clones ("v1.5")     | Yes    | **No** | Hardwired to pins 6/14; ELM327 firmware has no 125 kbps CAN setting |
| STN-based (OBDLink EX/MX+, vLinker FS) | Yes | Yes | Hardware pin switching + arbitrary CAN baud rates  |

The ELM327 v1.5 protocol table tops out at the fixed legislated OBD speeds — there is no 125 kbps option, so even physically jumpering a clone onto pins 3/11 would not get it onto Ford MS-CAN. This is why [FORScan recommends switch-capable adapters](./forscan/README.md), and why a clone-only owner will never see MS-CAN modules (IPC, HVAC, RFA, door modules, and the TCUs all live there).

## The STP Trick for MS-CAN on STN Chips

On STN-based adapters (STN1170-era: vLinker FS, OBDLink SX/MX family), MS-CAN is a documented built-in protocol selected with the STN proprietary `STP` command, not the ELM-style `ATSP`:

```
STP53        -> OK        (ISO 15765, 11-bit Tx, 125 kbps, MS-CAN transceiver, pins 3/11)
ATDPN        -> 53 [ST]   (confirms the switch)
ATSP6        -> OK        (back to HS-CAN, 500 kbps 11-bit)
```

Note that `ATSP 53` / `ATSP53` is _rejected_ with `?` on these firmwares — the extended protocol codes only work through `STP`. The protocol table from the [STN1100/STN1170 reference manual](https://www.scantool.net/scantool/downloads/682/obdlink_frpm_f.pdf) includes:

| Code | Protocol                                       |
| ---- | ---------------------------------------------- |
| 6    | CAN 500 kbps, 11-bit (HS-CAN, ELM-standard)    |
| 51-54| MS-CAN variants, 125 kbps, 11/29-bit, var DLC/DLC=8 |
| 31-36| SW-CAN / other speeds (GM single-wire etc.)     |

With `ATH1` (headers on), `ATCAF1` (ISO-TP auto formatting) and `ATCFC1` (flow control), UDS request/response works cleanly: send the request to the module's AsBuilt code (e.g. `ATSH754` + `3E00` for the TCU) and the reply comes from request ID + 8 with the ISO-TP framing already handled.

## Notes for Scripting Adapters Directly

Findings from driving these adapters without FORScan:

* **Bluetooth clones are classic SPP serial devices.** Modern BlueZ refuses them through the normal pairing/connect path (`br-connection-profile-unavailable`) because it has no SPP client profile. On Linux you can skip all of that: open a raw RFCOMM socket directly to the adapter's MAC on channel 1 — no pairing required — and speak AT commands over it. They accept connections unconditionally. Some clones only advertise as discoverable for a while after power-up, but remain connectable.
* **Cheap clones drop frames under load.** A module not answering a single query means nothing — retry before concluding a module is absent. Vehicle in RUN has noticeably higher bus traffic than accessory mode.
* **USB adapters need the `dialout` group** on typical Linux setups, or you get permission denied on `/dev/ttyUSB0`.
* The clone's `ATI` will lie about being an `ELM327 v1.5` even when interesting things are inside it — always try `STI` to check for an STN chip underneath.

## Sources

* [STN1100/STN1170 Family Reference and Programming Manual](https://www.scantool.net/scantool/downloads/682/obdlink_frpm_f.pdf)
* [FORScan forum on adapter MS-CAN support](https://forscan.org/forum/viewtopic.php?f=5&t=8)
