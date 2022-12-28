cmake_minimum_required(VERSION 3.5)

project(mav_msgs)

if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(rosidl_default_generators REQUIRED)

find_package(geometry_msgs REQUIRED)
find_package(std_msgs REQUIRED)

find_package(eigen3_cmake_module REQUIRED)
find_package(Eigen3)

include_directories(
  include
  ${EIGEN3_INCLUDE_DIRS}
)

set(DEPENDENCIES std_msgs geometry_msgs Eigen3)

set(msg_files
  "msg/Actuators.msg"
  "msg/AttitudeThrust.msg"
  "msg/RateThrust.msg"
  "msg/RollPitchYawrateThrust.msg"
  "msg/TorqueThrust.msg"
  "msg/Status.msg"
  "msg/FilteredSensorData.msg"
  "msg/GpsWaypoint.msg"
)

rosidl_generate_interfaces(${PROJECT_NAME}
  ${msg_files}
  DEPENDENCIES ${DEPENDENCIES}
  ADD_LINTER_TESTS
)

install(
  DIRECTORY include/
  DESTINATION include/
)

ament_export_dependencies(eigen3_cmake_module)
ament_export_include_directories(include)
ament_export_dependencies(rosidl_default_runtime)
ament_package()
