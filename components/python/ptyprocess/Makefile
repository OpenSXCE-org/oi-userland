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
# Copyright 2016 Alexander Pyhalov
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME= 	ptyprocess
COMPONENT_VERSION= 	0.5.1
COMPONENT_FMRI= 	library/python/ptyprocess
COMPONENT_SUMMARY= 	Run a subprocess in a pseudo terminal
COMPONENT_CLASSIFICATION=	Development/Python
COMPONENT_SRC= 		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE= 	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH= \
  sha256:0530ce63a9295bfae7bd06edc02b6aa935619f486f0f1dc0972f516265ee81a6
COMPONENT_ARCHIVE_URL= \
  https://pypi.python.org/packages/db/d7/b465161910f3d1cef593c5e002bff67e0384898f597f1a7fdc8db4c02bf6/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL=	https://pypi.python.org/pypi/ptyprocess
COMPONENT_LICENSE_FILE=	LICENSE
COMPONENT_LICENSE=	ISC

PYTHON_VERSIONS=2.7 3.4

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/setup.py.mk
include $(WS_MAKE_RULES)/ips.mk

build:		$(BUILD_32)

install:	$(INSTALL_32)

test:           $(NO_TESTS)

REQUIRED_PACKAGES += runtime/python-27
REQUIRED_PACKAGES += runtime/python-34
