cmake_minimum_required(VERSION 2.8.3)

project(sawyer_description)

find_package(catkin REQUIRED)

catkin_package()

# Configure the develspace pkg-config file
set(DATADIR "${PROJECT_SOURCE_DIR}")
configure_file(
  "${PROJECT_SOURCE_DIR}/${PROJECT_NAME}.pc.cmake"
  "${CATKIN_DEVEL_PREFIX}/lib/pkgconfig/${PROJECT_NAME}.pc")

# Configure the installspace pkg-config file
set(DATADIR "${CMAKE_INSTALL_PREFIX}/${CATKIN_PACKAGE_SHARE_DESTINATION}")
file(MAKE_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/catkin_generated/installspace)
configure_file(
  "${PROJECT_SOURCE_DIR}/${PROJECT_NAME}.pc.cmake"
  "${CMAKE_CURRENT_BINARY_DIR}/catkin_generated/installspace/${PROJECT_NAME}.pc")
install(
  FILES ${CMAKE_CURRENT_BINARY_DIR}/catkin_generated/installspace/${PROJECT_NAME}.pc
  DESTINATION lib/pkgconfig)

foreach(dir config meshes params urdf)
   install(DIRECTORY ${dir}/
      DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/${dir})
endforeach(dir)
