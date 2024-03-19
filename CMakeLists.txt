# Created by Marcel Paz Goldschen-Ohm <marcel.goldschen@gmail.com>

cmake_minimum_required(VERSION 3.11)

set(PROJECT_NAME QtOpenGLViewer)
project(${PROJECT_NAME} LANGUAGES CXX)

set(BUILD_TEST True)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

if(APPLE AND EXISTS /usr/local/opt/qt6)
  list(APPEND CMAKE_PREFIX_PATH "/usr/local/opt/qt6")
endif()

find_package(Qt6 COMPONENTS Core Widgets OpenGL OpenGLWidgets REQUIRED)
find_package(OpenGL REQUIRED)

add_library(${PROJECT_NAME} STATIC QtOpenGLViewer.cpp)
target_link_libraries(${PROJECT_NAME} Qt6::Core Qt6::Widgets Qt6::OpenGLWidgets)
