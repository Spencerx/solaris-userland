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
# Copyright (c) 2011, 2024, Oracle and/or its affiliates.
#
BUILD_BITS= 64
include ../../make-rules/shared-macros.mk

PATH = $(GNUBIN):$(USRBINDIR)

COMPONENT_NAME=		quilt
COMPONENT_VERSION=	0.68
COMPONENT_PROJECT_URL=	https://savannah.nongnu.org/projects/quilt/
COMPONENT_ARCHIVE_HASH=	\
    sha256:fe8c09de03c106e85b3737c8f03ade147c956b79ed7af485a1c8a3858db38426
COMPONENT_ARCHIVE_URL=	https://download.savannah.gnu.org/releases/quilt/$(COMPONENT_ARCHIVE)
COMPONENT_SIG_URL=	$(COMPONENT_ARCHIVE_URL).sig
COMPONENT_ANITYA_ID=	4143
COMPONENT_BAID=		166004

SYSTEM_TEST_TARGET= configure $(SYSTEM_TEST_64)

include $(WS_MAKE_RULES)/common.mk

COMPONENT_PRE_CONFIGURE_ACTION = \
    ($(CLONEY) $(SOURCE_DIR) $(@D))

COMPONENT_PREP_ACTION = \
    (cd $(@D) ; autoconf )

PATCH_LEVEL=	0

# without this, some make messages end up in the
# generated README and man pages.
COMPONENT_BUILD_ARGS+=	--no-print-directory

PERLBINDIR= $(USRDIR)/perl5/$(PERL_VERSION)/bin

CONFIGURE_OPTIONS += --sysconfdir=$(ETCDIR)
CONFIGURE_OPTIONS += --with-column=$(USRBINDIR)/column
CONFIGURE_OPTIONS += --with-cp=$(GNUBIN)/cp
CONFIGURE_OPTIONS += --with-date=$(GNUBIN)/date
CONFIGURE_OPTIONS += --with-getopt=$(GNUBIN)/getopt
CONFIGURE_OPTIONS += --with-grep=$(GNUBIN)/grep
CONFIGURE_OPTIONS += --with-tail=$(GNUBIN)/tail
CONFIGURE_OPTIONS += --with-tr=$(GNUBIN)/tr
CONFIGURE_OPTIONS += --with-sed=$(GNUBIN)/sed
CONFIGURE_OPTIONS += --with-diff=$(GNUBIN)/diff
CONFIGURE_OPTIONS += --with-find=$(GNUBIN)/find
CONFIGURE_OPTIONS += --with-patch=$(GNUBIN)/patch
CONFIGURE_OPTIONS += --with-perl=$(PERLBINDIR)/perl
CONFIGURE_OPTIONS += --with-pod2man=$(PERLBINDIR)/pod2man
CONFIGURE_OPTIONS += --with-xgettext=$(USRBINDIR)/gxgettext
CONFIGURE_OPTIONS += --with-msgfmt=$(USRBINDIR)/gmsgfmt

COMPONENT_INSTALL_ARGS +=	BUILD_ROOT=$(PROTO_DIR)

COMPONENT_TEST_TRANSFORMS += \
	'-e "s|^.* -> .*$$|XXX_REMOVE_XXX|g" ' \
	'-e "s|^Unescaped left brace.*$$|XXX_REMOVE_XXX|g" ' \
	'-e "s|^Generating.*$$|XXX_REMOVE_XXX|g" ' \
	'-e "s|^make.*: Leaving directory.*$$|XXX_REMOVE_XXX|g" ' \
	'-e "s|^make.*: Entering directory.*$$|XXX_REMOVE_XXX|g" ' \
	'-e "/^XXX_REMOVE_XXX$$/d" '

ASLR_MODE = $(ASLR_NOT_APPLICABLE)

REQUIRED_PACKAGES += archiver/gnu-tar
REQUIRED_PACKAGES += file/gnu-coreutils
REQUIRED_PACKAGES += file/gnu-findutils
REQUIRED_PACKAGES += $(PERL_PKG)
REQUIRED_PACKAGES += service/network/smtp/sendmail
REQUIRED_PACKAGES += shell/bash
REQUIRED_PACKAGES += shell/gnu-getopt
REQUIRED_PACKAGES += text/gawk
REQUIRED_PACKAGES += text/gnu-diffutils
REQUIRED_PACKAGES += text/gnu-grep
REQUIRED_PACKAGES += text/gnu-patch
REQUIRED_PACKAGES += text/gnu-sed
REQUIRED_PACKAGES += text/text-utilities
