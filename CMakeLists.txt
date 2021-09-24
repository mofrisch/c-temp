cmake_minimum_required(VERSION 3.0.0)
project(c-temp VERSION 0.1.0)

include(CTest)
enable_testing()
find_package(GTest REQUIRED)
include(GoogleTest)
add_executable(tests src/sample1.cc tests/test.cpp)
target_link_libraries(tests GTest::GTest GTest::Main)
# gtest_discover_tests(tests)
set_target_properties(tests PROPERTIES
    CXX_STANDARD 14
    CXX_STANDARD_REQUIRED ON
    CXX_EXTENSIONS OFF
)

add_executable(c-temp main.cpp)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
