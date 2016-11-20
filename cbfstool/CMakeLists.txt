# Ensure we have this at the top here.
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

# WORKAROUND Googles insaity.
include_directories(vbootstub)
add_subdirectory(vbootstub)

add_subdirectory(lzma)
add_subdirectory(lz4)
add_subdirectory(flashmap)

## Look for bison && flex
find_package(BISON REQUIRED)
find_package(FLEX REQUIRED)

BISON_TARGET(fmd_parser fmd_parser.y  ${CMAKE_CURRENT_BINARY_DIR}/fmd_parser.c
		DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/fmd_parser.h)
FLEX_TARGET(fmd_scanner fmd_scanner.l ${CMAKE_CURRENT_BINARY_DIR}/fmd_scanner.c
		DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/fmd_scanner.h)
ADD_FLEX_BISON_DEPENDENCY(fmd_scanner fmd_parser)

# generated fmd_parser.h && fmd_scanner.h by-products include path
include_directories(${CMAKE_CURRENT_BINARY_DIR})
##

add_library(common_lib
  common.c
  rmodule.c
  elfheaders.c
  xdr.c
)

# rmodtool: $(objutil)/cbfstool/rmodtool
add_executable("rmodtool" rmodtool.c)
target_link_libraries("rmodtool" common_lib)
install(TARGETS "rmodtool" DESTINATION sbin)

# fmaptool: $(objutil)/cbfstool/fmaptool
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/flashmap)
add_library(fmap_lib
  cbfs_sections.c
  fmap_from_fmd.c
  fmd.c

  # fmd_parser.c
  # fmd_scanner.c
  ${BISON_fmd_parser_OUTPUTS} ${FLEX_fmd_scanner_OUTPUTS}
)
add_executable("fmaptool" fmaptool.c)
target_link_libraries("fmaptool" flashmap_lib fmap_lib)
install(TARGETS "fmaptool" DESTINATION sbin)

# ifwitool: $(objutil)/cbfstool/ifwitool
add_executable("ifwitool" ifwitool.c)
target_link_libraries("ifwitool" common_lib)
install(TARGETS "ifwitool" DESTINATION sbin)

# cbfstool: $(objutil)/cbfstool/cbfstool
add_library(cbfs_lib
  compress.c
  cbfs_image.c
  cbfs-mkstage.c
  cbfs-mkpayload.c
  fit.c
  partitioned_file.c
# linux as payload
  linux_trampoline.c
  cbfs-payload-linux.c
)

add_executable("cbfstool" cbfstool.c)
target_link_libraries("cbfstool" cbfs_lib)
target_link_libraries("cbfstool" common_lib)
target_link_libraries("cbfstool" flashmap_lib)
target_link_libraries("cbfstool" fmap_lib)
target_link_libraries("cbfstool" lzma_lib)
target_link_libraries("cbfstool" lz4_lib)
target_link_libraries("cbfstool" vbootstub_lib)
target_link_libraries("cbfstool" commonlib)
install(TARGETS "cbfstool" DESTINATION sbin)
