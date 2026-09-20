cmake_minimum_required(VERSION 3.20)
project(argtable2 VERSION 2.14 LANGUAGES C)

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
