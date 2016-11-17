include_directories(${CMAKE_CURRENT_SOURCE_DIR})

# FMAP
add_library(flashmap_lib
  fmap.c
  kv_pair.c
  valstr.c
)
