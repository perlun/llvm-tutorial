cmake_minimum_required(VERSION 3.24)
project(llvm_tutorial)

find_package(LLVM REQUIRED CONFIG)

message(STATUS "Found LLVM ${LLVM_PACKAGE_VERSION}")
message(STATUS "Using LLVMConfig.cmake in: ${LLVM_DIR}")

set(CMAKE_CXX_STANDARD 14)

include_directories(${LLVM_INCLUDE_DIRS})
separate_arguments(LLVM_DEFINITIONS_LIST NATIVE_COMMAND ${LLVM_DEFINITIONS})
add_definitions(${LLVM_DEFINITIONS_LIST})

add_executable(llvm_tutorial
        toy.cpp)

# Find the libraries that correspond to the LLVM components
# that we wish to use
execute_process(COMMAND llvm-config --libs all
        OUTPUT_VARIABLE llvm_libs)

string(STRIP ${llvm_libs} llvm_libs)

# Link against LLVM libraries
target_link_libraries(llvm_tutorial ${llvm_libs})