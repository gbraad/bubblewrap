AM_CFLAGS = $(WARN_CFLAGS)
CLEANFILES =
EXTRA_DIST =

GITIGNOREFILES = build-aux/ gtk-doc.make config.h.in aclocal.m4

bin_PROGRAMS = bwrap

bwrap_srcpath := $(srcdir)
include Makefile-bwrap.am

install-exec-hook:
if PRIV_MODE_SETUID
	$(SUDO_BIN) chown root $(DESTDIR)$(bindir)/bwrap
	$(SUDO_BIN) chmod u+s $(DESTDIR)$(bindir)/bwrap
endif

check_PROGRAMS = test-bwrap

test-bwrap: bwrap
	rm -rf test-bwrap
	cp bwrap test-bwrap
if PRIV_MODE_SETUID
	$(SUDO_BIN) chown root test-bwrap
	$(SUDO_BIN) chmod u+s test-bwrap
endif

include Makefile-docs.am

TESTS = tests/test-basic.sh tests/test-run.sh
TESTS_ENVIRONMENT = PATH=$$(cd $(top_builddir) && pwd):$${PATH}

if ENABLE_BASH_COMPLETION
bashcompletiondir = $(BASH_COMPLETION_DIR)
dist_bashcompletion_DATA = completions/bash/bwrap
endif

-include $(top_srcdir)/git.mk
