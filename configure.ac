dnl Process this file with autoconf to produce a configure script.
AC_INIT([liblocker], [10.0.2])
AC_CONFIG_SRCDIR([locker.h])

AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_RANLIB
AC_PROG_MKDIR_P

AC_ARG_ENABLE([nfs],
	[AS_HELP_STRING([--enable-nfs], [support for kNFS lockers (deprecated)])])

if test "$enable_nfs" = "yes"; then
    AC_DEFINE([ENABLE_NFS],[1],[Support for kNFS lockers (deprecated).])

    AC_PATH_PROG(MOUNT_CMD, mount, , ${PATH}:/sbin:/usr/sbin)
    AC_PATH_PROG(UMOUNT_CMD, umount, , ${PATH}:/sbin:/usr/sbin)

    AC_MSG_CHECKING(if rpcsvc/mount.h needs sys/fs/nfs.h)
    AC_TRY_COMPILE([
#include <rpc/rpc.h>
#include <rpcsvc/mount.h>
    ], , AC_MSG_RESULT(no), AC_TRY_COMPILE([
#include <rpc/rpc.h>
#include <sys/fs/nfs.h>
#include <rpcsvc/mount.h>
    ], , AC_MSG_RESULT(yes)
    AC_DEFINE(NEED_SYS_FS_NFS_H),
    AC_MSG_ERROR(couldn't include rpcsvc/mount.h)))

    ATHENA_KRB4_REQUIRED
fi

ATHENA_KRB5_REQUIRED
ATHENA_AFS_REQUIRED
ATHENA_HESIOD_REQUIRED

AC_CONFIG_FILES([Makefile])
AC_OUTPUT