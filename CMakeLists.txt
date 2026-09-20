cmake_minimum_required(VERSION 3.20)
project(argtable2 VERSION 2.14 LANGUAGES C)

option(ARGTABLE2_BUILD_TESTS "Build PSP test executables" OFF)
option(ARGTABLE2_CHECK_EXAMPLES "Compile programming examples for validation" OFF)

configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/argtable2.pc.in"
    "${CMAKE_CURRENT_BINARY_DIR}/argtable2.pc"
    @ONLY
)

install(
    FILES "${CMAKE_CURRENT_BINARY_DIR}/argtable2.pc"
    DESTINATION lib/pkgconfig
)

add_subdirectory(src)

if(ARGTABLE2_BUILD_TESTS)
    add_subdirectory(tests)
endif()

if(ARGTABLE2_CHECK_EXAMPLES)
    add_subdirectory(example)
endif()
