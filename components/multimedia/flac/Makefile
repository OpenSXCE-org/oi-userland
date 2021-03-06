#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL)". You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2014 (c) Aurelien Larcher. All rights reserved.
#
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		flac
COMPONENT_VERSION=	1.3.1
COMPONENT_FMRI=		codec/flac
COMPONENT_CLASSIFICATION=System/Multimedia Libraries
COMPONENT_PROJECT_URL=	http://flac.sourceforge.net/
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_HASH=	\
    sha256:4773c0099dba767d963fd92143263be338c48702172e8754b9bc5103efe1c56c
COMPONENT_ARCHIVE_URL=	http://downloads.us.xiph.org/releases/flac/$(COMPONENT_ARCHIVE)
COMPONENT_BUGDB=	$(COMPONENT_FMRI)
COMPONENT_LICENSE=	Xiph.org BSD-style, binaries & media player plugins also use GPL v2, LGPL v2.1, documentation uses FDL v1.2
COMPONENT_LICENSE_FILE= $(COMPONENT_NAME).license
COMPONENT_SUMMARY=	An Open Source Lossless Audio Codec

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

CONFIGURE_OPTIONS  += --disable-static
CONFIGURE_OPTIONS  += --enable-shared
CONFIGURE_OPTIONS  += --disable-cpplibs
CONFIGURE_OPTIONS  += --disable-xmms-plugin
ifeq   ($(MACH), i386)
CONFIGURE_OPTIONS  += --enable-sse
ifeq   ($(BITS), 32)
CONFIGURE_OPTIONS  += --enable-asm-optimizations
else
CONFIGURE_OPTIONS  += --disable-asm-optimizations
endif
else
CONFIGURE_OPTIONS  += --disable-sse
CONFIGURE_OPTIONS  += --disable-asm-optimizations
endif
CONFIGURE_OPTIONS  += --disable-3dnow
CONFIGURE_OPTIONS  += --disable-altivec 

# common targets
build:		$(BUILD_32_and_64)

install:	$(INSTALL_32_and_64)

BUILD_PKG_DEPENDENCIES =	$(BUILD_TOOLS)

include $(WS_MAKE_RULES)/depend.mk
