ADD_LIBRARY(
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

INSTALL(
    TARGETS argtable2
    ARCHIVE DESTINATION lib
)

INSTALL(
    FILES argtable2.h
    DESTINATION include
)

SET_TARGET_PROPERTIES(
    argtable2
    PROPERTIES
        DEBUG_POSTFIX d
)
