# SPDX-License-Identifier: Apache-2.0

if(CONFIG_DW3000)


    # we *should* be able to add subdir dwt_ubw_drier and link against
    # uwb_driver, but if we do that all the args like architecture and stuff
    # aren't passed and things dont' work

    ## add CMakeLists.txt from qorvo, it defines uwb_driver lib
    #set(DWT_DW3000 ${CONFIG_DW3000_CHIP_DW3000})
    #set(DWT_DW3720 ${CONFIG_DW3000_CHIP_DW3720})
    #add_subdirectory(dwt_uwb_driver)

    zephyr_library()

    zephyr_library_sources(
        platform/deca_port.c
        platform/dw3000_hw.c
        platform/dw3000_spi.c
        dwt_uwb_driver/deca_compat.c
        dwt_uwb_driver/deca_interface.c
        dwt_uwb_driver/deca_rsl.c
        dwt_uwb_driver/lib/qmath/src/qmath.c
    )
    zephyr_library_sources_ifdef(CONFIG_DW3000_CHIP_DW3000 dwt_uwb_driver/dw3000/dw3000_device.c)
    zephyr_include_directories_ifdef(CONFIG_DW3000_CHIP_DW3000 dwt_uwb_driver/dw3000/)
    zephyr_library_sources_ifdef(CONFIG_DW3000_CHIP_DW3720 dwt_uwb_driver/dw3720/dw3720_device.c)
    zephyr_include_directories_ifdef(CONFIG_DW3000_CHIP_DW3720 dwt_uwb_driver/dw3720/)

    zephyr_include_directories(platform)
    zephyr_include_directories(dwt_uwb_driver)
    zephyr_include_directories(dwt_uwb_driver/lib/qmath/include)

    #zephyr_library_link_libraries(uwb_driver)

endif(CONFIG_DW3000)
