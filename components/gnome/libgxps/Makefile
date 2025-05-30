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
# Copyright (c) 2015, 2025, Oracle and/or its affiliates.
#

BUILD_BITS= 64_and_32
# All components using gobject-introspection must be built with gcc as
# gobject-introspection does not produce correct results when using Studio.
COMPILER= gcc
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		libgxps
COMPONENT_VERSION=	0.3.2
COMPONENT_PROJECT_URL=	https://wiki.gnome.org/Projects/libgxps
COMPONENT_ARCHIVE_HASH=	\
    sha256:6d27867256a35ccf9b69253eb2a88a32baca3b97d5f4ef7f82e3667fa435251c
COMPONENT_BUGDB=	gnome/libraries
COMPONENT_ANITYA_ID=	1629

COMPONENT_BAID=		107064
BUILD_STYLE=		meson

TEST_TARGET= $(SKIP_TEST)

include $(WS_MAKE_RULES)/gnome-component.mk

CONFIGURE_OPTIONS += -Denable-gtk-doc=true
CONFIGURE_OPTIONS += -Denable-man=true
CONFIGURE_OPTIONS += -Ddisable-introspection=true

REQUIRED_PACKAGES += developer/documentation-tool/gtk-doc
REQUIRED_PACKAGES += image/library/libjpeg
REQUIRED_PACKAGES += image/library/libpng16
REQUIRED_PACKAGES += image/library/libtiff
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/lcms2
REQUIRED_PACKAGES += library/libarchive
REQUIRED_PACKAGES += system/library/freetype-2
REQUIRED_PACKAGES += system/library/math
