cmake_minimum_required(VERSION 3.0.2)
set(PARENT_PROJECT_NAME "${PROJECT_NAME}")
project(clipscontrol)

if (PARENT_PROJECT_NAME)
  # add_compile_definitions(ROSPACKAGE=${PARENT_PROJECT_NAME})
  add_definitions(-DROSPACKAGE=${PARENT_PROJECT_NAME})
  # add_compile_definitions(QUERYKDB_H="${PARENT_PROJECT_NAME}/QueryKDB.h")
  add_definitions(-DQUERYKDB_H="${PARENT_PROJECT_NAME}/QueryKDB.h")
endif ()


set(CURSES_NEED_NCURSES TRUE)
set(CURSES_NEED_WIDE TRUE)
find_package(Curses REQUIRED)
# add_definitions(-w) # disable all warnings

file(GLOB CLIPSCONTROL_SRC
  ${PROJECT_SOURCE_DIR}/*.cpp
)


## Declare an executable
add_executable(${PROJECT_NAME}
  ${CLIPSCONTROL_SRC}
)

add_dependencies(${PROJECT_NAME}
  simulator_generate_messages_cpp
)

target_include_directories(${PROJECT_NAME}
  PUBLIC
  ${CURSES_INCLUDE_DIR}
  ${catkin_INCLUDE_DIRS}
)

target_link_libraries(${PROJECT_NAME}
  ${catkin_LIBRARIES}
  ${CURSES_LIBRARIES}
)

# set_target_properties(clips60
#   PROPERTIES
#   OUTPUT_NAME "lib${PROJECT_NAME}.so"
#   PREFIX ""
#   SUFFIX ""
# )
