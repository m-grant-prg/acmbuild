#########################################################################
#									#
# Script ID: ./configure.ac						#
# Author: Copyright (C) 2014-2021  Mark Grant				#
#									#
# Released under the GPLv3 only.					#
# SPDX-License-Identifier: GPL-3.0					#
#									#
# Purpose:								#
# Autoconfigure script file to configure acmbuild project.		#
#									#
# configure cmd line syntax:						#
# ./configure	[ --enable-testinghacks=<yes|no> [default: no] ]	#
#									#
# Parameters generic description. For specifics to this configure.ac	#
# please see inline comments at the point of definition:-		#
# --enable-testinghacks							#
#	This option should be used when the AT testing environment, (ie	#
#	using the build directory), requires differences in invocation.	#
#	An example would be a shell script invoking a program / script 	#
#	/ jar file. In the AT build directory the script should invoke	#
#	the target in the build system, whereas in production it might	#
#	invoke the target in datadir, datadir/java or pkgdatadir. If	#
#	this was left unchanged the test invocation of the script would	#
#	end up testing any old installed version of the target or	#
#	failing because it cannot be found.				#
#									#
# Layout: (Only relevant sections will exist).				#
# ChangeLog : High level ChangeLog					#
# SECTION  1: Initialisation & Setup					#
# SECTION  2: Architecture, target and host checks			#
# SECTION  3: Command line arguments					#
# SECTION  4: Compiler setup						#
# SECTION  5: Check for programs					#
# SECTION  6: Check for libraries					#
# SECTION  7: Check for header files					#
# SECTION  8: Check for types						#
# SECTION  9: Check for structures					#
# SECTION 10: Check for compiler characteristics			#
# SECTION 11: Check for library functions				#
# SECTION 12: Check for pkg-config files				#
# SECTION 13: Check for system services					#
# SECTION 14: Additional checks & variables				#
# SECTION 15: Specify the output files					#
#									#
#########################################################################

#########################################################################
#									#
# Changelog								#
#									#
# Date		Author	Version	Description				#
#									#
# 25/06/2014	MG	1.0.1	Started versioning of this script.	#
# 26/06/2014	MG	1.0.2	Use 'git describe --always' for AC_INIT	#
#				version as it returns a value as long	#
#				as there is at least 1 commit, even	#
#				with no tags. If no commits then	#
#				'Pre-Release' is used.			#
# 02/08/2014	MG	1.0.3	Change naming from AutoTools to		#
#				AutoConf and Make.			#
# 18/11/2014	MG	1.0.4	Re-structure to cope with OS		#
#				differences. Add check for GNU getopt.	#
# 24/11/2014	MG	1.0.5	Add support for passing overall package	#
#				version to Makefiles.			#
# 29/11/2014	MG	1.0.6	Remove redundant hashpling.		#
# 26/06/2015	MG	1.0.7	Remove BSD support.			#
# 27/09/2015	MG	1.0.8	Change to conform to AutoTools Template	#
#				version 1.0.4.				#
# 17/10/2015	MG	1.0.9	Restructure to conform to AutoTools	#
#				General Template v1.0.5.		#
# 25/02/2017	MG	1.0.10	Update sed edit substitution variable.	#
# 28/04/2017	MG	1.0.11	Make AC_INIT and pkgversion AC_SUBST	#
#				multi-line.				#
# 01/12/2017	MG	1.0.12	Add SPDX license tags to source files.	#
# 09/02/2018	MG	1.0.13	Shorten directory names to reduce	#
#				overall path length.			#
#				Update minimum AutoTools version.	#
#				Standardise configure.ac and macro	#
#				directory.				#
#				Use automake sub-directory and tar	#
#				Posix format directives.		#
# 07/04/2018	MG	1.0.14	Change package versioning to use	#
#				hard-coded value. This is due to the	#
#				use of github which produces source	#
#				tarballs which can be used for package	#
#				generation. These tarballs are used	#
#				outside of git so git versioning is not	#
#				possible, hence the hard-coded value.	#
#				Because of this, other packaging should	#
#				probably use the source tarball rather	#
#				than a dist tarball.			#
# 22/03/2019	MG	1.1.1	Pass bash path to scripts and Makefiles	#
#				Remove leading v from package version.	#
#				Add --enable-testinghacks option.	#
#				Re-vamp to new standard layout.		#
# 25/06/2019	MG	1.1.2	Improve header comments on CLAs.	#
# 28/06/2019	MG	1.1.3	Correct ARG_ENABLE help text.		#
# 11/06/2020	MG	1.1.4	Tighten up program checks.		#
# 19/11/2021	MG	1.1.5	If git is available and we are inside a	#
#				git tree then use git describe to add	#
#				further package version information.	#
#									#
#########################################################################


