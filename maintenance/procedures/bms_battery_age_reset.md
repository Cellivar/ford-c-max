# BMS Battery Age Reset Procedure

_Confirmed working in my car_.

When you get a new battery you MUST reset the BMS. [See more about batteries here.](/maintenance/low_voltage_battery.md).

If you have ForScan you may want to check the current value for Battery Days in Service if you're curious or troubleshooting. If it doesn't matter go right to the procedure.

## Procedure

1. Start the car in ACC mode
    * In a push-start C-Max press the start button with your foot OFF the brake.
2. Turn on the high beams 5 times
    * Pull the light stalk towards you for momentary activation.
3. Press and release the brake pedal 3 times.

There is no indicator for success.

## Verify the reset

Connect to your car in ForScan

1. Open the Table display
2. Edit the PID list, selecting the BdyCM Module
3. Find the PID for "Battery Days in Service" or similar and select it
4. Start the monitoring

The value should be 0 now.
