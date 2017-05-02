project(syslog-util)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -nostdinc")

include_directories(
	${CMAKE_SOURCE_DIR}/src/libinfo/gen.subproj
	${CMAKE_SOURCE_DIR}/src/libnotify
	${CMAKE_SOURCE_DIR}/src/launchd/liblaunch
	${CMAKE_SOURCE_DIR}/src/external/syslog/libsystem_asl.tproj/include
	${CMAKE_SOURCE_DIR}/src/external/libdispatch
	${CMAKE_CURRENT_SOURCE_DIR}/../aslcommon
	${CMAKE_CURRENT_BINARY_DIR}/../aslcommon
)

add_definitions(-DPRIVATE)

mig(../aslcommon/asl_ipc.defs)

set(syslog_sources
	syslog.c
	$<TARGET_OBJECTS:aslcommon>
	${CMAKE_CURRENT_BINARY_DIR}/../aslcommon/asl_ipcUser.c
)

add_darling_executable(syslog ${syslog_sources})

install(TARGETS syslog DESTINATION libexec/darling/usr/sin)
install(FILES syslog.1 DESTINATION libexec/darling/usr/share/man/man1)

