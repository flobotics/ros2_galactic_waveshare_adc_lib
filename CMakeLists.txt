cmake_minimum_required(VERSION 3.8)
project(ros2_galactic_waveshare_adc_lib)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic -lpthread -lm -lwiringPi)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)

add_library(ros2_galactic_waveshare_adc_lib SHARED
            src/ADS1256.c
            src/DEV_Config.c
            )

target_include_directories(ros2_galactic_waveshare_adc_lib PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>)
  
#ament_export_interfaces(export_ros2_galactic_waveshare_adc_lib HAS_LIBRARY_TARGET)
ament_export_targets(export_ros2_galactic_waveshare_adc_lib HAS_LIBRARY_TARGET)

install(
  DIRECTORY include/
  DESTINATION include
)

install(
  TARGETS ros2_galactic_waveshare_adc_lib
  EXPORT export_ros2_galactic_waveshare_adc_lib
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
  INCLUDES DESTINATION include
)

ament_export_include_directories(include)
ament_export_libraries(ros2_galactic_waveshare_adc_lib)

ament_package()
