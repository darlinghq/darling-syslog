project(syslog-util)

add_compile_options(
	-nostdinc
)

include_directories(
	${CMAKE_CURRENT_SOURCE_DIR}/../aslcommon
	${CMAKE_CURRENT_BINARY_DIR}/../aslcommon
)

add_definitions(
	-DPRIVATE
)

set(syslog_sources
	syslog.c
	$<TARGET_OBJECTS:aslcommon>
	$<TARGET_OBJECTS:asl_ipc_user>
)

add_darling_executable(syslog ${syslog_sources})

install(TARGETS syslog DESTINATION libexec/darling/usr/bin)
install(FILES syslog.1 DESTINATION libexec/darling/usr/share/man/man1)
