cmake_minimum_required(VERSION 3.16)
project(heat_method)

set(CMAKE_CXX_STANDARD 11)

# CGAL and its components
find_package( CGAL QUIET COMPONENTS  )

if ( NOT CGAL_FOUND )
    message(STATUS "This project requires the CGAL library, and will not be compiled.")
    return()
else()
    include_directories(${CGAL_INCLUDE_DIR})
endif()

# Boost and its components
find_package(Boost REQUIRED)

if ( NOT Boost_FOUND )
    message(STATUS "This project requires the Boost library, and will not be compiled.")
    return()
else()
    include_directories(${Boost_INCLUDE_DIRS})
endif()

find_package(Eigen3 3.3.0)

if (EIGEN3_FOUND)
    include_directories(${EIGEN3_INCLUDE_DIR})
else()
    message(STATUS "This project requires the Eigen library (3.3 or greater), and will not be compiled.")
    return()
endif()


# opengl
find_package(OpenGL REQUIRED)
find_package(glfw3 3.3 REQUIRED)
include_directories(/usr/local/include/KHR)
include_directories(${OPENGL_INCLUDE_DIR})
aux_source_directory(. DIRS_SRCS)

add_executable(${PROJECT_NAME} ${DIRS_SRCS})