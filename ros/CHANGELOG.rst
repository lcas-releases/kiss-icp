^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Changelog for package kiss_icp
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

0.4.1 (2024-07-11)
------------------
* dev-container
* Cleanup ROS package.xml and CMakeLists.txt (`#337 <https://github.com/LCAS/kiss-icp/issues/337>`_)
  Add missing system dependencies as wel
* Change target names (`#327 <https://github.com/LCAS/kiss-icp/issues/327>`_)
  * Change target names
  * This can be reverted, but it is related
  * Fix also tbb population
  * MakeAvailable for the win
  * Revert "This can be reverted, but it is related"
  This reverts commit 59b5d21607e66883ad71fa6b3ad3463075515d4a.
* Refactor KissICP pipeline to mantain just 1 pose instead of full trajectory. Fixes `#122 <https://github.com/LCAS/kiss-icp/issues/122>`_ (`#318 <https://github.com/LCAS/kiss-icp/issues/318>`_)
  * First draft for fixed_size_vector. Fixes `#122 <https://github.com/LCAS/kiss-icp/issues/122>`_
  * Pose pair, many ifs go Rhaus if this works
  * New adaptive threshold based on pose vector modification
  * Now has moved also rhaus from python
  * Push new draft with no new types
  * rename
  * Fix ROS2
  * Remove unused functions from cpp
  * Reduce code lines more
  * Change names and add some more comments
  * Marry python and C++ implementations
  * remove unused headers
  * Keep copy-pasting 🤦
  * Move poses array one level up, and add new deskew function to python API
  Now I like it even better. The `pipeline` is in charge of managing the
  trajectory of poses, as the KISS ICP method is invariant to this.
  * Renaming of Registration types and functions
  * from current to last
  * Renaming and reshaping in Adaptive threshold
  * More cosmesis on the AdaptiveThreshold
  * Remove constexpr
  * Ciao deskew with start/end pose
  * At least inline it
  * Const correcteness
  * New ATE from Benedikt PR
  * Revert "New ATE from Benedikt PR"
  This reverts commit af201c4e96030aa6820c150987fcd83335273b7e.
  ---------
  Co-authored-by: tizianoGuadagnino <frevo93@gmail.com>
  Co-authored-by: Benedikt Mersch <benedikt.mersch@gmail.com>
* Clean leftover from merge conflicts (`#301 <https://github.com/LCAS/kiss-icp/issues/301>`_)
  The logger should be kiss_icp_node, not odometry_Node
