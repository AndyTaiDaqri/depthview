cmake_minimum_required(VERSION 2.8)

project(depthview C CXX)


# Tell CMake to run moc when necessary:
set(CMAKE_AUTOMOC ON)
# As moc files are generated in the binary dir, tell CMake
# to always look for includes there:
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Widgets finds its own dependencies (QtGui and QtCore).
find_package(Qt5Widgets REQUIRED)

# The Qt5Widgets_INCLUDES also includes the include directories for
# dependencies QtCore and QtGui
include_directories(${Qt5Widgets_INCLUDES})

# We need add -DQT_WIDGETS_LIB when using QtWidgets in Qt 5.
add_definitions(${Qt5Widgets_DEFINITIONS})

# Executables fail to build with Qt 5 in the default configuration
# without -fPIE. We add that here.
set(CMAKE_CXX_FLAGS "${Qt5Widgets_EXECUTABLE_COMPILE_FLAGS}")

# OpenCV
#provide OpenCV location via -DOpenCV_DIR=<opencv install location>
find_package( OpenCV REQUIRED )

set (SRCS
    
    cameracontrol.cpp
    cameracontrol.h
    cameradatafeed.cpp
    cameradatafeed.h
    controlswidget.cpp
    controlswidget.h
    
    main.cpp
    mainwindow.cpp
    mainwindow.h
    videowidget.cpp
    videowidget.h

)

add_executable(depthview ${SRCS})

# The Qt5Widgets_LIBRARIES variable also includes QtGui and QtCore
target_link_libraries(depthview ${Qt5Widgets_LIBRARIES})
