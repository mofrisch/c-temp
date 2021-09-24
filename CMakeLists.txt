cmake_minimum_required(VERSION 3.21)

# The project itself
get_filename_component(my_project ${CMAKE_CURRENT_SOURCE_DIR} NAME)
project(${my_project})
add_executable(${my_project} main.c)
target_compile_options(${my_project} PRIVATE -std=c17 -Wall -Wextra -pedantic -Werror)

# CTest and Google Test
include(CTest)
enable_testing()
find_package(GTest REQUIRED)
include(GoogleTest)
add_executable(tests src/sample1.cc tests/test.cpp)
target_link_libraries(tests GTest::GTest GTest::Main)
set_target_properties(tests PROPERTIES
    CXX_STANDARD 11
    CXX_STANDARD_REQUIRED ON
    CXX_EXTENSIONS OFF
)

# Google benchmark
add_executable(bench bench/main.cpp)
find_package(benchmark REQUIRED)
target_link_libraries(bench PRIVATE benchmark::benchmark)
set_target_properties(bench PROPERTIES
    CXX_STANDARD 11
    CXX_STANDARD_REQUIRED ON
    CXX_EXTENSIONS OFF
)


# CPack
set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)

