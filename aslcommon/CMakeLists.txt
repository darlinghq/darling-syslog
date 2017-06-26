project(aslcommon)

add_compile_options(
	-nostdinc
)

# mig(asl_ipc.defs)

add_library(aslcommon OBJECT
	asl_common.c
	asl_memory.c
)
make_fat(aslcommon)
