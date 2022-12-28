cmake_minimum_required(VERSION 3.5)

project(mav_planning_msgs)

if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(rosidl_default_generators REQUIRED)

find_package(builtin_interfaces REQUIRED)
find_package(std_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(mav_msgs REQUIRED)
find_package(trajectory_msgs REQUIRED)

find_package(eigen3_cmake_module REQUIRED)
find_package(Eigen3)

include_directories(
  include
  ${EIGEN3_INCLUDE_DIRS}
)

set(DEPENDENCIES
  builtin_interfaces
  geometry_msgs
  sensor_msgs
  std_msgs
  mav_msgs
  trajectory_msgs)

set(msg_files
  "msg/Point2D.msg"
  "msg/PointCloudWithPose.msg"
  "msg/Polygon2D.msg"
  "msg/PolygonWithHoles.msg"
  "msg/PolygonWithHolesStamped.msg"
  "msg/PolynomialSegment.msg"
  "msg/PolynomialTrajectory.msg"
  "msg/PolynomialSegment4D.msg"
  "msg/PolynomialTrajectory4D.msg"
)

set(srv_files
  "srv/PlannerService.srv"
  "srv/PolygonService.srv"
  "srv/ChangeNameService.srv"
)


rosidl_generate_interfaces(${PROJECT_NAME}
  ${msg_files}
  ${srv_files}
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
