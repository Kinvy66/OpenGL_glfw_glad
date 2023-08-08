# OpenGL+GLFW+GLAD template Project for clion


## 环境
Windows10, Clion
编译器(以下均测试通过)：
- WSL2-Ubuntu20
- VS2022

## Cmake

```cmake
cmake_minimum_required(VERSION 3.16)
project(OpenGL_glfw_glad LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# glad
set(GLAD_DIR lib/glad)
list(APPEND INCLUDE_DIR ${GLAD_DIR}/include)

# glfw
set(GLFW_DIR lib/glfw)
option(GLFW_BUILD_EXAMPLES "Build the GLFW example programs" OFF)
option(GLFW_BUILD_TESTS "Build the GLFW test programs" OFF)
option(GLFW_BUILD_DOCS "Build the GLFW documentation" OFF)
option(GLFW_INSTALL "Generate installation target" OFF)
option(GLFW_DOCUMENT_INTERNALS "Include internals in documentation" OFF)
add_subdirectory(${GLFW_DIR} lib EXCLUDE_FROM_ALL)

list(APPEND INCLUDE_DIR ${GLFW_DIR}/include)
list(APPEND INCLUDE_DIR ${GLFW_DIR}/deps)

list(APPEND LINK_LIBS glfw)

list(APPEND OPENGL_SOURCE
        ${GLAD_DIR}/src/glad.c
        src/OpenGLDemo.cpp)
add_executable(OpenGLDemo ${OPENGL_SOURCE})
target_include_directories(OpenGLDemo PUBLIC ${INCLUDE_DIR})
target_link_libraries(OpenGLDemo PUBLIC ${LINK_LIBS})

```

## 参考
- https://www.bilibili.com/video/BV11R4y1q7tZ