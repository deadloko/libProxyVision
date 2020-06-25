cmake_minimum_required (VERSION 3.8 FATAL_ERROR)
project (sikulix_vision)

set (CMAKE_INCLUDE_CURRENT_DIR ON)

file (GLOB_RECURSE SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp"
                           "${CMAKE_CURRENT_SOURCE_DIR}/*.cxx")

include_directories ("${CMAKE_CURRENT_SOURCE_DIR}/sources"
	             "${OE_PREFIX_PATH}/usr/lib/jvm/java-8-openjdk-amd64/include/"
                     "${OE_PREFIX_PATH}/usr/lib/jvm/java-8-openjdk-amd64/include/linux"
                     "${OE_PREFIX_PATH}/usr/lib/jvm/openjdk-8/include/"
                     "${OE_PREFIX_PATH}/usr/lib/jvm/openjdk-8/include/linux")

find_library (OPENCV_CORE libopencv_core.so PATHS "${OE_PREFIX_PATH}/usr/lib/opencv_sikulix" REQUIRED)
find_library (OPENCV_IMGPROC libopencv_imgproc.so PATHS "${OE_PREFIX_PATH}/usr/lib/opencv_sikulix" REQUIRED)
find_library (OPENCV_HIGHGUI libopencv_highgui.so PATHS "${OE_PREFIX_PATH}/usr/lib/opencv_sikulix" REQUIRED)

add_library (VisionProxy SHARED ${SOURCES})
target_link_libraries (VisionProxy ${OPENCV_CORE} ${OPENCV_IMGPROC} ${OPENCV_HIGHGUI} tesseract)

install (TARGETS VisionProxy CONFIGURATIONS Release DESTINATION /usr/lib/)
