# cmake_minimum_required(VERSION 3.12)

# # rest of your project
# add_executable(usb_microphone
#     main.c
#     usb_descriptors.c
#     usb_microphone.c
# )

# target_include_directories(usb_microphone PRIVATE ${CMAKE_CURRENT_LIST_DIR})

# target_link_libraries(usb_microphone PRIVATE tinyusb_device tinyusb_board pico_pdm_microphone)

# # create map/bin/hex/uf2 file in addition to ELF.
# pico_add_extra_outputs(usb_microphone)

cmake_minimum_required(VERSION 3.12)

add_executable(usb_microphone
    main.c
    usb_descriptors.c
    usb_microphone.c
)

target_include_directories(usb_microphone PRIVATE ${CMAKE_CURRENT_LIST_DIR})

target_link_libraries(usb_microphone
    PRIVATE
    tinyusb_device
    tinyusb_board
    pico_pdm_microphone
)

# ✅ Define required TinyUSB config macros here
target_compile_definitions(usb_microphone PRIVATE
    CFG_TUSB_MCU=OPT_MCU_RP2040
    #ßCFG_TUSB_RHPORT0_MODE=OPT_MODE_DEVICE
    CFG_TUD_AUDIO=1
)

# Output map/bin/hex/uf2 files
pico_add_extra_outputs(usb_microphone)
