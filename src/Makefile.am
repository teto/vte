bin_PROGRAMS =
noinst_PROGRAMS = testvte

CLEANFILES =
DISTCLEANFILES =
MAINTAINERCLEANFILES =
EXTRA_DIST =

# The library

headerdir = $(includedir)/vte-$(VTE_API_VERSION)/vte
header_HEADERS = \
	vte/vte.h \
	vte/vtedeprecated.h \
	vte/vteenums.h \
	vte/vteglobals.h \
	vte/vtemacros.h \
	vte/vtepty.h \
	vte/vteregex.h \
	vte/vteterminal.h \
	$(NULL)

nodist_header_HEADERS = \
	vte/vtetypebuiltins.h \
	vte/vteversion.h \
	$(NULL)

lib_LTLIBRARIES = libvte-@VTE_API_MAJOR_VERSION@.@VTE_API_MINOR_VERSION@.la

EXTRA_libvte_@VTE_API_MAJOR_VERSION@_@VTE_API_MINOR_VERSION@_la_SOURCES = \
	box_drawing_generate.sh \
	marshal.list \
	vteseq-n.gperf \
	vteseq-n.cc \
	vtetypebuiltins.cc.template \
	vtetypebuiltins.h.template \
	$(NULL)

libvte_@VTE_API_MAJOR_VERSION@_@VTE_API_MINOR_VERSION@_la_SOURCES = \
	vte/vte.h \
	vte/vtedeprecated.h \
	vte/vteenums.h \
	vte/vteglobals.h \
	vte/vtemacros.h \
	vte/vtepty.h \
	vte/vteregex.h \
	vte/vteterminal.h \
	buffer.h \
	caps.cc \
	caps.h \
	debug.cc \
	debug.h \
	iso2022.cc \
	iso2022.h \
	keymap.cc \
	keymap.h \
	matcher.cc \
	matcher.h \
	pty.cc \
	reaper.cc \
	reaper.hh \
	ring.cc \
	ring.h \
	table.cc \
	table.h \
	vte.cc \
	vteaccess.cc \
	vteaccess.h \
	vteconv.cc \
	vteconv.h \
	vtedefines.hh \
	vtedraw.cc \
	vtedraw.hh \
	vtegtk.cc \
	vtegtk.hh \
	vteinternal.hh \
	vtepcre2.h \
	vtepty-private.h \
	vteregex.cc \
	vteregexinternal.hh \
	vterowdata.cc \
	vterowdata.h \
	vtespawn.cc \
	vtespawn.hh \
	vteseq.cc \
	vteseq-list.h \
	vtestream.cc \
	vtestream.h \
	vtestream-base.h \
	vtestream-file.h \
	vtetree.cc \
	vtetree.h \
	vtetypes.cc \
	vtetypes.hh \
	vteunistr.cc \
	vteunistr.h \
	vteutils.cc \
	vteutils.h \
	$(NULL)

nodist_libvte_@VTE_API_MAJOR_VERSION@_@VTE_API_MINOR_VERSION@_la_SOURCES = \
	box_drawing.h \
	marshal.cc \
	marshal.h \
	vteresources.cc \
	vtetypebuiltins.cc \
	vte/vtetypebuiltins.h \
	vte/vteversion.h \
	$(NULL)

libvte_@VTE_API_MAJOR_VERSION@_@VTE_API_MINOR_VERSION@_la_CPPFLAGS = \
	-DG_LOG_DOMAIN=\"Vte\" \
	-DVTE_API_VERSION=\"$(VTE_API_VERSION)\" \
	-DDATADIR='"$(datadir)"' \
	-DLIBEXECDIR='"$(libexecdir)"' \
	-DLOCALEDIR='"$(localedir)"' \
	-DGLIB_DISABLE_DEPRECATION_WARNINGS \
	-DVTE_COMPILATION \
	-I$(srcdir)/vte \
	-I$(builddir)/vte \
	$(AM_CPPFLAGS)

libvte_@VTE_API_MAJOR_VERSION@_@VTE_API_MINOR_VERSION@_la_CXXFLAGS = \
	$(VTE_CFLAGS) \
	$(AM_CXXFLAGS)

libvte_@VTE_API_MAJOR_VERSION@_@VTE_API_MINOR_VERSION@_la_LDFLAGS = \
	$(VTE_CXXLDFLAGS) \
	-version-info $(LT_VERSION_INFO) \
	$(AM_LDFLAGS)

libvte_@VTE_API_MAJOR_VERSION@_@VTE_API_MINOR_VERSION@_la_LIBADD = \
	$(VTE_LIBS)

# Generated sources

VTESEQ_BUILTSOURCES = vteseq-list.h vteseq-n.cc
BUILT_SOURCES = box_drawing.h marshal.cc marshal.h vtetypebuiltins.cc vte/vtetypebuiltins.h vteresources.cc $(VTESEQ_BUILTSOURCES)
MAINTAINERCLEANFILES += $(VTESEQ_BUILTSOURCES)
EXTRA_DIST += $(VTESEQ_BUILTSOURCES) box_drawing.txt box_drawing_generate.sh iso2022.txt
CLEANFILES += box_drawing.h marshal.cc marshal.h vtetypebuiltins.cc vte/vtetypebuiltins.h stamp-vtetypebuiltins.h vteresources.cc