* Fix and improve ROS visualization (`#285 <https://github.com/LCAS/kiss-icp/issues/285>`_)
  * Fix this madness
  Simplify implementation by debugging in an ego-centric way always.
  Since the KISS-ICP internal map is on the global coordinates, fetch the
  last ego-centric pose and apply it to the map. Seen from the
  cloud_frame_id (which is the sensor frame) everything should always work
  in terms of visualization, no matter the multi-sensor setup.
  * Now is safe to disable this by default
  * Simplify, borrow the header from the input pointcloud msg
  This actually makes the visualization closer to the Python visualizer
  * Disable path/odom visualization by default
  In the case where we are not computing the poses in an egocentric world
  (base_frame != "") and we are not publishing to the TF tree, then the
  visualization wouldn't make sense. Therefore, disable it by default
  * Changed my mind
  If someone doesn't have that particular frame defined, then the
  visualization won't work. Leave this default
  * Move responsability of handling tf frames out of Registration (`#288 <https://github.com/LCAS/kiss-icp/issues/288>`_)
  * Move responsability of handling tf frames out of Registration
  Since with this new changes PublishOdometry is the only member that
  requieres to know the user specified target-frame, it is not necesary to
  handle all this bits.
  This makes the implementation cleaner, easier to read and reduces the
  lines of code. Now RegisterFrame is a simple callback as few months ago
  one can read in seconds.
  * typo
  * Easier to read
  * We need this for LookupTransform
  * Remove unused variable
  * Revert "Remove unused variable"
  This reverts commit 424ee901c5442ef1f1651f48079c8cbf5a3f10bf.
  * Remove unnecessary check
  * Remove unnecessary exposed utility function from ROS API
  With this change this function is not exposed (which was never the
  intention to) to the header. This way we can also "hide" this into a
  private unnamed namesapces and benefit from inlining the simple function
  into the translation unit
  * Revert "Remove unnecessary exposed utility function from ROS API"
  This reverts commit 23cd7efafd133c4f209f8575d079dee2d14702ae.
  * Revert "Remove unnecessary check"
  This reverts commit d1dcb48762392aae879e84d849c8f4b9c6e6cc10.
  * merge conflicts :0
  * Remove unnecessary exposed utility function from ROS API (`#289 <https://github.com/LCAS/kiss-icp/issues/289>`_)
  * Move responsability of handling tf frames out of Registration
  Since with this new changes PublishOdometry is the only member that
  requieres to know the user specified target-frame, it is not necesary to
  handle all this bits.
  This makes the implementation cleaner, easier to read and reduces the
  lines of code. Now RegisterFrame is a simple callback as few months ago
  one can read in seconds.
  * typo
  * Easier to read
  * We need this for LookupTransform
  * Remove unused variable
  * Revert "Remove unused variable"
  This reverts commit 424ee901c5442ef1f1651f48079c8cbf5a3f10bf.
  * Remove unnecessary check
  * Remove unnecessary exposed utility function from ROS API
  With this change this function is not exposed (which was never the
  intention to) to the header. This way we can also "hide" this into a
  private unnamed namesapces and benefit from inlining the simple function
  into the translation unit
  * Revert "Remove unnecessary exposed utility function from ROS API"
  This reverts commit 23cd7efafd133c4f209f8575d079dee2d14702ae.
  * Remove unnecessary exposed utility function from ROS API
  With this change this function is not exposed (which was never the
  intention to) to the header. This way we can also "hide" this into a
  private unnamed namesapces and benefit from inlining the simple function
  into the translation unit
  * Revert "Remove unnecessary check"
  This reverts commit d1dcb48762392aae879e84d849c8f4b9c6e6cc10.
  ---------
  Co-authored-by: tizianoGuadagnino <frevo93@gmail.com>
  * too many merges
  * Merge Rviz and Python colors
  * Just make the default construction more clear
  ---------
  Co-authored-by: tizianoGuadagnino <frevo93@gmail.com>
* Refactor ROS parametrization (`#282 <https://github.com/LCAS/kiss-icp/issues/282>`_)
  * Move ros params from launch file to YAML
  * Reuse arguments for debug clouds
  * Rename odometry_node to kiss_icp_node
  odometry is way to generic
  * Rename node agin
  * Voxel size is optional paramter
  * Reads better like this
  * New parameter proposal
  * Add odometry covariance to ros node (`#283 <https://github.com/LCAS/kiss-icp/issues/283>`_)
  * Add fixed covariance to odometry msg
  * Add default value just in case
  * pre-commit
  * Expose number of icp iterations in ros (`#292 <https://github.com/LCAS/kiss-icp/issues/292>`_)
  * Expose registration params to ROS node
  * More merge conflicts
  * Default to multithread
* Remove unnecesary path publishing pipeline (`#284 <https://github.com/LCAS/kiss-icp/issues/284>`_)
* Auto 2257 fix double construction kiss icp cpp (`#294 <https://github.com/LCAS/kiss-icp/issues/294>`_)
  * First stop. Remove default constructor
  Since we can't guarantee how the pipeline is going to be constructed at
  runtime is better to force the user to wrap it in a pointer type to
  avoid having a default-constructed object that "should" be modified
  later on
  * Second stop: make the only kiss_icp::pipeline::KissICP consumer use ptr
  This way we guarantee that it's constructed once the `config\_` has been
  properly populated
  * Last stop: rename "odometry\_" for "kiss_icp\_"
  * Remove unnecessary class member
  * format
  * Remove unnncesary duplicated call
  * Update utility function to accoomodate for empty timestamps
