# CMakeLists.txt
cmake_minimum_required(VERSION 3.10)
project(Cifar10CMAKE)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Find OpenCV package
find_package(OpenCV 4.5.4 REQUIRED)
find_package(VART 3.5.0 REQUIRED)
find_package(UNILOG 3.5.0 REQUIRED)
find_package(Glog 0.4.0 REQUIRED)
find_package(Threads REQUIRED)
find_package(XIR 3.5.0)

message(STATUS "OpenCV version: ${OpenCV_VERSION}")
message(STATUS "VART version: ${VART_VERSION}")
message(STATUS "UNILOG version: ${UNILOG_VERSION}")
message(STATUS "GLOG version: 0.4.0")
message(STATUS "XIR version: ${XIR_VERSION}")

# Include directories
include_directories(${OpenCV_INCLUDE_DIRS})
include_directories(include)

# Common source files
set(COMMON_SOURCES
    src/common.cpp 
)

# Define the first executable
add_executable(main_int8
    ${COMMON_SOURCES}
    src/main_int8.cc
)

# Define the second executable
add_executable(get_dpu_fps
    ${COMMON_SOURCES}
    src/get_dpu_fps.cc 
)

# Define the third executable
add_executable(test
    ${COMMON_SOURCES}
    src/test.cpp
)

# Link libraries for the first executable
target_link_libraries(main_int8
    ${OpenCV_LIBS}
    vart-runner
    xir
    unilog
    glog
    Threads::Threads
)

# Link libraries for the second executable
target_link_libraries(get_dpu_fps
    ${OpenCV_LIBS}
    vart-runner
    xir
    unilog
    glog
    Threads::Threads
)

# Link libraries for the third executable
target_link_libraries(test
    ${OpenCV_LIBS}
    vart-runner
    xir
    unilog
    glog
    Threads::Threads
)