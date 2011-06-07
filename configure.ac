#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.67])
AC_INIT([cntlm],[0.91rc6],[smorar@gmail.com])
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

AC_CONFIG_FILES([libcntlm/Makefile cntlm/Makefile Makefile])
AC_OUTPUT
