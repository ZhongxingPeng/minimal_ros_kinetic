cmake_minimum_required(VERSION 2.8.3)
project(message_filters)

if(NOT WIN32)
  set_directory_properties(PROPERTIES COMPILE_OPTIONS "-Wall;-Wextra")
endif()

find_package(catkin REQUIRED COMPONENTS roscpp xmlrpcpp rosconsole)
catkin_package(
  INCLUDE_DIRS include
  LIBRARIES message_filters
  CATKIN_DEPENDS roscpp xmlrpcpp rosconsole
)
catkin_python_setup()

find_package(Boost REQUIRED COMPONENTS signals thread)

include_directories(include ${catkin_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS})
link_directories(${catkin_LIBRARY_DIRS})

add_library(${PROJECT_NAME} src/connection.cpp)
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES} ${Boost_LIBRARIES})

install(TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION})

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h")

