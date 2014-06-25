#! /usr/bin/env bash
##########################################################################
##									##
## Script ID: ./configure.ac						##
## Author: Mark Grant							##
##									##
## Purpose:								##
## Autoconfigure script file to configure atbuild project.		##
##									##
##########################################################################

##########################################################################
##									##
## Changelog								##
##									##
## Date		Author	Version	Description				##
##									##
## 25/06/2014	MG	1.0.1	Started versioning of this script.	##
##									##
##########################################################################


AC_PREREQ([2.65])
AC_INIT([atbuild AutoTools Distribution Build Script], m4_esyscmd([git describe | tr -d '\n']), [m.grant.prg@gmail.com], [atbuild])

AM_INIT_AUTOMAKE

AC_CONFIG_FILES([Makefile
		src/scripts/Makefile
		src/manpages/man1/Makefile])

# Checks for programs.

AC_CHECK_PROG(BASH, bash, yes, no)
if test "x$BASH" = "xno" ; then
   	AC_MSG_ERROR([bash not found])
fi

AC_CHECK_PROG(TAR, tar, yes, no)
if test "x$TAR" = "xno" ; then
   	AC_MSG_ERROR([tar not found])
fi

AC_CHECK_PROG(TXT2MAN, txt2man, yes, no)
if test "x$TXT2MAN" = "xno" ; then
   	AC_MSG_ERROR([txt2man not found])
fi

# Checks for libraries.

# Checks for header files.

# Checks for typedefs, structures, and compiler characteristics.

# Checks for library functions.

AC_OUTPUT
