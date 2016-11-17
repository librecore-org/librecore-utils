include_directories(${CMAKE_CURRENT_SOURCE_DIR})
# WORKAROUND shitty include paths..
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../cbfstool)
# WORKAROUND Googles insaity.
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../cbfstool/vboot_justenough)

# COMMONLIB
add_library(commonlib
#  cbfs.c
#  fsp_relocate.c
  lz4_wrapper.c
  mem_pool.c
  region.c
)
