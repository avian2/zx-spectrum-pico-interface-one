cmake_minimum_required(VERSION 3.13)

include(pico_sdk_import.cmake)

project(zx_pico_rom_project C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

set(PICO_COPY_TO_RAM 1)

pico_sdk_init()

if (TARGET tinyusb_device)

  add_executable(zx_pico_if1_fw
    zx_pico_if1_fw.c
    roms.h
  )

  target_link_libraries(zx_pico_if1_fw pico_stdlib pico_multicore pico_mem_ops)

  pico_enable_stdio_usb(zx_pico_if1_fw 0)
  pico_enable_stdio_uart(zx_pico_if1_fw 0)

  pico_add_extra_outputs(zx_pico_if1_fw)

elseif(PICO_ON_DEVICE)
   message(WARNING "not building because TinyUSB submodule is not initialized in the SDK")
endif()
