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
# Copyright (c) 2024, 2025, Oracle and/or its affiliates.
#

BUILD_BITS=		64

include ../../make-rules/shared-macros.mk

COMPONENT_NAME=		libpaper
COMPONENT_VERSION=	2.2.6
COMPONENT_ARCHIVE_HASH=	sha256:500d39dc58768ee09688738c8b5bfe07640ba2fd6c25a6dc78810eb69c719e93
COMPONENT_ARCHIVE_URL=	https://github.com/rrthomas/libpaper/releases/download/v$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL=	https://github.com/rrthomas/libpaper
COMPONENT_BUGDB=        library/libpaper
COMPONENT_ANITYA_ID=	15136
COMPONENT_BAID=		329220

include $(WS_MAKE_RULES)/common.mk

CONFIGURE_OPTIONS +=	--sysconfdir=$(ETCDIR)

# Settings needed to make tests passing
COMPONENT_PRE_CONFIGURE_ACTION  = ($(CLONEY) $(SOURCE_DIR) $(@D));
CONFIGURE_OPTIONS +=	--enable-relocatable
unexport SHELLOPTS
