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
BUILD_BITS= 64_and_32
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		expect
COMPONENT_VERSION=	5.45.4
COMPONENT_BAID=		136345
COMPONENT_PROJECT_URL=	https://core.tcl.tk/expect/
COMPONENT_SRC=		$(COMPONENT_NAME)$(COMPONENT_VERSION)
COMPONENT_ARCHIVE_HASH=	\
    sha256:49a7da83b0bdd9f46d04a04deec19c7767bb9a323e40c4781f89caf760b92c34
COMPONENT_ARCHIVE_URL=	https://sourceforge.net/projects/expect/files/Expect/$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)/download
COMPONENT_ANITYA_ID=	771

include $(WS_MAKE_RULES)/common.mk

SCRIPTS = timed-run timed-read ftp-rfc autopasswd lpunlock weather \
          passmass rftp kibitz rlogin-cwd xpstat tkpasswd dislocate xkibitz \
          tknewsbiff unbuffer mkpasswd cryptdir decryptdir autoexpect multixterm
COMPONENT_PREP_ACTION += (cd $(@D); autoreconf -fiv); 

COMPONENT_PRE_CONFIGURE_ACTION = \
	($(CLONEY) $(SOURCE_DIR) $(@D))

COMPONENT_BUILD_TARGETS = all ${SCRIPTS}

# 64-bit executables should also be delivered to relevant MACH subdirectory.
CONFIGURE_BINDIR.64= $(USRBINDIR64)
CONFIGURE_OPTIONS +=		--enable-shared
CONFIGURE_OPTIONS +=		--with-tcl="$(COMPONENT_DIR)/../tcl/build/$(MACH$(BITS))"
CONFIGURE_OPTIONS +=		--with-tclinclude="$(COMPONENT_DIR)/../tcl/build/$(MACH$(BITS))/generic"
CONFIGURE_OPTIONS.64 += 	-enable-64bit
CONFIGURE_OPTIONS.sparc.64 +=	--enable-64bit-vis

CC += $(CC_BITS)

COMPONENT_TEST_MASTER = $(COMPONENT_TEST_RESULTS_DIR)/results-all.master
COMPONENT_TEST_TARGETS = test
COMPONENT_TEST_TRANSFORMS += \
	'-e "s|$(WS_TOP)|\\$$(WS_TOP)|g"' \
	'-e "/Nothing to be done/d"' \
	'-e "/Leaving directory/d"' \
	'-e "/Entering directory/d"' \
	'-e "/TCL_LIBRARY=/d"' \
	'-e "s|tcl/build/$(MACH$(BITS))|\\$$(TCLBUILD)|g"'

# special targets due to tcl internals dependencies
../tcl/build/%/.built:
	(cd ../tcl ; $(GMAKE) build)

$(CONFIGURE_32):	../tcl/build/$(MACH32)/.built
$(CONFIGURE_64):	../tcl/build/$(MACH64)/.built

REQUIRED_PACKAGES += runtime/tcl-8
REQUIRED_PACKAGES += shell/ksh93
REQUIRED_PACKAGES += system/library/math
