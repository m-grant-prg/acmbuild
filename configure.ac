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
## 26/06/2014	MG	1.0.2	Use 'git describe --always' for AC_INIT	##
##				version as it returns a value as long	##
##				as there is at least 1 commit, even	##
##				with no tags. If no commits then	##
##				'Pre-Release' is used.			##
## 29/07/2014	MG	1.0.3	Include check to ensure make is		##
##				installed.				##
##									##
##########################################################################


AC_PREREQ([2.65])
AC_INIT([atbuild AutoTools Distribution Build Script], m4_esyscmd([git describe --always 1>/dev/null 2>/dev/null && git describe --always | tr -d '\n' || echo 'Pre-Release' | tr -d '\n']), [m.grant.prg@gmail.com], [atbuild])

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

AC_CHECK_PROG(MAKE, make, yes, no)
if test "x$MAKE" = "xno" ; then
   	AC_MSG_ERROR([make not found])
fi

# Checks for libraries.

# Checks for header files.

# Checks for typedefs, structures, and compiler characteristics.

# Checks for library functions.

AC_OUTPUT
