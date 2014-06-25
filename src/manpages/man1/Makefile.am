#! /usr/bin/env bash
##########################################################################
##									##
## Script ID: src/manpages/man1/Makefile.am				##
## Author: Mark Grant							##
##									##
## Purpose:								##
## Automake script file to generate atbuild manual pages from source.	##
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


manpagessrcdir = $(srcdir)

../../../manpages/man1/atbuild.1: Makefile
	mkdir -p $(@D)
	rm -f $@
	txt2man -t atbuild -s 1 -v "atbuild Manual" \
		$(manpagessrcdir)/$(@F).txt > $@

atbuild.1: $(manpagessrcdir)/atbuild.1.txt

man1_MANS = ../../../manpages/man1/atbuild.1

EXTRA_DIST = $(manpagessrcdir)/atbuild.1.txt
