cmake_minimum_required (VERSION 3.0)
project (TimeIt)

enable_testing() #Enables CTest functionality in CMake

find_package(MPI)   #CMake built-in routine to find most MPI packages

add_executable(TimeIt TimeIt.c)  # Adds TimeIt and 
add_executable(MPITimeIt MPITimeIt.c) # MPITimeIt build targets with their source code files 

#Needs an include path to the mpi.h file and to the MPI library
target_include_directories(MPITimeIt PUBLIC.${MPI_INCLUDE_PATH})

file(GLOB TESTFILES RELATIVE 
    "${CMAKE_CURRENT_SOURCE_DIR}" "*.ctest")
foreach(TESTFILE ${TESTFILES})
    add_test(NAME ${TESTFILE} WORKING_DIRECTORY
        ${CMAKE_BINARY_DIR} 
    COMMAND sh 
        ${CMAKE_CURRENT_SOURCE_DIR}/${TESTFILE})
endforeach()

add_custom_target(distclean
    COMMAND rm -rf CmakeCache.txt CMakeFiles
    CTesty)