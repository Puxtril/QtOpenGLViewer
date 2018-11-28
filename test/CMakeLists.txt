# Created by Marcel Paz Goldschen-Ohm <marcel.goldschen@gmail.com>

# !!! Set env variable QT5_DIR to <Qt install prefix>/lib/cmake/Qt5
# For macx xcode project: cmake -G Xcode <dir of CMakeLists.txt>

cmake_minimum_required(VERSION 3.0.2)

set(PROJECT_NAME test_QtOpenGLViewer)
project(${PROJECT_NAME} VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11) # This is equal to QMAKE_CXX_FLAGS += -std=c++0x
set(CMAKE_INCLUDE_CURRENT_DIR ON) # Search in current dir.
set(CMAKE_AUTOMOC ON) # Run moc automatically for Qt.
set(CMAKE_AUTOUIC ON) # Run uic automatically for *.ui files.
set(CMAKE_AUTORCC ON) # Run automatically for *.qrc files.

if(APPLE AND EXISTS /usr/local/opt/qt5)
	# Homebrew installs Qt5 (up to at least 5.9.1) in
	# /usr/local/qt5, ensure it can be found by CMake since
	# it is not in the default /usr/local prefix.
	list(APPEND CMAKE_PREFIX_PATH "/usr/local/opt/qt5")
endif()

find_package(Qt5 COMPONENTS Core Widgets OpenGL REQUIRED)
find_package(OpenGL REQUIRED)

set(SOURCES ../QtOpenGLViewer.cpp test_QtOpenGLViewer.cpp)
set(HEADERS ../QtOpenGLViewer.h test_QtOpenGLViewer.h)

add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS})
target_include_directories(${PROJECT_NAME} PUBLIC ..)
qt5_use_modules(${PROJECT_NAME} Widgets OpenGL)
target_link_libraries(${PROJECT_NAME} ${QT_LIBRARIES} ${OPENGL_LIBRARIES})