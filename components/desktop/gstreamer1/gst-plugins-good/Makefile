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

BUILD_BITS =            32_and_64
# All components using gobject-introspection must be built with gcc as
# gobject-introspection does not produce correct results when using Studio.
COMPILER =              gcc
include ../../../../make-rules/shared-macros.mk

COMPONENT_NAME=		gst-plugins-good
COMPONENT_VERSION=	1.24.12
COMPONENT_PROJECT_URL=	https://gstreamer.freedesktop.org/
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_HASH= \
	sha256:d0e66e2f935d1575f6adbef7d0a2b3faba7360344383c51bf0233b39e0489a64
COMPONENT_ARCHIVE_URL=	https://gstreamer.freedesktop.org/src/$(COMPONENT_NAME)/$(COMPONENT_ARCHIVE)
COMPONENT_SIG_URL=	$(COMPONENT_ARCHIVE_URL).asc
COMPONENT_BUGDB=	gnome/multimedia
COMPONENT_ANITYA_ID=	1263

COMPONENT_BAID=		324179

BUILD_STYLE=		meson
PYTHON_VERSION = 3.11

include $(WS_MAKE_RULES)/common.mk

CXXFLAGS += -std=c++14

# We EOF'ed aalib - no need for ascii-art terminal output
CONFIGURE_OPTIONS += -Daalib=disabled
# No need for firewire support.
CONFIGURE_OPTIONS += -Ddv1394=disabled
# Linux only; requires ALSA.
CONFIGURE_OPTIONS += -Dmonoscope=disabled

CONFIGURE_OPTIONS += -Dbz2=enabled
CONFIGURE_OPTIONS += -Dcairo=enabled
CONFIGURE_OPTIONS += -Djpeg=enabled
CONFIGURE_OPTIONS += -Doss=enabled
CONFIGURE_OPTIONS += -Doss4=enabled
CONFIGURE_OPTIONS += -Dpng=enabled
CONFIGURE_OPTIONS += -Dpulse=enabled
CONFIGURE_OPTIONS += -Dsoup=enabled
CONFIGURE_OPTIONS += -Dspeex=enabled
CONFIGURE_OPTIONS += -Dtaglib=enabled
CONFIGURE_OPTIONS += -Dvpx=enabled

# Missing header to build it...
CONFIGURE_OPTIONS += -Dv4l2=disabled

# Requires GNU version of msgfmt...
COMPONENT_INSTALL_ENV += PATH="$(GNUBIN):$(PATH)"

COMPONENT_TEST_MASTER = $(COMPONENT_TEST_RESULTS_DIR)/results-$(BITS)-$(MACH).master
COMPONENT_TEST_ENV += -i
COMPONENT_TEST_ARGS =   -k 0

REQUIRED_PACKAGES += codec/flac
REQUIRED_PACKAGES += codec/libogg
REQUIRED_PACKAGES += codec/libtheora
REQUIRED_PACKAGES += codec/libvorbis
REQUIRED_PACKAGES += codec/libvpx
REQUIRED_PACKAGES += codec/speex
REQUIRED_PACKAGES += image/library/libjpeg
REQUIRED_PACKAGES += image/library/libpng16
REQUIRED_PACKAGES += library/audio/pulseaudio
REQUIRED_PACKAGES += library/audio/taglib
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += library/desktop/gdk-pixbuf
REQUIRED_PACKAGES += library/desktop/gobject/gobject-introspection
REQUIRED_PACKAGES += library/desktop/gstreamer-1
REQUIRED_PACKAGES += library/desktop/gstreamer-1/gst-plugins-base
REQUIRED_PACKAGES += library/desktop/gtk3
REQUIRED_PACKAGES += library/desktop/orc
REQUIRED_PACKAGES += library/desktop/pango
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/libsoup-3
REQUIRED_PACKAGES += library/libxml2
REQUIRED_PACKAGES += library/ncurses
REQUIRED_PACKAGES += library/security/nettle
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += runtime/python-311
REQUIRED_PACKAGES += system/library/gcc/gcc-c++-runtime
REQUIRED_PACKAGES += system/library/gcc/gcc-c-runtime
REQUIRED_PACKAGES += system/library/math
REQUIRED_PACKAGES += x11/library/libx11
REQUIRED_PACKAGES += x11/library/libxdamage
REQUIRED_PACKAGES += x11/library/libxext
REQUIRED_PACKAGES += x11/library/libxfixes
REQUIRED_PACKAGES += x11/library/libxtst
REQUIRED_PACKAGES += x11/library/libxv
