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

## **Project Report:**
https://drive.google.com/file/d/1LD8eEFN391IebFb8fQUxXiR8IwaVuNOx/view?usp=sharing
