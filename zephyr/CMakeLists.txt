#
# Copyright (c) 2018 Nordic Semiconductor
#
# SPDX-License-Identifier: LicenseRef-Nordic-5-Clause
#

if(CONFIG_BT_LL_SOFTDEVICE_HEADERS_INCLUDE AND NOT CONFIG_BT_LL_SOFTDEVICE_HEADERS_INCLUDE_PATH_OVERRIDE)
  zephyr_include_directories(${CMAKE_CURRENT_LIST_DIR}/../include)
endif()

if(NOT CONFIG_BT_LL_SOFTDEVICE OR NOT CONFIG_BT_LL_SOFTDEVICE_BUILD_TYPE_LIB)
  return()
endif()

if(CONFIG_BT_LL_SOFTDEVICE_PERIPHERAL)
  set(SDC_VARIANT peripheral)
elseif(CONFIG_BT_LL_SOFTDEVICE_CENTRAL)
  set(SDC_VARIANT central)
elseif(CONFIG_BT_LL_SOFTDEVICE_MULTIROLE)
  set(SDC_VARIANT multirole)
else()
  message(WARNING "No SoftDevice Controller variant selected")
  return()
endif()

set(SDC_SOC ${CONFIG_MPSL_SOC})
set(SDC_FLOAT_TYPE ${CONFIG_MPSL_LIB_FLOAT_ABI})
set(SDC_HEADERS_INCLUDE ON)
set(SDC_HEADERS_INCLUDE_PATH_OVERRIDE ON)

add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/.. ${CMAKE_CURRENT_BINARY_DIR}/softdevice_controller)
zephyr_link_libraries(softdevice_controller)
