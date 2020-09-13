cmake_minimum_required(VERSION 3.10)
project(YOLOv4-tracker)

set(CMAKE_CXX_STANDARD 17)

find_package( Threads )
find_package(PkgConfig)
pkg_check_modules(GSTREAMER REQUIRED gstreamer-1.0 gstreamer-video-1.0)

include_directories(
        /opt/nvidia/deepstream/deepstream-5.0/sources/includes/
        ${GLIB_INCLUDE_DIRS}
        ${GSTREAMER_INCLUDE_DIRS}
)

link_directories(
        /opt/nvidia/deepstream/deepstream-5.0/lib/
        ${GLIB_LIBRARY_DIRS}
        ${GSTREAMER_LIBRARY_DIRS}
)

include_directories(src)
include_directories(include)

set(SOURCE_FILES src/main.cpp)
add_executable(${CMAKE_PROJECT_NAME} ${SOURCE_FILES})

target_link_libraries(
        ${CMAKE_PROJECT_NAME}
        nvdsgst_meta
        nvds_meta
        ${GSTREAMER_LIBRARIES}
        ${OpenCV_LIBS}
        ${CMAKE_THREAD_LIBS_INIT}
)