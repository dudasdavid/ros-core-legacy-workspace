cmake_minimum_required(VERSION 3.0.2)
project(camera_info_manager)

find_package(catkin REQUIRED COMPONENTS camera_calibration_parsers image_transport roscpp roslib sensor_msgs)

find_package(Boost)
catkin_package(INCLUDE_DIRS include
               LIBRARIES ${PROJECT_NAME}
               CATKIN_DEPENDS camera_calibration_parsers
               DEPENDS Boost roscpp sensor_msgs
)

include_directories(include)
include_directories(${catkin_INCLUDE_DIRS})

# add a library
add_library(${PROJECT_NAME} src/camera_info_manager.cpp)
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES})

install(TARGETS ${PROJECT_NAME}
        ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION}
        COMPONENT main
)
install(DIRECTORY include/${PROJECT_NAME}/
        DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)

#if(CATKIN_ENABLE_TESTING)
#  find_package(rostest)
  # Unit test uses gtest, but needs rostest to create a ROS environment.
  # Hence, it must be created as a normal executable, not using
  # catkin_add_gtest() which runs an additional test without rostest
#  add_executable(unit_test tests/unit_test.cpp)
#  target_link_libraries(unit_test ${PROJECT_NAME} ${GTEST_LIBRARIES} ${catkin_LIBRARIES})

#  add_rostest(tests/unit_test.test DEPENDENCIES unit_test)
#endif()
