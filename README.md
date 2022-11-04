# APRIS Robot Challenge 2022
APRIS web page:
- http://www.sigemb.jp/APRIS/2022/

Environments:
- https://github.com/hisazumi/aprisrc-sitl/tree/forairsim

This repository is using following template:
- https://github.com/hisazumi/gnc

## About this repository
This is team4.  
This repository is prototype for drone control program.

**Remember to change your name from `aprisrc-2022` to `gnc` when you clone!**

example of drone control:
1. you must copy `waypoint.dat` in this repository to `/home/$USER`  
(e.g. `cp ./wayposint.dat ~/`)
1. run `SITL`, `AirSim`, `roslaunch iq_sim apm.launch`  
(`SITL` = `sim_vehicle.py -v ArduCopter -f airsim-copter`)
1. you should wait until this message in `SITL`: `AP: EKF3 IMU0 is using GPS` and `AP: EKF3 IMU1 is using GPS`
1. run `rosrun gnc ctrl`
1. each time you run the following command, drone will move:  
(FYI: You can use tab completion)
```
rostopic pub /gnc_node/cmd std_msgs/String "data: 'start'"
```


## What is `waypoint.dat` file
The drone moves to the coordinates written in `waypoint.dat`.

If the `waypoint.dat` was written as follows:
```
2,2,3,
2,-2,3,
-2,-2,3,
-2,2,3,
0,0,3
```
1. the drone will moves to top right, (2, 2, 3)
1. the drone will moves to bottom right, (2, -2, 3)
1. the drone will moves to bottom left, (-2, -2, 3)
1. the drone will moves to top left, (-2, 2, 3)
1. the drone will moves to origin, (0, 0, 3)
1. Thereafter, the drone always will move to the origin, (0, 0, 1)

For detailed implementation, see `gen/gnc.cpp/gnc_set_destination_from_file()`.
