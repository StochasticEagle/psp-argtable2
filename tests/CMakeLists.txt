set(ARGTABLE2_TEST_TARGETS
    fntests
    test_date
    test_dbl
    test_file
    test_int
    test_lit
    test_rex
)

foreach(test_target IN LISTS ARGTABLE2_TEST_TARGETS)
    add_executable(${test_target} ${test_target}.c)
    target_link_libraries(${test_target} PRIVATE argtable2)
endforeach()
