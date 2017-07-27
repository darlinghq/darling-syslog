project(syslog)

mig(aslcommon/asl_ipc.defs)

add_library(asl_ipc_user OBJECT
	aslcommon/asl_ipcUser.c
)
make_fat(asl_ipc_user)

add_library(asl_ipc_server OBJECT
	aslcommon/asl_ipcServer.c
)
make_fat(asl_ipc_server)

add_subdirectory(aslcommon)
add_subdirectory(libsystem_asl.tproj)
add_subdirectory(syslogd.tproj)
add_subdirectory(aslmanager.tproj)
add_subdirectory(util.tproj)