#########################################
#					#
# SECTION  1: Initialisation & Setup	#
#					#
#########################################

AC_REVISION([$Revision: 1.1.5 $])

AC_PREREQ([2.69])

#
# The following macro uses git, if available, to provide versioning information.
# The logic is as follows:-
# If git is not available, is not initialised or no commit has been made, then
# the local variable pkg_version will be used.
# If git is available but no Tag has been created then just a commit identifier
# will be used.
# If git is available and a tag has been created then the most recent tag, plus
# number of commits since the tag, plus a commit identifier will be used.
# The package version in ac init will be used to create an output variable which
# can be used by ac output and / or the sed setup below to substitute bookmarks
# in source files.
#
# Set pkg_version for a default hard-coded version number.
m4_define(pkg_version, 1.3.12)

AC_INIT([AutoTools Build Script], m4_esyscmd([ \
	git describe --always 1>/dev/null 2>/dev/null \
	&& sed --help 1>/dev/null 2>/dev/null \
	&& git describe --always | sed 's/v//' | tr -d '\n' \
	|| echo pkg_version | tr -d '\n']),
	[m.grant.prg@gmail.com], [acmbuild])

AC_MSG_NOTICE(initialisation and setup)

AC_SUBST(pkgversion, $PACKAGE_VERSION)

#
# Passes the options to all am files. Puts objects in the sub-directory
# containing the source. Forces tar to use --format=posix in make dist.
# This also checks :-	BSD install	make variable set	mkdir -p
#			gawk
#
AM_INIT_AUTOMAKE([-Wall -Werror subdir-objects tar-pax])

#
# Standard macros will be automatically placed in m4.
# Programmer defined macros should be placed in, say, m4extra which allows us
# to exclude the standard macros from being git tracked. This other directory
# must be specified as an include option in the Makefile.am ACLOCAL_AMFLAGS
# e.g.
# ACLOCAL_AMFLAGS = -I m4 -I m4extra
#
AC_CONFIG_MACRO_DIR([m4])


#########################################
#					#
# SECTION  3: Command line arguments	#
#					#
#########################################

AC_MSG_NOTICE(checking command line arguments)

#
# The following allows for an enable-testinghacks=yes/no command line option.
# The conditional TESTINGHACKS is made available to the makefiles.
# This allows different variable substitutions depending on whether in a test
# environment or a production build / install environment.
#
AC_ARG_ENABLE(testinghacks,
	AS_HELP_STRING([--enable-testinghacks], \
			[build with testing hacks for local testing]),
	[case "${enableval}" in
	yes) testinghacks=true ;;
	no)  testinghacks=false ;;
	*) AC_MSG_ERROR(bad value ${enableval} for --enable-testinghacks) ;;
	esac],testinghacks=false)
AM_CONDITIONAL(TESTINGHACKS, test x$testinghacks = xtrue)

if test "x${testinghacks}" = xtrue; then
	AC_MSG_NOTICE(building with testing hacks for local testing)
	AC_SUBST(scriptloc,"\$(builddir)")
else
	AC_SUBST(scriptloc,"\$(pkglibexecdir)")
fi


#########################################
#					#
# SECTION  5: Check for programs	#
#					#
#########################################

AC_MSG_NOTICE(checking for basic programs that have AutoConf checks)

