cmake_minimum_required (VERSION 3.2)

option(SQLITE_ORM_OMITS_CODECVT "Omits codec testing" OFF)

option(SqliteOrm_SysSqlite "Use system version of sqlite library" OFF)

if(SqliteOrm_SysSqlite)
    message(FATAL_ERROR "WIP: please, disable the SqliteOrm_SysSqlite option.")
else()
    add_subdirectory(third_party/sqlite)
endif()

add_executable(unit_tests tests.cpp tests2.cpp tests3.cpp tests4.cpp tests5.cpp private_getters_tests.cpp pragma_tests.cpp explicit_columns.cpp core_functions_tests.cpp index_tests.cpp constraints/composite_key.cpp static_tests.cpp operators/arithmetic_operators.cpp operators/like.cpp operators/glob.cpp operators/in.cpp operators/cast.cpp operators/is_null.cpp operators/not_operator.cpp operators/bitwise.cpp dynamic_order_by.cpp prepared_statement_tests/select.cpp prepared_statement_tests/get_all.cpp prepared_statement_tests/get_all_pointer.cpp prepared_statement_tests/get_all_optional.cpp prepared_statement_tests/update_all.cpp prepared_statement_tests/remove_all.cpp prepared_statement_tests/get.cpp prepared_statement_tests/get_pointer.cpp prepared_statement_tests/get_optional.cpp prepared_statement_tests/update.cpp prepared_statement_tests/remove.cpp prepared_statement_tests/insert.cpp prepared_statement_tests/replace.cpp prepared_statement_tests/insert_range.cpp prepared_statement_tests/replace_range.cpp prepared_statement_tests/insert_explicit.cpp pragma_tests.cpp simple_query.cpp static_tests/is_bindable.cpp static_tests/arithmetic_operators_result_type.cpp static_tests/tuple_conc.cpp static_tests/node_tuple.cpp static_tests/bindable_filter.cpp static_tests/count_tuple.cpp static_tests/member_traits_tests.cpp static_tests/select_return_type.cpp constraints/default.cpp constraints/unique.cpp constraints/foreign_key.cpp constraints/check.cpp table_tests.cpp statement_serializator_tests/primary_key.cpp statement_serializator_tests/column_names.cpp statement_serializator_tests/autoincrement.cpp statement_serializator_tests/arithmetic_operators.cpp statement_serializator_tests/core_functions.cpp statement_serializator_tests/comparison_operators.cpp statement_serializator_tests/unique.cpp statement_serializator_tests/foreign_key.cpp statement_serializator_tests/collate.cpp statement_serializator_tests/check.cpp statement_serializator_tests/index.cpp statement_serializator_tests/indexed_column.cpp unique_cases/get_all_with_two_tables.cpp unique_cases/prepare_get_all_with_case.cpp unique_cases/index_named_table_with_fk.cpp unique_cases/issue525.cpp unique_cases/delete_with_two_fields.cpp unique_cases/join_iterator_ctor_compilation_error.cpp get_all_custom_containers.cpp select_asterisk.cpp backup_tests.cpp transaction_tests.cpp)


if(SQLITE_ORM_OMITS_CODECVT)
	message(STATUS "SQLITE_ORM_OMITS_CODECVT is enabled")
	target_compile_definitions(unit_tests PRIVATE SQLITE_ORM_OMITS_CODECVT=1)
endif()

target_link_libraries(unit_tests PRIVATE sqlite_orm Catch2::Catch2)

add_test(NAME "All_in_one_unit_test"
    COMMAND unit_tests
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR})
