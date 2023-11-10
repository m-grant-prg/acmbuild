#########################################################################
#									#
# Author: Copyright (C) 2014-2019, 2021, 2023  Mark Grant		#
#									#
# Released under the GPLv3 only.					#
# SPDX-License-Identifier: GPL-3.0-only					#
#									#
# Purpose:								#
# Automake script file to generate acmbuild manual pages from source.	#
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
