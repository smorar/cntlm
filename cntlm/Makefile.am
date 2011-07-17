bin_PROGRAMS = cntlm
cntlm_SOURCES = \
				acl.h \
				acl.c \
				conf.h \
				conf.c \
				direct.h \
				direct.c \
				forward.h \
				forward.c \
				globals.h \
				http.h \
				http.c \
				main.c \
				pages.h \
				pages.c \
				scanner.h \
				scanner.c
cntlm_CPPFLAGS = -I$(top_srcdir)/libcntlm
cntlm_LDFLAGS = -lpthread
cntlm_LDADD = ../libcntlm/libcntlm.la