* Contributors: Ignacio Vizzo, Marc Hanheide, Tiziano Guadagnino

0.4.0 (2024-02-29)
------------------
* Nacho/remove ros 1 support (`#280 <https://github.com/LCAS/kiss-icp/issues/280>`_)
  * Initial cleanup
  * Add rolling to build
  * Fix styling
  * Update READMEs
  * Bump version
  * Update README.md
  * Wipe out last ROS 1 traces
  ---------
  Co-authored-by: Benedikt Mersch <benedikt.mersch@gmail.com>
* Contributors: Ignacio Vizzo

0.3.0 (2024-02-22)
------------------
* Nacho/re enable ipc (`#253 <https://github.com/LCAS/kiss-icp/issues/253>`_)
  * Add composable launch example
  * Use SensorDataQoS() as default to enable IPC
  * Change rviz configuration
  * Use `unique_ptr` to allow for true IPC
  * Move component registration to translation unit
  It's the same but seems to be a more common practice in ROS 2 codebases
  * Fix sytle
  * Delete unnecessary unique_ptrs after PR conversation
* Add support for multi-sensor scenarios (`#232 <https://github.com/LCAS/kiss-icp/issues/232>`_)
  * Fix TF tree usage in ROS 2 wrapper
  * Transform the pose instead of the pointcloud
  * remove include
  * Remove default base_frame parameter value
  This will make KISS-ICP work ego-centric as default
  * Remove unused variable
  * Do not reuse pose_msg.pose
  * I'm not ever sure why we did that in first instance
  * Be more explicit about the stamps and frame_id of the headers
  * Extract publishing mechanism to a new function (`#246 <https://github.com/LCAS/kiss-icp/issues/246>`_)
  * Convert class member function to more useful utility
  And fix a small bug, the order was of the transformation before was the
  opposite, and therefore we were obtaining base2cloud. Since we multiply
  by both sides we can't really see the difference, but it was
  conceptually wrong.
  * Bring back debugging clouds to ros driver
  * re-arange logic on when and when not to publish clouds
  * fix lofic
  * Update rviz2
  * Loosing my mind already with this debugging info
  * Backport tf multisensor fix (`#245 <https://github.com/LCAS/kiss-icp/issues/245>`_)
  * Build system changes for tf fix
  * Modify params for tf fix
  * Add ROS 1 tf fixes similar to ROS 2
  * Update rviz config
  * Remove unused debug publishers
  * Remove unnecessary smart pointers
  * Update ROS 1 to match ROS 2 changes
  * Fix style
  * Remove sophus from build system
  Fixing now the CI is a big pain
  * Remove unnecessary alias
  ---------
  Co-authored-by: Tim Player <tim@overland.ai>
  Co-authored-by: raw_t <37455909+tizianoGuadagnino@users.noreply.github.com>
  Co-authored-by: tizianoGuadagnino <frevo93@gmail.com>
* Bump version
* Style change (`#229 <https://github.com/LCAS/kiss-icp/issues/229>`_)
  Change quotes ("") for brackets (<>). Logic is unaffected
* add tf parameters to launch file (`#208 <https://github.com/LCAS/kiss-icp/issues/208>`_)
* Fix param declaration (`#199 <https://github.com/LCAS/kiss-icp/issues/199>`_)
* fix: typo (`#196 <https://github.com/LCAS/kiss-icp/issues/196>`_)
* Tiziano/normalize timestamps (`#193 <https://github.com/LCAS/kiss-icp/issues/193>`_)
  * Add min-max normalization on the ROS side
  * Same timestamp normalization on the python side
  * Fix SB
