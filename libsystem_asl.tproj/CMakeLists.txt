project(libsystem_asl)

add_definitions(
	-DPRIVATE
)

mig(../aslcommon/asl_ipc.defs)

set(DYLIB_INSTALL_NAME "/usr/lib/system/libsystem_asl.dylib")
add_circular(system_asl FAT
	SOURCES
		src/asl.c
		src/asl_client.c
		src/asl_core.c
		src/asl_fd.c
		src/asl_file.c
		src/asl_legacy1.c
		src/asl_msg.c
		src/asl_msg_list.c
		src/asl_object.c
		src/asl_store.c
		src/asl_string.c
		src/asl_util.c
		src/syslog.c
		${CMAKE_CURRENT_BINARY_DIR}/../aslcommon/asl_ipcUser.c
	OBJECTS
		$<TARGET_OBJECTS:aslcommon>
	SIBLINGS
		system_c
		system_kernel
		system_info
		libdispatch_shared
		system_malloc
		launch
		platform
		system_blocks
		compiler_rt
		system_notify
		system_pthread
		system_duct
		system_dyld
		xpc
)

install(TARGETS system_asl DESTINATION libexec/darling/usr/lib/system)
