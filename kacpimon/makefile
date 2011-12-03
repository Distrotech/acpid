# kacpimon makefile

sources = acpi_ids.c kacpimon.c connection_list.c input_layer.c libnetlink.c \
	netlink.c
target = kacpimon
# debug build
#CFLAGS = -g -O0 -Wall -Wextra -Wundef -Wshadow -Werror
# release build
#CFLAGS = -O2 -Wall -Wextra -Wundef -Wshadow -Werror
# hybrid build, optimized, but with debugging symbols (Debian-style)
CFLAGS = -g -O2 -Wall -Wextra -Wundef -Wshadow -Werror

objects := $(sources:.c=.o)

# Default target
$(target) : $(objects)

depends := $(sources:.c=.d)

# Dependency files can be made from .c files like this...
# (the sed line adds the .d file itself as a target)
%.d : %.c
	@set -e; \
	rm -f $@; \
	$(CPP) -MM $(CPPFLAGS) $< > $@.$$$$; \
	sed 's,\($*\)\.o[ :]*,\1.o $@ : ,g' < $@.$$$$ > $@; \
	rm -f $@.$$$$

# Pull in all dependencies from the .d files.
-include $(depends)

SBIN = /usr/sbin
install: $(target)
	mkdir -p $(SBIN)
	install -m 750 kacpimon $(SBIN)

DISTTMP=/tmp
DISTNAME=kacpimon
FULLTMP = $(DISTTMP)/$(DISTNAME)
dist:
	rm -rf $(FULLTMP)
	mkdir -p $(FULLTMP)
	cp -a * $(FULLTMP)
	find $(FULLTMP) -type d -name CVS | xargs rm -rf
	make -C $(FULLTMP) clean
	rm -f $(FULLTMP)/cscope.out
	find $(FULLTMP) -name '*~' | xargs rm -f
	# Get rid of previous dist
	rm -f $(FULLTMP)/$(DISTNAME).tar.gz
	tar -C $(DISTTMP) -zcvf $(DISTNAME).tar.gz $(DISTNAME)
	rm -rf $(FULLTMP)

.PHONY : clean
clean :
	rm -f $(depends) $(objects) $(target)

