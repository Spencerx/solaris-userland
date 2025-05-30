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
# Copyright (c) 2016, 2024, Oracle and/or its affiliates.
#
BUILD_BITS= 64
COMPILER= gcc
include ../../make-rules/shared-macros.mk

COMPONENT_NAME=		augeas
COMPONENT_VERSION=	1.13.0
COMPONENT_PROJECT_URL=	https://www.augeas.net/
COMPONENT_ARCHIVE_HASH=	\
	sha256:5002f33f42365ab78be974609a0f3b76a4c277fc404ec79f516305cab5ce5de1
COMPONENT_ARCHIVE_URL=	https://github.com/hercules-team/augeas/releases/download/release-$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)
COMPONENT_ANITYA_ID=	7017

COMPONENT_BAID=	129171

include $(WS_MAKE_RULES)/common.mk

# GNU Build System files have to be regenerated for automake 1.16.
# It can be removed when the upstream starts to use a newer automake version.
COMPONENT_PREP_ACTION = (cd $(@D) ; autoreconf -fiv)

# Regenerate our patched configure.ac
COMPONENT_PRE_CONFIGURE_ACTION = (cd $(SOURCE_DIR); autoconf)
COMPONENT_PRE_CONFIGURE_ACTION +=  ;($(CLONEY) $(SOURCE_DIR) $(@D))

CONFIGURE_OPTIONS  +=	--infodir=$(CONFIGURE_INFODIR)
CONFIGURE_OPTIONS  +=	--disable-dependency-tracking

# GNU binaries like gnu grep needs to be used for some tests to pass
COMPONENT_TEST_ENV +=	PATH="$(GNUBIN):$(PATH)"
COMPONENT_TEST_ARGS = -k
COMPONENT_TEST_TRANSFORMS += \
        '-n ' \
        '-e "/passed/p" ' \
        '-e "/failed/p" ' \
        '-e "/Checks:/p" ' \
        '-e "/Total:/p" ' \
        '-e "/Passed/p" ' \
        '-e "/Failed/p" ' \
        '-e "/Failure expected/p" ' \
        '-e "/SKIP/p" ' \
        '-e "/PASS/p" ' \
        '-e "/FAIL/p" '

# XXX why does this coredump without the workaround?
# Fixes coredump in gnulib-test/test-localename test
CONFIGURE_OPTIONS  +=           ac_cv_func_newlocale=no

REQUIRED_PACKAGES += library/libxml2
REQUIRED_PACKAGES += library/ncurses
REQUIRED_PACKAGES += library/readline
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/gcc/gcc-c-runtime
