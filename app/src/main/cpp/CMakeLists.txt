cmake_minimum_required(VERSION 3.22.1)
project(GroveApp)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(ANDROID)
    add_definitions(-DCINDER_ANDROID=1)
    add_definitions(-DCINDER_GL_ES_3=1)
endif()

file(GLOB SOURCES 
    "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/**/*.cpp"
)

add_library(${PROJECT_NAME} SHARED ${SOURCES})

target_link_libraries(${PROJECT_NAME}
    android
    GLESv3
    EGL
    log
)
