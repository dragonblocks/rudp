cmake_minimum_required(VERSION 3.14)
project(Rudp)

add_compile_options(
	-Wall
)

if("${CMAKE_BUILD_TYPE}" STREQUAL "Debug")
	add_compile_definitions("_DEBUG")
endif()

add_library(rudp
	rudp.c
	platform_adpt.c
	crc32.c
)

target_link_libraries(rudp
	pthread
	rt
)
target_include_directories(rudp
	PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}
)

add_executable(nblk_svr nblk_svr.c)
target_link_libraries(nblk_svr rudp)

add_executable(rudpsvr rudpsvr.c)
target_link_libraries(rudpsvr rudp)

add_executable(rudpclt rudpclt.c)
target_link_libraries(rudpclt rudp)

add_executable(simulconn simulconn.c)
target_link_libraries(simulconn rudp)

# add_executable(punch rudp_punch.c)
# target_link_libraries(punch rudp)

add_executable(rudpsels rudpsels.c)
target_link_libraries(rudpsels rudp)

add_executable(rudpsel rudpsel.c)
target_link_libraries(rudpsel rudp)

add_executable(rudpselc rudpselc.c)
target_link_libraries(rudpselc rudp)
