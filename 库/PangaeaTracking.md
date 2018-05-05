# PangaeaTracking

This is the implementation of the following ICCV2015 paper:

    Direct, Dense, and Deformable: Template-Based Non-Rigid 3D Reconstruction from RGB Video
    Rui Yu, Chris Russell, Neill D. F. Campbell, Lourdes Agapito

For more information about this work, please visit the [project website](http://www0.cs.ucl.ac.uk/staff/R.Yu/direct_nrsfm/direct_nrsfm.html).

This github repository is maintained by Rui Yu (R.Yu@cs.ucl.ac.uk).
Contact me if you have any questions.

# 1. Building the System

### 1.1 Requirements

PangaeaTracking has been tested in Ubuntu 14.04 only. Several 3rd party libraries are needed for compiling PangaeaTracking.

  - OpenGL / GLU / GLEW / X11 / TBB / LMDB / HDF5
```
   sudo apt-get install libgl1-mesa-dev
   sudo apt-get install libglu1-mesa-dev
   sudo apt install freeglut3-dev
   sudo apt-get install libglew-dev  libglew2.0  #libglew1.8 
   sudo apt-get install libx11-dev
   sudo apt-get install libtbb-dev
   sudo apt-get install liblmdb-dev
   sudo apt-get install libhdf5-serial-dev
```
  - OPENCV (e.g. version 2.4.8 or later)
    available at http://opencv.org/

  - Ceres Solver
    available at http://ceres-solver.org/

  - wxWidgets
    available at https://www.wxwidgets.org/

  - Boost
    available at http://www.boost.org/

### 1.2 Build Process

  To compile the system, do the following:

```
  ./build.sh
```
https://www.cnblogs.com/zhming26/p/6164131.html


export LIBRARY_PATH=/usr/lib/x86_64-linux-gnu/:$LIBRARY_PATH




# enable pretty build (comment to see full commands)
Q ?= @

# Set DEBUG to 1 for debugging
#DEBUG := 1

# if only want to visualize saving results and don't do tracking,
# you could set VIS_ONLY to 1 and compile without ceres solver,
# but eigen3 is still needed.
# VIS_ONLY := 1

ifeq ($(DEBUG), 1)
	BUILD_DIR := build_debug
else
	BUILD_DIR := build
endif

VIS_ONLY ?= 0
ifeq ($(VIS_ONLY), 1)
	BUILD_DIR := $(BUILD_DIR)/PangaeaVis
else
	BUILD_DIR := $(BUILD_DIR)/PangaeaTracking
endif

LIB_BUILD_DIR := $(BUILD_DIR)/lib
BIN_BUILD_DIR := $(BUILD_DIR)/bin

# All the directories containing code
# SRC_DIRS := src/main_engine
MAIN_DIRS := $(shell find src/main_engine -type d -exec bash -c "find {} -maxdepth 1 \
	\( -name '*.cpp' \) | grep -q ." \; -print)
GUI_DIRS := $(shell find src/gui_app -type d -exec bash -c "find {} -maxdepth 1 \
	\( -name '*.cpp' \) | grep -q ." \; -print)
SRC_DIRS := $(MAIN_DIRS) $(GUI_DIRS)

ALL_BUILD_DIRS := $(addprefix $(BUILD_DIR)/, $(SRC_DIRS))
ALL_BUILD_DIRS += $(LIB_BUILD_DIR)

EIGEN_INCLUDE := -I/usr/include/eigen3/unsupported -I/usr/include/eigen3

WX_INCLUDE := `wx-config --cxxflags`

FLAGS_INCLUDE := $(EIGEN_INCLUDE) $(WX_INCLUDE) -I./include -I./include/third_party -I /usr/include/hdf5/serial

# Library dependencies
GL_LIB := -lGL -lGLU -lX11 -lGLEW

WX_LIB := `wx-config --libs --gl-libs`

BOOST_LIB := -lboost_filesystem -lboost_system -lboost_thread

OPENCV_LIB := -lopencv_core -lopencv_highgui -lopencv_imgproc -lopencv_imgcodecs

CERES_LIB := -lceres -lglog -ltbb -ltbbmalloc -lcholmod -lccolamd \
	-lcamd -lcolamd -lamd -lsuitesparseconfig -llapack -lf77blas -latlas

LMDB_LIB := -llmdb

HDF5_LIB := -lhdf5_serial_hl -lhdf5_serial

LIBRARY_DIRS += $(LIB_BUILD_DIR)
LDFLAGS := $(WX_LIB) $(BOOST_LIB) $(OPENCV_LIB) $(CERES_LIB) $(GL_LIB) $(LMDB_LIB) $(HDF5_LIB)
LDFLAGS += $(foreach library_dir, $(LIBRARY_DIRS), -L$(library_dir))

# Setting compiler and building flags
CXX := g++
#CXXFLAGS += -std=c++11 -fopenmp -fPIC $(FLAGS_INCLUDE)
CXXFLAGS += -std=c++11 -fopenmp $(FLAGS_INCLUDE) -w -fpermissive

# Debugging
ifeq ($(DEBUG), 1)
	CXXFLAGS += -DDEBUG -g -O0
#	CXXFLAGS += -DDEBUG -O
else
	CXXFLAGS += -DNDEBUG -O2 -ffast-math -Wno-unused-result
endif

# Automatic dependency generation
CXXFLAGS += -MMD -MP

# Disable offsetof macro warnings
CXXFLAGS += -Wno-invalid-offsetof

# Get all source files
MAIN_ENGINE_SRCS := $(shell find src/main_engine -name "*.cpp" ! -name "Deform*.cpp")
#MAIN_ENGINE_SRCS := $(shell find src/main_engine -name "*.cpp" )
GUI_SRCS := $(shell find src/gui_app -name "*.cpp" ! -name "PangaeaTracking.cpp")
GUI_APP_SRCS := $(shell find src/gui_app -name "PangaeaTracking.cpp")
CONSOLE_APP_SRCS := $(shell find src/console_app -name "PangaeaTracking_console.cpp")

CONSOLE_BIN := $(BIN_BUILD_DIR)/PangaeaTracking_console

ifeq ($(VIS_ONLY), 0)
	MAIN_ENGINE_SRCS += src/main_engine/tracker/DeformNRSFMTracker.cpp
	MAIN_LIB := $(LIB_BUILD_DIR)/libmain_engine.a
	GUI_BIN := $(BIN_BUILD_DIR)/PangaeaTracking
	LDFLAGS := -lmain_engine $(LDFLAGS)
else
	CXXFLAGS += -DVIS_ONLY
	MAIN_LIB := $(LIB_BUILD_DIR)/libmain_engine_vis.a
	GUI_BIN := $(BIN_BUILD_DIR)/PangaeaTracking_vis
	LDFLAGS := -lmain_engine_vis $(LDFLAGS)
endif

# The objects corresponding to the source files
MAIN_OBJS := $(addprefix $(BUILD_DIR)/, ${MAIN_ENGINE_SRCS:.cpp=.o})
GUI_OBJS := $(addprefix $(BUILD_DIR)/, ${GUI_SRCS:.cpp=.o})

# Output files for automatic dependency generation
DEPS := $(MAIN_OBJS:.o=.d) $(GUI_OBJS:.o=.d)

ifeq ($(VIS_ONLY), 1)
	APP := $(GUI_BIN)
else
	APP := $(CONSOLE_BIN) $(GUI_BIN)
endif

#ORIGIN := \$$ORIGIN
#.PHONY:

.PHONY: all

all: $(APP)

$(CONSOLE_BIN): $(MAIN_LIB) | $(BIN_BUILD_DIR)
	@ echo CXX/LD -o $@
	$(Q) $(CXX) $(CONSOLE_APP_SRCS) -o $@ $(CXXFLAGS) $(LINKFLAGS) $(LDFLAGS)

$(GUI_BIN): $(GUI_OBJS) $(MAIN_LIB) | $(BIN_BUILD_DIR)
#	@ echo $(MAIN_ENGINE_SRCS)
#	@ echo $(MAIN_OBJS)
	@ echo CXX/LD -o $@
	$(Q) $(CXX) $(GUI_APP_SRCS) -o $@ $(GUI_OBJS) $(CXXFLAGS) $(LINKFLAGS) $(LDFLAGS)

# $(CXX) $(GUI_APP_SRCS) $(CXXFLAGS) -o $@ $(GUI_OBJS) $(LINKFLAGS) $(WX_PATH) $(LIBS_LINKER) -L./build/lib -Wl,-rpath,$(ORIGIN)/../lib -lmain_engine_vis
# $(CXX) $(GUI_APP_SRCS) $(CXXFLAGS) -o $@ $(GUI_OBJS) -lmain_engine_vis $(LINKFLAGS) $(LDFLAGS)
# $(Q)$(CXX) $< -o $@ $(LINKFLAGS) $(LDFLAGS) \
# -Wl,-rpath, -lmain_engine_vis

#@ echo AR -o $@
#$(Q)ar rcs $@ $(MAIN_OBJS)
#@ echo $(MAIN_OBJS)

$(MAIN_LIB): $(MAIN_OBJS) | $(LIB_BUILD_DIR)
	@ echo AR -o $@
	$(Q)ar rcs $@ $(MAIN_OBJS)
#	@ echo $(MAIN_OBJS)
#	@ echo LD -o $@
#	$(Q)$(CXX) -shared -o $@ $(MAIN_OBJS) $(LINKFLAGS) $(LDFLAGS)
#	$(Q)$(CXX) -o $@ $(MAIN_OBJS) $(LINKFLAGS) $(LDFLAGS)

# Define build targets
$(BUILD_DIR)/%.o: %.cpp | $(ALL_BUILD_DIRS)
	@ echo CXX $<
	$(Q)$(CXX) $< $(CXXFLAGS) -c -o $@

$(ALL_BUILD_DIRS):
	@ mkdir -p $@

$(BIN_BUILD_DIR):
	@ mkdir -p $@

-include $(DEPS)




# 2. Data

One example sequence is available at [google drive](https://drive.google.com/drive/folders/0B8-9V4y1N7pxZExaMlE3bnc3Mzg).
Download the data and unzip data/Yiwan/yiwan.tar.

# 3. Examples

After building PangaeaTracking and preparing the data, you are ready to run the scripts in examples folder.
Check examples/Yiwan.sh for usage.

# 4. GUI Usage

For rotating the 3d model in 2d image plane, use the middle mouse button.

------
