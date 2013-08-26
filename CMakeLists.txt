project(nphys-data)
cmake_minimum_required(VERSION 2.8.6)

set(CMAKE_INCLUDE_CURRENT_DIR TRUE)
add_subdirectory(src)

# Set package information
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "MIME types and icons for Klusters, Neuroscope and NDManager")
set(CPACK_PACKAGE_NAME "nphys-data" )
set(CPACK_PACKAGE_VERSION_MAJOR "2")
set(CPACK_PACKAGE_VERSION_MINOR "0")
SET(CPACK_PACKAGE_VERSION_PATCH "0")
set(CPACK_PACKAGE_VERSION "${CPACK_PACKAGE_VERSION_MAJOR}.${CPACK_PACKAGE_VERSION_MINOR}.${CPACK_PACKAGE_VERSION_PATCH}")
set(CPACK_PACKAGE_INSTALL_DIRECTORY "nphys-data")

# Determine distribution and release
execute_process(COMMAND lsb_release -si OUTPUT_VARIABLE DISTRIBUTION OUTPUT_STRIP_TRAILING_WHITESPACE)
execute_process(COMMAND lsb_release -sc OUTPUT_VARIABLE RELEASE OUTPUT_STRIP_TRAILING_WHITESPACE)

# Set package name and type (deb vs rpm)
if(DISTRIBUTION STREQUAL "Ubuntu")

  # Set Debian-specific information (see http://www.cmake.org/Wiki/CMake:CPackPackageGenerators)
  set(CPACK_DEBIAN_PACKAGE_ARCHITECTURE "all")
  set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Michaël Zugaro")
  set(CPACK_DEBIAN_PACKAGE_SECTION "Science")
  set(CPACK_DEBIAN_PACKAGE_RECOMMENDS "klusters, neuroscope, ndmanager")
  set(CPACK_DEBIAN_PACKAGE_HOMEPAGE "http://klusters.sourceforge.net")
  set(CPACK_GENERATOR "DEB")
  set(CPACK_PACKAGE_FILE_NAME ${CPACK_PACKAGE_NAME}_${CPACK_PACKAGE_VERSION}-${RELEASE}_${CPACK_DEBIAN_PACKAGE_ARCHITECTURE})
  set(CPACK_DEBIAN_PACKAGE_CONTROL_EXTRA "${CMAKE_CURRENT_SOURCE_DIR}/postinst;${CMAKE_CURRENT_SOURCE_DIR}/postrm;" )

elseif(DISTRIBUTION MATCHES "openSUSE.*")

  # Set openSUSE-specific information (see http://www.cmake.org/Wiki/CMake:CPackPackageGenerators)
  set(CPACK_RPM_PACKAGE_ARCHITECTURE "noarch")
  set(CPACK_PACKAGE_CONTACT "Michaël Zugaro")
  set(CPACK_RPM_PACKAGE_GROUP "Science")
  set(CPACK_RPM_PACKAGE_LICENSE "GPL")		
  set(CPACK_RPM_PACKAGE_SUGGESTS "klusters, neuroscope, ndmanager")
  set(CPACK_RPM_PACKAGE_URL "http://klusters.sourceforge.net")
  set(CPACK_GENERATOR "RPM")
  set(CPACK_PACKAGE_FILE_NAME ${CPACK_PACKAGE_NAME}-${CPACK_PACKAGE_VERSION}-${RELEASE}.${CPACK_RPM_PACKAGE_ARCHITECTURE})
  set(CPACK_RPM_POST_INSTALL_SCRIPT_FILE "${CMAKE_CURRENT_SOURCE_DIR}/postinst")
  set(CPACK_RPM_POST_UNINSTALL_SCRIPT_FILE "${CMAKE_CURRENT_SOURCE_DIR}/postrm")

endif()

include(CPack)
