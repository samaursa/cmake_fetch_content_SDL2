cmake_minimum_required(VERSION 3.11)

project(testProj)

include(FetchContent)

FetchContent_Declare(
  SDL2
  GIT_REPOSITORY "https://github.com/spurious/SDL-mirror"
  )

FetchContent_GetProperties(SDL2)
if(NOT sdl2_POPULATED)
  FetchContent_Populate(SDL2)
  message(STATUS "Catch source dir: ${sdl2_SOURCE_DIR}")
  message(STATUS "Catch binary dir: ${sdl2_BINARY_DIR}")
  add_subdirectory(${sdl2_SOURCE_DIR} ${sdl2_BINARY_DIR})
endif()

add_executable(testExe
  main.cpp
  )

message(STATUS "Catch include dir: ${sdl2_SOURCE_DIR}/include")

target_link_libraries(testExe SDL2)

# the following line is necessary, target_link_libraries for SDL2
# does not automatically set the correct include directories
target_include_directories(testExe PUBLIC ${sdl2_SOURCE_DIR}/include)
