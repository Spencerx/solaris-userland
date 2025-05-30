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
# Copyright (c) 2011, 2025, Oracle and/or its affiliates.
#
BUILD_BITS= 64
# GCC produces faster gzip on amd64 (not on SPARC).
ifeq ($(shell uname -p),i386)
COMPILER= gcc
endif
include ../../make-rules/shared-macros.mk

COMPONENT_NAME=		gzip
COMPONENT_VERSION=	1.14
COMPONENT_BAID=	326223
COMPONENT_ARCHIVE_HASH=	\
    sha256:613d6ea44f1248d7370c7ccdeee0dd0017a09e6c39de894b3c6f03f981191c6b
COMPONENT_ANITYA_ID=	1290

# Enable adiheap and adistack security extensions
ADIHEAP_MODE =	$(ADIHEAP_ENABLE)
ADISTACK_MODE =	$(ADISTACK_ENABLE)

SYSTEM_TEST_TARGET= configure $(SYSTEM_TEST_64)
include $(WS_MAKE_RULES)/gnu-component.mk

CONFIGURE_OPTIONS +=	--infodir=$(CONFIGURE_INFODIR)

# Fix references to Solaris renamed programs (z*->gz*) in man pages, info
# pages and in wrapper scripts.
COMPONENT_PRE_INSTALL_ACTION = \
	(cd $(COMPONENT_SRC) ; \
	 for file in `ls *.1 doc/*.info z*.in` ; do \
		mv $$file $$file.tmp ; \
		$(GSED) -f $(COMPONENT_DIR)/renaming.sed $$file.tmp > $$file ; \
		$(RM) $$file.tmp ; \
	 done)

# Rename installed programs and man pages in proto dir (z*->gz*).
COMPONENT_POST_INSTALL_ACTION = \
	(for dir in $(PROTOUSRBINDIR) $(PROTOUSRSHAREMAN1DIR) ; do \
		cd $$dir; \
	 	for zfile in `ls z*`; do \
			mv $$zfile g$$zfile ; \
		done ; \
	 done);

# Provide missing man pages.
COMPONENT_POST_INSTALL_ACTION += \
	(cd $(PROTOUSRSHAREMAN1DIR); \
	 for man in gzegrep.1 gzfgrep.1 ; do \
		$(RM) $$man; echo ".so man1/gzgrep.1" > $$man; \
	 done);

# Get the binaries to test from the component build area.
COMPONENT_TEST_ENV +=	PATH=$(BUILD_DIR_$(BITS)):/usr/xpg4/bin:$(USRBINDIR)

# Use the installed gzip binary from /usr/bin.
COMPONENT_SYSTEM_TEST_ENV +=	PATH=/usr/xpg4/bin:$(USRBINDIR)

COMPONENT_TEST_TRANSFORMS += \
	'-n ' \
	'-e "/PASS/p" ' \
	'-e "/FAIL/p" '

# We can't use auto hardlink processing because we don't ship 'uncompress'
# (we drop it in generate file), so it does not appear in the p5m and so it
# can't be detected.
PKG_HARDLINKS += usr/bin/gunzip

REQUIRED_PACKAGES += shell/bash
REQUIRED_PACKAGES += system/xopen/xcu4
