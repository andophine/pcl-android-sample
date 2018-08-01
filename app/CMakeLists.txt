cmake_minimum_required(VERSION 3.4.1)

project(helloPcl)

#notice the "recycling" of CMAKE_C_FLAGS
#this is necessary to pick up android flags
set( CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -pedantic" )

set(PCL_INCLUDE ${CMAKE_CURRENT_SOURCE_DIR}/libs/pcl-android/include)
set(BOOST_ANDROID_INCLUDE ${CMAKE_CURRENT_SOURCE_DIR}/libs/boost-android/include)
set(FLANN_INCLUDE ${CMAKE_CURRENT_SOURCE_DIR}/libs/flann-android/include)
set(EIGEN_INCLUDE ${CMAKE_CURRENT_SOURCE_DIR}/libs/eigen)

set(BOOST_LIBRARIES ${CMAKE_CURRENT_SOURCE_DIR}/libs/boost-android/lib)
set(PCL_LIBRARIES ${CMAKE_CURRENT_SOURCE_DIR}/libs/pcl-android/lib)
set(FLANN_LIBRARIES ${CMAKE_CURRENT_SOURCE_DIR}/libs/flann-android/lib)


#IMPORTANT

#test for ANDROID and look for stuff not relevant to android.
if(NOT ANDROID)
#jni is available by default on android
find_package(JNI REQUIRED)
include_directories(${JNI_INCLUDE_DIRS})
endif()


#this will be overridden by the android toolchain
set( LIBRARY_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/lib/pc CACHE PATH
        "Single Directory for all Libraries")

#make sure to used shared in in the jni library, as this will be loaded by java

include_directories(
    ${PCL_INCLUDE}
    ${BOOST_ANDROID_INCLUDE}
    ${FLANN_INCLUDE}
    ${EIGEN_INCLUDE}
    )
link_directories(
    ${BOOST_LIBRARIES}
    ${PCL_LIBRARIES}
    ${FLANN_LIBRARIES}
    )

#here to avoid link error on openmp
link_libraries("-fopenmp")

add_library(JNIHelloPCL SHARED src/main/cpp/jni_hellopcl.cpp)
target_link_libraries(
    JNIHelloPCL
    log
    pcl_kdtree
    pcl_io
    boost_system
    boost_filesystem
    flann_s
    flann_cpp_s
    pcl_common
    )


