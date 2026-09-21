AC_INIT([libvmod-jq], [0.3.0])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_SRCDIR(src/vmod_jq.vcc)
AC_CONFIG_HEADERS([config.h])

AM_INIT_AUTOMAKE([foreign color-tests parallel-tests])

AC_DISABLE_STATIC

AC_PROG_CC
LT_INIT

AC_ARG_ENABLE([gcov],
  [AS_HELP_STRING([--enable-gcov],
     [enable code coverage analysis (default=no)])],
  [AC_PATH_PROG([GENHTML], [genhtml])
   AC_PATH_PROG([GCOV], [gcov])
   AC_PATH_PROG([LCOV], [lcov])
   CFLAGS="$CFLAGS -fprofile-arcs -ftest-coverage"])
AM_CONDITIONAL(USE_LCOV,
  [test x$GENHTML != x && test x$GCOV != x && test x$LCOV != x])

AC_SEARCH_LIBS([jq_init], [jq], [],
  AC_MSG_ERROR([jq is required.]))


AC_PATH_PROGS([RST2MAN], [rst2man rst2man.py])
test -z "$RST2MAN" && AC_MSG_ERROR([rst2man is required.])

VCACHE_REQUIRE(
	[[vinyl],[9.1.0]],
	[[varnish],[9.1.0]],
)

VCACHE_VMODS([jq])

VMOD_TESTS="$(cd $srcdir/src && echo tests/*.vtc)"
AC_SUBST(VMOD_TESTS)

AC_CONFIG_FILES([Makefile src/Makefile])
AC_OUTPUT
