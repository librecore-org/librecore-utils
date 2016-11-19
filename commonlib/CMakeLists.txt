include_directories(${CMAKE_CURRENT_SOURCE_DIR})

# COMMONLIB
add_library(commonlib
  fsp_relocate_stub.c
  lz4_wrapper.c
  mem_pool.c
  region.c
)
