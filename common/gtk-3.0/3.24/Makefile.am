include ../common.am

dark/gtk-main.css: gtk-dark.css | dark
	cp "$<" "$@"
dark/gtk-main-dark.css: | dark
	touch "$@"

%/gtk.css %/gtk-dark.css: | %
	echo '@import url("resource:///org/gnome/arc-theme/$(subst gtk,gtk-main,$(notdir $@))");' > "$@"

%/assets: | %
	(cd "$(dir $@)" && $(LN_S) ../assets assets)

%/gtk.gresource.xml: | %/assets
	echo "<?xml version='1.0' encoding='UTF-8'?><gresources><gresource prefix='/org/gnome/arc-theme'>$(patsubst %,<file preprocess='to-pixdata'>%</file>,$(normal) $(hidpi))<file>gtk-main.css</file>$(if $(filter $(dir $@),dark/),,<file>gtk-main-dark.css</file>)</gresource></gresources>" > "$@"

%/gtk.gresource: %/gtk.gresource.xml %/gtk-main.css %/gtk-main-dark.css $(normal) $(hidpi)
	glib-compile-resources --sourcedir="$(dir $<)" --target="$@" "$<"

gtk3themedark_DATA = dark/gtk.css dark/gtk.gresource

