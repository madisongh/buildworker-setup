dnl
dnl configure.ac - autoconf script for buildworker-setup
dnl
dnl Copyright (c) 2020-2026, Matthew Madison
dnl
AC_INIT([buildworker-setup], [0.5.3])
AC_DEFINE([BUILDWORKER_SETUP_VERSION_MAJOR], [0], [Major version])
AC_DEFINE([BUILDWORKER_SETUP_VERSION_MINOR], [5], [Minor version])
AC_DEFINE([BUILDWORKER_SETUP_VERSION_MAINT], [3], [Maintenance level])
AM_INIT_AUTOMAKE([subdir-objects foreign])
AM_SILENT_RULES([yes])
AC_COPYRIGHT([
Copyright (c) 2020-2026, Matthew Madison
])
AC_CONFIG_MACRO_DIR([m4])

AC_PREREQ([2.69])
LT_PREREQ([2.4])
LT_INIT([])

AC_CANONICAL_HOST
AC_PROG_INSTALL
AC_PROG_SED

AC_ARG_WITH([workerdir],
    AS_HELP_STRING([--with-workerdir=PATH], [path of build worker directory]),
    [], [with_workerdir=/scratch/buildworker])
AC_SUBST([WORKERDIR], [$with_workerdir])

AC_ARG_WITH([workeruser],
    AS_HELP_STRING([--with-workeruser=NAME], [username of build worker]),
    [], [with_workeruser=builder])
AC_SUBST([WORKERUSER], [$with_workeruser])

AC_ARG_WITH([scripts-version],
    AS_HELP_STRING([--with-scripts-version=VER], [version of buildworker-scripts package to install]),
    [], [with_scripts_version=0.1.0-pre3])
AC_SUBST([WORKER_SCRIPTS_VERSION_FULL], [$with_scripts_version])
scripts_version_trimmed=`echo "$with_scripts_version" | sed -e's/-pre[[0-9]]*$//'`
AC_SUBST([WORKER_SCRIPTS_VERSION], [$scripts_version_trimmed])

AC_ARG_WITH([git-aws-secrets-version],
    AS_HELP_STRING([--with-git-aws-secrets-version=VER], [version of git-credential-aws-secrets package to install]),
    [], [with_git_aws_secrets_version=0.0.2])
AC_SUBST([WORKER_GCAS_VERSION], [$with_git_aws_secrets_version])

AC_ARG_ENABLE([digsigserver],
    AS_HELP_STRING([--enable-digisgserver], [enable use of digsigserver, default YES]),
    [enable_digsig=$enableval],
    [enable_digsig=yes])
AM_CONDITIONAL(DIGSIG_ENABLED, [test "$enable_digsig" = "yes"])

AC_ARG_WITH([digsigserver-version],
    AS_HELP_STRING([--with-digsigserver-version=VER], [version of digsigserver package to install]),
    [], [with_digsigserver_version=0.16.0])
AC_SUBST([WORKER_DIGSIG_VERSION], [$with_digsigserver_version])

AC_ARG_WITH([keyfile-uri],
    AS_HELP_STRING([--with-keyfile-uri=NAME], [URL for digsigserver keys]),
    [], [with_keyfile_uri=file:///usr/share/digsigserver/keyfiles])
AC_SUBST([KEYFILE_URI], [$with_keyfile_uri])

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

AC_CONFIG_FILES([Makefile src/buildworker-init src/buildworker-environment-setup src/run-buildbot-worker src/digsig-setup src/run-digsigserver src/buildworker.service src/buildworker-setup.service src/digsigserver.service])
AC_OUTPUT
