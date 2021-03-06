# Copyright © 2014 Cisco Systems, Inc.  All rights reserved.
# Copyright © 2014      University of Wisconsin-La Crosse.
#                         All rights reserved.
#
# See COPYING in top-level directory.
#
# $HEADER$
#

DIST_SUBDIRS = jansson

if BUILD_NETLOC
SUBDIRS = jansson

AM_CPPFLAGS = \
        $(JANSSON_CPPFLAGS) \
        $(NETLOC_CPPFLAGS) \
        $(HWLOC_CPPFLAGS)

# If we're in standalone mode, build the installable library.
# Otherwise, build the embedded library.

if HWLOC_BUILD_STANDALONE
lib_LTLIBRARIES = libnetloc.la
else
noinst_LTLIBRARIES = libnetloc_embedded.la
endif

sources = \
        support.h \
        topology.c \
        metadata.c \
        api.c \
        support.c \
        data_types.c \
        data_collect.c \
        pathfinder.c \
        lookup_table.c \
        export.c \
        map.c

ldflags = $(JANSSON_LDFLAGS)

# Installable library

libnetloc_la_SOURCES = $(sources)
libnetloc_la_LDFLAGS = $(ldflags) -version-info $(libnetloc_so_version)
libnetloc_la_LIBADD = \
        $(top_builddir)/hwloc/libhwloc.la \
        $(JANSSON_LIBS)

# Embedded library (note the lack of a .so version number -- that
# intentionally only appears in the installable library).  Also note
# the lack of _LDFLAGS -- all libs are added by the upper layer (via
# HWLOC_EMBEDDED_LIBS).

libnetloc_embedded_la_SOURCES = $(sources)
libnetloc_embedded_la_LDFLAGS = $(ldflags)
libnetloc_embedded_la_LIBADD = \
        $(HWLOC_top_builddir)/hwloc/libhwloc_embedded.la \
        $(JANSSON_LIBS)

endif BUILD_NETLOC