* Add options to toggle odom and alias tf (continued from `#92 <https://github.com/LCAS/kiss-icp/issues/92>`_) (`#149 <https://github.com/LCAS/kiss-icp/issues/149>`_)
  * Add options to toggle odom and alias publishing to avoid tf conflicts from other sources
  * add default params to launch file
  * Whitespace
  * Change name and make publish_alias_tf\_ also a class member
  * Implement for ROS 2
  ---------
  Co-authored-by: Will Baker <william+gitlab@polymathrobotics.com>
  Co-authored-by: Ignacio Vizzo <ignaciovizzo@gmail.com>
* Account for multiple timestamp datatypes for PointCloud2 messages (`#169 <https://github.com/LCAS/kiss-icp/issues/169>`_)
  * Add first draft for the fix
  * Use switch-case instead
  * Try templated lambda
  * Cannot do this trick with the switch case (cross initialization
  problem), if-else-if works cause we have different scopes
  * Fix normalization and some styling agreements
  * backport to ROS2
  * Drop melodic support
  EOL since a while now
  ---------
  Co-authored-by: tizianoGuadagnino <frevo93@gmail.com>
* Nacho/sync ros wrappers (`#188 <https://github.com/LCAS/kiss-icp/issues/188>`_)
  * Inline all util functions
  * Merge implementations (wip)
  * ROS 2 instead of ROS2
  * Sacrufice missuse of pointers for similar wrappers
  * Convert everything to pointers
  * Propagate use of pointers
  I hate this
  * Consisten with ROS 1
* Enable zero-copy (`#171 <https://github.com/LCAS/kiss-icp/issues/171>`_)
  * Enable zero-copy
  * Precommit fix
  * Workaround for intra-process support of StaticTransformBroadcaster
  * Drop ROS 2 Foxy support, add Iron instead
  * Shorten code by using declarations
  * Don't explicitly return rvalue reference
  Turns out not to be necessary:
  - https://github.com/PRBonn/kiss-icp/pull/171#pullrequestreview-1527833342
  * Inline all utility functions
  ---------
  Co-authored-by: Ignacio Vizzo <ignaciovizzo@gmail.com>
* Contributors: Giacomo Franchini, Ignacio Vizzo, Maik, Patrick Roncagliolo, RyuYamamoto, Will Baker, raw_t, tizianoGuadagnino

0.2.10 (2023-07-05)
-------------------
* 179 pydantic settings broke kiss icp python due to its major version update to 201 (`#180 <https://github.com/LCAS/kiss-icp/issues/180>`_)
  * Reduce major version of pyadantic to be less pedantic
  * Bump version
* As ROS2 rclcpp Component [`#162 <https://github.com/LCAS/kiss-icp/issues/162>`_] (`#163 <https://github.com/LCAS/kiss-icp/issues/163>`_)
  * As rclcpp Component
  * Lint
  * Lint
  * Fixes
  * ConstSharedPtr cb
  * Lint
* Fix typo (`#160 <https://github.com/LCAS/kiss-icp/issues/160>`_)
* Contributors: Ignacio Vizzo, Patrick Roncagliolo

0.2.9 (2023-04-12)
------------------
* Bump version
* Contributors: Ignacio Vizzo

0.2.8 (2023-04-11)
------------------
* Bump version
* Nacho/hot fix pipeline (`#136 <https://github.com/LCAS/kiss-icp/issues/136>`_)
* Contributors: Ignacio Vizzo

0.2.6 (2023-04-07)
------------------
* Bump version
  Improved rosbag support
* Contributors: Ignacio Vizzo

