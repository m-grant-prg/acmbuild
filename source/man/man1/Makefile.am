#! /usr/bin/env bash
#########################################################################
#									#
# Script ID: source/man/man1/Makefile.am				#
# Author: Copyright (C) 2014-2017  Mark Grant				#
#									#
# Released under the GPLv3 only.					#
# SPDX-License-Identifier: GPL-3.0					#
#									#
# Purpose:								#
# Automake script file to generate acmbuild manual pages from source.	#
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
# 27/09/2015	MG	1.0.3	Change to conform to AutoTools Template	#
#				version 1.0.4.				#
# 17/10/2015	MG	1.0.4	Restructure to conform to AutoTools	#
#				General Template v1.0.5.		#
# 28/04/2017	MG	1.0.5	Output from $(edit) was being ignored.	#
#				Rename source file extension .man.in	#
# 01/12/2017	MG	1.0.6	Add SPDX license tags to source files.	#
#				Determine the manual section from the	#
#				target suffix. If the suffix is blank	#
#				(foo.) or if there is no suffix (foo)	#
#				then error out.				#
#									#
#########################################################################


acmbuild.1: Makefile
	mkdir -p $(@D)
	rm -f $@ $@.tmp
	$(edit) $(srcdir)/$(@F).man.in > $@.tmp
	targfile=$(@F);	\
	if [[ $$targfile == *"."* ]]; then \
		if [[ $${targfile##*.} == "" ]]; then \
			echo "Source file suffix used as section but empty."; \
			exit 1; \
		else \
			section=$${targfile##*.}; \
		fi; \
	else \
		echo "Source file suffix used as section but no dot & empty."; \
		exit 1; \
	fi; \
	txt2manwrap $(@F) $$section "acmbuild Manual" $@.tmp $@
	rm -f $@.tmp

acmbuild.1: $(srcdir)/acmbuild.1.man.in

man_MANS = acmbuild.1

EXTRA_DIST = $(srcdir)/acmbuild.1.man.in

CLEANFILES = *.tmp acmbuild.1
