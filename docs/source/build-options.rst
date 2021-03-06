.. Copyright (c) 2016, Johan Mabille, Sylvain Corlay and Wolf Vollprecht

   Distributed under the terms of the BSD 3-Clause License.

   The full license is in the file LICENSE, distributed with this software.

Build and configuration
=======================

Build
-----

``xtensor`` build supports the following options:

- ``BUILD_TESTS``: enables the ``xtest`` and ``xbenchmark`` targets (see below).
- ``DOWNLOAD_GTEST``: downloads ``gtest`` and builds it locally instead of using a binary installation.
- ``GTEST_SRC_DIR``: indicates where to find the ``gtest`` sources instead of downloading them.
- ``XTENSOR_ENABLE_ASSERT``: activates the assertions in ``xtensor``.
- ``XTENSOR_CHECK_DIMENSION``: turns on ``XTENSOR_ENABLE_ASSERT`` and activates dimension checks in ``xtensor``.
  Note that the dimensions check should not be activated if you expect ``operator()`` to perform broadcasting.
- ``XTENSOR_USE_XSIMD``: enables simd acceleration in ``xtensor``. This requires that you have xsimd_ installed
  on your system.

All these options are disabled by default. Enabling ``DOWNLOAD_GTEST`` or
setting ``GTEST_SRC_DIR`` enables ``BUILD_TESTS``.

If the ``BUILD_TESTS`` option is enabled, the following targets are available:

- xtest: builds an run the test suite.
- xbenchmark: builds and runs the benchmarks.

For instance, building the test suite of ``xtensor`` with assertions enabled:

.. code::

    mkdir build
    cd build
    cmake -DBUILD_TESTS=ON -DXTENSOR_ENABLE_ASSERT=ON ../
    make xtest

Building the test suite of ``xtensor`` where the sources of ``gtest`` are
located in e.g. ``/usr/share/gtest``:

.. code::

    mkdir build
    cd build
    cmake -DGTEST_SRC_DIR=/usr/share/gtest ../
    make xtest

.. _configuration-label:

Configuration
-------------

``xtensor`` can be configured via macros, which must be defined *before*
including any of its header. Here is a list of available macros:

- ``XTENSOR_ENABLE_ASSERT``: enables assertions in xtensor, such as bound check.
- ``XTENSOR_ENABLE_CHECK_DIMENSION``: enables the dimensions check in ``xtensor``. Note that this option should not be turned
  on if you expect ``operator()`` to perform broadcasting.
- ``XTENSOR_USE_XSIMD``: enables SIMD acceleration in ``xtensor``. This requires that you have xsimd_ installed
  on your system.
- ``XTENSOR_DEFAULT_DATA_CONTAINER(T, A)``: defines the type used as the default data container for tensors and arrays. ``T``
  is the ``value_type`` of the container and ``A`` its ``allocator_type``.
- ``XTENSOR_DEFAULT_SHAPE_CONTAINER(T, EA, SA)``: defines the type used as the default shape container for tensors and arrays.
  ``T`` is the ``value_type`` of the data container, ``EA`` its ``allocator_type``, and ``SA`` is the ``allocator_type``
  of the shape container.
- ``XTENSOR_DEFAULT_LAYOUT``: defines the default layout (row_major, column_major, dynamic) for tensors and arrays. We *strongly*
  discourage using this macro, which is provided for testing purpose. Prefer defining alias types on tensor and array
  containers instead.

.. _xsimd: https://github.com/QuantStack/xsimd
