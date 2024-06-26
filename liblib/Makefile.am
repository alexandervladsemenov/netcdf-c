## This is a automake file, part of Unidata's netCDF package.
# Copyright 2018, see the COPYRIGHT file for more information.

# This Makefile assembles the correct libnetcdf based on various
# configure flags. It is assumed that all the relevant convenience
# libraries have been built (e.g. libsrc, libsrc4, libncdap3, libcdmr,
# libncdap4, fortran).

# Put together AM_CPPFLAGS and AM_LDFLAGS.
include $(top_srcdir)/lib_flags.am

# This is our output, the netcdf library the user will install.
lib_LTLIBRARIES = libnetcdf.la

##
# These linker flags specify libtool version info.
# See http://www.gnu.org/software/libtool/manual/libtool.html#Libtool-versioning
# for information regarding incrementing `-version-info`.
##

libnetcdf_la_LDFLAGS = -version-info @netCDF_SO_VERSION@ ${NOUNDEFINED}

libnetcdf_la_CPPFLAGS = ${AM_CPPFLAGS}
libnetcdf_la_LIBADD =
CLEANFILES =

# The v2 API...
if BUILD_V2
libnetcdf_la_LIBADD += ${top_builddir}/libdispatch/libnetcdf2.la
endif # BUILD_V2

# The output library will always include netcdf3 and dispatch
# libraries
libnetcdf_la_LIBADD += ${top_builddir}/libdispatch/libdispatch.la	\
			${top_builddir}/libsrc/libnetcdf3.la

# + PnetCDF
if USE_PNETCDF
AM_CPPFLAGS += -I${top_srcdir}/libsrcp
libnetcdf_la_LIBADD += ${top_builddir}/libsrcp/libnetcdfp.la
endif # USE_PNETCDF

# + hdf5
if USE_HDF5
AM_CPPFLAGS += -I${top_srcdir}/libhdf5
libnetcdf_la_LIBADD += ${top_builddir}/libhdf5/libnchdf5.la
endif # USE_HDF5

# + hdf4
if USE_HDF4
AM_CPPFLAGS += -I${top_srcdir}/libhdf4
libnetcdf_la_LIBADD += ${top_builddir}/libhdf4/libnchdf4.la
endif # USE_HDF4

# + dap
if NETCDF_ENABLE_DAP
AM_CPPFLAGS += -I${top_srcdir}/libdap2 -I${top_srcdir}/oc
libnetcdf_la_LIBADD += ${top_builddir}/libdap2/libdap2.la
libnetcdf_la_LIBADD += ${top_builddir}/oc2/liboc.la
endif # NETCDF_ENABLE_DAP

if NETCDF_ENABLE_DAP4
AM_CPPFLAGS += -I${top_srcdir}/libdap4
libnetcdf_la_LIBADD += ${top_builddir}/libdap4/libdap4.la
endif # NETCDF_ENABLE_DAP4

AM_CPPFLAGS += -I${top_srcdir}/libncxml
if NETCDF_ENABLE_DAP4
libnetcdf_la_LIBADD += ${top_builddir}/libncxml/libncxml.la
else
if NETCDF_ENABLE_S3_INTERNAL
libnetcdf_la_LIBADD += ${top_builddir}/libncxml/libncxml.la
endif
endif # NETCDF_ENABLE_S3_INTERNAL || NETCDF_ENABLE_DAP4

# NetCDF-4 ...
if USE_NETCDF4
AM_CPPFLAGS += -I${top_srcdir}/libsrc4
libnetcdf_la_LIBADD += ${top_builddir}/libsrc4/libnetcdf4.la
endif #USE_NETCDF4

if NETCDF_ENABLE_NCZARR
AM_CPPFLAGS += -I${top_srcdir}/libnczarr
libnetcdf_la_LIBADD += ${top_builddir}/libnczarr/libnczarr.la
if NETCDF_ENABLE_S3_AWS
libnetcdf_la_LIBADD += ${aws_cpp_sdk_core_LIBS} ${aws_cpp_sdk_s3_LIBS}
endif
endif #NETCDF_ENABLE_NCZARR

if NETCDF_ENABLE_PLUGINS
AM_CPPFLAGS += -I${top_srcdir}/libncpoco
libnetcdf_la_LIBADD += ${top_builddir}/libncpoco/libncpoco.la
endif #NETCDF_ENABLE_PLUGINS

if ISCYGWIN
# Force binary mode for file read/write
AM_LDFLAGS += -lbinmode
endif

# We need at least one source file
libnetcdf_la_SOURCES = nc_initialize.c
EXTRA_DIST=CMakeLists.txt
