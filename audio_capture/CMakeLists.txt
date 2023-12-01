cmake_minimum_required(VERSION 3.21.0)

project(audio_capture)

find_package(catkin REQUIRED COMPONENTS roscpp audio_common_msgs)

find_package(PkgConfig)
pkg_check_modules(GSTREAMER REQUIRED IMPORTED_TARGET gstreamer-1.0)
pkg_check_modules(GSTREAMER-AUDIO REQUIRED gstreamer-audio-1.0)


find_package(Boost REQUIRED COMPONENTS thread)

include_directories(${catkin_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS})

catkin_package()

add_executable(audio_capture src/audio_capture.cpp)
target_link_libraries(audio_capture ${catkin_LIBRARIES} PkgConfig::GSTREAMER ${Boost_LIBRARIES})
add_dependencies(audio_capture ${catkin_EXPORTED_TARGETS})

install(TARGETS audio_capture
   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})

install(DIRECTORY launch
   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
