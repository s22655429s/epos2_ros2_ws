# epos2_ros2_ws
$rosdep install --from-paths src --ignore-src -r -y
$colcon build --symlink-install --cmake-args -DCMAKE_EXPORT_COMPILE_COMMANDS=ON
$. install/setup.bash 
$sudo /etc/init.d/udev restart
$ros2 run epos_hardware install_udev_rules
$ros2 action send_goal /joint_trajectory_controller/follow_joint_trajectory control_msgs/action/FollowJointTrajectory -f "{
  trajectory: {
    joint_names: [joint_1],
    points: [
      { positions: [0.1], time_from_start: { sec: 2 } },
      { positions: [-0.1], time_from_start: { sec: 4 } },
      { positions: [0], time_from_start: { sec: 6 } }
    ]
  }
}"
