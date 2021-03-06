#
#  Copyright (c) 2016, The OpenThread Authors.
#  All rights reserved.
#
#  Redistribution and use in source and binary forms, with or without
#  modification, are permitted provided that the following conditions are met:
#  1. Redistributions of source code must retain the above copyright
#     notice, this list of conditions and the following disclaimer.
#  2. Redistributions in binary form must reproduce the above copyright
#     notice, this list of conditions and the following disclaimer in the
#     documentation and/or other materials provided with the distribution.
#  3. Neither the name of the copyright holder nor the
#     names of its contributors may be used to endorse or promote products
#     derived from this software without specific prior written permission.
#
#  THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
#  AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
#  IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
#  ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE
#  LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
#  CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
#  SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
#  INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
#  CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
#  ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
#  POSSIBILITY OF SUCH DAMAGE.
#

include $(abs_top_nlbuild_autotools_dir)/automake/pre.am

#
# Local headers to build against and distribute but not to install
# since they are not part of the package.
#
noinst_HEADERS                                                      = \
    test_lowpan.hpp                                                   \
    test_platform.h                                                   \
    test_util.h                                                       \
    test_util.hpp                                                     \
    $(NULL)

#
# Other files we do want to distribute with the package.
#
EXTRA_DIST                                                          = \
    $(NULL)

if OPENTHREAD_BUILD_TESTS
# C preprocessor option flags that will apply to all compiled objects in this
# makefile.

AM_CPPFLAGS                                                         = \
    -DOPENTHREAD_FTD=1                                                \
    -DOPENTHREAD_MTD=0                                                \
    -DOPENTHREAD_RADIO=0                                              \
    -I$(top_srcdir)/include                                           \
    -I$(top_srcdir)/src                                               \
    -I$(top_srcdir)/src/core                                          \
    $(NULL)

if OPENTHREAD_EXAMPLES_POSIX
AM_CPPFLAGS                                                        += \
    -I$(top_srcdir)/examples/platforms                                \
    $(NULL)
endif

if OPENTHREAD_PLATFORM_POSIX_APP
AM_CPPFLAGS                                                        += \
    -DOPENTHREAD_PLATFORM_POSIX_APP=1                                 \
    -I$(top_srcdir)/src/posix/platform                                \
    $(NULL)
endif

COMMON_LDADD                                                        = \
    $(NULL)

if OPENTHREAD_ENABLE_NCP
COMMON_LDADD                                                       += \
    $(top_builddir)/src/ncp/libopenthread-ncp-ftd.a                   \
    $(NULL)
endif

COMMON_LDADD                                                       += \
    $(top_builddir)/src/core/libopenthread-ftd.a                      \
    -lpthread                                                         \
    $(NULL)

if OPENTHREAD_ENABLE_BUILTIN_MBEDTLS
COMMON_LDADD                                                       += \
    $(top_builddir)/third_party/mbedtls/libmbedcrypto.a               \
    $(NULL)
endif

if OPENTHREAD_PLATFORM_POSIX_APP
COMMON_LDADD                                                       += \
    -lutil
    $(NULL)
endif

# Test applications that should be run when the 'check' target is run.

check_PROGRAMS                                                      = \
    test-toolchain                                                    \
    $(NULL)

if OPENTHREAD_ENABLE_FTD
check_PROGRAMS                                                     += \
    test-aes                                                          \
    test-child                                                        \
    test-child-table                                                  \
    test-heap                                                         \
    test-hmac-sha256                                                  \
    test-ip6-address                                                  \
    test-link-quality                                                 \
    test-linked-list                                                  \
    test-lowpan                                                       \
    test-mac-frame                                                    \
    test-message                                                      \
    test-message-queue                                                \
    test-netif                                                        \
    test-network-data                                                 \
    test-priority-queue                                               \
    test-pskc                                                         \
    test-string                                                       \
    test-timer                                                        \
    $(NULL)

if OPENTHREAD_ENABLE_NCP
check_PROGRAMS                                                     += \
    test-hdlc                                                         \
    test-ncp-buffer                                                   \
    test-spinel-decoder                                               \
    test-spinel-encoder                                               \
    $(NULL)
endif
endif # OPENTHREAD_ENABLE_FTD

XFAIL_TESTS                                                         = \
    $(NULL)

if OPENTHREAD_WITH_ADDRESS_SANITIZER
check_PROGRAMS                 += test-address-sanitizer
XFAIL_TESTS                    += test-address-sanitizer
test_address_sanitizer_SOURCES  = test_address_sanitizer.cpp
endif # OPENTHREAD_WITH_ADDRESS_SANITIZER


# Test applications and scripts that should be built and run when the
# 'check' target is run.

TESTS                                                               = \
    $(check_PROGRAMS)                                                 \
    $(NULL)

# The additional environment variables and their values that will be
# made available to all programs and scripts in TESTS.

TESTS_ENVIRONMENT                                                   = \
    top_srcdir='$(top_srcdir)'                                        \
    $(NULL)

COMMON_SOURCES               = test_platform.cpp test_util.cpp

# Source, compiler, and linker options for test programs.

test_aes_LDADD               = $(COMMON_LDADD)
test_aes_SOURCES             = $(COMMON_SOURCES) test_aes.cpp

