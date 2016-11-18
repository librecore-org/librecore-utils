# Ensure we have this at the top here.
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

## Look for bison && flex
find_package(BISON REQUIRED)
find_package(FLEX REQUIRED)

BISON_TARGET(blobtool_parser blobtool.y  ${CMAKE_CURRENT_BINARY_DIR}/blobtool_parser.c
		DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/blobtool_parser.h)
FLEX_TARGET(blobtool_lexer blobtool.l ${CMAKE_CURRENT_BINARY_DIR}/blobtool_lexer.c
		DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/blobtool_lexer.h)
ADD_FLEX_BISON_DEPENDENCY(blobtool_lexer blobtool_parser)

# generated blobtool_parser.h && blobtool_lexer.h by-products include path
include_directories(${CMAKE_CURRENT_BINARY_DIR})
##

add_executable("blobtool"
  # blobtool_parser.c
  # blobtool_lexer.c
  ${BISON_blobtool_parser_OUTPUTS} ${FLEX_blobtool_lexer_OUTPUTS}
)
install(TARGETS "blobtool" DESTINATION sbin)
install(FILES "gbe-ich9m.spec" DESTINATION share/doc/blobtool/examples)
install(FILES "gbe-ich9m.set" DESTINATION share/doc/blobtool/examples)
install(FILES "ifd-x200.spec" DESTINATION share/doc/blobtool/examples)
install(FILES "ifd-x200.set" DESTINATION share/doc/blobtool/examples)
