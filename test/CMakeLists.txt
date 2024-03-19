# Created by Marcel Paz Goldschen-Ohm <marcel.goldschen@gmail.com>

cmake_minimum_required(VERSION 3.11)

set(PROJECT_NAME test_QtOpenGLViewer)
project(${PROJECT_NAME} LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)

find_package(Qt6 COMPONENTS Core Widgets OpenGL OpenGLWidgets REQUIRED)
find_package(OpenGL REQUIRED)

add_library(QtOpenGLViewer STATIC "${CMAKE_CURRENT_SOURCE_DIR}/../QtOpenGLViewer.cpp")
target_include_directories(QtOpenGLViewer PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/..)
target_link_libraries(QtOpenGLViewer Qt6::Core Qt6::Widgets Qt6::OpenGLWidgets)

add_executable(${PROJECT_NAME} "${CMAKE_CURRENT_SOURCE_DIR}/test_QtOpenGLViewer.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/test_QtOpenGLViewer.h")
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/..)
target_link_libraries(${PROJECT_NAME} OpenGL::OpenGL OpenGL::GLU Qt6::Core Qt6::Widgets Qt6::OpenGLWidgets QtOpenGLViewer)
