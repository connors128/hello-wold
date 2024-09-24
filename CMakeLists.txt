cmake_minimum_required(VERSION 3.22)
project(hello_world)

set(CMAKE_CXX_STANDARD 23)

include(FetchContent)
FetchContent_Declare(
        googletest
        # Specify the commit you depend on and update it regularly.
        URL https://github.com/google/googletest/archive/b514bdc898e2951020cbdca1304b75f5950d1f59.zip
)

# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)
include(GoogleTest)

add_executable(hello_world src/main.cpp)

enable_testing()
add_executable(hello_world_test tests/main.cpp
        tests/src/test_Addition.cpp
        )
target_link_libraries(
        hello_world_test
        gtest_main
)
gtest_discover_tests(hello_world_test)