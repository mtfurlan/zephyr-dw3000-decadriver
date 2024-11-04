# SPDX-License-Identifier: Apache-2.0

if(CONFIG_DW3000)

# add CMakeLists.txt from qorvo, it defines uwb_driver lib
set(DWT_DW3000 ${CONFIG_DW3000_CHIP_DW3000})
set(DWT_DW3720 ${CONFIG_DW3000_CHIP_DW3720})
add_subdirectory(dwt_uwb_driver)

# for some reason this doesn't work, and my application can't find deca_device_api.h
# adding it to zephyr lib lower down but I don't like it
target_include_directories(uwb_driver PUBLIC dwt_uwb_driver)


#TODO: pass optimizations from zephyr
target_compile_options(uwb_driver PRIVATE -ggdb)
#zephyr_library_cc_option(-Wno-unused-function)





zephyr_library()
zephyr_library_sources(
    #platform/deca_compat.c
    platform/deca_port.c
    platform/dw3000_hw.c
    platform/dw3000_spi.c
)
zephyr_include_directories(platform)
# this shouldn't be necessary vvv
zephyr_include_directories(dwt_uwb_driver)
zephyr_library_link_libraries(uwb_driver)

endif(CONFIG_DW3000)
