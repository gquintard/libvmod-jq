AM_CFLAGS = $(VCACHEAPI_CFLAGS)

TESTS_ENVIRONMENT = PATH=$(VCACHE_BINDIR):$(VCACHE_SBINDIR):$$PATH

vmod_LTLIBRARIES = libvmod_jq.la

libvmod_jq_la_LDFLAGS = $(VMOD_LDFLAGS) $(LIBS)

libvmod_jq_la_SOURCES = \
	vmod_jq.c
nodist_libvmod_jq_la_SOURCES = \
	vcc_jq_if.c \
	vcc_jq_if.h

dist_man_MANS = vmod_jq.3

@BUILD_VMOD_JQ@

TEST_EXTENSIONS = .vtc
VTC_LOG_COMPILER = vtest -v -E@VTESTEXT@ \
	-Dvmod_topbuild=$(abs_top_builddir) -Dvmod_topsrc=$(abs_top_srcdir)
TESTS = @VMOD_TESTS@

EXTRA_DIST = vmod_jq.vcc \
	$(TESTS)

CLEANFILES = $(builddir)/vcc_if.c \
	$(builddir)/vcc_if.h \
	$(builddir)/vmod_jq.man.rst \
	$(builddir)/vmod_jq.rst \
	$(builddir)/$(dist_man_MANS)

if USE_LCOV
check-local:
	$(LCOV) -c -d .libs -o .libs/$(PACKAGE).info
	$(GENHTML) -o lcov .libs/$(PACKAGE).info
	$(GCOV) -o .libs/libvmod_jq-vcc_if.gcno vmod_jq.c

clean-local:
	rm -rf lcov
endif
