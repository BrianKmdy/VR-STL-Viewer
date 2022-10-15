# CMakeList.txt : CMake project for VR-STL-Viewer, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_C_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if ((MSVC) AND (MSVC_VERSION GREATER_EQUAL 1914))
    add_compile_options("/Zc:__cplusplus" "/permissive-")
    # target_compile_options(stxxl INTERFACE "/Zc:__cplusplus")
endif()

find_package(Qt6 REQUIRED COMPONENTS Widgets)
qt_standard_project_setup()

find_package(VTK REQUIRED)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

# find_package(Qt6 REQUIRED COMPONENTS Widgets Core Gui Sql)

include_directories(${VTK_USE_FILE} ${Qt6_INCLUDES} ${Qt6Widgets_INCLUDE_DIRS})

FILE(GLOB SOURCES "*.cpp" "*.cc" "*.c" "*.h")
# file(GLOB_RECURSE SOURCES "*.cpp")

# Add source to this project's executable.
add_executable (${PROJECT_NAME} ${SOURCES})

target_link_libraries(${PROJECT_NAME} ${VTK_LIBRARIES} Qt6::Core Qt6::Widgets)

# TODO: Add tests and install targets if needed.
