#########################################################################
#									#
# Author: Copyright (C) 2014-2019, 2021, 2023  Mark Grant		#
#									#
# Released under the GPLv3 only.					#
# SPDX-License-Identifier: GPL-3.0-only					#
#									#
# Purpose:								#
# Automake script file to generate acmbuild scripts from source.	#
#									#
#########################################################################


acmbuild: Makefile
	mkdir -p $(@D)
	rm -f $@ $@.tmp
	test -f ./$@.in || srcdir=$(srcdir)/; \
	$(edit) $${srcdir}$(@F).sh.in > $@.tmp
	mv $@.tmp $@
	chmod a+x $@
acmbuild: $(srcdir)/acmbuild.sh.in

bootstrap.sh: Makefile
	mkdir -p $(@D)
	rm -f $@ $@.tmp
	test -f ./$@.in || srcdir=$(srcdir)/; \
	$(edit) $${srcdir}$(@F).in > $@.tmp
	mv $@.tmp $@
	chmod a+x $@
bootstrap.sh: $(srcdir)/bootstrap.sh.in


bin_SCRIPTS = acmbuild

pkglibexec_SCRIPTS = bootstrap.sh


EXTRA_DIST = $(srcdir)/acmbuild.sh.in $(srcdir)/bootstrap.sh.in


CLEANFILES = *.tmp acmbuild bootstrap.sh

