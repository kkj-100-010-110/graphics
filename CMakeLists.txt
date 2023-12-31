cmake_minimum_required(VERSION 3.13)

set(PROJECT_NAME opengl_example)
set(CMAKE_CXX_STANDARD 17)
if (APPLE)
    set(CMAKE_CXX_FLAGS "-framework Cocoa -framework IOKit -framework OpenGL")
endif()

set(WINDOW_NAME "OpenGL Example")
set(WINDOW_WIDTH 960)
set(WINDOW_HEIGHT 540)

project(${PROJECT_NAME})
add_executable(${PROJECT_NAME}
    opengl_example/src/main.cpp
    opengl_example/src/common.cpp opengl_example/src/common.h
    opengl_example/src/shader.cpp opengl_example/src/shader.h
    opengl_example/src/program.cpp opengl_example/src/program.h
    opengl_example/src/context.cpp opengl_example/src/context.h
    opengl_example/src/buffer.cpp opengl_example/src/buffer.h
    opengl_example/src/vertex_layout.cpp opengl_example/src/vertex_layout.h
    opengl_example/src/image.cpp opengl_example/src/image.h
    opengl_example/src/texture.cpp opengl_example/src/texture.h
    )

include(Dependency.cmake)

# 우리 프로젝트에 include / lib 관련 옵션 추가
target_include_directories(${PROJECT_NAME} PUBLIC ${DEP_INCLUDE_DIR})
target_link_directories(${PROJECT_NAME} PUBLIC ${DEP_LIB_DIR})
target_link_libraries(${PROJECT_NAME} PUBLIC ${DEP_LIBS})

target_compile_definitions(${PROJECT_NAME} PUBLIC
    WINDOW_NAME="${WINDOW_NAME}"
    WINDOW_WIDTH=${WINDOW_WIDTH}
    WINDOW_HEIGHT=${WINDOW_HEIGHT}
    )

# Dependency들이 먼저 build 될 수 있게 관계 설정
add_dependencies(${PROJECT_NAME} ${DEP_LIST})