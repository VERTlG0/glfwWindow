cmake_minimum_required(VERSION 3.9)

#set(CMAKE_C_COMPILER "gcc-8.2")
#set(CMAKE_CXX_COMPILER "/usr/bin/g++-8")

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

project(glfwWindow)

find_package(glfw3 3.2 REQUIRED)
find_package(GLEW 2.1 REQUIRED)
find_package(OpenGL REQUIRED)

add_executable(glfwWindow main.cpp)

if (UNIX)
    target_include_directories(glfwWindow PUBLIC 
            ${OPENGL_INCLUDE_DIR}
            ${GLFW_INCLUDE_DIR}
            ${glew_INCLUDE_DIR})
            
    target_link_libraries(glfwWindow 
            ${OPENGL_gl_LIBRARY}
            ${GLFW3_LIBRARY} glfw 
            ${GLEW_LIBRARY} GL GLU GLEW
            GLEW::GLEW)
endif (UNIX)

if (WIN32)
    target_link_libraries (glfwWindow
        ${OPENGL_LIBRARIES} glfw3 glew32s glu32 opengl32)
endif(WIN32)

install(TARGETS glfwWindow RUNTIME DESTINATION bin)
