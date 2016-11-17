cmake_minimum_required(VERSION 2.8)

# Project details.
project(librecore-utils)

SET(${PROJECT_NAME}_MAJOR_VERSION 0)
SET(${PROJECT_NAME}_MINOR_VERSION 1)
SET(${PROJECT_NAME}_PATCH_LEVEL 0)

# Add local repository for FindXXX.cmake modules.
SET(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake/modules/" ${CMAKE_MODULE_PATH})

###############
# RPM Packaging
###############
SET(VERSION "1.0.0")
set(CPACK_PACKAGE_VERSION ${VERSION})
set(CPACK_GENERATOR "TGZ;RPM;DEB")
set(CPACK_PACKAGE_NAME ${PROJECT_NAME})
set(CPACK_PACKAGE_RELEASE 1)
set(CPACK_PACKAGE_CONTACT "Edward O'Callaghan")
set(CPACK_PACKAGE_VENDOR "librecore")
set(CPACK_PACKAGE_URL "librecore.org")
set(CPACK_RPM_PACKAGE_LICENSE "GPL 2.0")
set(CPACK_RPM_PACKAGE_GROUP "User Interface/Desktops")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "The librecore firmware support utils")
set(CPACK_RPM_PACKAGE_DESCRIPTION "The librecore utils project contains all the supporting
userland components for both developers and users alike.")
set(CPACK_PACKAGING_INSTALL_PREFIX ${CMAKE_INSTALL_PREFIX})
set(CPACK_PACKAGE_FILE_NAME "${CPACK_PACKAGE_NAME}-${CPACK_PACKAGE_VERSION}-${CPACK_PACKAGE_RELEASE}.${CMAKE_SYSTEM_PROCESSOR}")
include(CPack)

# Add main target.
add_subdirectory(inteltool)
add_subdirectory(ectool)