#
# The small set of tools you can expect to find on any machine.
#
# awk		date		grep		od
# basename	diff		join		rm
# cat		dirname		ln		rmdir
# cc		egrep		ls		sed
# chgrp		expr		mkdir		sleep
# chown		expr (‘|’)	mkfifo		sort
# chmod		expr (‘:’)	mknod		tar
# cmp		fgrep		mktemp		touch
# cp		find		mv		tr
#
# (For further information including limitations to the above, see Section 11.15
# in the GNU AutoConf Manual).
#
# If using am init automake, gl early or lt init the following programs are
# automatically checked:-
#
# am init automake
#	BSD install	mkdir -p	gawk
#
# gl early
#	ar	grep	egrep	ranlib
#
# lt init
#	fgrep	ranlib	sed
#
# Basic and AutoTools program checks.
#
AC_PROG_AWK
AC_PROG_EGREP
AC_PROG_FGREP
AC_PROG_GREP
AC_PROG_LN_S
AC_PROG_MKDIR_P
AC_PROG_SED

AC_MSG_NOTICE(checking for some standard AutoTools required programs)
AC_PROG_INSTALL

AC_MSG_NOTICE(checking for particular programs required by this build)
AC_CHECK_PROG([ECHO], [echo], [yes], [no])
if test "x$ECHO" = "xno" ; then
	AC_MSG_ERROR([echo not found])
fi

AC_CHECK_PROG([TXT2MAN], [txt2man], [yes], [no])
if test "x$TXT2MAN" = "xno" ; then
	AC_MSG_ERROR([txt2man not found])
fi

AC_CHECK_PROG([TXT2MANWRAP], [txt2manwrap], [yes], [no])
if test "x$TXT2MANWRAP" = "xno" ; then
	AC_MSG_ERROR([txt2manwrap not found])
fi

AC_MSG_NOTICE(checking for particular programs required at build and run time)
AC_PATH_PROG([BASH], [bash], [no])
if test "x$BASH" = "xno" ; then
	AC_MSG_ERROR([bash not found])
fi

AC_CHECK_PROG([TAR], [tar], [yes], [no])
if test "x$TAR" = "xno" ; then
	AC_MSG_ERROR([tar not found])
fi

AC_MSG_NOTICE(checking for particular programs required at run time)
AC_CHECK_PROG(CAT, cat, yes, no)
if test "x$CAT" = "xno" ; then
	AC_MSG_WARN(cat not found - needed at run time)
fi

AC_CHECK_PROG([GETOPT], [getopt], [yes], [no])
if test "x$GETOPT" = "xno" ; then
	AC_MSG_WARN(getopt not found - needed at run time)
fi

AC_CHECK_PROG(PRINTF, printf, yes, no)
if test "x$PRINTF" = "xno" ; then
	AC_MSG_WARN(printf not found - needed at run time)
fi

AC_MSG_NOTICE(checking for programs which may be required at run time)
AC_CHECK_PROG(GCC, gcc, yes, no)
if test "x$GCC" = "xno" ; then
	AC_MSG_WARN(gcc not found - may be needed at run time)
fi

AC_CHECK_PROG(GIT, git, yes, no)
if test "x$GIT" = "xno" ; then
	AC_MSG_WARN(git not found - may be needed at run time)
fi

AC_CHECK_PROG(GNULIB_TOOL, gnulib-tool, yes, no)
if test "x$GNULIB_TOOL" = "xno" ; then
	AC_MSG_WARN(gnulib-tool not found - may be needed at run time)
fi

AC_CHECK_PROG(CGCC, cgcc, yes, no)
if test "x$CGCC" = "xno" ; then
	AC_MSG_WARN(sparse not found - may be needed at run time)
fi


#################################################
#						#
# SECTION 14: Additional checks & variables	#
#						#
#################################################

AC_MSG_NOTICE(processing additional checks and variables)

