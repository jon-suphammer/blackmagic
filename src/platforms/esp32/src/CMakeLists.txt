# This file was automatically generated for projects
# without default 'CMakeLists.txt' file.

FILE(GLOB_RECURSE app_sources ${CMAKE_SOURCE_DIR}/src/*.*)


set(SOURCES 
#../../common/cdcacm.c 
../../common/swdptap.c
../../common/jtagtap.c
#../../common/timing.c
../../../gdb_main.c
../../../command.c  
../../../crc32.c  
../../../exception.c  
../../../gdb_hostio.c  
../../../gdb_main.c  
../../../gdb_packet.c
../../../remote.c  
../../../hex_utils.c  
../../../main.c  
../../../morse.c  
#traceswo.c
platform.c
gdb_if.c)

set(TARGETS 
../../../target/adiv5.c          
../../../target/cortexa.c   
../../../target/lpc11xx.c   
../../../target/lpc_common.c   
../../../target/nxpke04.c   
../../../target/samd.c      
../../../target/stm32h7.c           
../../../target/target.c
../../../target/cortexm.c   
../../../target/jtag_devs.c   
#../../../target/jtagtap_generic.c   
../../../target/lpc15xx.c   
../../../target/sam3x.c     
../../../target/samx5x.c    
../../../target/stm32l0.c           
../../../target/adiv5_jtagdp.c   
../../../target/kinetis.c           
../../../target/lpc17xx.c   
../../../target/msp432.c       
../../../target/sam4l.c     
../../../target/stm32f1.c   
../../../target/stm32l0.c
../../../target/stm32l4.c
../../../target/adiv5_swdp.c     
../../../target/efm32.c     
../../../target/jtag_scan.c   
../../../target/lmi.c               
../../../target/lpc43xx.c   
../../../target/lpc546xx.c   
../../../target/nrf51.c         
../../../target/stm32f4.c   
../../../target/stm32g0.c   
../../../target/rp.c
../../../target/sam3x.c
../../../target/sam4l.c
../../../target/samx5x.c
../../../target/stm32h7.c
../../../target/ch32f1.c
#../../../target/swdptap_generic.c
)

idf_component_register(SRCS main.c ${SOURCES} ${TARGETS}
	INCLUDE_DIRS
		${CMAKE_SOURCE_DIR} "../include"
		${CMAKE_SOURCE_DIR} "../../../include"
		${CMAKE_SOURCE_DIR} "../../common"
		${CMAKE_SOURCE_DIR} "../../../target"
		${CMAKE_SOURCE_DIR} "../../../../libopencm3/include")

add_definitions(-DPC_HOSTED=0)