0.2.5 (2023-04-06)
------------------
* Fix macOS python wheels
* Bump version
* Nacho/cleanup 3rdparty cmake (`#129 <https://github.com/LCAS/kiss-icp/issues/129>`_)
  * Cleanup Sophus.cmake build script
  * Cleanup eigen target
  We now run cmake and check the compiler actually supports eigen. Before
  it was a raw copy-paste of the code
  * Attempt to improve the cmake usage
  * add tsl to the same idea
  * Fix lol
  * Simplify
  * typo
  * Use own fork again
  * cleanup script
  * Almost there with sophus
  * Fix sophus target
  * Bump min required cmake version
  This is to make sure that FetchContent_Declare has the SYSTEM flag
  avaialbe. This improves the superbuild usage in general
  * Bump bit more the cmake min requirement
  * Be less strict for developers who actually have installed the
  dependencies
  * Bump cmake version in CI
  * Ignore this
  * Attempt to fix windows build
  * ROS2 now also requires to have cmake 3.25
  This is the main disadvantage of this whole change
  * tbb release mode to fix windows build
* More robust detection of ROS 1 vs ROS 2 (`#107 <https://github.com/LCAS/kiss-icp/issues/107>`_)
  * add .vscode to ignore files
  * FIX: Allow using colcon to build for ROS 1
  * Add ros_environment dependency to expose ROS_VERSION env var in build farms
  ---------
  Co-authored-by: Ignacio Vizzo <ignaciovizzo@gmail.com>
* Add black and clang-format style checks + pre-commit config (`#102 <https://github.com/LCAS/kiss-icp/issues/102>`_)
  * Remove deployment stage from gitlab
  * Add clang-format check
  * pre-commit trailing whitespace and eol
  * Add pre-commit hooks
  * Add black formatter
  * Change name of the job
* Contributors: Ignacio Vizzo, Jose Luis Blanco-Claraco

0.2.3 (2023-03-26)
------------------
* Bump version
* Add launch to install (`#88 <https://github.com/LCAS/kiss-icp/issues/88>`_)
  When using install space instead of devel you must mark launch files to be installed else there will be no launch files found when trying to launch the package.
  http://docs.ros.org/en/jade/api/catkin/html/howto/format2/installing_other.html
* fix: add missing condition in package.xml (`#84 <https://github.com/LCAS/kiss-icp/issues/84>`_)
  * fix: add missing condition in package.xml
  * address review
  ---------
* Relax the cmake_minimum_version for dev builds
* Nacho/update cmake requirement (`#80 <https://github.com/LCAS/kiss-icp/issues/80>`_)
  * Fix out-of-tree builds
  At least this fails!
  * Update README
  * Update
* Contributors: Daisuke Nishimatsu, Ignacio Vizzo, Will Baker

0.2.2 (2023-02-23 17:57)
------------------------
* Improve rosbag ROS1 and ROS2 readers
  Some small styling mistakes + guess ros2 bagfile topic
* Fix ROS2 foxy build and add it to the CI/CD. Closes `#76 <https://github.com/LCAS/kiss-icp/issues/76>`_ (`#77 <https://github.com/LCAS/kiss-icp/issues/77>`_)
* Update rviz config
* Contributors: Ignacio Vizzo

0.2.1 (2023-02-23 12:03)
------------------------
* Minor fix on standalone folders
* Contributors: tizianoGuadagnino

0.2.0 (2023-02-23 11:54)
------------------------
* Merge pull request `#74 <https://github.com/LCAS/kiss-icp/issues/74>`_ from PRBonn/nacho/tweaks_ros2_node
  Add ROS2 support
* Improve (a bit) README
* Massive refactoring of the entire project.
  Thanks ROS2 for complicating stuff like this :)
* Contributors: Ignacio Vizzo, raw_t

0.1.3 (2023-02-17)
------------------

0.1.2 (2023-01-26)
------------------

0.1.1 (2023-01-24)
------------------

0.1.0 (2023-01-19)
------------------

0.0.14 (2023-01-13)
-------------------

0.0.13 (2023-01-11)
-------------------

0.0.7 (2022-10-14)
------------------

0.0.6 (2022-10-04)
------------------

0.0.5 (2022-09-30)
------------------
