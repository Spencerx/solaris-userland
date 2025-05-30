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
# Copyright (c) 2016, 2025, Oracle and/or its affiliates.
#

BUILD_BITS= 64
# Uses gcc-specific options (e.g. -Wall) which cause Studio build failures.
COMPILER= gcc
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		gnome-initial-setup
COMPONENT_VERSION=	41.4
COMPONENT_ARCHIVE_HASH= \
	sha256:96ecd2db6e76c513b18c606dc262bb523228c4aaedbed6a07811e568fd5db642
COMPONENT_BUGDB=	gnome/session
COMPONENT_ANITYA_ID=	13132

COMPONENT_BAID=		119381
BUILD_STYLE=		meson

TEST_TARGET= $(NO_TESTS)

include $(WS_MAKE_RULES)/gnome-component.mk

# Assumes GNU msgfmt in PATH.
CONFIGURE_ENV += PATH="$(GNUBIN):$(PATH)"
COMPONENT_BUILD_ENV += PATH="$(GNUBIN):$(PATH)"
COMPONENT_INSTALL_ENV += PATH="$(GNUBIN):$(PATH)"

CONFIGURE_OPTIONS += -Dsystemd=false
CONFIGURE_OPTIONS += -Dcheese=disabled

# gnome-initial-setup/pages/account/um-utils.c uses UT_NAMESIZE from the Linux
# <utmp.h> - map it to the equivalent value in the Solaris <utmp.h>
CPPFLAGS += -DUT_NAMESIZE=_UTMP_USER_LEN

REQUIRED_PACKAGES += gnome/gsettings-desktop-schemas
REQUIRED_PACKAGES += library/desktop/gdk-pixbuf
REQUIRED_PACKAGES += library/desktop/gtk3
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/gnome/gnome-desktop
REQUIRED_PACKAGES += library/gnome/libsecret
REQUIRED_PACKAGES += system/display-manager/gdm
REQUIRED_PACKAGES += system/input-method/ibus
REQUIRED_PACKAGES += system/library/accountsservice
REQUIRED_PACKAGES += system/library/fontconfig
REQUIRED_PACKAGES += system/library/math
REQUIRED_PACKAGES += system/library/polkit
