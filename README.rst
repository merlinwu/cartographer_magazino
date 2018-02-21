.. Copyright 2016 The Cartographer Authors
             2018 Magazino GmbH

.. Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

..      http://www.apache.org/licenses/LICENSE-2.0

.. Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.

================================================
Cartographer ROS for Magazino Robotics Platforms
================================================

Purpose
=======

`Cartographer`_ is a system that provides real-time simultaneous localization
and mapping (`SLAM`_) in 2D and 3D across multiple platforms and sensor
configurations. This repository provides Cartographer SLAM for `Magazino
Robotics`_ platforms via `Cartographer ROS`_. This is a simplified integration
for testing and evaluation purposes only.

.. _Cartographer: https://github.com/googlecartographer/cartographer
.. _Cartographer ROS: https://github.com/googlecartographer/cartographer_ros
.. _SLAM: https://en.wikipedia.org/wiki/Simultaneous_localization_and_mapping
.. _Magazino Robotics: https://www.magazino.eu/?lang=en

Documentation
=============

We currently support bagfiles recorded on Magazino TORU robots. Support for
other platforms like SOTO may be added in the future.

TORU
====

Run the simulation demo (mapping) with the hallway dataset:

.. code-block:: bash

  cd data  # (where you stored the bagfiles)
  roslaunch cartographer_toru demo_toru_simulation.launch bag_filename:=$(pwd)/hallway_return.bag playback_rate:=2

Use the ``write_state`` ROS service to serialize the state to a ``.pbstream`` file:

.. code-block:: bash

  rosservice call /write_state "filename: 'hallway_return.pbstream'"

Run the localization demo:

.. code-block:: bash

  roslaunch cartographer_toru demo_toru_localization.launch map_filename:=$(pwd)/hallway_return.pbstream bag_filename:=$(pwd)/hallway_localization.bag

Run the offline node:

.. code-block:: bash

  roslaunch cartographer_toru offline_toru_2d.launch bag_filenames:=$(pwd)/hallway_return.bag

The offline node uses a lower grid resolution by default (see ``toru.lua``).