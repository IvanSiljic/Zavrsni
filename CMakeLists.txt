cmake_minimum_required(VERSION 3.28)
project(Zavrsni)

set(CMAKE_CXX_STANDARD 20)

include_directories(include)

file(GLOB_RECURSE SOURCES src/*.cpp src/glad.c)

add_executable(Zavrsni ${SOURCES}
        include/mesh.h
        include/model.h)

# Platform-specific settings
if(WIN32)
    # Path to GLFW include and lib directories (adjust these paths accordingly)
    include_directories(path_to_glfw_include)
    link_directories(path_to_glfw_lib)

    # Link GLFW and OpenGL for Windows
    set(OpenGlLinkers glfw3 opengl32)
elseif(UNIX AND NOT APPLE)
    find_package(OpenGL REQUIRED)
    find_package(assimp REQUIRED)
    find_package(glfw3 REQUIRED)
    set(OpenGlLinkers glfw ${OPENGL_gl_LIBRARY} assimp)
endif()

# Link GLFW and OpenGL
target_link_libraries(Zavrsni ${OpenGlLinkers})
