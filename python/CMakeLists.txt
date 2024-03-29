# Copyright 2011 Free Software Foundation, Inc.
#
# This file is part of GNU Radio
#
# GNU Radio is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3, or (at your option)
# any later version.
#
# GNU Radio is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with GNU Radio; see the file COPYING.  If not, write to
# the Free Software Foundation, Inc., 51 Franklin Street,
# Boston, MA 02110-1301, USA.

########################################################################
# Include python install macros
########################################################################
include(GrPython)
if(NOT PYTHONINTERP_FOUND)
    return()
endif()

########################################################################
# Install python sources
########################################################################
GR_PYTHON_INSTALL(
    FILES
    __init__.py
    lora_receiver.py
    lorasocket.py
    loraconfig.py DESTINATION ${GR_PYTHON_DIR}/lora
)

if(HAS_MONGODB)
    GR_PYTHON_INSTALL(
        FILES
        message_mongodb_sink.py DESTINATION ${GR_PYTHON_DIR}/lora
    )
endif(HAS_MONGODB)

########################################################################
# Handle the unit tests
########################################################################
include(GrTest)


#让CMake知道qa_receiver这个测试的存在，要修改Python文件夹下的CMakeLists.txt.
set(GR_TEST_TARGET_DEPS gnuradio-lora)
set(GR_TEST_PYTHON_DIRS ${CMAKE_BINARY_DIR}/swig)
GR_ADD_TEST(qa_receiver ${PYTHON_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/qa_receiver.py)
