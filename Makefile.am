# buildworker-setup makefile
#
# Copyright (c) 2020-2026, Matthew Madison
#

AUTOMAKE_OPTIONS = subdir-objects foreign
ACLOCAL_AMFLAGS = -I m4
SUBDIRS =
DIST_SUBDIRS =

EXTRA_DIST = src/buildworker-init.in src/buildworker.service.in src/buildworker-setup.service.in \
             src/digsigserver.service.in src/buildworker-environment-setup.in \
             src/run-buildbot-worker.in src/run-digsigserver.in src/digsig-setup.in

base_scripts = buildworker-init buildworker-environment-setup run-buildbot-worker

systemdsystemunit_DATA = buildworker-setup.service buildworker.service
templatedir = $(prefix)/share/buildworker

if DIGSIG_ENABLED
template_DATA = digsigserver.service digsig-setup
digsig_scripts = run-digsigserver
else
digsig_scripts =
endif

dist_sbin_SCRIPTS = $(base_scripts) $(digsig_scripts)

buildworker-init: src/buildworker-init
	sed -e's,\$${prefix},$(prefix),g' -e's,$${exec_prefix},$(exec_prefix),g' < $< >$@
buildworker-environment-setup: src/buildworker-environment-setup
	sed -e's,\$${prefix},$(prefix),g' -e's,$${exec_prefix},$(exec_prefix),g' < $< >$@
run-buildbot-worker: src/run-buildbot-worker
	sed -e's,\$${prefix},$(prefix),g' -e's,$${exec_prefix},$(exec_prefix),g' < $< >$@
buildworker-setup.service: src/buildworker-setup.service
	sed -e's,\$${prefix},$(prefix),g' -e's,$${exec_prefix},$(exec_prefix),g' < $< >$@
buildworker.service: src/buildworker.service
	sed -e's,\$${prefix},$(prefix),g' -e's,$${exec_prefix},$(exec_prefix),g' < $< >$@
if DIGSIG_ENABLED
run-digsigserver: src/run-digsigserver
	sed -e's,\$${prefix},$(prefix),g' -e's,$${exec_prefix},$(exec_prefix),g' < $< >$@
digsig-setup: src/digsig-setup
	sed -e's,\$${prefix},$(prefix),g' -e's,$${exec_prefix},$(exec_prefix),g' < $< >$@
digsigserver.service: src/digsigserver.service
	sed -e's,\$${prefix},$(prefix),g' -e's,$${exec_prefix},$(exec_prefix),g' < $< >$@
endif
