option(CodeCoverage "CodeCoverage" ON)
set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/tests/cmake/modules/)

# Configure google-test as a downloadable library.
include(External_GTest.cmake)


add_executable(math_test
        ${PROJECT_SOURCE_DIR}/tests/src/math_test.cpp
        ${PROJECT_SOURCE_DIR}/src/functions.cpp
        )

target_link_libraries(math_test
        gtest gtest_main
        )

# Tell ctest about my tests
include(GoogleTest)
gtest_add_tests(
        TARGET math
        TEST_LIST math_test
)

# set each target to timeout if not finished within 10 sec
set_tests_properties(${myTests_targets} PROPERTIES TIMEOUT 10)

if (CodeCoverage MATCHES ON)
    set(CMAKE_CXX_FLAGS "-O0 -g -fprofile-arcs -ftest-coverage ")
    include(CodeCoverage)
    setup_target_for_coverage(math_test_coverage math_test coverage)
endif ()
