# SPDX-License-Identifier: Apache-2.0

if(CONFIG_FPU)
    set(TYPE hfp)
else()
    set(TYPE sfp)
endif()

# use zephyr_library_import in order to get it linked with the
# -Wl,--whole-archive flag (keep all symbols)
zephyr_library_import(embedded_mac ${CMAKE_CURRENT_SOURCE_DIR}/lib/cmsis_v1/embedded_mac/libembedded_mac_arm-m4-${TYPE}_R11.9.2.a)
zephyr_library_import(uci_backend_coordinator ${CMAKE_CURRENT_SOURCE_DIR}/lib/cmsis_v1/uci/uci_backend/libuci_backend_arm-m4-${TYPE}_R11.9.2.a)
zephyr_library_import(uci_backend ${CMAKE_CURRENT_SOURCE_DIR}/lib/cmsis_v1/uci/uci_backend/libuci_backend_coordinator_arm-m4-${TYPE}_R11.9.2.a)
zephyr_library_import(uci_core ${CMAKE_CURRENT_SOURCE_DIR}/lib/cmsis_v1/uci/uci_core/libuci_core_arm-m4-${TYPE}_R11.9.2.a)

zephyr_include_directories(
    include/uci/coordinator
    include/uci/uci_backend
    include/uci
    include/compat/common
    include/compat/cmsis
    include/compat
    include/mcps
    include
    include/uwbmac
    include/uwb_driver_interface)
