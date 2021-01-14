project(syslog)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/libsystem_asl.tproj/include)

mig(aslcommon/asl_ipc.defs)

create_symlink(
	"${DARLING_ROOT_RELATIVE_TO_SDK}/../../src/external/syslog/aslcommon/asl_ipc.h"
	"${CMAKE_BINARY_DIR}/${DARLING_SDK_RELATIVE_PATH}/usr/include/asl_ipc.h"
)

add_custom_target(syslog_generate_mig_headers
	DEPENDS
		"${CMAKE_CURRENT_BINARY_DIR}/aslcommon/asl_ipc.h"
)

add_darling_object_library(asl_ipc_user
	aslcommon/asl_ipcUser.c
)
make_fat(asl_ipc_user)

add_darling_object_library(asl_ipc_server
	aslcommon/asl_ipcServer.c
)
make_fat(asl_ipc_server)

add_subdirectory(aslcommon)
add_subdirectory(libsystem_asl.tproj)
add_subdirectory(syslogd.tproj)
add_subdirectory(aslmanager.tproj)
add_subdirectory(util.tproj)
