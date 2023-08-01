#########################################################################
#									#
# Script ID: ./Makefile.am						#
# Author: Copyright (C) 2014-2019, 2021, 2023  Mark Grant		#
#									#
# Released under the GPLv3 only.					#
# SPDX-License-Identifier: GPL-3.0-only					#
#									#
# Purpose:								#
# Automake script file to generate acmbuild project from source.	#
#									#
#########################################################################

#########################################################################
#									#
# Changelog								#
#									#
# Date		Author	Version	Description				#
#									#
# 25/06/2014	MG	1.0.1	Started versioning of this script.	#
# 02/08/2014	MG	1.0.2	Change naming from AutoTools to		#
#				AutoConf and Make.			#
# 17/10/2015	MG	1.0.3	Restructure to conform to AutoTools	#
#				General Template v1.0.5.		#
# 01/12/2017	MG	1.0.4	Add SPDX license tags to source files.	#
# 09/02/2018	MG	1.0.5	Shorten directory names to reduce	#
#				overall path length.			#
#				Add standard macro directory.		#
# 07/04/2018	MG	1.0.6	Add srctarball target to build a source	#
#				tarball in the build directory. Uses	#
#				git archive to archive HEAD.		#
# 09/06/2018	MG	1.0.7	Add info messages to srctarball target.	#
# 27/10/2018	MG	1.0.8	Change srctarball target to build with	#
#				src between package name and version in	#
#				filename.				#
# 16/03/2019	MG	1.0.9	Remove unnecessary shebang.		#
#				Change source tarball name to be the	#
#				same as that in GitHub releases. This	#
#				aids integrating with rpm generation.	#
#				Add install of standard GNU files like	#
#				AUTHORS, etc.				#
# 25/06/2019	MG	1.0.10	To enable make distcheck to work, any	#
#				hard-coded paths requiring permissions	#
#				such as /etc or fixed locations such as	#
#				/usr/share/java must be accommodated,	#
#				so set the configure flags to be used	#
#				by make distcheck.			#
# 08/11/2021	MG	1.0.11	Add misc directory to DIST.		#
# 21/11/2021	MG	1.0.12	Tighten SPDX tag.			#
# 01/08/2023	MG	1.0.13	Enable use of v1.1.1~rc1 type vesrion	#
#									#
#########################################################################


ACLOCAL_AMFLAGS = -I m4


AM_DISTCHECK_CONFIGURE_FLAGS =


SUBDIRS = src/prg/bash src/man/1


doc_DATA = AUTHORS ChangeLog COPYING NEWS README


EXTRA_DIST = $(srcdir)/AUTHORS $(srcdir)/ChangeLog $(srcdir)/COPYING \
		$(srcdir)/NEWS $(srcdir)/README $(srcdir)/misc


srctarball:
	@cwd="$${PWD}" && \
	varg="$$(echo @PACKAGE_VERSION@ | sed -e s/\-rc/\~rc/ )" && \
	targ="$${cwd}/@PACKAGE_TARNAME@-$${varg}.tar.gz" && \
	cd @srcdir@ && \
	echo "making srctarball from @srcdir@" && \
	echo "GA	$${targ}" && \
	git archive --format=tar.gz \
		--prefix=@PACKAGE_TARNAME@-$${varg}/ \
		--output=$${targ} \
		HEAD && \
	cd -

