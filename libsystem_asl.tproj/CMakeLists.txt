project(libsystem_asl)

cmake_minimum_required(VERSION 2.4.0)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -nostdinc -D__DARWIN_UNIX03 -fPIC -DPRIVATE")
set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -nostdlib")
include_directories(${CMAKE_SOURCE_DIR}/src/libc/darwin)
include_directories(${CMAKE_SOURCE_DIR}/src/external/libdispatch)
include_directories(${CMAKE_SOURCE_DIR}/src/external/libclosure)
include_directories(${CMAKE_SOURCE_DIR}/src/duct/include)
include_directories(${CMAKE_SOURCE_DIR}/src/launchd/liblaunch)
include_directories(${CMAKE_SOURCE_DIR}/src/libinfo/membership.subproj)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

mig(asl_ipc.defs)

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

