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
# Copyright (c) 2019, 2025, Oracle and/or its affiliates.
#
BUILD_BITS=		64_and_32
COMPILER=		gcc
include ../../make-rules/shared-macros.mk

COMPONENT_NAME=		lasso
COMPONENT_VERSION=	2.8.2
BASEURL=		https://dev.entrouvert.org
COMPONENT_PROJECT_URL=	$(BASEURL)/projects/lasso
COMPONENT_ARCHIVE_HASH= \
    sha256:6a1831bfdbf8f424c7508aba47b045d51341ec0fde9122f38b0b86b096ef533e
COMPONENT_ARCHIVE_URL=	\
	$(BASEURL)/releases/$(COMPONENT_NAME)/$(COMPONENT_ARCHIVE)
COMPONENT_BUGDB=	library/lasso
COMPONENT_ANITYA_ID=	96894

COMPONENT_BAID=		146907

TEST_TARGET= $(NO_TESTS)
include $(WS_MAKE_RULES)/common.mk

CONFIGURE_OPTIONS+=	--disable-php7
CONFIGURE_OPTIONS+=	--disable-perl
CONFIGURE_OPTIONS+=	--disable-java
CONFIGURE_OPTIONS+=	--disable-python
CONFIGURE_OPTIONS+=	PATH="$(GNUBIN):$$PATH"
CONFIGURE_OPTIONS.64+=	--with-pkg-config=$(PKG_CONFIG_PATH.64)

CONFIGURE_OPTIONS.32+=	--with-pkg-config=$(PKG_CONFIG_PATH.32)

COMPONENT_POST_CONFIGURE_ACTION.32 += ( \
	$(FIND) $(@D) -name Makefile | while read f; do $(GSED) -i '/^LASSO_LIBS/s;-L/usr/lib;;g' $$f; done ) ;
COMPONENT_POST_CONFIGURE_ACTION.64 += ( \
	$(FIND) $(@D) -name Makefile | while read f; do $(GSED) -i '/^LASSO_LIBS/s;-L/usr/lib/$(MACH64);;g' $$f; done ) ;

REQUIRED_PACKAGES+=	system/library
REQUIRED_PACKAGES+=	library/security/openssl-3
REQUIRED_PACKAGES+=	library/glib2
REQUIRED_PACKAGES+=	system/library/math
REQUIRED_PACKAGES+=	library/libxml2
REQUIRED_PACKAGES+=	library/xmlsec
REQUIRED_PACKAGES+=	library/libxslt
REQUIRED_PACKAGES+=	library/zlib
