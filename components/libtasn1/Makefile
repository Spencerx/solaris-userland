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
# Copyright (c) 2010, 2025, Oracle and/or its affiliates.
#
BUILD_BITS= 64_and_32
include ../../make-rules/shared-macros.mk

COMPONENT_NAME=		libtasn1
COMPONENT_VERSION=	4.20.0
COMPONENT_ARCHIVE_HASH= \
    sha256:92e0e3bd4c02d4aeee76036b2ddd83f0c732ba4cda5cb71d583272b23587a76c
COMPONENT_BUGDB=	library/libtasn1
COMPONENT_ANITYA_ID=	1734

COMPONENT_BAID=		195971

COMPONENT_BUILD_TARGETS = all info

include $(WS_MAKE_RULES)/gnu-component.mk

CONFIGURE_OPTIONS += --sysconfdir=/etc
CONFIGURE_OPTIONS += --includedir=$(CONFIGURE_INCLUDEDIR)
CONFIGURE_OPTIONS += --infodir=$(CONFIGURE_INFODIR)
CONFIGURE_OPTIONS += --disable-static
CONFIGURE_OPTIONS += --enable-shared

include ../../make-rules/shared-targets.mk

TEST_TARGET:	install

COMPONENT_TEST_MASTER = $(COMPONENT_TEST_RESULTS_DIR)/results-all.master

COMPONENT_TEST_TRANSFORMS += \
        '-n -e "/PASS/p" ' \
        '-e "/FAIL/p" ' \
        '-e "/All/p" '

