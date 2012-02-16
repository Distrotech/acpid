AM_DISTCHECK_CONFIGURE_FLAGS = --enable-kacpimon
if KACPIMON
DIST_SUBDIRS =   kacpimon
endif
AM_CFLAGS = -Wall -Wmissing-declarations -Wmissing-prototypes -Wredundant-decls -Wshadow -Wstrict-prototypes -Wformat=2
AM_CPPFLAGS = -include $(top_srcdir)/config.h

sbin_PROGRAMS = acpid
bin_PROGRAMS = acpi_listen

acpid_SOURCES = acpid.c acpi_ids.c connection_list.c event.c input_layer.c inotify_handler.c libnetlink.c log.c netlink.c proc.c sock.c ud_socket.c \
				acpid.h  acpi_genetlink.h  acpi_ids.h  config.h  connection_list.h  event.h  genetlink.h  inotify_handler.h  input_layer.h  \
				libnetlink.h  log.h  netlink.h  proc.h  sock.h  ud_socket.h

acpi_listen_SOURCES = acpi_listen.c log.c ud_socket.c

dist_man8_MANS = acpid.8 acpi_listen.8

dist_doc_DATA = COPYING Changelog README TESTPLAN TODO

