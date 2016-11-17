# Look for pciutils
find_package(PCIUTILS REQUIRED)
include_directories(${PCIUTILS_INCLUDE_DIR})
# Look for zlib
find_package(ZLIB REQUIRED)
include_directories(${ZLIB_INCLUDE_DIR})

include_directories(${CMAKE_CURRENT_BINARY_DIR})

set(OUTPUT_BIN "inteltool")

add_library(inteltool_lib
  rootcmplx.c
  powermgt.c
  memory.c
  cpu.c
  gpio.c
  pcie.c
  amb.c
  spi.c
  gfx.c
  ahci.c
  ivy_memory.c
)

add_executable(${OUTPUT_BIN} inteltool.c)
target_link_libraries(${OUTPUT_BIN} inteltool_lib)
target_link_libraries(${OUTPUT_BIN} ${PCIUTILS_LIBRARIES})
target_link_libraries(${OUTPUT_BIN} ${ZLIB_LIBRARIES})

install(TARGETS ${OUTPUT_BIN} DESTINATION sbin)
