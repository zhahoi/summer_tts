cmake_minimum_required(VERSION 3.10)
project(summer_tts)

set(CMAKE_CXX_FLAGS " -O3 -fopenmp -std=c++11 ")
set(CMAKE_C_FLAGS " -O3 -fopenmp -std=c++11 ")

set(PROJECT_NAME "summer_tts")

## Compile as C++11, supported in ROS Kinetic and newer
# add_compile_options(-std=c++11)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
)

## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)


## Uncomment this if the package has a setup.py. This macro ensures
## modules and global scripts declared therein get installed
## See http://ros.org/doc/api/catkin/html/user_guide/setup_dot_py.html
# catkin_python_setup()

################################################
## Declare ROS messages, services and actions ##
################################################

## To declare and build messages, services or actions from within this
## package, follow these steps:
## * Let MSG_DEP_SET be the set of packages whose message types you use in
##   your messages/services/actions (e.g. std_msgs, actionlib_msgs, ...).
## * In the file package.xml:
##   * add a build_depend tag for "message_generation"
##   * add a build_depend and a exec_depend tag for each package in MSG_DEP_SET
##   * If MSG_DEP_SET isn't empty the following dependency has been pulled in
##     but can be declared for certainty nonetheless:
##     * add a exec_depend tag for "message_runtime"
## * In this file (CMakeLists.txt):
##   * add "message_generation" and every package in MSG_DEP_SET to
##     find_package(catkin REQUIRED COMPONENTS ...)
##   * add "message_runtime" and every package in MSG_DEP_SET to
##     catkin_package(CATKIN_DEPENDS ...)
##   * uncomment the add_*_files sections below as needed
##     and list every .msg/.srv/.action file to be processed
##   * uncomment the generate_messages entry below
##   * add every package in MSG_DEP_SET to generate_messages(DEPENDENCIES ...)

## Generate messages in the 'msg' folder
# add_message_files(
#   FILES
#   Message1.msg
#   Message2.msg
# )

## Generate services in the 'srv' folder
# add_service_files(
#   FILES
#   Service1.srv
#   Service2.srv
# )

## Generate actions in the 'action' folder
# add_action_files(
#   FILES
#   Action1.action
#   Action2.action
# )

## Generate added messages and services with any dependencies listed here
# generate_messages(
#   DEPENDENCIES
#   std_msgs
# )

################################################
## Declare ROS dynamic reconfigure parameters ##
################################################

## To declare and build dynamic reconfigure parameters within this
## package, follow these steps:
## * In the file package.xml:
##   * add a build_depend and a exec_depend tag for "dynamic_reconfigure"
## * In this file (CMakeLists.txt):
##   * add "dynamic_reconfigure" to
##     find_package(catkin REQUIRED COMPONENTS ...)
##   * uncomment the "generate_dynamic_reconfigure_options" section below
##     and list every .cfg file to be processed

## Generate dynamic reconfigure parameters in the 'cfg' folder
# generate_dynamic_reconfigure_options(
#   cfg/DynReconf1.cfg
#   cfg/DynReconf2.cfg
# )

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if your package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES summer_tts
#  CATKIN_DEPENDS roscpp rospy std_msgs
#  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
# include_directories(
# # include
#   ${catkin_INCLUDE_DIRS}
# )

## Declare a C++ library
# add_library(${PROJECT_NAME}
#   src/${PROJECT_NAME}/summer_tts.cpp
# )

## Add cmake target dependencies of the library
## as an example, code may need to be generated before libraries
## either from message generation or dynamic reconfigure
# add_dependencies(${PROJECT_NAME} ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