box_drawing.h: box_drawing.txt box_drawing_generate.sh
	$(AM_V_GEN) $(srcdir)/box_drawing_generate.sh < $< > $@

marshal.cc: marshal.list
	$(AM_V_GEN) $(GLIB_GENMARSHAL) --prefix=_vte_marshal --header --body --internal $< > $@

marshal.h: marshal.list
	$(AM_V_GEN) $(GLIB_GENMARSHAL) --prefix=_vte_marshal --header --internal $< > $@

vte/vtetypebuiltins.h: stamp-vtetypebuiltins.h
	@true
stamp-vtetypebuiltins.h: vtetypebuiltins.h.template vte/vteenums.h vte/vtedeprecated.h
	$(AM_V_GEN) $(GLIB_MKENUMS) --template $< $(filter %.h,$^) > xgen-vtbh \
	&& (cmp -s xgen-vtbh vte/vtetypebuiltins.h || cp xgen-vtbh vte/vtetypebuiltins.h ) \
	&& rm -f xgen-vtbh \
	&& echo timestamp > $(@F)

vtetypebuiltins.cc: vtetypebuiltins.cc.template vte/vteenums.h vte/vtedeprecated.h
	$(AM_V_GEN) $(GLIB_MKENUMS) --template $< $(filter %.h,$^) > xgen-vtbc \
	&& (cmp -s xgen-vtbc vtetypebuiltins.cc || cp xgen-vtbc vtetypebuiltins.cc ) \
	&& rm -f xgen-vtbc

vteseq-n.cc: vteseq-n.gperf
	$(AM_V_GEN) $(top_srcdir)/missing --run gperf -m 100 $< > $@.tmp && \
	mv -f $@.tmp $@

vteseq-list.h: vteseq-n.gperf
	$(AM_V_GEN) echo '/* Generated file.  Do not edit */' > $@.tmp && \
	cat $^ | grep -v '^#' | grep '\<VTE_SEQUENCE_HANDLER\>'| sed 's/.*, //' | LANG=C sort -u >> $@.tmp && \
	mv -f $@.tmp $@

vteresources.cc: vte.gresource.xml Makefile $(shell $(GLIB_COMPILE_RESOURCES) --generate-dependencies vte.gresource.xml)
	$(AM_V_GEN)$(GLIB_COMPILE_RESOURCES) --target $@ --sourcedir . --generate-source --c-name _vte $<

# C Test application

testvte_SOURCES = \
	vteapp.c \
	vtepcre2.h \
	debug.c \
	debug.h \
	$(NULL)

testvte_CPPFLAGS = \
	-DGLIB_DISABLE_DEPRECATION_WARNINGS \
	-DGDK_DISABLE_DEPRECATION_WARNINGS \
	-I$(srcdir)/vte \
	-I$(builddir)/vte \
	$(AM_CPPFLAGS)

testvte_CFLAGS = \
	$(VTE_CFLAGS) \
	$(AM_CFLAGS)

testvte_LDADD = \
	libvte-$(VTE_API_VERSION).la \
	$(VTE_LIBS)

# Misc unit tests and utilities

noinst_PROGRAMS += interpret slowcat
noinst_SCRIPTS = decset osc window
EXTRA_DIST += $(noinst_SCRIPTS)

check_PROGRAMS = \
	dumpkeys \
	reaper \
	reflect-text-view \
	reflect-vte mev \
	table \
	xticker \
	vteconv \
	vtestream-file \
	test-vtetypes \
	$(NULL)

dist_check_SCRIPTS = \
	check-doc-syntax.sh \
	test-vte-sh.sh \
	$(NULL)

TESTS = \
	reaper \
	table \
	test-vtetypes \
	vteconv \
	vtestream-file \
	$(dist_check_SCRIPTS) \
	$(NULL)

TESTS_ENVIRONMENT = \
	srcdir="$(srcdir)" \
	top_builddir="$(top_builddir)" \
	VTE_API_VERSION="$(VTE_API_VERSION)" \
	$(NULL)

reaper_CPPFLAGS = -DMAIN -I$(srcdir) -I $(builddir) $(AM_CPPFLAGS)
reaper_CXXFLAGS = $(VTE_CFLAGS) $(AM_CXXFLAGS)
reaper_SOURCES = \
	debug.cc \
	debug.h \
	reaper.cc \
	reaper.hh \
	$(NULL)
reaper_LDADD = $(VTE_LIBS)

reflect_text_view_CPPFLAGS = -DUSE_TEXT_VIEW -I$(srcdir) -I $(builddir) $(AM_CPPFLAGS)
reflect_text_view_CFLAGS = $(VTE_CFLAGS) $(AM_CFLAGS)
reflect_text_view_SOURCES = reflect.c
reflect_text_view_LDADD = $(VTE_LIBS)

