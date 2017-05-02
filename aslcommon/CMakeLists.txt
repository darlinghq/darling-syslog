project(aslcommon)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -nostdinc")

include_directories(
	${CMAKE_SOURCE_DIR}/src/libinfo/gen.subproj
	${CMAKE_CURRENT_SOURCE_DIR}/../libsystem_asl.tproj/include
	${CMAKE_SOURCE_DIR}/src/external/libdispatch
)

mig(asl_ipc.defs)

add_library(aslcommon OBJECT
	asl_common.c
	asl_memory.c
)
make_fat(aslcommon)

