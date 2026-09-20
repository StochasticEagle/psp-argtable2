add_library(
    argtable2_example_checks OBJECT
    argcustom.c
    argxxx.c
    callbacks.c
    echo.c
    hasoptvalue.c
    ls.c
    multisyntax.c
    mv.c
    myprog.c
    rm.c
    uname.c
)

target_link_libraries(argtable2_example_checks PRIVATE argtable2)
