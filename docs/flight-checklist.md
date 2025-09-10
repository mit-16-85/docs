# Flight Checklist At-A-Glance

Refer to longform documentation [here](./flight.md).

## Pre-Flight :: Setup

- [ ] Move drone to flight space
    - [ ] Place drone in flight space.
    - [ ] Initial Safety Check:
        - [ ] Net is taut
        - [ ] Takeoff / landing space is large enough
        - [ ] Takeoff / landing space is free of FOD
- [ ] Mocap setup
    - [ ] Power on mocap
    - [ ] Configure mocap software on `AMSTRONG`
- [ ] Setup `aldrin`
    - [ ] Login
    - [ ] Connect correct telemetry radio
    - [ ] Run following commands
    ```
    # terminal 1
    qgc

    # terminal 2
    zenoh

    # terminal 3
    mocap
    ```
- [ ] Power on drone
    - [ ] Attach beeper to `4S` and `6S` batteries
    - [ ] Confirm voltages are within expected ranges
    - [ ] Attach batteries to drone and confirm velcro straps are snug
    - [ ] Connect `4S` battery to the electronics
    - [ ] Confirm NUC is powered on, if not press the Power button
    - [ ] Confirm space is free of unneccessary personnel
    - [ ] Announce loudly you are powering on drone
    - [ ] Connect `6S` battery to the electronics
    - [ ] Confirm battery velcro straps are still snug
    - [ ] Seal flight nets
    - [ ] Confirm all personnel have left the flight space
    - [ ] Seal control room net
- [ ] Power RC Transmitter
    - [ ] Fetch correct RC Transmitter
    - [ ] Decide an operator, lanyard stays on operator's neck at all times
    - [ ] Review RC Transmitter controls
    - [ ] Confirm Kill switch is clearly denoted with tape or some other marking
    - [ ] Confirm switches are in correct positions
        - [ ] **Throttle Off:** `J3 down`
        - [ ] **Disarmmed:** `SF down`
        - [ ] **Land Mode:** `SA down`
        - [ ] **Kill Switch Enabled:** `SD down`
    - [ ] Power on RC Transmitter
    - [ ] Click through any alerts and confirm `cap` profile
    - [ ] Confirm RC Transmitter has appropriate battery
- [ ] Run drone code
    - [ ] Open another terminal on `aldrin`. Connect to the drone and run the following command with: 
    ```
    # terminal 4
    ssh d01
    dynus
    ```
    - [ ] Confirm terminal output is normal
    - [ ] Confirm QGroundControl has Green status (this may take a minute)

## Pre-Flight :: Final Safety Check
- [ ] Confirm flight space is clear of personnel
- [ ] Confirm the flight space and control room nets are secured
- [ ] Confirm the operator has the correct RC transmitter, it is powered on, in the right mode, and they are wearing the lanyard
- [ ] Confirm the RC transmitter switches are in the correct configuration
- [ ] Confirm no batteries are beeping
- [ ] Confirm all computer readouts look good
- [ ] Loudly announce to the flight space: "Taking off!"

## Flight Operations :: Takeoff
- [ ] Undo the Kill Switch: `SD up`
- [ ] Switch to desired flight mode:
    - **Position Mode:** `SA up`
    - **Offboard Mode:** `SA middle`
- [ ] Arm the drone: `SF up`
- [ ] Gently ease up on the throttle `J3` to takeoff
- [ ] Achieve hovering conditions
- [ ] Perform flight

## Flight Operations :: Landing
- [ ] Navigate to above desired landing location
- [ ] Gently ease up on the throttle to land
- [ ] Throttle completely down `J3`
- [ ] Disarm drone: `SF down`
- [ ] Land Mode: `SA down`
- [ ] Activate Kill Switch: `SD down`
- [ ] Terminate any software
- [ ] Disconnect `6S` battery
- [ ] Disconnect `4S` battery (as needed)

## Cleanup
- [ ] Close all applications on `aldrin`
- [ ] Confirm any all data files are transfered off of `aldrin` and your drone
- [ ] Logoff `aldrin`
- [ ] Return batteries to appropriate charge / discharge bins
- [ ] Remove battery beepers and return to bag
- [ ] If possible, charge batteries to replace what you used
- [ ] Return drone to storage location
- [ ] Return RC transmitter to storage location
- [ ] Return telemetry radio to storage location
- [ ] Turn off mocap