test_child_LDADD             = $(COMMON_LDADD)
test_child_SOURCES           = $(COMMON_SOURCES) test_child.cpp

test_child_table_LDADD       = $(COMMON_LDADD)
test_child_table_SOURCES     = $(COMMON_SOURCES) test_child_table.cpp

test_hdlc_LDADD              = $(COMMON_LDADD)
test_hdlc_SOURCES            = $(COMMON_SOURCES) test_hdlc.cpp

test_heap_LDADD              = $(COMMON_LDADD)
test_heap_SOURCES            = $(COMMON_SOURCES) test_heap.cpp

test_hmac_sha256_LDADD       = $(COMMON_LDADD)
test_hmac_sha256_SOURCES     = $(COMMON_SOURCES) test_hmac_sha256.cpp

test_ip6_address_LDADD       = $(COMMON_LDADD)
test_ip6_address_SOURCES     = $(COMMON_SOURCES) test_ip6_address.cpp

test_link_quality_LDADD      = $(COMMON_LDADD)
test_link_quality_SOURCES    = $(COMMON_SOURCES) test_link_quality.cpp

test_linked_list_LDADD       = $(COMMON_LDADD)
test_linked_list_SOURCES     = $(COMMON_SOURCES) test_linked_list.cpp

test_lowpan_LDADD            = $(COMMON_LDADD)
test_lowpan_SOURCES          = $(COMMON_SOURCES) test_lowpan.cpp

test_mac_frame_LDADD         = $(COMMON_LDADD)
test_mac_frame_SOURCES       = $(COMMON_SOURCES) test_mac_frame.cpp

test_message_LDADD           = $(COMMON_LDADD)
test_message_SOURCES         = $(COMMON_SOURCES) test_message.cpp

test_message_queue_LDADD     = $(COMMON_LDADD)
test_message_queue_SOURCES   = $(COMMON_SOURCES) test_message_queue.cpp

test_ncp_buffer_LDADD        = $(COMMON_LDADD)
test_ncp_buffer_SOURCES      = $(COMMON_SOURCES) test_ncp_buffer.cpp

test_netif_LDADD             = $(COMMON_LDADD)
test_netif_SOURCES           = $(COMMON_SOURCES) test_netif.cpp

test_network_data_LDADD      = $(COMMON_LDADD)
test_network_data_SOURCES    = $(COMMON_SOURCES) test_network_data.cpp

test_priority_queue_LDADD    = $(COMMON_LDADD)
test_priority_queue_SOURCES  = $(COMMON_SOURCES) test_priority_queue.cpp

test_pskc_LDADD              = $(COMMON_LDADD)
test_pskc_SOURCES            = $(COMMON_SOURCES) test_pskc.cpp

test_string_LDADD            = $(COMMON_LDADD)
test_string_SOURCES          = $(COMMON_SOURCES) test_string.cpp

test_spinel_decoder_LDADD    = $(COMMON_LDADD)
test_spinel_decoder_SOURCES  = $(COMMON_SOURCES) test_spinel_decoder.cpp

test_spinel_encoder_LDADD    = $(COMMON_LDADD)
test_spinel_encoder_SOURCES  = $(COMMON_SOURCES) test_spinel_encoder.cpp

test_timer_LDADD             = $(COMMON_LDADD)
test_timer_SOURCES           = $(COMMON_SOURCES) test_timer.cpp

test_toolchain_LDADD         = $(NULL)
test_toolchain_SOURCES       = test_toolchain.cpp test_toolchain_c.c

PRETTY_FILES                                                        = \
    $(noinst_HEADERS)                                                 \
    $(test_address_sanitizer_SOURCES)                                 \
    $(test_aes_SOURCES)                                               \
    $(test_child_SOURCES)                                             \
    $(test_child_table_SOURCES)                                       \
    $(test_hdlc_SOURCES)                                              \
    $(test_heap_SOURCES)                                              \
    $(test_hmac_sha256_SOURCES)                                       \
    $(test_link_quality_SOURCES)                                      \
    $(test_linked_list_SOURCES)                                       \
    $(test_lowpan_SOURCES)                                            \
    $(test_mac_frame_SOURCES)                                         \
    $(test_message_queue_SOURCES)                                     \
    $(test_message_SOURCES)                                           \
    $(test_ncp_buffer_SOURCES)                                        \
    $(test_netif_SOURCES)                                             \
    $(test_network_data_SOURCES)                                      \
    $(test_priority_queue_SOURCES)                                    \
    $(test_pskc_SOURCES)                                              \
    $(test_spinel_decoder_SOURCES)                                    \
    $(test_spinel_encoder_SOURCES)                                    \
    $(test_string_SOURCES)                                            \
    $(test_timer_SOURCES)                                             \
    $(test_toolchain_SOURCES)                                         \
    $(NULL)

if OPENTHREAD_BUILD_COVERAGE
CLEANFILES                   = $(wildcard *.gcda *.gcno)
endif # OPENTHREAD_BUILD_COVERAGE

endif # OPENTHREAD_BUILD_TESTS

include $(abs_top_nlbuild_autotools_dir)/automake/post.am

