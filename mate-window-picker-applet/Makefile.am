libexec_PROGRAMS=mate-window-picker-applet

PKGDATADIR = $(datadir)/mate-window-picker-applet
AM_CFLAGS=\
	$(MATEWINDOWPICKER_DEPS_CFLAGS) 		\
	$(GCC_FLAGS) 				\
	-I$(top_builddir)			\
	-I$(top_srcdir)				\
	-D_GNU_SOURCE 				\
	-DMATELOCALEDIR=\""$(datadir)/locale"\" \
	-DPKGDATADIR=\"$(PKGDATADIR)\" \
	-DMATEWINDOWPICKER_MENU_UI_DIR=\""$(xmluidir)"\"

mate_window_picker_applet_LDADD = \
	$(MATEWINDOWPICKER_DEPS_LIBS) \
	-lm

mate_window_picker_applet_SOURCES = \
	applet.c \
	task-item.c \
	task-item.h \
	task-list.c \
	task-list.h \
	task-title.c \
	task-title.h 

appletdir       = $(datadir)/mate-panel/applets
applet_in_files = org.mate.panel.MateWindowPicker.mate-panel-applet.in
applet_DATA     = $(applet_in_files:.mate-panel-applet.in=.mate-panel-applet)

$(applet_in_files): $(applet_in_files).in Makefile
	$(AM_V_GEN)sed \
	-e "s|\@LOCATION\@|$(APPLET_LOCATION)|" \
	$< > $@

org.mate.panel.MateWindowPicker.mate-panel-applet: org.mate.panel.MateWindowPicker.mate-panel-applet.in $(INTLTOOL_MERGE) $(wildcard $(top_srcdir)/po/*po) ; $(INTLTOOL_MERGE) $(top_srcdir)/po $< $@ -d -u -c $(top_builddir)/po/.intltool-merge-cache

APPLET_LOCATION=$(libexecdir)/mate-window-picker-applet

servicedir       = $(datadir)/dbus-1/services
service_in_files = org.mate.panel.applet.MateWindowPickerFactory.service.in
service_DATA     = $(service_in_files:.service.in=.service)

org.mate.panel.applet.MateWindowPickerFactory.service: $(service_in_files)
	$(AM_V_GEN) $(SED) \
	-e "s|\@LOCATION\@|$(APPLET_LOCATION)|" \
	$< > $@

@INTLTOOL_XML_NOMERGE_RULE@
gsettings_SCHEMAS = org.mate.panel.applet.mate-window-picker-applet.gschema.xml

gsettings_SCHEMAS_in_in = $(gsettings_SCHEMAS:.xml=.xml.in.in)
@GSETTINGS_RULES@

%.gschema.xml.in: %.gschema.xml.in.in Makefile
	$(AM_V_GEN) $(SED) -e 's^\@GETTEXT_PACKAGE\@^$(GETTEXT_PACKAGE)^g' < $< > $@

xmluidir = $(datadir)/mate-panel/ui
xmlui_DATA = mate-window-picker-applet-menu.xml

EXTRA_DIST = \
	org.mate.panel.MateWindowPicker.mate-panel-applet.in.in \
	$(service_in_files) \
	$(ui_DATA) \
	$(convert_DATA) \
	$(gsettings_SCHEMAS_in_in) \
	$(xmlui_DATA)

CLEANFILES = \
	$(applet_DATA) \
	$(applet_DATA).in \
	$(gsettings_SCHEMAS_in) \
	$(gsettings_SCHEMAS) \
	$(service_DATA)

clean:
	rm -f $(desktop_DATA) $(desktop_DATA).in
