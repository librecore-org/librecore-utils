include_directories(${CMAKE_CURRENT_SOURCE_DIR})

set(OUTPUT_BIN "ectool")

add_library(ec_lib
  ec.c
)

add_executable(${OUTPUT_BIN} ectool.c)
target_link_libraries(${OUTPUT_BIN} ec_lib)

install(TARGETS ${OUTPUT_BIN} DESTINATION sbin)
