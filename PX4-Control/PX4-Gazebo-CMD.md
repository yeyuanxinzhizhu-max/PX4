# 一、启动gazebo仿真

在/home/yxwang/Projects/PX4-Autopilot/路径下，按需执行下面任一条命令

| Vehicle                                                      | Command                           | `PX4_SYS_AUTOSTART` |
| :----------------------------------------------------------- | :-------------------------------- | :------------------ |
| [Quadrotor(x500)](https://docs.px4.io/main/zh/sim_gazebo_gz/vehicles.html#x500-quadrotor) | `make px4_sitl gz_x500`           | 4001                |
| [Quadrotor(x500) with Depth Camera](https://docs.px4.io/main/zh/sim_gazebo_gz/vehicles.html#x500-quadrotor-with-depth-camera) | `make px4_sitl gz_x500_depth`     | 4002                |
| [Quadrotor(x500) with Vision Odometry](https://docs.px4.io/main/zh/sim_gazebo_gz/vehicles.html#x500-quadrotor-with-visual-odometry) | `make px4_sitl gz_x500_vision`    | 4005                |
| [VTOL](https://docs.px4.io/main/zh/sim_gazebo_gz/vehicles.html#standard-vtol) | `make px4_sitl gz_standard_vtol`  | 4004                |
| [Plane](https://docs.px4.io/main/zh/sim_gazebo_gz/vehicles.html#standard-plane) | `make px4_sitl gz_rc_cessna`      | 4003                |
| [Advanced Plane](https://docs.px4.io/main/zh/sim_gazebo_gz/vehicles.html#advanced-plane) | `make px4_sitl gz_advanced_plane` | 4008                |

```
make px4_sitl gz_x500
make px4_sitl gz_x500_depth
make px4_sitl gz_x500_vision
make px4_sitl gz_standard_vtol
make px4_sitl gz_rc_cessna
make px4_sitl gz_advanced_plane
```



# 二、启动QGC地面站

在/home/yxwang/Softwares/QGroundControl/路径下，执行下面这条命令。

```bash
./QGroundControl.AppImage
```

# 三、启动PX4-Control键盘控制

打开任一新终端，执行下面这条命令，连接PX4和MAVROS。

```bash
roslaunch mavros px4.launch fcu_url:="udp://:14540@127.0.0.1:14557"
```

输入下面这条命令，查看ROS Topic中是否有MAVROS的话题。

```bash
rostopic list
```

在/home/yxwang/Projects/PX4-Control/路径下，执行下面这几条命令。如果没有报错，即可正常运行。由于当前是键盘控制节点，需要读取外舍，因此需要进入root权限。

```bash
sudo su
source ./devel/setup.bash
rosrun px4_keyboard_control px4_keyboard_control_node
```

下面是键盘控制无人机运动的对应表，在控制PX4仿真的无人机时，需要先按键 T启动外部控制，然后按键G解锁无人机后，才能正常控制其飞行。

| 键盘按键 | 对应功能                            |
| -------- | ----------------------------------- |
| T        | 外部控制启用                        |
| G        | 无人机解锁                          |
| B        | 无人机锁定                          |
| Q        | 无人机上升                          |
| A        | 无人机停止升降                      |
| Z        | 无人机下降                          |
| J        | 无人机向左运动                      |
| L        | 无人机向右运动                      |
| I        | 无人机向前运动                      |
| K        | 无人机停止运动                      |
| ，       | 无人机向后运动                      |
| U        | 顺时针转向                          |
| O        | 逆时针转向                          |
| H        | 线加速度和角加速度归零              |
| N        | 控制姿态                            |
| Y        | 从控制cmd_vel模式转换到控制pose模式 |

