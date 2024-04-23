cmake_minimum_required(VERSION 3.0)
project(GLFWrapper)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# if linux
if(UNIX)
  find_package(SDL2 REQUIRED)
endif()
find_package(OpenGL REQUIRED)

# Add GLFW as a submodule
add_subdirectory(submodules/glfw)

# Include directories
include_directories(${PROJECT_SOURCE_DIR}/submodules/glfw/include)

# Add your library
add_library(GLFWrapper
    GLFWrapper.h
    GLFWrapper.cpp)

# Link GLFW and OpenGL to your library
target_link_libraries(GLFWrapper PRIVATE glfw OpenGL::GL)

# Include directories for GLFW and OpenGL
target_include_directories(GLFWrapper PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/submodules/glfw/include
    ${OPENGL_INCLUDE_DIR} # assuming OpenGL package has been found
)

# Add platform-specific dependencies
if(UNIX)
    find_package(SDL2 REQUIRED)
    target_link_libraries(GLFWrapper PRIVATE ${SDL2_LIBRARIES})
    target_include_directories(GLFWrapper PRIVATE ${SDL2_INCLUDE_DIRS})
endif()
