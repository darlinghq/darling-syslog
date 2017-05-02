project(aslmanager)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -nostdinc")

include_directories(
	${CMAKE_SOURCE_DIR}/src/libinfo/gen.subproj
	${CMAKE_SOURCE_DIR}/src/libnotify
	${CMAKE_SOURCE_DIR}/src/launchd/liblaunch
	${CMAKE_SOURCE_DIR}/src/external/syslog/libsystem_asl.tproj/include
	${CMAKE_SOURCE_DIR}/src/external/libdispatch
	${CMAKE_SOURCE_DIR}/src/copyfile
	${CMAKE_CURRENT_SOURCE_DIR}/../aslcommon
)

add_definitions(-DPRIVATE)

set(aslmanager_sources
	aslmanager.c
	#cache_delete.c
	daemon.c
	$<TARGET_OBJECTS:aslcommon>
)

add_darling_executable(aslmanager ${aslmanager_sources})
target_link_libraries(aslmanager z)

install(TARGETS aslmanager DESTINATION libexec/darling/usr/sbin)
install(FILES aslmanager.8 DESTINATION libexec/darling/usr/share/man/man8)
install(FILES com.apple.aslmanager.plist DESTINATION libexec/darling/System/Library/LaunchDaemons)

