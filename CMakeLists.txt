# Minimum Version
cmake_minimum_required(VERSION 2.6)

# Smart Message Language library -- libsml
project(libsml)

# Include Directories
include_directories(./sml/include)


## Shared library
add_library(sml SHARED 
	./sml/src/sml_attention_response.c 
	./sml/src/sml_boolean.c 
	./sml/src/sml_close_request.c 
	./sml/src/sml_close_response.c 
	./sml/src/sml_crc16.c 
	./sml/src/sml_file.c 
	./sml/src/sml_get_list_request.c 
	./sml/src/sml_get_list_response.c 
	./sml/src/sml_get_proc_parameter_request.c 
	./sml/src/sml_get_proc_parameter_response.c 
	./sml/src/sml_get_profile_list_request.c 
	./sml/src/sml_get_profile_list_response.c 
	./sml/src/sml_get_profile_pack_request.c 
	./sml/src/sml_get_profile_pack_response.c 
	./sml/src/sml_list.c 
	./sml/src/sml_open_request.c 
	./sml/src/sml_set_proc_parameter_request.c 
	./sml/src/sml_time.c 
	./sml/src/sml_message.c 
	./sml/src/sml_number.c 
	./sml/src/sml_octet_string.c 
	./sml/src/sml_open_response.c 
	./sml/src/sml_shared.c 
	./sml/src/sml_status.c 
	./sml/src/sml_transport.c 
	./sml/src/sml_tree.c 
	./sml/src/sml_value.c
)

# Link uuid
target_link_libraries(sml uuid)

# Install Lib
install(TARGETS sml LIBRARY DESTINATION lib)

## Example executable
add_executable(sml_server ./examples/sml_server.c)

# Link sml
target_link_libraries(sml_server sml)


## Test executable
add_executable(sml_test ./test/test_main.c
    ./test/unity/unity.c
    ./test/unity/unity_fixture.c
    ./test/src/sml_value_test.c
    ./test/src/sml_buffer_test.c
    ./test/src/test_helper.c
    ./test/src/sml_list_test.c
    ./test/src/sml_tree_test.c
    ./test/src/sml_get_profile_pack_request_test.c
    ./test/src/sml_message_test.c
    ./test/src/sml_time_test.c
    ./test/src/sml_boolean_test.c
    ./test/src/sml_open_request_test.c
    ./test/src/sml_file_test.c
    ./test/src/sml_octet_string_test.c
    ./test/src/sml_status_test.c
    ./test/src/sml_number_test.c
)

# Link sml
target_link_libraries(sml_test sml)

# Add test
enable_testing()
add_test(test_all sml_test)


