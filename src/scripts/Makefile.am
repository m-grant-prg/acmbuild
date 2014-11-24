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
##									##
##########################################################################


edit = sed \
	-e 's|@bindir[@]|$(bindir)|g' \
	-e 's|@pkgdatadir[@]|$(pkgdatadir)|g' \
	-e 's|@sysconfdir[@]|$(sysconfdir)|g' \
	-e 's|@prefix[@]|$(prefix)|g' \
	-e 's|@pkgversion[@]|$(pkgversion)|g'

scriptssrcdir = $(srcdir)

../../scripts/acmbuild: Makefile
	mkdir -p $(@D)
	rm -f $@ $@.tmp
	test -f ./$@.in || scriptssrcdir=$(scriptssrcdir)/; \
	$(edit) $${scriptssrcdir}$(@F).in >$@.tmp

	mv $@.tmp $@

	chmod a+x $@

acmbuild: $(scriptssrcdir)/acmbuild.in

bin_SCRIPTS = ../../scripts/acmbuild

EXTRA_DIST = $(scriptssrcdir)/acmbuild.in
