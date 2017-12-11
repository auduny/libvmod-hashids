AM_CPPFLAGS = @VMOD_INCLUDES@ -Wall -Werror

vmoddir = @VMOD_DIR@
vmod_LTLIBRARIES = libvmod_hashids.la

libvmod_hashids_la_LDFLAGS = -module -export-dynamic -avoid-version -shared

libvmod_hashids_la_SOURCES = \
	vmod_hashids.c

nodist_libvmod_hashids_la_SOURCES = \
	vcc_if.c \
	vcc_if.h

vmod_hashids.lo: vcc_if.c vcc_if.h

vcc_if.c: vcc_if.h

vcc_if.h: @VMODTOOL@ $(top_srcdir)/src/vmod_hashids.vcc
	@VMODTOOL@ $(top_srcdir)/src/vmod_hashids.vcc

VMOD_TESTS = $(top_srcdir)/src/tests/*.vtc
.PHONY: $(VMOD_TESTS)

$(top_srcdir)/src/tests/*.vtc: libvmod_hashids.la
	@VARNISHTEST@ -Dvarnishd=@VARNISHD@ -Dvmod_topbuild=$(abs_top_builddir) $@

check: $(VMOD_TESTS)

EXTRA_DIST = \
	vmod_hashids.vcc \
	$(VMOD_TESTS)

CLEANFILES = \
	$(builddir)/vcc_if.c \
	$(builddir)/vcc_if.h \
	$(builddir)/vmod_hashids.rst \
	$(builddir)/vmod_hashids.man.rst
