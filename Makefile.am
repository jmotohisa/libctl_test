# libctl: flexible Guile-based control files for scientific software
# Copyright (C) 1998, 1999, 2000, 2001, 2002, Steven G. Johnson
#
# This file may be used without restriction.  It is in the public
# domain, and is NOT restricted by the terms of any GNU license.
#
# This library is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# Lesser General Public License for more details.
#
# Steven G. Johnson can be contacted at stevenj@alum.mit.edu.

##############################################################################

# Makefile.am for programs using libctl (assumes that automake is
# being used, of course).  You should only need to change the definitions
# in this section of the file.  Replace "test1" with the name of
# your program.

SPECIFICATION_FILE = test1.scm
EXTRA_DIST = test1.scm.in README run.ctl

# change "noinst" to "bin" and uncomment pkgdata line to 'make install' program
noinst_PROGRAMS = test1
# pkgdata_DATA = $(SPECIFICATION_FILE)

MY_SOURCES = test1.c # plus any other .c/.h files you need

MY_LIBS    =         # extra libs you need go here
MY_LDFLAGS =         # extra -L flags go here
MY_CPPFLAGS =        # extra -I include flags go here
MY_DEFS =            # extra -D define flags go here

# what is printed out when invoking your program with --version:
VERSION_STRING = "test1 @VERSION@"

# The following variables should be detected and set by autoconf:

# libctl install. dir., e.g. /usr/local/share/libctl
LIBCTL_DIR = @LIBCTL_DIR@

# gen-ctl-io program
GEN_CTL_IO = @GEN_CTL_IO@

# location of libctl headers and library for this project
LIBCTL_CPPFLAGS = -I$(top_srcdir)/utils -I$(top_builddir)/src
LIBCTL = -lctl # change to -lctl for your project

##############################################################################
#   don't (normally) edit below except to replace "test1" with your name   #
##############################################################################

CTL_DEFS = -DCTL_SCM='"'$(LIBCTL_DIR)/base/ctl.scm'"' \
       -DINCLUDE_SCM='"'$(LIBCTL_DIR)/base/include.scm'"' \
          -DSPEC_SCM='"'$(pkgdatadir)/$(SPECIFICATION_FILE)'"' \
    -DVERSION_STRING='"'$(VERSION_STRING)'"'

test1_SOURCES = $(MY_SOURCES)
nodist_test1_SOURCES = main.c geom.c ctl-io.h ctl-io.c
BUILT_SOURCES = $(nodist_test1_SOURCES)
test1_LDADD = $(MY_LIBS) $(LIBCTL)
test1_LDFLAGS = $(MY_LDFLAGS)
test1_CPPFLAGS = $(MY_CPPFLAGS) $(MY_DEFS) $(CTL_DEFS) $(LIBCTL_CPPFLAGS)

main.c: $(LIBCTL_DIR)/base/main.c
	cp -f $(LIBCTL_DIR)/base/main.c $@

geom.c: $(LIBCTL_DIR)/utils/geom.c
	cp -f $(LIBCTL_DIR)/utils/geom.c $@

ctl-io.c: $(SPECIFICATION_FILE) $(LIBCTL_DIR)/utils/geom.scm
	$(GEN_CTL_IO) --code -o $@ $(SPECIFICATION_FILE) $(LIBCTL_DIR)

ctl-io.h: $(SPECIFICATION_FILE) $(LIBCTL_DIR)/utils/geom.scm
	$(GEN_CTL_IO) --header -o $@ $(SPECIFICATION_FILE) $(LIBCTL_DIR)

clean-local:
	rm -f ctl-io.* main.* geom.*
