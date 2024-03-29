# This file will be processed with automake to create Makefile.in

##############################
# Applets
##############################

appletdir       = $(APPLETDIR)
applet_in_files = \
	org.ayatana.panel.IndicatorApplet.panel-applet.in \
	org.ayatana.panel.IndicatorAppletComplete.panel-applet.in \
	org.ayatana.panel.IndicatorAppletAppmenu.panel-applet.in \
	org.ayatana.panel.FastUserSwitchApplet.panel-applet.in
applet_DATA     = $(applet_in_files:.panel-applet.in=.panel-applet)

%.panel-applet.in: %.panel-applet.in.in Makefile
	$(AM_V_GEN)sed \
	    -e "s|\@LIBEXECDIR\@|$(libexecdir)|" \
	    $< > $@

%.panel-applet: %.panel-applet.in $(INTLTOOL_MERGE) $(wildcard $(top_srcdir)/po/*po) ; $(AM_V_GEN) LC_ALL=C $(INTLTOOL_MERGE) $(top_srcdir)/po $< $@ -d -u -c $(top_builddir)/po/.intltool-merge-cache


##############################
# DBus Services
##############################

servicedir       = $(datadir)/dbus-1/services
service_in_files = \
	org.gnome.panel.applet.IndicatorAppletFactory.service.in \
	org.gnome.panel.applet.IndicatorAppletCompleteFactory.service.in \
	org.gnome.panel.applet.IndicatorAppletAppmenuFactory.service.in \
	org.gnome.panel.applet.FastUserSwitchAppletFactory.service.in
service_DATA     = $(service_in_files:.service.in=.service)

%.service: %.service.in Makefile
	$(AM_V_GEN)sed \
	    -e "s|\@LIBEXECDIR\@|$(libexecdir)|" \
	    $< > $@


##############################
# Icons
##############################

iconsdir = $(datadir)/icons/hicolor/scalable/apps

icons_DATA = indicator-applet.svg

gtk_update_icon_cache = gtk-update-icon-cache -f -t $(datadir)/icons/hicolor

install-data-hook: update-icon-cache
uninstall-hook: update-icon-cache
update-icon-cache:
	@-if test -z "$(DESTDIR)"; then \
		echo "Updating Gtk icon cache."; \
		$(gtk_update_icon_cache); \
	else \
		echo "*** Icon cache not updated.  After (un)install, run this:"; \
		echo "***   $(gtk_update_icon_cache)"; \
	fi


##############################
# Autojunk
##############################

CLEANFILES =					\
	$(applet_in_files)			\
	$(applet_DATA)				\
	$(service_DATA)				\
	*.bak

EXTRA_DIST =					\
	$(icons_DATA)				\
	$(applet_in_files:.in=.in.in)		\
	$(service_in_files)

MAINTAINERCLEANFILES =				\
	Makefile.in


