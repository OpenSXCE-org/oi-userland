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

COMPONENT_NAME= 	ipython_genutils
COMPONENT_VERSION= 	0.1.0
COMPONENT_FMRI= 	library/python/ipython_genutils
COMPONENT_SUMMARY= 	Vestigial utilities from IPython
COMPONENT_CLASSIFICATION=	Development/Python
COMPONENT_SRC= 		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE= 	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH= \
  sha256:3a0624a251a26463c9dfa0ffa635ec51c4265380980d9a50d65611c3c2bd82a6
COMPONENT_ARCHIVE_URL= \
  $(call pypi_url)
COMPONENT_PROJECT_URL=	https://pypi.python.org/pypi/ipython_genutils
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
