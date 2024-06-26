cmake_minimum_required(VERSION 3.5)
project(abhiswarming)

# --------------------------------------------------------------------------- #
# Find dependencies.
find_package(ament_cmake REQUIRED)

# --------------------------------------------------------------------------- #
#  Install.

# Install project launch files.
install(
  DIRECTORY
    launch/
  DESTINATION share/${PROJECT_NAME}/launch
)

# Install project configuration files.
install(
  DIRECTORY
    config/
  DESTINATION share/${PROJECT_NAME}/config
)

# Install model files
install(
  DIRECTORY
    models/
  DESTINATION share/${PROJECT_NAME}/models
)

# Install world files
install(
  DIRECTORY
    worlds/
  DESTINATION share/${PROJECT_NAME}/worlds
)


### Enable if necessary

# # Install project rviz files. 
# install(
#   DIRECTORY
#     rviz/
#   DESTINATION share/${PROJECT_NAME}/rviz
# )

# --------------------------------------------------------------------------- #
#  Build tests.

if(BUILD_TESTING)
  # Override default flake8 configuration.
  set(ament_cmake_flake8_CONFIG_FILE ${CMAKE_SOURCE_DIR}/.flake8)

  # Add linters.
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

# --------------------------------------------------------------------------- #
#  Call last.

ament_package()
