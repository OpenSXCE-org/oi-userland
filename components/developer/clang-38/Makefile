#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"), version 1.0.
# You may only use this file in accordance with the terms of version
# 1.0 of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source.  A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2016 Aurelien Larcher.  All rights reserved.
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME= clang-38
LLVM_NAME=llvm
CLANG_NAME=cfe

COMPONENT_VERSION= 3.8.1
COMPONENT_MAJOR_VERSION= \
  $(shell echo $(COMPONENT_VERSION) | $(GSED) -e 's/\([0-9]\+\.[0-9]\+\).*/\1/')
COMPONENT_PROJECT_URL = http://llvm.org/
COMPONENT_FMRI= developer/clang-3.8
COMPONENT_CLASSIFICATION= Development/C
COMPONENT_SUMMARY= LLVM tools and Clang compiler
COMPONENT_SRC= $(LLVM_NAME)-$(COMPONENT_VERSION).src
COMPONENT_ARCHIVE= $(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_HASH= \
  sha256:6e82ce4adb54ff3afc18053d6981b6aed1406751b8742582ed50f04b5ab475f9
COMPONENT_ARCHIVE_URL= \
  http://llvm.org/releases/$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)
COMPONENT_LICENSE= BSD

COMPONENT_ARCHIVE_1=    $(CLANG_NAME)-$(COMPONENT_VERSION).src.tar.xz
COMPONENT_ARCHIVE_HASH_1= \
  sha256:4cd3836dfb4b88b597e075341cae86d61c63ce3963e45c7fe6a8bf59bb382cdf
COMPONENT_ARCHIVE_URL_1= http://llvm.org/releases/$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE_1)

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/cmake.mk
include $(WS_MAKE_RULES)/ips.mk

CMAKE_PREFIX= /usr/clang/$(COMPONENT_MAJOR_VERSION)

PATH=/usr/sbin:/usr/bin:/usr/perl5/bin:/usr/gnu/bin

COMPONENT_POST_UNPACK_ACTION += \
  $(UNPACK) $(USERLAND_ARCHIVES)$(COMPONENT_ARCHIVE_1) && \
	mv $(CLANG_NAME)-$(COMPONENT_VERSION).src $(COMPONENT_SRC)/tools/clang

COMPONENT_PRE_CONFIGURE_ACTION =        (cp -a $(SOURCE_DIR)/* $(@D))

COMPONENT_POST_INSTALL_ACTION =  \
for file in `echo $(PROTO_DIR)/$(CMAKE_PREFIX)/bin/*`; do \
	elfedit -e 'dyn:runpath $$ORIGIN/../lib' $$file ; \
done && \
for file in `echo $(PROTO_DIR)/$(CMAKE_PREFIX)/lib/*.so`; do \
	elfedit -e 'dyn:delete RUNPATH' $$file ; \
	elfedit -e 'dyn:delete RPATH' $$file ; \
done && \
for file in \
	`ggrep -rlh '^\#!*/usr/bin/env python' $(PROTO_DIR)/$(CMAKE_PREFIX)`; do \
  sed -i -e 's,^\#!*/usr/bin/env python,\#!$(PYTHON),' $$file; \
done

COMPONENT_TEST_TARGETS = check-all
COMPONENT_TEST_ENV += PATH=/usr/gnu/bin:/usr/bin

CMAKE_OPTIONS += -DCMAKE_C_COMPILER=$(CC)
CMAKE_OPTIONS += -DCMAKE_CXX_COMPILER=$(CXX)
CMAKE_OPTIONS += -DGCC_INSTALL_PREFIX=$(GCC_ROOT)
CMAKE_OPTIONS += -DCMAKE_CXX_LINK_FLAGS="-L$(GCC_ROOT)/lib -Wl,-rpath,$(GCC_ROOT)/lib"
CMAKE_OPTIONS += -DLLVM_ENABLE_ASSERTIONS=ON
CMAKE_OPTIONS += -DCMAKE_BUILD_TYPE="Release"


build: $(BUILD_32)

install: $(INSTALL_32)

test: $(TEST_32)

REQUIRED_PACKAGES += library/libxml2
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/g++-4-runtime
REQUIRED_PACKAGES += system/library/gcc-4-runtime
REQUIRED_PACKAGES += system/library/math
