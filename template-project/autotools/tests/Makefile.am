include $(top_srcdir)/build-aux/init.mk
include $(top_srcdir)/build-aux/autotest.mk

# Add available warnings flags.
AM_CXXFLAGS += $(WARNING_CXXFLAGS)

# Package the following files.
EXTRA_DIST += package.m4.in

# Clean atconfig (do not distribute it).
CLEANFILES += atconfig

# Source which are shared by all tests.
COMMON_SOURCES = common.hh

# simple-test
check_PROGRAMS = simple-test
simple_test_SOURCES = simple-test.cc $(COMMON_SOURCES)
simple_test_LDADD = $(top_builddir)/src/lib@PACKAGE_TARNAME@.la
simple_test_CPPFLAGS = $(AM_CPPFLAGS) &PKG_DEPS_CFLAGS&

.PHONY: generate-reference

# Re-generate reference outputs.
generate-reference: $(check_PROGRAMS)
	@echo "Generating references...";	\
	for i in $(check_PROGRAMS); do		\
	 IN="$(srcdir)/$$i.stdin";		\
	 OUT="$(srcdir)/$$i.stdout";		\
	 if test -f "$$IN"; then 		\
	  "./$$i" < $$IN > $$OUT || true;	\
	 else					\
	  "./$$i" > $$OUT || true;		\
	 fi					\
	done


# ------------ #
# Test suite.  #
# ------------ #

# Distribute reference files.
EXTRA_DIST +=					\
	simple-test.stdout
