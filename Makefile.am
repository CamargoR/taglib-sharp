SUBDIRS = \
       	  src    \
       	  examples \
       	  docs

pkgconfig_in_files = taglib-sharp.pc.in
pkgconfigdir = $(datadir)/pkgconfig
pkgconfig_DATA = $(pkgconfig_in_files:.pc.in=.pc)

EXTRA_DIST =             \
   $(pkgconfig_in_files) \
   TaglibSharp.sln

DISTCLEANFILES = taglib-sharp.pc

MAINTAINERCLEANFILES = \
	compile \
	INSTALL \
	config.h.in \
	aclocal.m4 \
	ltmain.sh \
	Makefile.in \
	depcomp \
	missing \
	install-sh \
	configure \
	config.sub \
	config.guess \
	mkinstalldirs


all: sln_build
	echo "Building TaglibSharp solution"

test: all
	nuget install NUnit.Runners -Version 3.9.0 -OutputDirectory packages
	$(MONO) packages/NUnit.ConsoleRunner.3.9.0/tools/nunit3-console.exe --labels=All $(srcdir)/src/TaglibSharp.Tests/bin/Debug/$(TARGET_FRAMEWORK)/TaglibSharp.Tests.dll

distwin: all
	mkdir -p $(srcdir)/$(WINDIR)
	cp $(srcdir)/NEWS $(srcdir)/$(WINDIR)/NEWS.txt
	cp $(srcdir)/ChangeLog $(srcdir)/$(WINDIR)/ChangeLog.txt
	cp $(srcdir)/COPYING $(srcdir)/$(WINDIR)/COPYING.txt
	cp $(srcdir)/README.md $(srcdir)/$(WINDIR)/README.txt
	cp $(srcdir)/AUTHORS $(srcdir)/$(WINDIR)/AUTHORS.txt
	if [ -e $(srcdir)/windows-files ];					\
	  then cp -r $(srcdir)/windows-files/* $(srcdir)/$(WINDIR);		\
	fi
	cd $(srcdir)/src && make distwin
	zip -9 -r $(srcdir)/$(WINDIR).zip $(srcdir)/$(WINDIR)
	rm -rf $(srcdir)/$(WINDIR)

include $(top_srcdir)/build/msbuild.include
