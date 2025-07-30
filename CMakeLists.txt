cmake_minimum_required(VERSION 3.14)
project(FEMHeatEquation LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Options
option(USE_OPENMP "Enable OpenMP" ON)
option(USE_MPI "Enable MPI" OFF)
option(BUILD_PYTHON_BINDINGS "Enable Python bindings" OFF)

# Include paths
include_directories(include)

# Eigen
find_package(Eigen3 REQUIRED)

# OpenMP
if(USE_OPENMP)
    find_package(OpenMP REQUIRED)
endif()

# MPI
if(USE_MPI)
    find_package(MPI REQUIRED)
endif()

# Sources
add_executable(fem_main
    src/main.cpp
    src/mesh.cpp
    src/assembler.cpp
    src/solver.cpp
)

target_link_libraries(fem_main PRIVATE Eigen3::Eigen)

if(OpenMP_FOUND)
    target_link_libraries(fem_main PRIVATE OpenMP::OpenMP_CXX)
endif()

if(MPI_FOUND)
    target_link_libraries(fem_main PRIVATE MPI::MPI_CXX)
endif()

# Python bindings optionnel
if(BUILD_PYTHON_BINDINGS)
    find_package(pybind11 REQUIRED)
    pybind11_add_module(fem_py python/fem_bindings.cpp src/mesh.cpp src/assembler.cpp src/solver.cpp)
    target_link_libraries(fem_py PRIVATE Eigen3::Eigen)
endif()
