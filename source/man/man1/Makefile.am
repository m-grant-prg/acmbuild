#! /usr/bin/env bash
#########################################################################
#									#
# Script ID: source/man/man1/Makefile.am				#
# Author: Mark Grant							#
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
#									#
#########################################################################


acmbuild.1: Makefile
	mkdir -p $(@D)
	rm -f $@ $@.tmp
	$(edit) $(srcdir)/$(@F).man.in > $@.tmp
	txt2manwrap $(@F) 1 "acmbuild Manual" $@.tmp $@
	rm -f $@.tmp

acmbuild.1: $(srcdir)/acmbuild.1.man.in

man_MANS = acmbuild.1

EXTRA_DIST = $(srcdir)/acmbuild.1.man.in

CLEANFILES = *.tmp acmbuild.1
