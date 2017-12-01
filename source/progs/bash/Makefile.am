#! /usr/bin/env bash
#########################################################################
#									#
# Script ID: source/progs/bash/Makefile.am				#
# Author: Copyright (C) 2014-2017  Mark Grant				#
#									#
# Released under the GPLv3 only.					#
# SPDX-License-Identifier: GPL-3.0					#
#									#
# Purpose:								#
# Automake script file to generate acmbuild script from source.		#
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
# 24/11/2014	MG	1.0.3	Add script substitution variable for	#
#				overall package version.		#
# 27/09/2015	MG	1.0.4	Change to conform to AutoTools Template	#
#				version 1.0.4.				#
# 17/10/2015	MG	1.0.5	Restructure to conform to AutoTools	#
#				General Template v1.0.5.		#
# 28/04/2017	MG	1.0.6	Rename source file extension .sh.in	#
# 01/12/2017	MG	1.0.7	Add SPDX license tags to source files.	#
#									#
#########################################################################


acmbuild: Makefile
	mkdir -p $(@D)
	rm -f $@ $@.tmp
	test -f ./$@.sh.in || srcdir=$(srcdir)/; \
	$(edit) $${srcdir}$(@F).sh.in > $@.tmp

	mv $@.tmp $@

	chmod a+x $@

acmbuild: $(srcdir)/acmbuild.sh.in

bin_SCRIPTS = acmbuild

EXTRA_DIST = $(srcdir)/acmbuild.sh.in

CLEANFILES = *.tmp acmbuild
