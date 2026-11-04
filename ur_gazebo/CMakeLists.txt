cmake_minimum_required(VERSION 3.14.0)

project(ur_gazebo)

find_package(catkin REQUIRED)

catkin_package()

if (CATKIN_ENABLE_TESTING)
  find_package(roslaunch REQUIRED)

  # The roslaunch-test files below include launch files that resolve $(find gazebo_ros). In
  # environments without the Gazebo stack (e.g. CI images without gazebo_ros_pkgs), these
  # tests would abort with an unhandled rospkg.ResourceNotFound error and result in a failure.
  # Instead, these tests will only be enabled when gazebo_ros is actually available.
  find_package(gazebo_ros QUIET)
  if (gazebo_ros_FOUND)
    roslaunch_add_file_check(tests/roslaunch_test_ur3.xml)
    roslaunch_add_file_check(tests/roslaunch_test_ur3e.xml)
    roslaunch_add_file_check(tests/roslaunch_test_ur5.xml)
    roslaunch_add_file_check(tests/roslaunch_test_ur5e.xml)
    roslaunch_add_file_check(tests/roslaunch_test_ur10.xml)
    roslaunch_add_file_check(tests/roslaunch_test_ur10e.xml)
    roslaunch_add_file_check(tests/roslaunch_test_ur8long.xml)
    roslaunch_add_file_check(tests/roslaunch_test_ur15.xml)
    roslaunch_add_file_check(tests/roslaunch_test_ur18.xml)
    roslaunch_add_file_check(tests/roslaunch_test_ur16e.xml)
    roslaunch_add_file_check(tests/roslaunch_test_ur20.xml)
    roslaunch_add_file_check(tests/roslaunch_test_ur30.xml)
  else()
    message(STATUS "ur_gazebo: skipping tests because gazebo_ros was not found")
  endif()

endif()

install(DIRECTORY config launch urdf
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
