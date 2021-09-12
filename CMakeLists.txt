cmake_minimum_required(VERSION 3.20)
project(ECE_506)
set(CMAKE_CXX_STANDARD 11)
include_directories(include)


if(APPLE)
    message(STATUS "You are using MACOS X")
    message("its a safe practice to install gcc instead of using default sdk compiler with brew install gcc")
    set(CMAKE_C_COMPILER "/opt/homebrew/bin/gcc-11")
    set(CMAKE_CXX_COMPILER "/opt/homebrew/bin/g++-11")
    find_package(OpenMP REQUIRED)
    find_package(MPI)
    if(OpenMP_FOUND)
        message(STATUS "OPENMP FOUND" )
        else()
        message(FATAL_ERROR "OpenMP not found change compiler")
       endif()
    if(MPI_FOUND)
        message(STATUS "MPI FOUND")
        else()
        message(STATUS "OpenMP Found MPI missing")
        endif()
    add_library(sortlib src/arrayQueue.c src/bfs.c src/bitmap.c src/edgelist.c src/graph.c src/sort.c src/timer.c src/vertex.c)
    add_executable(ECE_506 src/main.c)
    target_link_libraries(ECE_506  OpenMP::OpenMP_CXX MPI::MPI_CXX sortlib)


else()
    find_package(OpenMP REQUIRED)
    if(OpenMP_FOUND)
        message(STATUS "OPENMP FOUND" )
    else()
        message(FATAL_ERROR "OpenMP not found change compiler")
    endif()
    if(MPI_FOUND)
        message(STATUS "MPI FOUND")
    else()
        message(STATUS "OpenMP Found MPI missing")
    endif()
    add_library(sortlib src/arrayQueue.c src/bfs.c src/bitmap.c src/edgelist.c src/graph.c src/sort.c src/timer.c src/vertex.c)
    add_executable(ECE_506 src/main.c)
    target_link_libraries(ECE_506  OpenMP::OpenMP_CXX MPI::MPI_CXX sortlib)

    endif()





