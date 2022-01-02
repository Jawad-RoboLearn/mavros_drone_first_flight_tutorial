# Mavros-PX4 Drone First Flight Tutorial
This tutorial will cover the complete setup of drone, PX4-mavros based software setup, and the first ROS package for controlling the drone

# Step 1: Drone Setup
You need some electronics
1: A drone mechanical frame with 4 motors and 4 propellers (2 propellers with CCW (R written on propeller) and 2 with CW (L written on propeller) suitable propeller type)

2: 4 ESC's (Please check the motor max current rating before buying the ESC). Tip: My motor amperes at max thrust are 24A so I have used >30A ESC's. 

3: Pixhawk 4 (PX4)

4: Raspberry Pi 4

5: Radio transmitter and receiver

6: GPS provided with PX4 board

7: FTDI USB2TTL (3.3v) chip and USB cable 

8: A power distribution board that will give you 12 and 5 v channels

# My Drone (For reference)
1: QAV 250 type frame with 2 CCW / 2 CW propellers (Model: 5045) and 4 BLDC motors. (Tip: Your motors cummulative thrust will be > 2 x drone weight)

2: ESCs 30A

3: PX4, Raspberry pi 4

4: Radio Link transmitter and R9DS receiver

5: GPS provided by PX4

6: FTDI chip easily available

7: Power board 1: 12 V and 5V used for motor and raspberry pi 4. For PX4 I have used APM galvanometer voltage sensor power module APM PIX PX4 Power Module 3A BEC whose input 12 V is from the main power board 1. The power board 1 is connected with the battery. 

# Setting up the parameters in Q-ground control 
1: Connect the USB cable with PX4 and your PC. Open Q ground control. Update the latest firmware and choose the airframe.

2: Do Accelerometer, magnetometer calibrations.

3: Then calibrate the joystick. 

4: Set Flight modes: Choose a button on RC and setup three modes (For me they are Position - Manual - Land). Choose the RC button that have three states top-mid-bottom

5: Set emergency kill switch, arming switch and offboard switch, and RTL switch (use different on-off switches on your RC transmitter)

6: Calibrate motors: Plug out the battery port first, press motor calibrate button and then connect the battery plug. 

7: In motors section: See each motor can rotate according to the direction you want to, according to Airframe reference.

8: Set up parameters for Telem2 port, because your PX4 will communicate with raspberry pi 4 through telem2 port and USB2TTL setup. 

(Imp link: https://docs.px4.io/master/en/companion_computer/pixhawk_companion.html)

    >> MAV_1_CONFIG = TELEM 2 (MAV_1_CONFIG is often used to map the TELEM 2 port)
    
    >> MAV_1_MODE = Onboard
    
    >> SER_TEL2_BAUD = 921600 (921600 or higher recommended for applications like log streaming or FastRTPS)
    
9: Set up parameters for EKF2 fusion with vicon (Assume we are not using GPS and using vicon)

    >> EKF2_AID_MASK -> Tick mark only the fields "vision position fusion" and "vision yaw fusion" instead of GPS
    
    >> EKF2_HGT_MODE set to "vision" instead of barometer
    
    >> EKF2_EV_DELAY set to "50 ms". Technically, should be measured (follow instructions on px4 guide (https://docs.px4.io/master/en/ros/external_position_estimation.html)
    
    >> EKF2_EVA_NOISE set to the minimum value (2.86 degrees in our case), ie you are saying that the vicon data is absolutely true
    
    >> EKF2_EVP_NOISE set to the minimum value (0.01 meters in our case), same as above

# Set up Telem2 port 
Follow this link >> https://docs.px4.io/master/en/companion_computer/pixhawk_companion.html

# Prepare the raspberry pi 4 with Ubuntu 18.04-raspi-arm64. Set up for the first time and WIFI
Follow the detailed Gist, I have written 
https://gist.github.com/Jawad-RoboLearn/e409b64dec736c01c4dd1d4ecd2339fb

# Prepare the vicon and get the data
Follow the detailed Gist, I have written
https://gist.github.com/Jawad-RoboLearn/53a99356153530f61cf5f880487eb766


