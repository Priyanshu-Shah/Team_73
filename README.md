# **Team_73** 
## Modified PX4 Quadcopter Autopilot

## **Usage:**
1. Clone this repository
2. 'run ./tools/setup/ubuntu.sh' for installing required dependencies in the linux machine
3. 'make px4_sitl gazebo-classic_iris' for running the simulation in loop in gazebo classic simulator using the iris model
4. Use pxh shell commands like commander takeoff/land to operate the quadcopter
5. Use commander fail to induce single motor failure 
   usage: commander fail <motor_index> <delay_time>
   example: 'commander fail 0 5' will fail motor index 0 after delay time of 5 seconds


## **Code changes:**

![Flowchart - Frame 1 (1)](https://github.com/user-attachments/assets/57ad04b1-290c-4027-b5d6-0a164a6721a4)


**FailureDetector.cpp** (src/module/commander/failsafe/failure_detector/FailureDetector.cpp): Updated the failsafe detection function to enable custom motor failure without triggering failsafe error.

**Vehicle_command.h file** (build/px4_sitl_default/uORB/topics/vehicle_command.h): Added a message VEHICLE_MOTOR_FAILURE to the topic messages list. 

**Commander.cpp file** (src/modules/commander/commander.cpp): Method ‘custom_command’ deals with all pxh shell commands starting with ‘commander’. We add a conditional statement to tackle arguement 'fail' along with parameters for motor_id and delay_seconds. Commander.cpp publishes to vehicle_commmand topic.


**FunctionMotors.hpp file** (src/lib/mixer_modules/functions/FunctionMotors.hpp): Subscribes to vehicle_command topic and awaits for VEHICLE_MOTOR_FAILURE message to be published. Declared _motor_failure_states (array to track if a motor failure is scheduled), _failures_active (array to track if a motor failure is currently active), _failure_trigger_time (array to store the trigger time for each motor failure). Upon finding the failure message, the declared variables are populated and power to designated motor is turned to 0 via update values method after the designated time. Also added DetectMotorFailure method in run method, which subscribes to actuator_motor topic, and checks if the control data is within the threshold range, "Motor i output is consistently high. Possible failure detected." is logged.
 
