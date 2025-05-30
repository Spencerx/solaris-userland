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
include ../ofed-component-macros.mk

COMPONENT_NAME=		libibumad
COMPONENT_VERSION=	1.3.10.2
COMPONENT_ARCHIVE_HASH=	\
	sha256:500f74e31bd9f3d6c32dea912de3a2d1b299f3f23d7abd893652dd45c77a7e2e
COMPONENT_ARCHIVE_URL=	https://www.openfabrics.org/downloads/management/$(COMPONENT_ARCHIVE)
COMPONENT_BUGDB=	library/ofuv_lib
COMPONENT_ANITYA_ID=	1636

include ../ofed-component.mk

# Required by GCC 14 - needs to be evaluated and properly fixed.
CFLAGS += -Wno-implicit-function-declaration

LIBS +=	-libverbs

CLEANUP_FILES = $(PROTOUSRSHAREMAN3DIR)/umad_free.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_done.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_send.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_recv.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_init.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_dump.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_poll.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_size.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_debug.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_alloc.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_get_ca.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_get_fd.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_status.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_get_mad.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_set_grh.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_set_addr.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_get_pkey.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_get_port.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_set_pkey.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_register.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_addr_dump.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_open_port.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_release_ca.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_close_port.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_unregister.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_set_grh_net.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_get_mad_addr.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_set_addr_net.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_release_port.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_register_oui.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_get_cas_names.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_get_issm_path.3 \
	$(PROTOUSRSHAREMAN3DIR)/umad_get_ca_portguids.3

COMPONENT_POST_INSTALL_ACTION = \
	$(RM) $(PROTO_DIR)/$(CONFIGURE_LIBDIR.32)/$(COMPONENT_NAME).la;\
	$(RM) $(PROTO_DIR)/$(CONFIGURE_LIBDIR.64)/$(COMPONENT_NAME).la;\
	$(RM) $(CLEANUP_FILES)

