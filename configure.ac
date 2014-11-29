##########################################################################
##									##
## Script ID: ./configure.ac						##
## Author: Mark Grant							##
##									##
## Purpose:								##
## Autoconfigure script file to configure acmbuild project.		##
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
## 02/08/2014	MG	1.0.3	Change naming from AutoTools to		##
##				AutoConf and Make.			##
## 18/11/2014	MG	1.0.4	Re-structure to cope with OS		##
##				differences. Add check for GNU getopt.	##
## 24/11/2014	MG	1.0.5	Add support for passing overall package	##
##				version to Makefiles.			##
## 29/11/2014	MG	1.0.6	Remove redundant hashpling.		##
##									##
##########################################################################


AC_PREREQ([2.65])
AC_INIT([acmbuild AutoConf Make Distribution Build Script], m4_esyscmd([git describe --always 1>/dev/null 2>/dev/null && git describe --always | tr -d '\n' || echo 'Pre-Release' | tr -d '\n']), [m.grant.prg@gmail.com], [acmbuild])

AC_SUBST(pkgversion, m4_esyscmd([git describe --always 1>/dev/null 2>/dev/null && git describe --always | tr -d '\n' || echo 'Pre-Release' | tr -d '\n']))

AM_INIT_AUTOMAKE

AC_CONFIG_FILES([Makefile
		src/scripts/Makefile
		src/manpages/man1/Makefile])

AC_CANONICAL_HOST

# Checks for programs.
AC_MSG_NOTICE([checking for required $host_os specific programs])
case $host_os in
	*bsd*)	AC_MSG_NOTICE([using $host_os...])
		AC_CHECK_PROG(GETOPT, getopt, yes, no, path = '/usr/local/bin')
		if test "x$GETOPT" = "xno" ; then
			AC_MSG_ERROR([getopt not found])
		fi
		;;
	# linux*)	Allow fall through for now as the defaults are linux.
	*)	AC_MSG_NOTICE([using defaults...])
		AC_CHECK_PROG(GETOPT, getopt, yes, no)
		if test "x$GETOPT" = "xno" ; then
			AC_MSG_ERROR([getopt not found])
		fi
		;;
esac

AC_MSG_NOTICE([checking for required generic programs])
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
