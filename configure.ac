dnl
dnl configure.ac - autoconf script for buildworker-setup
dnl
dnl Copyright (c) 2020 Matthew Madison
dnl
AC_INIT([buildworker-setup], [0.1.0])
AC_DEFINE([BUILDWORKER_SETUP_VERSION_MAJOR], [0], [Major version])
AC_DEFINE([BUILDWORKER_SETUP_VERSION_MINOR], [1], [Minor version])
AC_DEFINE([BUILDWORKER_SETUP_VERSION_MAINT], [0], [Maintenance level])
AM_INIT_AUTOMAKE([subdir-objects foreign])
AM_SILENT_RULES([yes])
AC_COPYRIGHT([
Copyright (c) 2020 Matthew Madison
])
AC_CONFIG_MACRO_DIR([m4])

AC_PREREQ([2.69])
LT_PREREQ([2.4])
LT_INIT([])

AC_CANONICAL_HOST
AC_PROG_INSTALL

AC_ARG_WITH([workerdir],
    AS_HELP_STRING([--with-workerdir=PATH], [path of build worker directory]),
    [], [with_workerdir=/scratch/buildworker])
AC_SUBST([WORKERDIR], [$with_workerdir])

AC_ARG_WITH([workeruser],
    AS_HELP_STRING([--with-workeruser=NAME], [username of build worker]),
    [], [with_workeruser=builder])
AC_SUBST([WORKERUSER], [$with_workeruser])

AC_ARG_WITH([buildbot-worker-prefix],
    AS_HELP_STRING([--with-buildbot-worker-prefix=PATH], [location of buildbot-worker package]),
    [], [with_buildbot_worker_prefix=/usr])
AC_SUBST([BBWORKER_PREFIX], [$with_buildbot_worker_prefix])

AC_ARG_WITH([etcdefaultdir],
    AS_HELP_STRING([--with-etcdefaultdir=PATH], [path to directory to hold build worker environment variable settings]),
    [], [with_etcdefaultdir=/etc/default])
AC_SUBST([ETCDEFAULTDIR], [$with_etcdefaultdir])

AC_ARG_WITH([systemdsystemunitdir],
    AS_HELP_STRING([--with-systemdsystemunitdir=DIR], [location for systemd service files]),
    [], [with_systemdsystemunitdir=check])

PKG_PROG_PKG_CONFIG([0.29])

AS_IF([test "x$with_systemdsystemunitdir" = "xcheck"],
    [with_systemdsystemunitdir=`$PKG_CONFIG --variable systemdsystemunitdir systemd`])
AC_SUBST([systemdsystemunitdir], [$with_systemdsystemunitdir])

AC_CONFIG_FILES(Makefile src/buildworker-init src/buildworker.service src/buildworker-setup.service)
AC_OUTPUT
