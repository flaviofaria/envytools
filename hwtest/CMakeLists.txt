project(ENVYTOOLS C)
cmake_minimum_required(VERSION 2.6)

find_package(PkgConfig REQUIRED)
pkg_check_modules(PC_PCIACCESS pciaccess)

if (PC_PCIACCESS_FOUND)

add_executable(hwtest hwtest.c common.c vram.c nv01_pgraph.c nv10_tile.c nv50_ptherm.c nv84_ptherm.c)
target_link_libraries(hwtest nva nvhw m)

install(TARGETS hwtest
	RUNTIME DESTINATION bin
	LIBRARY DESTINATION lib${LIB_SUFFIX}
	ARCHIVE DESTINATION lib${LIB_SUFFIX})

else(PC_PCIACCESS_FOUND)
	message("Warning: hwtest won't be built because of un-met dependencies (pciaccess)")
endif(PC_PCIACCESS_FOUND)