reflect_vte_CPPFLAGS = -DUSE_VTE  -I$(srcdir) -I $(builddir) $(AM_CPPFLAGS)
reflect_vte_CFLAGS = $(VTE_CFLAGS) $(AM_CFLAGS)
reflect_vte_SOURCES = reflect.c
reflect_vte_LDADD = libvte-$(VTE_API_VERSION).la $(VTE_LIBS)

interpret_SOURCES = \
	buffer.h \
	caps.cc \
	caps.h \
	debug.cc \
	debug.h \
	iso2022.cc \
	iso2022.h \
	matcher.cc \
	matcher.h \
	table.cc \
	table.h \
	vteconv.cc \
	vteconv.h \
	vtetree.cc \
	vtetree.h \
	interpret.c
interpret_CPPFLAGS = \
	-DINTERPRET_MAIN \
	-DVTE_API_VERSION=\"$(VTE_API_VERSION)\" \
	-I$(srcdir) \
	-I$(builddir) \
	$(AM_CPPFLAGS)
interpret_CFLAGS = \
	$(GLIB_CFLAGS) \
	$(GOBJECT_CFLAGS) \
	$(GTK_CFLAGS) \
	$(AM_CFLAGS)
interpret_CXXFLAGS = \
	$(GLIB_CFLAGS) \
	$(GOBJECT_CFLAGS) \
	$(GTK_CFLAGS) \
	$(AM_CXXFLAGS)
interpret_LDADD = \
	$(GLIB_LIBS) \
	$(GOBJECT_LIBS)

slowcat_SOURCES = \
	slowcat.c \
	$(NULL)
slowcat_CPPFLAGS = -I$(srcdir) -I$(builddir) $(AM_CPPFLAGS)
slowcat_CFLAGS = $(GLIB_CFLAGS) $(AM_CFLAGS)
slowcat_LDADD = $(GLIB_LIBS)

table_SOURCES = \
	buffer.h \
	caps.cc \
	caps.h \
	debug.cc \
	debug.h \
	matcher.cc \
	matcher.h \
	table.cc \
	table.h \
	vteconv.cc \
	vteconv.h \
	$(NULL)
table_CPPFLAGS = \
	-DTABLE_MAIN \
	-I$(srcdir) \
	-I$(builddir) \
	$(AM_CPPFLAGS)
table_CXXFLAGS = \
	$(GLIB_CFLAGS) \
	$(AM_CXXFLAGS)
table_LDADD = \
	$(GLIB_LIBS) \
	$(GOBJECT_LIBS)

test_vtetypes_SOURCES = \
	vtetypes.cc \
	vtetypes.hh \
	$(NULL)
test_vtetypes_CPPFLAGS = \
	-DMAIN \
	-I$(srcdir) \
	-I$(builddir) \
	$(AM_CPPFLAGS)
test_vtetypes_CXXFLAGS = \
	$(VTE_CFLAGS) \
	$(AM_CXXFLAGS)
test_vtetypes_LDADD = \
	$(VTE_LIBS) \
	$(NULL)

vtestream_file_SOURCES = \
	vtestream-base.h \
	vtestream-file.h \
	vtestream.cc \
	vtestream.h \
	vteutils.cc \
	vteutils.h \
	$(NULL)
vtestream_file_CPPFLAGS = \
	-DVTESTREAM_MAIN \
	-I$(srcdir) \
	-I$(builddir) \
	$(AM_CPPFLAGS)
vtestream_file_CXXFLAGS = \
	$(VTE_CFLAGS) \
	$(AM_CXXFLAGS)
vtestream_file_LDADD = \
	$(VTE_LIBS)

vteconv_SOURCES = buffer.h debug.cc debug.h vteconv.cc vteconv.h
vteconv_CPPFLAGS = -DVTECONV_MAIN -I$(srcdir) -I$(builddir) $(AM_CPPFLAGS)
vteconv_CXXFLAGS = $(VTE_CFLAGS) $(AM_CXXFLAGS)
vteconv_LDADD = $(VTE_LIBS)

dumpkeys_SOURCES = dumpkeys.c
dumpkeys_CPPFLAGS = -I$(srcdir) -I$(builddir) $(AM_CPPFLAGS)
dumpkeys_CFLAGS = $(GLIB_CFLAGS) $(AM_CFLAGS)
dumpkeys_LDADD = $(GLIB_LIBS)

mev_SOURCES = mev.c
mev_CPPFLAGS = -I$(srcdir) -I$(builddir) $(AM_CPPFLAGS)
mev_CFLAGS = $(GLIB_CFLAGS) $(AM_CFLAGS)
mev_LDADD = $(GLIB_LIBS)

xticker_SOURCES = xticker.c
xticker_CPPFLAGS = -I$(srcdir) -I$(builddir) $(AM_CPPFLAGS)
xticker_CFLAGS = $(GLIB_CFLAGS) $(AM_CFLAGS)
xticker_LDADD = $(GLIB_LIBS)

# Shell

profiledir = $(sysconfdir)/profile.d
dist_profile_DATA = vte.sh

.DELETE_ON_ERROR:

-include $(top_srcdir)/git.mk
