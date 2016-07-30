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

COMPONENT_NAME= 	traitlets
COMPONENT_VERSION= 	4.2.2
COMPONENT_FMRI= 	library/python/traitlets
COMPONENT_SUMMARY= 	Traitlets Python config system
COMPONENT_CLASSIFICATION=	Development/Python
COMPONENT_SRC= 		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE= 	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH= \
  sha256:7d7e3070484b2fe490fa55e0acf7023afc5ed9ddabec57405f25c355158e152a
COMPONENT_ARCHIVE_URL= \
  https://pypi.python.org/packages/a4/07/9b7636322c152ab1dacae9d38131067523d6ce5ca926a656586f6f947e77/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL=	https://pypi.python.org/pypi/traitlets
COMPONENT_LICENSE_FILE=	COPYING.md
COMPONENT_LICENSE=	BSD

PYTHON_VERSIONS=2.7 3.4

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/setup.py.mk
include $(WS_MAKE_RULES)/ips.mk

build:		$(BUILD_32)

install:	$(INSTALL_32)

test:           $(NO_TESTS)

REQUIRED_PACKAGES += runtime/python-27
REQUIRED_PACKAGES += runtime/python-34
