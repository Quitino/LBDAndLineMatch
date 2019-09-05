cmake_minimum_required(VERSION 2.8.3)
PROJECT(Line)


set(CMAKE_BUILD_TYPE "Release")
set(CMAKE_CXX_FLAGS "-std=c++11")
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall -g")


set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)


set(OpenCV_DIR /opt/ros/kinetic/share/OpenCV-3.3.1-dev)
SET(ARPACK_INCLUDE_DIRS "/usr/include/arpack++/")
SET(ARPACK_LINK_DIR "/usr/lib/")

find_package(OpenCV REQUIRED)
#find_package(ARPACK REQUIRED)


#INCLUDE_DIRECTORIES(${ARPACK_INCLUDE_DIR} /usr/local/include/opencv)
#LINK_DIRECTORIES(${ARPACK_LINK_DIR} /usr/local/lib)


set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)


include_directories(
  ${PROJECT_SOURCE_DIR}/include
  ${OpenCV_INCLUDE_DIRS}
  ${ARPACK_INCLUDE_DIRS}
)

add_library(LineMatchingLib SHARED
    src/PairwiseLineMatching.cpp
    src/LineDescriptor.cpp
    src/EDLineDetector.cpp)

target_link_libraries(LineMatchingLib 
${OpenCV_LIBS} 
arpack 
/usr/lib/x86_64-linux-gnu/libsuperlu.so 
arpack++
  )


ADD_EXECUTABLE(Test_Single_LMA src/Demo_LBD_single.cpp)
TARGET_LINK_LIBRARIES(Test_Single_LMA   LineMatchingLib ${OpenCV_LIBS})

ADD_EXECUTABLE(Test_Bat_LMA src/Demo_LBD_Multi.cpp)
TARGET_LINK_LIBRARIES(Test_Bat_LMA LineMatchingLib ${OpenCV_LIBS})


