add_library(
    argtable2 STATIC
    arg_date.c
    arg_dbl.c
    arg_end.c
    arg_file.c
    arg_int.c
    arg_lit.c
    arg_rem.c
    arg_rex.c
    arg_str.c
    argtable2.c
    getopt.c
    getopt1.c
)

target_include_directories(
    argtable2
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
        $<INSTALL_INTERFACE:include>
)

install(
    TARGETS argtable2
    ARCHIVE DESTINATION lib
)

install(
    FILES argtable2.h
    DESTINATION include
)

set_target_properties(
    argtable2
    PROPERTIES
        DEBUG_POSTFIX d
)
