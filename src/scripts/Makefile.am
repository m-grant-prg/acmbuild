#! /usr/bin/env bash
##########################################################################
##									##
## Script ID: src/scripts/Makefile.am					##
## Author: Mark Grant							##
##									##
## Purpose:								##
## Automake script file to generate atbuild script from source.		##
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


edit = sed \
	-e 's|@bindir[@]|$(bindir)|g' \
	-e 's|@pkgdatadir[@]|$(pkgdatadir)|g' \
	-e 's|@sysconfdir[@]|$(sysconfdir)|g' \
	-e 's|@prefix[@]|$(prefix)|g'

scriptssrcdir = $(srcdir)

../../scripts/atbuild: Makefile
	mkdir -p $(@D)
	rm -f $@ $@.tmp
	test -f ./$@.in || scriptssrcdir=$(scriptssrcdir)/; \
	$(edit) $${scriptssrcdir}$(@F).in >$@.tmp

	mv $@.tmp $@

	chmod a+x $@

atbuild: $(scriptssrcdir)/atbuild.in

bin_SCRIPTS = ../../scripts/atbuild

EXTRA_DIST = $(scriptssrcdir)/atbuild.in