## Declare a C++ executable
## With catkin_make all packages are built within a single CMake context
## The recommended prefix ensures that target names across packages don't collide
# add_executable(${PROJECT_NAME}_node src/summer_tts_node.cpp)
add_executable(${PROJECT_NAME}_node
               ./src/summer_tts_node.cpp
               ./src/tn/glog/src/demangle.cc
               ./src/tn/glog/src/logging.cc
               ./src/tn/glog/src/raw_logging.cc
               ./src/tn/glog/src/symbolize.cc
               ./src/tn/glog/src/utilities.cc
               ./src/tn/glog/src/vlog_is_on.cc
               ./src/tn/glog/src/signalhandler.cc
               ./src/tn/gflags/src/gflags.cc
               ./src/tn/gflags/src/gflags_reporting.cc
               ./src/tn/gflags/src/gflags_completions.cc
               ./src/tn/openfst/src/lib/compat.cc
               ./src/tn/openfst/src/lib/flags.cc
               ./src/tn/openfst/src/lib/fst.cc
               ./src/tn/openfst/src/lib/fst-types.cc
               ./src/tn/openfst/src/lib/mapped-file.cc
               ./src/tn/openfst/src/lib/properties.cc
               ./src/tn/openfst/src/lib/symbol-table.cc
               ./src/tn/openfst/src/lib/symbol-table-ops.cc
               ./src/tn/openfst/src/lib/util.cc
               ./src/tn/openfst/src/lib/weight.cc
               ./src/tn/processor.cc
               ./src/tn/token_parser.cc
               ./src/tn/utf8_string.cc
               ./src/engipa/EnglishText2Id.cpp
               ./src/engipa/InitIPASymbols.cpp
               ./src/engipa/alphabet.cpp
               ./src/engipa/ipa.cpp
               ./src/hz2py/hanzi2phoneid.cpp
               ./src/hz2py/Hanz2Piny.cpp
               ./src/hz2py/pinyinmap.cpp
               ./src/nn_op/nn_conv1d.cpp
               ./src/nn_op/nn_softmax.cpp
               ./src/nn_op/nn_layer_norm.cpp
               ./src/nn_op/nn_relu.cpp
               ./src/nn_op/nn_gelu.cpp
               ./src/nn_op/nn_tanh.cpp
               ./src/nn_op/nn_flip.cpp
               ./src/nn_op/nn_cumsum.cpp
               ./src/nn_op/nn_softplus.cpp
               ./src/nn_op/nn_clamp_min.cpp
               ./src/nn_op/nn_sigmoid.cpp
               ./src/nn_op/nn_conv1d_transposed.cpp
               ./src/nn_op/nn_leaky_relu.cpp
               ./src/platform/tts_file_io.cpp
               ./src/platform/tts_logger.cpp
               ./src/utils/utils.cpp
               ./src/modules/iStft.cpp
               ./src/modules/hann.cpp
               ./src/modules/attention_encoder.cpp
               ./src/modules/multi_head_attention.cpp
               ./src/modules/ffn.cpp
               ./src/modules/ConvFlow.cpp
               ./src/modules/DDSConv.cpp
               ./src/modules/ElementwiseAffine.cpp
               ./src/modules/random_gen.cpp
               ./src/modules/ResidualCouplingLayer.cpp
               ./src/modules/ResBlock1.cpp
               ./src/modules/WN.cpp
               ./src/modules/pqmf.cpp
               ./src/models/TextEncoder.cpp
               ./src/models/StochasticDurationPredictor.cpp
               ./src/models/FixDurationPredictor.cpp
               ./src/models/DurationPredictor_base.cpp
               ./src/models/ResidualCouplingBlock.cpp
               ./src/models/Generator_base.cpp
               ./src/models/Generator_hifigan.cpp
               ./src/models/Generator_MS.cpp
               ./src/models/Generator_Istft.cpp
               ./src/models/Generator_MBB.cpp
               ./src/models/SynthesizerTrn.cpp)


target_include_directories(${PROJECT_NAME}_node PUBLIC 
                                             ${catkin_INCLUDE_DIRS}
                                             ./eigen-3.4.0
                                             ./include
                                             ./src/tn/header
                                             ./src/header
                                             )

## Rename C++ executable without prefix
## The above recommended prefix causes long target names, the following renames the
## target back to the shorter version for ease of user use
## e.g. "rosrun someones_pkg node" instead of "rosrun someones_pkg someones_pkg_node"
# set_target_properties(${PROJECT_NAME}_node PROPERTIES OUTPUT_NAME node PREFIX "")

## Add cmake target dependencies of the executable
## same as for the library above
add_dependencies(${PROJECT_NAME}_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

## Specify libraries to link a library or executable target against
target_link_libraries(${PROJECT_NAME}_node
  ${catkin_LIBRARIES}
  glog gflags 
)

#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/api/catkin/html/adv_user_guide/variables.html

## Mark executable scripts (Python etc.) for installation
## in contrast to setup.py, you can choose the destination
# catkin_install_python(PROGRAMS
#   scripts/my_python_script
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark executables for installation
## See http://docs.ros.org/melodic/api/catkin/html/howto/format1/building_executables.html
# install(TARGETS ${PROJECT_NAME}_node
#   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark libraries for installation
## See http://docs.ros.org/melodic/api/catkin/html/howto/format1/building_libraries.html
# install(TARGETS ${PROJECT_NAME}
#   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION}
# )

## Mark cpp header files for installation
# install(DIRECTORY include/${PROJECT_NAME}/
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
#   FILES_MATCHING PATTERN "*.h"
#   PATTERN ".svn" EXCLUDE
# )

## Mark other files for installation (e.g. launch and bag files, etc.)
# install(FILES
#   # myfile1
#   # myfile2
#   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
# )

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_summer_tts.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
