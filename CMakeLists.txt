cmake_minimum_required (VERSION 3.5)
project(Cpp_Opengl_Setup LANGUAGES C CXX)

set(CMAKE_C_STANDARD 17)
set(CMAKE_C_STANDARD_REQUIRED ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# *.x can not be used in add_executable() and add_custom_command()
file(GLOB SOURCES
    lib/*.c
    hello_hexagonal_star.cpp
)

# Include header files here, don't need to add into add_executable()
include_directories(include)
add_executable(hello_hexagonal_star ${SOURCES})

if(MSVC)
    # In target_link_libraries() must add ${CMAKE_SOURCE_DIR}
    target_link_libraries(hello_hexagonal_star
        ${CMAKE_SOURCE_DIR}/lib/glfw3.lib
    )
elseif(MINGW)
    target_link_libraries(hello_hexagonal_star
        ${CMAKE_SOURCE_DIR}/lib/libglfw3.a
    )
endif()
