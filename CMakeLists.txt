cmake_minimum_required(VERSION 3.28)

project(
    sample_project
    VERSION 1.0
    LANGUAGES C
)

add_executable("${CMAKE_PROJECT_NAME}")
set_target_properties(
    "${CMAKE_PROJECT_NAME}" 
    PROPERTIES
    C_STANDARD 23
)
file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/src/*.c")
target_sources(
    "${CMAKE_PROJECT_NAME}" 
    PRIVATE 
    ${SOURCES}
)
target_include_directories(
    "${CMAKE_PROJECT_NAME}"
    PRIVATE
    "${CMAKE_CURRENT_SOURCE_DIR}/include"
)
target_compile_definitions(
    "${CMAKE_PROJECT_NAME}"
    PRIVATE
    $<$<CONFIG:Debug>:SAMPLE_PROJECT_DEBUG>
    $<$<CONFIG:Release>:SAMPLE_PROJECT_RELEASE>
)
if (MSVC)
    target_compile_options("${CMAKE_PROJECT_NAME}" PRIVATE /Wall /WX)
else()
    target_compile_options("${CMAKE_PROJECT_NAME}" PRIVATE -Wall -Wextra -Wpedantic -Werror)
endif()
