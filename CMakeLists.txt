project(syslog)

mig(aslcommon/asl_ipc.defs)

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
