# Ensure we have this at the top here.
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_executable("cbmem" cbmem.c)
install(TARGETS "cbmem" DESTINATION sbin)
