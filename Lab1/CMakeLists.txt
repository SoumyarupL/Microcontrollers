add_executable(multitest_incremental multitest.c)

# must match with pio filename and executable name from above
pico_generate_pio_header(multitest_incremental ${CMAKE_CURRENT_LIST_DIR}/hsync.pio)
pico_generate_pio_header(multitest_incremental ${CMAKE_CURRENT_LIST_DIR}/vsync.pio)
pico_generate_pio_header(multitest_incremental ${CMAKE_CURRENT_LIST_DIR}/rgb.pio)

# must match with executable name and source file names
target_sources(multitest_incremental PRIVATE multitest.c vga_graphics.c)

# Add pico_multicore which is required for multicore functionality
target_link_libraries(multitest_incremental PRIVATE pico_stdlib pico_multicore pico_bootsel_via_double_reset hardware_sync hardware_spi hardware_pio hardware_dma hardware_adc hardware_irq hardware_uart)

pico_enable_stdio_usb(multitest_incremental 1)
pico_enable_stdio_uart(multitest_incremental 0)

# create map/bin/hex file etc.
pico_add_extra_outputs(multitest_incremental)
