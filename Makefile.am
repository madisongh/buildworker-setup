# buildworker-setup makefile
#
# Copyright (c) 2020 Matthew Madison
#

AUTOMAKE_OPTIONS = subdir-objects foreign
ACLOCAL_AMFLAGS = -I m4
SUBDIRS =
DIST_SUBDIRS =

EXTRA_DIST = src/buildworker-init.in src/buildworker.service.in src/buildworker-setup.service.in \
             src/digsigserver.service.in

dist_sbin_SCRIPTS = buildworker-init
systemdsystemunit_DATA = buildworker-setup.service buildworker.service digsigserver.service

buildworker-init: src/buildworker-init
	sed -e's,\$${prefix},$(prefix),g' -e's,$${exec_prefix},$(exec_prefix),g' < $< >$@
buildworker-setup.service: src/buildworker-setup.service
	sed -e's,\$${prefix},$(prefix),g' -e's,$${exec_prefix},$(exec_prefix),g' < $< >$@
buildworker.service: src/buildworker.service
	sed -e's,\$${prefix},$(prefix),g' -e's,$${exec_prefix},$(exec_prefix),g' < $< >$@
digsigserver.service: src/digsigserver.service
	sed -e's,\$${prefix},$(prefix),g' -e's,$${exec_prefix},$(exec_prefix),g' < $< >$@