#
# Now set up a sed sequence to substitute bookmarks in script files with either
# standard GNU Directory Variables, or with programmer-defined variables set up
# using an AC_SUBST macro above. This sed sequence will be invoked at programmer
# discretion at sub-directory Makefile.am level.
# ----------------------
#
# prefix	/usr/local (typically)
#	exec_prefix	${prefix}
#		bindir	${exec_prefix}/bin	user executables
#		sbindir	${exec_prefix}/sbin	system admin executables
#		libexecdir	${exec_prefix}/libexec	program executables
#		libdir	${exec_prefix}/lib	object code libraries
#	sysconfdir	 ${prefix}/etc	read-only single-machine data
#	sharedstatedir	${prefix}/com	modifiable architecture-independent data
#	localstatedir	${prefix}/var	modifiable single-machine data
#	runstatedir	${localstatedir}/run
#	includedir	${prefix}/include	C header files
#	oldincludedir	$usr/include	C header files
#	datarootdir	${prefix}/share	read-only arch.-independent data root
#		localedir	${datarootdir}/locale	locale-dependent data
#		datadir	${datarootdir}	read-only architecture-independent data
#		mandir	${datarootdir}/man	man documentation
#		infodir	${datarootdir}/info	info documentation
#		docdir	${datarootdir}/doc/${PACKAGE}	documentation root
#			htmldir	${docdir}	html documentation
#			dvidir	${docdir}	dvi documentation
#			pdfdir	${docdir}	pdf documentation
#			psdir	${docdir}	ps documentation
#		lispdir	${datarootdir}/emacs/site-lisp
#	pkgdatadir	${datarootdir}/${PACKAGE}
#	pkgincludedir	${includedir}/${PACKAGE}
#	pkglibdir	${libdir}/${PACKAGE}
#	pkglibexecdir	${libexecdir}/${PACKAGE}
#
AC_SUBST([edit], ["sed \
		-e 's|@scriptloc[@]|\$(scriptloc)|g' \
		-e 's|@bashlocation[@]|\$(BASH)|g' \
		-e 's|@pkgversion[@]|\$(pkgversion)|g' \
		-e 's|@prefix[@]|\$(prefix)|g' \
		-e 's|@exec_prefix[@]|\$(exec_prefix)|g' \
		-e 's|@bindir[@]|\$(bindir)|g' \
		-e 's|@sbindir[@]|\$(sbindir)|g' \
		-e 's|@libexecdir[@]|\$(libexecdir)|g' \
		-e 's|@libdir[@]|\$(libdir)|g' \
		-e 's|@sysconfdir[@]|\$(sysconfdir)|g' \
		-e 's|@sharedstatedir[@]|\$(sharedstatedir)|g' \
		-e 's|@localstatedir[@]|\$(localstatedir)|g' \
		-e 's|@runstatedir[@]|\$(runstatedir)|g' \
		-e 's|@includedir[@]|\$(includedir)|g' \
		-e 's|@oldincludedir[@]|\$(oldincludedir)|g' \
		-e 's|@datarootdir[@]|\$(datarootdir)|g' \
		-e 's|@localedir[@]|\$(localedir)|g' \
		-e 's|@datadir[@]|\$(datadir)|g' \
		-e 's|@mandir[@]|\$(mandir)|g' \
		-e 's|@infodir[@]|\$(infodir)|g' \
		-e 's|@docdir[@]|\$(docdir)|g' \
		-e 's|@htmldir[@]|\$(htmldir)|g' \
		-e 's|@dvidir[@]|\$(dvidir)|g' \
		-e 's|@pdfdir[@]|\$(pdfdir)|g' \
		-e 's|@psdir[@]|\$(psdir)|g' \
		-e 's|@lispdir[@]|\$(lispdir)|g' \
		-e 's|@pkgdatadir[@]|\$(pkgdatadir)|g' \
		-e 's|@pkgincludedir[@]|\$(pkgincludedir)|g' \
		-e 's|@pkglibdir[@]|\$(pkglibdir)|g' \
		-e 's|@pkglibexecdir[@]|\$(pkglibexecdir)|g'"])


#########################################
#					#
# SECTION 15: Specify the output files	#
#					#
#########################################

AC_MSG_NOTICE(processing output files)

#
# Non-Makefile files to generate.
# AC_CONFIG_FILES should not be used to substitute AutoConf Installation
# Directory Variables, (bindir and friends), except in Makefiles and pkg-config
# files. See GNU AutoConf manual section 4.8.2 Installation Directory Variables.
#

# Project Makefiles to create.
AC_CONFIG_FILES([Makefile
		src/prg/bash/Makefile
		src/man/1/Makefile])

AC_OUTPUT

