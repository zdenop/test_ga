# CMakeLists files in this project can refer to the root source directory of the
# project as ${HELLO_SOURCE_DIR} and to the root binary directory of the project
# as ${HELLO_BINARY_DIR}.
cmake_minimum_required(VERSION 3.1.3)
project(HELLO C CXX)

set(MINIMUM_WEBPMUX_VERSION 0.5.0)
option(LIBWEBP_SUPPORT "Build with WebP support" ON)
option(OPENJPEG_SUPPORT "Build with OpenJPEG support" ON)

find_package(GIF)
if(GIF_FOUND)
  set(libs_private "${libs_private} -lgif")
endif()
find_package(JPEG)
if(JPEG_FOUND)
  set(pkgs_private "${pkgs_private} libjpeg")
endif()
find_package(PNG)
if(PNG_FOUND)
  set(pkgs_private "${pkgs_private} libpng")
endif()
find_package(TIFF)
if(TIFF_FOUND)
  set(pkgs_private "${pkgs_private} libtiff-4")
endif()
find_package(ZLIB)
if(ZLIB_FOUND)
  set(pkgs_private "${pkgs_private} zlib")
endif()
if(LIBWEBP_SUPPORT)
  find_package(WebP ${MINIMUM_WEBPMUX_VERSION})  #  CONFIG REQUIRED
  set(pkgs_private "${pkgs_private} libwebp libwebpmux")
endif()
if(OPENJPEG_SUPPORT)
  find_package(OpenJPEG)  # CONFIG REQUIRED
  set(pkgs_private "${pkgs_private} libopenjp2")
endif()

message(STATUS "Used ZLIB library: ${ZLIB_LIBRARIES}")
message(STATUS "Used PNG library:  ${PNG_LIBRARIES}")
message(STATUS "Used JPEG library: ${JPEG_LIBRARIES}")
message(STATUS "Used TIFF library: ${TIFF_LIBRARIES}")
message(STATUS "Used GIF library:  ${GIF_LIBRARIES}")
message(STATUS "Used OPENJPEG library: ${OPENJPEG_LIBRARIES}")
message(STATUS "Used WEBP library: ${WEBP_LIBRARIES}")

message(STATUS "Used WebP_FOUND library: ${WebP_FOUND}")
message(STATUS "Used OpenJPEG_FOUND library: ${OpenJPEG_FOUND}")
