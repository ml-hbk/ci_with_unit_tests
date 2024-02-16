cmake_minimum_required(VERSION 3.25)

project(ci_with_unit_test VERSION 2.0.1 LANGUAGES CXX)


option(BUILD_TESTS "Have unit tests build" OFF)

include(FetchContent)

add_executable(
    hello
    main.cpp
)


if(BUILD_TESTS)
    FetchContent_Declare(
        googletest
        URL https://github.com/google/googletest/archive/v1.12.0.zip
    )

    set(INSTALL_GTEST OFF)
    FetchContent_MakeAvailable(googletest)

    enable_testing()

    add_executable(
        hello_test
        test.cpp
    )

    target_link_libraries(hello_test GTest::gtest GTest::gtest_main) 

    add_test(NAME hello_test COMMAND hello_test
        --report_level=no
        --log_level=all
    )
endif()
