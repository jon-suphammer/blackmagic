cmake_minimum_required(VERSION 3.5)

project(esp32_blackmagic C)

set(SUPPORTED_TARGETS esp32)
    # Include for ESP-IDF build system functions
    include($ENV{IDF_PATH}/tools/cmake/idf.cmake)
    # Create idf::esp32 and idf::freertos static libraries
    idf_build_process(esp32
                    # try and trim the build; additional components
                    # will be included as needed based on dependency tree
                    #
                    # although esptool_py does not generate static library,
                    # processing the component is needed for flashing related
                    # targets and file generation
                    COMPONENTS esp32 freertos esptool_py nvs_flash
                    SDKCONFIG ${CMAKE_BINARY_DIR}/sdkconfig
                    BUILD_DIR ${CMAKE_BINARY_DIR})

include_directories($ENV{IDF_PATH}/components/nvs_flash/include
    ../../include 
    ../common
    ../../target
    .
    ../../../libopencm3/include)

set(elf_file ${CMAKE_PROJECT_NAME}.elf)

set(SOURCES 
#../common/cdcacm.c 
../common/swdptap.c
../common/jtagtap.c
../common/timing.c
../../gdb_main.c
../../command.c  
../../crc32.c  
../../exception.c  
../../gdb_hostio.c  
../../gdb_main.c  
../../gdb_packet.c
../../remote.c  
../../hex_utils.c  
../../main.c  
../../morse.c  
#traceswo.c
platform.c
gdb_if.c)

set(TARGETS 
../../target/adiv5.c          
../../target/cortexa.c   
../../target/lpc11xx.c   
../../target/lpc_common.c   
../../target/nxpke04.c   
../../target/samd.c      
../../target/stm32h7.c           
../../target/target.c
../../target/cortexm.c   
../../target/jtag_devs.c   
#../../target/jtagtap_generic.c   
../../target/lpc15xx.c   
../../target/sam3x.c     
../../target/samx5x.c    
../../target/stm32l0.c           
../../target/adiv5_jtagdp.c   
../../target/kinetis.c           
../../target/lpc17xx.c   
../../target/msp432.c       
../../target/sam4l.c     
../../target/stm32f1.c   
../../target/stm32l4.c
../../target/adiv5_swdp.c     
../../target/efm32.c     
../../target/jtag_scan.c   
../../target/lmi.c               
../../target/lpc43xx.c   
../../target/nrf51.c         
../../target/stm32f4.c   
#../../target/swdptap_generic.c
)

add_executable(${elf_file} ${SOURCES} ${TARGETS} main.c)

# Link the static libraries to the executable
target_link_libraries(${elf_file} idf::esp32 idf::freertos idf::spi_flash)
# Attach additional targets to the executable file for flashing,
# linker script generation, partition_table generation, etc.
idf_build_executable(${elf_file})

set(CMAKE_EXPORT_COMPILE_COMMANDS 1)
