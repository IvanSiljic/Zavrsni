cmake_minimum_required(VERSION 3.28)
project(Zavrsni)

set(CMAKE_CXX_STANDARD 20)

include_directories(include)

file(GLOB_RECURSE SOURCES src/*.cpp src/glad.c)

file(GLOB_RECURSE HEADERS include/*.h)

add_executable(Zavrsni ${SOURCES} ${HEADERS})

# Platform-specific settings
if(WIN32)
    set(OpenGlLinkers glfw3 opengl32)
    include_directories(path_to_glfw_include)
    link_directories(path_to_glfw_lib)
elseif(UNIX AND NOT APPLE)
    find_package(OpenGL REQUIRED)
    set(OpenGlLinkers glfw ${OPENGL_gl_LIBRARY})
endif()

# Link GLFW and OpenGL
target_link_libraries(Zavrsni ${OpenGlLinkers})
