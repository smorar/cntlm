ACLOCAL_AMFLAGS = -I m4
VER=`cat VERSION`
SUBDIRS = libcntlm cntlm
man_MANS = doc/cntlm.1
sysconf_DATA = doc/cntlm.conf

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = libcntlm.pc

win: buildwin
buildwin:
	@echo
	@echo "* This build target must be run from a Cywgin shell on Windows *"
	@echo "* and you also need InnoSetup installed                        *"
	@echo
	rm -f win/cntlm_manual.pdf
	groff -t -e -mandoc -Tps doc/cntlm.1 | ps2pdf - win/cntlm_manual.pdf
	cat doc/cntlm.conf | unix2dos > win/cntlm.ini
	cat COPYRIGHT LICENSE | unix2dos > win/license.txt
	sed "s/\$$VERSION/$(VER)/g" win/setup.iss.in > win/setup.iss
	cp /bin/cygwin1.dll /bin/cygrunsrv.exe win/
	cp cntlm/cntlm.exe win/
	strip win/cntlm.exe
	@echo
	@echo Now open folder "win", right-click "setup.iss", then "Compile".
	@echo InnoSetup will generate a new installer cntlm-X.XX-setup.exe
	@echo

