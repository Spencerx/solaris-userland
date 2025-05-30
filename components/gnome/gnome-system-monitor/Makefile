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

BUILD_BITS =            64
# All components using gobject-introspection must be built with gcc as
# gobject-introspection does not produce correct results when using Studio.
COMPILER =              gcc
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		gnome-system-monitor
COMPONENT_VERSION=	45.0.2
COMPONENT_PROJECT_URL=  https://help.gnome.org/users/gnome-system-monitor/
COMPONENT_ARCHIVE_HASH= \
	sha256:c5e272d90bf9986a3f8613d76e0d27fa42dfacee5c0192e73921bb94b1868a2e
COMPONENT_ARCHIVE_URL= \
        https://download.gnome.org/sources/$(COMPONENT_NAME)/$(basename $(COMPONENT_MAJOR_MINOR))/$(COMPONENT_ARCHIVE)
COMPONENT_BUGDB=        gnome/applications
COMPONENT_ANITYA_ID=	13137

COMPONENT_BAID=		156901
BUILD_STYLE=            meson

include $(WS_MAKE_RULES)/gnome-component.mk

CFLAGS += -std=c11
CXXFLAGS += -std=c++11
# Uses gcc-specific language extensions.
CXXFLAGS.studio += -features=extensions

# To get localtime_r.
CPPFLAGS += -D__EXTENSIONS__

CONFIGURE_OPTIONS += --libexecdir="$(USRLIBDIR)"
CONFIGURE_OPTIONS += -Dsystemd=false
CONFIGURE_OPTIONS += -Dwnck=true

# Assumes GNU msgfmt is in PATH.
CONFIGURE_ENV += PATH="$(GNUBIN):$(PATH)"
COMPONENT_BUILD_ENV += PATH="$(GNUBIN):$(PATH)"
COMPONENT_INSTALL_ENV += PATH="$(GNUBIN):$(PATH)"

REQUIRED_PACKAGES += gnome/gsettings-desktop-schemas
REQUIRED_PACKAGES += image/library/librsvg
REQUIRED_PACKAGES += library/c++/glibmm
REQUIRED_PACKAGES += library/c++/sigcpp
# atkmm dependency can be removed when upgrading to 46.0 or later
REQUIRED_PACKAGES += library/desktop/c++/atkmm
REQUIRED_PACKAGES += library/desktop/c++/gtkmm3
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += library/desktop/gdk-pixbuf
REQUIRED_PACKAGES += library/desktop/gtk3
REQUIRED_PACKAGES += library/desktop/libhandy
REQUIRED_PACKAGES += library/desktop/libwnck3
REQUIRED_PACKAGES += library/desktop/pango
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/libgtop
REQUIRED_PACKAGES += system/library/gcc/gcc-c++-runtime
REQUIRED_PACKAGES += system/library/gcc/gcc-c-runtime
REQUIRED_PACKAGES += system/library/math
