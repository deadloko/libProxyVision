cmake_minimum_required (VERSION 3.8 FATAL_ERROR)
project (sikulix_vision)

set (CMAKE_INCLUDE_CURRENT_DIR ON)

file (GLOB_RECURSE SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp"
                           "${CMAKE_CURRENT_SOURCE_DIR}/*.cxx")

include_directories ("${CMAKE_CURRENT_SOURCE_DIR}/sources"
                     "/usr/lib/jvm/java-8-openjdk-amd64/include/"
                     "/usr/lib/jvm/java-8-openjdk-amd64/include/linux"
                     "/usr/lib/jvm/openjdk-8/include/"
                     "/usr/lib/jvm/openjdk-8/include/linux")

add_library (VisionProxy SHARED ${SOURCES})
target_link_libraries (VisionProxy opencv_core opencv_imgproc opencv_highgui tesseract)
