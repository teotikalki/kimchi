#
# Kimchi
#
# Copyright IBM Corp, 2013-2016
#
# This library is free software; you can redistribute it and/or
# modify it under the terms of the GNU Lesser General Public
# License as published by the Free Software Foundation; either
# version 2.1 of the License, or (at your option) any later version.
#
# This library is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# Lesser General Public License for more details.
#
# You should have received a copy of the GNU Lesser General Public
# License along with this library; if not, write to the Free Software
# Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301  USA

AC_INIT([kimchi], [m4_esyscmd([./build-aux/pkg-version --version])])

AC_SUBST([PACKAGE_VERSION],
         [m4_esyscmd([./build-aux/pkg-version --version])])

AC_SUBST([PACKAGE_RELEASE],
         [m4_esyscmd([./build-aux/pkg-version --release])])

# Testing for version and release
AS_IF([test "x$PACKAGE_VERSION" = x],
      AC_MSG_ERROR([package version not defined]))
AS_IF([test "x$PACKAGE_RELEASE" = x],
      AC_MSG_ERROR([package release not defined]))

AC_CONFIG_AUX_DIR([build-aux])
AM_INIT_AUTOMAKE([-Wno-portability])
AM_PATH_PYTHON([2.6])
AC_PATH_PROG([PEP8], [pep8], [/usr/bin/pep8])
AC_PATH_PROG([GIT], [git], [/usr/bin/git])
AC_PATH_PROG([RPMLINT], [rpmlint], [/usr/bin/rpmlint])
AC_PYTHON_MODULE([unittest])
AC_SUBST([HAVE_PYMOD_UNITTEST])
AC_SUBST([PYTHON_VERSION])
AM_GNU_GETTEXT([external])
AM_GNU_GETTEXT_VERSION([0.10])
AC_PATH_PROG([CHEETAH], [cheetah], [/usr/bin/cheetah])

# Checking for pyflakes
AC_PATH_PROG([PYFLAKES], [pyflakes])
if test "x$PYFLAKES" = "x"; then
  AC_MSG_WARN([pyflakes not found])
fi

AC_ARG_ENABLE(
    [sample],
    [AS_HELP_STRING(
        [--enable-sample],
        [enable sample plugin @<:@default=no@:>@]
    )],
    ,
    [enable_sample="no"]
)

if test "${enable_sample}" = "yes"; then
AC_SUBST([ENABLE_SAMPLE], [True])
else
AC_SUBST([ENABLE_SAMPLE], [False])
fi

# check for systemd
PKG_PROG_PKG_CONFIG
AC_ARG_WITH([systemdsystemunitdir],
    AS_HELP_STRING([--with-systemdsystemunitdir=DIR], [Directory for systemd service files]),
    [], [with_systemdsystemunitdir=$($PKG_CONFIG --variable=systemdsystemunitdir systemd)])
if test "x$with_systemdsystemunitdir" != xno; then
    AC_SUBST([systemdsystemunitdir], [$with_systemdsystemunitdir])
fi

AC_ARG_WITH(
    [spice-html5],
    [AS_HELP_STRING([--with-spice-html5],
                    [Build Kimchi with spice-html5 @<:@default=no@:>@])],
    ,
    [with_spice_html5="no"]
)
AM_CONDITIONAL([WITH_SPICE], [test "x$with_spice_html5" = xyes])

AC_CONFIG_FILES([
    po/Makefile.in
    po/gen-pot
    Makefile
    docs/Makefile
    distros.d/Makefile
    control/Makefile
    control/vm/Makefile
    model/Makefile
    ui/Makefile
    ui/config/Makefile
    ui/css/Makefile
    ui/images/Makefile
    ui/js/Makefile
    ui/spice-html5/Makefile
    ui/spice-html5/css/Makefile
    ui/spice-html5/pages/Makefile
    ui/spice-html5/thirdparty/Makefile
    ui/pages/Makefile
    ui/pages/help/Makefile
    ui/pages/tabs/Makefile
    ui/pages/help/en_US/Makefile
    ui/pages/help/de_DE/Makefile
    ui/pages/help/es_ES/Makefile
    ui/pages/help/fr_FR/Makefile
    ui/pages/help/it_IT/Makefile
    ui/pages/help/ja_JP/Makefile
    ui/pages/help/ko_KR/Makefile
    ui/pages/help/pt_BR/Makefile
    ui/pages/help/ru_RU/Makefile
    ui/pages/help/zh_CN/Makefile
    ui/pages/help/zh_TW/Makefile
    ui/serial/Makefile
    ui/serial/libs/Makefile
    ui/serial/html/Makefile
    contrib/Makefile
    contrib/DEBIAN/Makefile
    contrib/DEBIAN/control
    contrib/kimchi.spec.fedora
    contrib/kimchi.spec.suse
    tests/Makefile
    xmlutils/Makefile
],[
    chmod +x po/gen-pot
])

AC_OUTPUT
