cmake_minimum_required(VERSION 3.21.0)

project(audio_play)

find_package(catkin REQUIRED COMPONENTS roscpp audio_common_msgs)

find_package(PkgConfig)
pkg_check_modules(GSTREAMER REQUIRED IMPORTED_TARGET gstreamer-1.0)

find_package(Boost REQUIRED COMPONENTS thread)

include_directories(${catkin_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS})

catkin_package()

add_executable(audio_play src/audio_play.cpp)
target_link_libraries(audio_play ${catkin_LIBRARIES} PkgConfig::GSTREAMER ${Boost_LIBRARIES}) 
add_dependencies(audio_play ${catkin_EXPORTED_TARGETS})

install(TARGETS audio_play 
   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})

install(DIRECTORY launch
   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
