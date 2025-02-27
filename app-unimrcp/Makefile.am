MAINTAINERCLEANFILES   = Makefile.in

AM_CPPFLAGS            = -I$(top_srcdir)/include $(UNIMRCP_INCLUDES) $(ASTERISK_INCLUDES)
AM_CFLAGS              = -DAST_MODULE_SELF_SYM="__internal_app_unimrcp"

mod_LTLIBRARIES        = app_unimrcp.la

app_unimrcp_la_SOURCES = audio_queue.c \
                         speech_channel.c \
                         ast_unimrcp_framework.c \
                         app_msg_process_dispatcher.c \
												 app_channel_methods.c \
                         app_datastore.c \
                         app_mrcpsynth.c \
                         app_mrcprecog.c \
                         app_mrcpverif.c \
                         app_synthandrecog.c \
                         app_recogverif.c \
                         app_unimrcp.c
app_unimrcp_la_LDFLAGS = -avoid-version -no-undefined -module
app_unimrcp_la_LIBADD  = $(UNIMRCP_LIBS)

XMLDOC_FILES           = app_mrcpsynth.c \
                         app_mrcprecog.c \
                         app_mrcpverif.c \
                         app_recogverif.c \
                         app_synthandrecog.c \
                         app_datastore.c

all-local: .xmldocs/app_unimrcp-en_US.xml

.xmldocs/app_unimrcp-en_US.xml: $(XMLDOC_FILES)
	mkdir -p .xmldocs
	@printf "Building Documentation: $@"
	@echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>" > $@
	@echo "<!DOCTYPE docs SYSTEM \"appdocsxml.dtd\">" >> $@
	@echo "<docs xmlns:xi=\"http://www.w3.org/2001/XInclude\">" >> $@
	@for i in $(XMLDOC_FILES); do \
		$(AWK) -f $(top_srcdir)/build/xmldocs/get_documentation $$i >> $@ ; \
	done ;
	@echo
	@echo "</docs>" >> $@ 

clean-local:
	rm -rf .xmldocs

install-data-local:
	test -d $(DESTDIR)$(asterisk_xmldoc_dir) || $(mkinstalldirs) $(DESTDIR)$(asterisk_xmldoc_dir)
	test -d $(DESTDIR)$(asterisk_conf_dir) || $(mkinstalldirs) $(DESTDIR)$(asterisk_conf_dir)
	$(INSTALL) -m 644 .xmldocs/*.xml $(DESTDIR)$(asterisk_xmldoc_dir)
	test -f $(DESTDIR)$(asterisk_conf_dir)/mrcp.conf || $(INSTALL) -m 644 $(top_srcdir)/conf/mrcp.conf $(DESTDIR)$(asterisk_conf_dir)

load: 
	asterisk -rx "module load app_unimrcp.so"

unload: 
	asterisk -rx "module unload app_unimrcp.so"
