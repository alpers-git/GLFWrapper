cmake_minimum_required(VERSION 3.0)
project(GLFWrapper)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Add GLFW as a submodule
add_subdirectory(submodules/glfw)

# Include directories
include_directories(${PROJECT_SOURCE_DIR}/submodules/glfw/include)

# Add your library
add_library(GLFWrapper GLFWrapper.cpp)

# Link GLFW to your library
target_link_libraries(GLFWrapper glfw)
