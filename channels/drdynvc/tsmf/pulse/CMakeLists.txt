# FreeRDP: A Remote Desktop Protocol Client
# FreeRDP cmake build script
#
# Copyright 2011 O.S. Systems Software Ltda.
# Copyright 2011 Otavio Salvador <otavio@ossystems.com.br>
# Copyright 2011 Marc-Andre Moreau <marcandre.moreau@gmail.com>
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

set(TSMF_PULSE_SRCS
	tsmf_pulse.c)

include_directories(..)
include_directories(${PULSEAUDIO_INCLUDE_DIR})

add_library(tsmf_pulse ${TSMF_PULSE_SRCS})
set_target_properties(tsmf_pulse PROPERTIES PREFIX "")

if(WITH_MONOLITHIC_BUILD)
	target_link_libraries(tsmf_pulse ${PULSEAUDIO_LIBRARY} freerdp)
else()
	target_link_libraries(tsmf_pulse ${PULSEAUDIO_LIBRARY} freerdp-utils)
endif()

install(TARGETS tsmf_pulse DESTINATION ${FREERDP_PLUGIN_PATH})

