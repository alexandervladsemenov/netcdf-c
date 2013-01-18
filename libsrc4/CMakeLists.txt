SET(CMAKE_INCLUDE_CURRENT_DIR ON)

INCLUDE_DIRECTORIES(".")

# Process these files with m4.

SET(libsrc4_SOURCES nc4dispatch.c nc4attr.c nc4dim.c nc4file.c nc4grp.c nc4type.c nc4var.c ncfunc.c nc4internal.c nc4hdf.c)

IF(LOGGING)
	SET(libsrc4_SOURCES ${libsrc4_SOURCES} error4.c)
ENDIF()

add_library(netcdf4 OBJECT ${libsrc4_SOURCES}) 

###
# Options related to the man page generation.
###

###
# The C API man page.
###

set(man_MANS netcdf.3)

set(ARGS_MANPAGE -DAPI=C)

IF (USE_NETCDF4)
	SET(ARGS_MANPAGE ${ARGS_MANPAGE} -DNETCDF4=TRUE)
ENDIF(USE_NETCDF4)

IF (BUILD_DAP)
	SET(ARGS_MANPAGE ${ARGS_MANPAGE} -DDAP=TRUE)
ENDIF(BUILD_DAP)

IF (BUILD_PARALLEL)
	SET(ARGS_MANPAGE ${ARGS_MANPAGE} -DPARALLEL_IO=TRUE)
ENDIF(BUILD_PARALLEL)


