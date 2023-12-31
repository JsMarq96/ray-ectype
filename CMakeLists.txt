cmake_minimum_required(VERSION 3.21)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

project(ectype)

file(GLOB H_SOURCES "src/*.h")
file(GLOB CPP_SOURCES "src/*.cpp")
file(GLOB C_SOURCES "src/*.c")
file(GLOB SUBFOLDER_H_SOURCES "src/*/*.h")
file(GLOB SUBFOLDER_CPP_SOURCES "src/*/*.cpp")
file(GLOB SUBFOLDER_C_SOURCES "src/*/*.c")

# ImGUI
include_directories(libraries/imgui/)
include_directories(libraries/imgui/backends/)
set(IMGUI_IMPL_SRC libraries/imgui/backends/imgui_impl_glfw.cpp 
                   libraries/imgui/backends/imgui_impl_opengl3.cpp)
file(GLOB IMGUI_SRC "libraries/imgui/*.cpp")

add_executable(ectype ${IMGUI_IMPL_SRC} ${IMGUI_SRC} ${C_SOURCES} ${CPP_SOURCES} ${H_SOURCES} ${SUBFOLDER_H_SOURCES} ${SUBFOLDER_C_SOURCES} ${SUBFOLDER_CPP_SOURCES})

target_compile_options(ectype PRIVATE -pthread)
set_target_properties(ectype PROPERTIES OUTPUT_NAME "ectype")

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_INSTALL OFF CACHE BOOL "" FORCE)
add_subdirectory(libraries/glfw)

add_subdirectory(libraries/gl3w)

add_subdirectory(libraries/glm)

target_link_libraries(ectype glm glfw gl3w)