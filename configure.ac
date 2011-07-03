dnl Process this file with autoconf to produce a configure script.

dnl Copyright (C) 2011 Sameer Morar.
dnl
dnl This file is part of cntlm
dnl
dnl cntlm is free software; you can redistribute it and/or modify
dnl it under the terms of the GNU Lesser General Public License as
dnl published by the Free Software Foundation; either version 2.1 of
dnl the License, or (at your option) any later version.
dnl
dnl cntlm is distributed in the hope that it will be useful,
dnl but WITHOUT ANY WARRANTY; without even the implied warranty of
dnl MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
dnl GNU Lesser General Public License for more details.
dnl
dnl You should have received a copy of the GNU Lesser General Public
dnl License along with cntlm; if not, write to the Free Software
dnl Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA
dnl 02110-1301, USA

AC_PREREQ([2.67])
AC_INIT([cntlm],[0.91rc6],[dave@awk.cz])
AM_INIT_AUTOMAKE
AC_CONFIG_SRCDIR([cntlm/main.c])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([m4])

# Checks for programs.
AC_PROG_CC
AC_PROG_INSTALL
AM_PROG_CC_C_O

# Checks for libraries.
LT_INIT

# Checks for header files.
AC_CHECK_HEADERS([arpa/inet.h fcntl.h netdb.h netinet/in.h stddef.h stdint.h stdlib.h string.h strings.h sys/param.h sys/socket.h sys/time.h syslog.h termios.h unistd.h pthread.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_HEADER_STDBOOL
AC_TYPE_INT64_T
AC_TYPE_SIZE_T
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T
AC_TYPE_UINT64_T
AC_TYPE_UINT8_T
AC_CHECK_TYPE([socklen_t], ,[
   AC_MSG_CHECKING([for socklen_t equivalent])
   AC_CACHE_VAL([curl_cv_socklen_t_equiv],
   [
	 # Systems have either "struct sockaddr *" or
	 # "void *" as the second argument to getpeername
	 curl_cv_socklen_t_equiv=
	 for arg2 in "struct sockaddr" void; do
	  for t in int size_t unsigned long "unsigned long"; do
	     AC_TRY_COMPILE([
		#include <sys/types.h>
		#include <sys/socket.h>

		int getpeername (int, $arg2 *, $t *);
	     ],[
		$t len;
		getpeername(0,0,&len);
	     ],[
		curl_cv_socklen_t_equiv="$t"
		break
	     ])
	  done
	 done

	 if test "x$curl_cv_socklen_t_equiv" = x; then
	  AC_MSG_ERROR([Cannot find a type to use in place of socklen_t])
	 fi
      ])
      AC_MSG_RESULT($curl_cv_socklen_t_equiv)
      AC_DEFINE_UNQUOTED(socklen_t, $curl_cv_socklen_t_equiv,
			[type to use in place of socklen_t if not defined])],
      [#include <sys/types.h>
#include <sys/socket.h>])

#AC_CHECK_TYPE([socklen_t], [],
#            [AC_DEFINE_UNQUOTED([socklen_t], [uint32_t],
#               [Define to `uint32_t'
#                if <sys/socket.h> does not define.])])

# Checks for library functions.
AC_FUNC_FORK
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_CHECK_FUNCS([dup2 gethostbyname gethostname inet_ntoa memset select socket strcasecmp strchr strcspn strdup strerror strncasecmp strstr strtol strtoul])
AC_C_BIGENDIAN

AC_CONFIG_FILES([
	libcntlm/Makefile
	cntlm/Makefile
	Makefile
	libcntlm.pc
	libcntlm.spec
	libcntlm/cntlm.h
])
AC_OUTPUT
