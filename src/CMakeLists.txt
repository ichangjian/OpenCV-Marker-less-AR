cmake_minimum_required(VERSION 3.10)
project(CVAR)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}  -Wall   -O3  -std=c++11")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall   -O3")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

include_directories(Main)
include_directories(ObjRecog)
include_directories(Overlay)
include_directories(Tracking)

find_package(GLUT REQUIRED)
find_package(OpenGL REQUIRED) 
find_package(PNG)
find_package(OpenCV)

if(OpenCV_FOUND)
    include_directories(${OpenCV_INCLUDE_DIRS})
    set(SRC_FILES 
    Overlay/viewModel.h
    Overlay/viewModel.cpp
    Overlay/modelObjectFactory.cpp
    Overlay/slideModelObject.cpp
    Overlay/mqoModelObject.cpp
    Overlay/GLMetaseq.c
    Overlay/mqoSeqModelObject.cpp

    ObjRecog/controlOR.cpp
    ObjRecog/imageDB.cpp
    ObjRecog/visualWords.h
    ObjRecog/visualWords.cpp

    Tracking/trackingOBJ.cpp
    Tracking/kltTrackingOBJ.cpp

    Main/guiAR.cpp
    Main/orException.cpp
    Main/main.cpp
    Main/utilFunctions.cpp
    Main/cameraCalibration.cpp
    Main/commonCvFunctions.cpp)

    add_executable(ar ${SRC_FILES})
    target_link_libraries(ar  ${OpenCV_LIBRARIES} ${OPENGL_LIBRARIES} ${GLUT_LIBRARY} ${PNG_LIBRARY} )
endif()