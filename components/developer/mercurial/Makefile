#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#

#
# Copyright (c) 2011, 2016, Oracle and/or its affiliates. All rights reserved.
#

include ../../../make-rules/shared-macros.mk

PATH=/usr/bin:/usr/gnu/bin:/usr/sbin

COMPONENT_NAME=		mercurial
COMPONENT_VERSION=	3.8.4
COMPONENT_REVISION=	1
COMPONENT_PROJECT_URL=	http://mercurial-scm.org/
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	\
    sha256:4b2e3ef19d34fa1d781cb7425506a05d4b6b1172bab69d6ea78874175fdf3da6
COMPONENT_ARCHIVE_URL=	https://www.mercurial-scm.org/release/$(COMPONENT_ARCHIVE)
COMPONENT_BUGDB=	utility/hg

# Mercurial does not yet support Python 3.
PYTHON_VERSIONS = 2.7 2.6

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/setup.py.mk
include $(WS_MAKE_RULES)/ips.mk

COMPONENT_POST_INSTALL_ACTION = \
	(cd $(PROTO_DIR)/usr/bin ; $(MV) -f hg hg-$(PYTHON_VERSION))

PKG_PROTO_DIRS +=	$(COMPONENT_SRC)/contrib
PKG_PROTO_DIRS +=	$(COMPONENT_SRC)/doc

# Use bash in sh mode for the tests; using /bin/sh on Solaris hasn't always
# worked, and using /bin/bash doesn't always work, either.  Also skip the
# tests which try to check all the code in the userland gate.  And finally,
# test the bits from the proto area, rather than rebuilding.  Given the way the
# test suite works, the hg executable must be named "hg".
TEST_BLACKLIST = \
	test-check-code.t \
	test-check-config.t \
	test-devel-warnings.t \
	test-hghave.t \
	test-module-imports.t \
	test-run-tests.t
COMPONENT_PRE_TEST_ACTION = \
	(cd $(BUILD_DIR); rm -f sh; ln -s /bin/bash sh; \
	printf "%s\n" $(TEST_BLACKLIST) > blacklist); \
	(cd $(PROTOUSRBINDIR); rm -f hg; ln -s hg-$(PYTHON_VERSION) hg)

COMPONENT_TEST_DIR =	$(COMPONENT_SRC)/tests
COMPONENT_TEST_ENV =	PYTHONPATH=$(PROTO_DIR)/$(PYTHON_LIB)
COMPONENT_TEST_ENV +=	TERM=dumb
COMPONENT_TEST_ENV +=	HGTEST_JOBS=$(or $(HGTEST_JOBS),1)
COMPONENT_TEST_ENV +=	PATH=/usr/gnu/bin:/usr/bin
COMPONENT_TEST_ARGS =	./run-tests.py \
			--shell $(BUILD_DIR)/sh \
			--with-hg $(PROTOUSRBINDIR)/hg \
			--blacklist $(BUILD_DIR)/blacklist

ASLR_MODE = $(ASLR_NOT_APPLICABLE)

# Assuming you have docutils installed, update the manpages patch for a new
# mercurial version based on the patches applied to the source and to the
# manpage generator.  This works either against source that's already been
# patched with the older manpages.patch or against a fresh tarball.  Eventually
# we'll have docutils in the CBE and we'll be able to regenerate the manpages
# as part of the build, rather than patching them.
#
# Only build this target if it doesn't already exist, since this recipe is just
# for the component maintainer's benefit.
patches/manpages.patch: $(SOURCE_DIR)/.unpacked \
    $(SOURCE_DIR)/.patched-rst.patch $(SOURCE_DIR)/.patched-hgmanpage.patch
	if [[ -f $@ ]]; then exit 0; fi; \
	if [[ -f $(COMPONENT_SRC)/doc/hg.1.~1~ ]]; then \
		cd $(COMPONENT_SRC)/doc; gmake man || true; cd ../..; \
		for f in hg.1 hgignore.5 hgrc.5; do \
			diff -u $(COMPONENT_SRC)/doc/$$f.~1~ $(COMPONENT_SRC)/doc/$$f; \
		done > $@; \
	else \
		for f in hg.1 hgignore.5 hgrc.5; do \
			cp -p $(COMPONENT_SRC)/doc/$$f $(COMPONENT_SRC)/doc/$$f.orig; \
		done; \
		cd $(COMPONENT_SRC)/doc; gmake man || true; cd ../..; \
		for f in hg.1 hgignore.5 hgrc.5; do \
			diff -u $(COMPONENT_SRC)/doc/$$f.orig $(COMPONENT_SRC)/doc/$$f; \
		done > $@; \
	fi || true

# common targets
build:		$(BUILD_32)

install:	$(INSTALL_32)

test:		install $(TEST_32)

REQUIRED_PACKAGES += runtime/python-26
REQUIRED_PACKAGES += runtime/python-27
REQUIRED_PACKAGES += system/library
