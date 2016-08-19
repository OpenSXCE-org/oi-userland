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
# Copyright 2016 Alexander Pyhalov
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		drm
COMPONENT_VERSION=	0.5.11
COMPONENT_PROJECT_URL=	http://openindiana.org
COMPONENT_SUMMARY=	DRM Kernel Drivers
COMPONENT_SRC=		$(COMPONENT_NAME)
COMPONENT_ARCHIVE_HASH=	\
    sha256:3435a7a2ab1506629b2b9ee65232f66ea9b03d355006773b9abb65a316811a97
COMPONENT_FMRI=		driver/graphics/drm
COMPONENT_CLASSIFICATION=	Drivers/Display
COMPONENT_LICENSE=	CDDL
COMPONENT_LICENSE_FILE=	COPYING

include $(WS_TOP)/make-rules/justmake.mk
include $(WS_TOP)/make-rules/ips.mk

PATH=/usr/gnu/bin:/usr/bin

CC=/opt/gcc/4.4.4/bin/gcc

COMPONENT_BUILD_ENV += CC="$(CC)"
COMPONENT_BUILD_ENV += CFLAGS="$(CFLAGS)"

# common targets
download::

clobber: clean

$(SOURCE_DIR)/.prep:
	$(TOUCH) $@

build: $(BUILD_32_and_64)

install: $(INSTALL_32_and_64)

clean::
	$(MAKE) -C $(SOURCE_DIR) clean
	$(RM) $(SOURCE_DIR)/.prep

