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
BUILD_BITS=	64
COMPILER=	gcc
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		foomatic-db-engine
# version (4.0) is relative to foomatic-db-engine
#  ...do not combine foomatic-db with foomatic-db-engine of the different versions
FOO_VERSION=		4.0
# Latest foomatic-db-engine patchlevel where the snapshot is derived from.
# Makes the IPS versioning monotonously growing.
FOO_PATCHLEVEL=		14
DAILY_VERSION=		20250519
COMPONENT_VERSION=	$(FOO_VERSION)-$(DAILY_VERSION)
IPS_COMPONENT_VERSION=	$(FOO_VERSION).$(FOO_PATCHLEVEL).$(DAILY_VERSION)
COMPONENT_BAID=		329526
COMPONENT_ARCHIVE=	$(COMPONENT_NAME)-$(COMPONENT_VERSION).tar.gz
COMPONENT_ARCHIVE_HASH=	sha256:d5d9fce2a597cabef2f282c2482a1ec34c2061b118abc7a7c782efef529a4b8f
COMPONENT_ARCHIVE_URL=	http://www.openprinting.org/download/foomatic/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL=	https://wiki.linuxfoundation.org/openprinting/database/foomatic
COMPONENT_BUGDB=	utility/foomatic
COMPONENT_ANITYA_ID=	828

TEST_TARGET= $(NO_TESTS)
include $(WS_MAKE_RULES)/common.mk

CONFIGURE_OPTIONS +=	PERL=$(PERL)
CONFIGURE_OPTIONS +=	TAR=/usr/gnu/bin/tar
# foomatic-filters (pkg:/.../foomatic-rip) keeps "filter.conf" here:
CONFIGURE_OPTIONS +=	--sysconfdir=$(ETCDIR)/gnu

COMPONENT_PREP_ACTION += (cd $(@D); autoreconf -fiv);

# the build system does not support building outside of the source tree
COMPONENT_PRE_CONFIGURE_ACTION = $(CLONEY) $(SOURCE_DIR) $(@D) ;

# setup perl build
COMPONENT_PRE_CONFIGURE_ACTION += cd $(@D)/lib ; $(PERL) Makefile.PL

# publish for only one version of perl
PERL_VERSIONS = $(PERL_VERSION)

# install perl modules including Foomatic::Defaults
# the perl .packlist contains the path to the file as built rather than
# as installed. Fix to be installed path, ie remove PROTO_DIR.
VENDORARCH= $(shell $(PERL) -e 'use Config; print $$Config{vendorarch}')
PACKLIST=   $(VENDORARCH)/auto/Foomatic/.packlist
COMPONENT_POST_INSTALL_ACTION = \
 ( cd $(@D)/lib ; $(GMAKE) install_vendor DESTDIR=$(PROTO_DIR) ) ; \
 $(INSTALL) -m 0644 -t $(PROTO_DIR)/usr/perl5/vendor_perl/$(PERL_VERSION)/Foomatic/ $(@D)/lib/Foomatic/Defaults.pm ; \
 sed -e "s/$(subst /,\\/,$(PROTO_DIR))//g" $(PROTO_DIR)/$(PACKLIST) \
     >> $(PROTO_DIR)/$(PACKLIST).fixed ; \
 $(MV) $(PROTO_DIR)/$(PACKLIST).fixed $(PROTO_DIR)/$(PACKLIST)

foomatic-db-engine.license:
	cat $(SOURCE_DIR)/COPYING foomatic-db-engine.copyright > $@

REQUIRED_PACKAGES += library/libxml2
REQUIRED_PACKAGES += $(PERL_PKG)
REQUIRED_PACKAGES += shell/bash
