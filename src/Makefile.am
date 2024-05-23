AM_CPPFLAGS = -I$(top_srcdir)/include -I$(top_srcdir)

AM_CFLAGS = $(GLOBAL_CFLAGS) $(libcurl_CFLAGS) $(libplist_CFLAGS)

AM_LDFLAGS = $(libcurl_LIBS) $(libplist_LIBS)

lib_LTLIBRARIES = libtatsu.la
libtatsu_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(LIBTATSU_SO_VERSION) -no-undefined
libtatsu_la_LIBADD =
libtatsu_la_SOURCES =	\
	tss.c \
	tatsu.c \
	common.h

if WIN32
libtatsu_la_LDFLAGS += -avoid-version -static-libgcc
libtatsu_la_LIBADD += -lws2_32
endif

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = libtatsu-1.0.pc
