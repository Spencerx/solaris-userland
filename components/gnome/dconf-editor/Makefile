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
# Copyright (c) 2015, 2024, Oracle and/or its affiliates.
#

BUILD_BITS =            64
# All components using gobject-introspection must be built with gcc as
# gobject-introspection does not produce correct results when using Studio.
COMPILER =              gcc
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		dconf-editor
COMPONENT_VERSION=	45.0.1
COMPONENT_PROJECT_URL=	http://wiki.gnome.org/dconf
COMPONENT_ARCHIVE_HASH= \
	sha256:1180297678eedae6217cc514a2638c187d2f1d1ef2720cb9079b740c429941dd
COMPONENT_ARCHIVE_URL= \
	https://download.gnome.org/sources/$(COMPONENT_NAME)/$(basename $(COMPONENT_MAJOR_MINOR))/$(COMPONENT_ARCHIVE)
COMPONENT_BUGDB=        gnome/gconf
COMPONENT_ANITYA_ID=	100776

COMPONENT_BAID=		153196
BUILD_STYLE=            meson

TEST_TARGET= $(NO_TESTS)

include $(WS_MAKE_RULES)/gnome-component.mk

# Required by GCC 14 - needs to be evaluated and properly fixed.
CFLAGS += -Wno-incompatible-pointer-types

# Assumes GNU xgettext in PATH
CONFIGURE_ENV += PATH=$(GNUBIN):$(PATH)
COMPONENT_BUILD_ENV += PATH="$(GNUBIN):$(PATH)"
COMPONENT_INSTALL_ENV += PATH="$(GNUBIN):$(PATH)"

REQUIRED_PACKAGES += developer/vala
REQUIRED_PACKAGES += library/desktop/pango
REQUIRED_PACKAGES += library/desktop/gtk3
REQUIRED_PACKAGES += library/desktop/libhandy
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/gnome/dconf
REQUIRED_PACKAGES += library/libxml2
