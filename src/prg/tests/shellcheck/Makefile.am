#########################################################################
#									#
# Author: Copyright (C) 2026  Mark Grant				#
#									#
# Released under the GPLv3 only.					#
# SPDX-License-Identifier: GPL-3.0-only					#
#									#
# Purpose:								#
# AutoMake script file to generate tests.				#
#									#
#########################################################################


run-shellcheck.sh: Makefile
	mkdir -p $(@D)
	rm -f $@ $@.tmp
	test -f ./$@.in || srcdir=$(srcdir)/; \
	$(edit) $${srcdir}$(@).in > $@.tmp
	mv $@.tmp $@
	chmod a+x $@
run-shellcheck.sh: $(srcdir)/run-shellcheck.sh.in


check_DATA = run-shellcheck.sh


EXTRA_DIST = $(srcdir)/run-shellcheck.sh.in


CLEANFILES = *.tmp run-shellcheck.sh

