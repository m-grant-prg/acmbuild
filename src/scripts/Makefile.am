#! /usr/bin/env bash
##########################################################################
##									##
## Script ID: src/scripts/Makefile.am					##
## Author: Mark Grant							##
##									##
## Purpose:								##
## Automake script file to generate acmbuild script from source.	##
##									##
##########################################################################

##########################################################################
##									##
## Changelog								##
##									##
## Date		Author	Version	Description				##
##									##
## 25/06/2014	MG	1.0.1	Started versioning of this script.	##
## 02/08/2014	MG	1.0.2	Change naming from AutoTools to		##
##				AutoConf and Make.			##
## 24/11/2014	MG	1.0.3	Add script substitution variable for	##
##				overall package version.		##
## 27/09/2015	MG	1.0.4	Change to conform to AutoTools Template	##
##				version 1.0.4.				##
##									##
##########################################################################


acmbuild: Makefile
	mkdir -p $(@D)
	rm -f $@ $@.tmp
	test -f ./$@.in || srcdir=$(srcdir)/; \
	$(edit) $${srcdir}$(@F).in > $@.tmp

	mv $@.tmp $@

	chmod a+x $@

acmbuild: $(srcdir)/acmbuild.in

bin_SCRIPTS = acmbuild

EXTRA_DIST = $(srcdir)/acmbuild.in

CLEANFILES = *.tmp acmbuild

