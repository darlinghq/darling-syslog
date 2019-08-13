project(aslcommon)

add_compile_options(
	-nostdinc
)

add_darling_object_library(aslcommon
	asl_common.c
	asl_memory.c
)
make_fat(aslcommon)
