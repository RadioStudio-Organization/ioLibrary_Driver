# W5500 Library Configuration
cmake_minimum_required(VERSION 3.13)

# W5500 specific sources
set(W5500_SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/Ethernet/W5500/w5500.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Ethernet/wizchip_conf.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Ethernet/socket.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Internet/DNS/dns.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Internet/DHCP/dhcp.c
    
)

# W5500 include directories
set(W5500_INCLUDES
    ${CMAKE_CURRENT_SOURCE_DIR}/Ethernet
    ${CMAKE_CURRENT_SOURCE_DIR}/Ethernet/W5500
    ${CMAKE_CURRENT_SOURCE_DIR}/Internet/DNS
    ${CMAKE_CURRENT_SOURCE_DIR}/Internet/DHCP
    ${CMAKE_CURRENT_SOURCE_DIR}
)

# Create W5500 library
add_library(w5500_lib STATIC ${W5500_SOURCES})

target_include_directories(w5500_lib PUBLIC ${W5500_INCLUDES})

# Compile definitions
target_compile_definitions(w5500_lib PUBLIC
    _WIZCHIP_=5500
    _WIZCHIP_IO_MODE_=_WIZCHIP_IO_MODE_SPI_
)

# Link to your main project
target_link_libraries(${PROJECT_NAME} w5500_lib)
# Wiznet lib