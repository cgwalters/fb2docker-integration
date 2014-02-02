AC_PREREQ([2.63])
AC_INIT([fb2docker-integration], [2014.1], [walters@verbum.org], [fb2docker-integration], [https://github.com/cgwalters/rpm-ostree])
AC_CONFIG_HEADER([config.h])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_AUX_DIR([build-aux])

OS_NAME="FB2Docker"
OS_ID=$PACKAGE_TARNAME
OS_VERSION=$PACKAGE_VERSION
OS_PRETTY_NAME="$OS_NAME Fedora Remix $OS_VERSION"

AC_SUBST([OS_NAME])
AC_SUBST([OS_ID])
AC_SUBST([OS_VERSION])
AC_SUBST([OS_PRETTY_NAME])

AM_INIT_AUTOMAKE([1.11 -Wno-portability foreign no-define tar-ustar no-dist-gzip dist-xz])
AM_MAINTAINER_MODE([enable])
AM_SILENT_RULES([yes])

AM_PATH_PYTHON([2.6])
PKG_PROG_PKG_CONFIG

AC_PROG_CC
AM_PROG_CC_C_O

changequote(,)dnl
if test "x$GCC" = "xyes"; then
  WARN_CFLAGS="-Wall -Werror=strict-prototypes -Werror=missing-prototypes \
		-Werror=implicit-function-declaration \
		-Werror=pointer-arith -Werror=init-self -Werror=format=2 \
		-Werror=format-security \
		-Werror=missing-include-dirs -Werror=aggregate-return \
		-Werror=declaration-after-statement"
fi
changequote([,])dnl
AC_SUBST(WARN_CFLAGS)

# Initialize libtool
LT_PREREQ([2.2.4])
LT_INIT([disable-static])

PKG_CHECK_MODULES(GIO_UNIX, [gio-unix-2.0 >= 2.34.0])

AC_ARG_WITH([systemdsystemunitdir],
            AS_HELP_STRING([--with-systemdsystemunitdir=DIR],
                           [Directory for systemd service files]),
                [with_systemdsystemunitdir=$withval], [with_systemdsystemunitdir=$($PKG_CONFIG --variable=systemdsystemunitdir systemd)])
AC_SUBST(SYSTEMD_SYSTEM_UNIT_DIR, [$with_systemdsystemunitdir])

AC_CONFIG_FILES([
Makefile
])
AC_OUTPUT

echo "
    $PACKAGE $VERSION
"
