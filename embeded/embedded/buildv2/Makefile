#******************************************************************************
#*                                                                            *
#* This program is distributed in the hope that it will be useful, but        *
#* WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY *
#* or FITNESS FOR A PARTICULAR PURPOSE. This file and program are licensed    *
#* under the GNU Lesser General Public License Version 3, 29 June 2007.       *
#* The complete license can be accessed from the following location:          *
#* http://opensource.org/licenses/lgpl-3.0.html                               *
#*                                                                            *
#* Author: Yun Li (yunli.open@gmail.com)                                      *
#*   Date: 05/22/2010                                                         *
#*                                                                            *
#******************************************************************************

#******************************************************************************
# REVISION HISTORY
# ================
# 
# Date     Version  Name          Description
# -------- -------  ------------  --------------------------------------------
#
# -------- -------  ------------  --------------------------------------------
#
#******************************************************************************
 
ROOT = $(realpath ..)
BUILD = $(realpath .)

COMMON_DIRS = \
    $(ROOT)/code/tools/err2str \
    $(ROOT)/code/platform/common/src \
    $(ROOT)/code/platform/arch/x86/simulator/src \
    $(ROOT)/code/platform/driver/ctrlc/src \
    $(ROOT)/code/platform/driver/flash/share/src \
    $(ROOT)/code/platform/driver/flash/39vf040/src \
    $(ROOT)/code/platform/board/simulator/src \
    $(ROOT)/code/platform/memory/v1/src \
    $(ROOT)/code/platform/memory/v2/src \
    $(ROOT)/code/platform/memory/v3/src \
    $(ROOT)/code/platform/timer/v1/src \
    $(ROOT)/code/platform/timer/v2/src \
    $(ROOT)/code/platform/timer/v3/src \
    $(ROOT)/code/platform/timer/v4/src \
    $(ROOT)/code/platform/task/v1/src \
    $(ROOT)/code/platform/task/v2/src \
    $(ROOT)/code/platform/task/v3/src \
    $(ROOT)/code/platform/sync/v1/src \
    $(ROOT)/code/platform/sync/v2/src \
    $(ROOT)/code/platform/sync/v3/src \
    $(ROOT)/code/platform/device/src \
    
NONUT_DIRS = \
    $(ROOT)/code/application/stackframe \
    $(ROOT)/code/application/return \
    $(ROOT)/code/application/memory/heap/v1 \
    $(ROOT)/code/application/memory/heap/v2 \
    $(ROOT)/code/application/memory/heap/v3 \
    $(ROOT)/code/application/memory/mpool \
    $(ROOT)/code/application/timer/v1 \
    $(ROOT)/code/application/timer/v2 \
    $(ROOT)/code/application/timer/v3 \
    $(ROOT)/code/application/timer/v4 \
    $(ROOT)/code/application/module \
    $(ROOT)/code/application/task/v1 \
    $(ROOT)/code/application/task/v2 \
    $(ROOT)/code/application/sync/semaphore \
    $(ROOT)/code/application/sync/mutex \
    $(ROOT)/code/application/sync/event \
    $(ROOT)/code/application/sync/prioinv \
    $(ROOT)/code/application/sync/prioinh \
    $(ROOT)/code/application/sync/queue \
    $(ROOT)/code/application/sync/deadlock \
    $(ROOT)/code/application/sync/recursive \
    
UT_DIRS = \
    $(ROOT)/tests/platform/common \
    $(ROOT)/tests/platform/task \

MAKE_DIRS := $(COMMON_DIRS)

ifeq ("$(MAKECMDGOALS)", "")
MAKECMDGOALS = release
endif

ifeq ("$(MAKECMDGOALS)", "release")
MAKE_DIRS += $(NONUT_DIRS)
endif
ifeq ("$(MAKECMDGOALS)", "debug")
MAKE_DIRS += $(NONUT_DIRS)
endif
ifeq ("$(MAKECMDGOALS)", "unitest")
MAKE_DIRS += $(UT_DIRS)
endif
ifeq ("$(MAKECMDGOALS)", "clean")
MAKE_DIRS += $(NONUT_DIRS) $(UT_DIRS)
endif

RM = rm
RMFLAGS = -fr
RMS = release debug unitest

DIR_UNITEST = unitest

.PHONY: release debug clean touch unitest test force
release debug clean unitest:
	@set -e; \
	for DIR in $(MAKE_DIRS); \
	do \
		cd $$DIR && $(MAKE) -r ROOT=$(ROOT) BUILD=$(BUILD) $@;\
	done
	@set -e; \
	if [ "$(MAKECMDGOALS)" = "clean" ] ; then $(RM) $(RMFLAGS) $(RMS) ; fi; \
	if [ "$(MAKECMDGOALS)" = "unitest" ] ; then touch $(DIR_UNITEST)/unitested; fi
	@echo ""
	@echo ":-) Completed"
	@echo ""

UTS = $(wildcard $(DIR_UNITEST)/unitest_*.exe)

ifeq ("$(MAKECMDGOALS)", "test")
ifeq ("$(wildcard $(DIR_UNITEST)/unitested)", "")
$(error Did you forget to run 'make unitest'?)
endif
endif

$(DIR_UNITEST)/unitest_%: force 
	./$@
test: $(UTS)
	@touch $(DIR_UNITEST)/tested

force:

touch:
	@echo "Processing ..."
	@find $(ROOT) -exec touch {} \;
	@echo ""
	@echo ":-) Completed"
	@echo ""
