#  Copyright (C) 2011 University of Southern California
#                     and Andrew D. Smith
#
#  Authors: Andrew D. Smith
# 
#  This is free software; you can redistribute it and/or modify
#  it under the terms of the GNU General Public License as published by
#  the Free Software Foundation; either version 2 of the License, or
#  (at your option) any later version.
# 
#  This software is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU General Public License for more details.
# 
#  You should have received a copy of the GNU General Public License
#  along with this software; if not, write to the Free Software
#  Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA
#  02110-1301 USA
#

ifndef SRC_ROOT
SRC_ROOT=../..
endif

ifndef SMITHLAB_CPP
$(error SMITHLAB_CPP variable undefined)
endif

PROGS = lc_approx fastLiftOver

COMMON_DIR = $(SRC_ROOT)/src/common
INCLUDEDIRS =  $(SMITHLAB_CPP) $(COMMON_DIR)
INCLUDEARGS = $(addprefix -I,$(INCLUDEDIRS))

LIBS = -lgsl -lgslcblas 

CXX = g++
CFLAGS = -Wall -fmessage-length=50
CXXFLAGS = -Wall -fmessage-length=50
OPTFLAGS = -O2
DEBUGFLAGS = -g

ifdef DEBUG
CXXFLAGS += $(DEBUGFLAGS)
endif

ifdef OPT
CXXFLAGS += $(OPTFLAGS)
endif

all: $(PROGS)

install: $(PROGS)
	@mkdir -p $(SRC_ROOT)/bin
	@install -m 755 $(PROGS) $(SRC_ROOT)/bin

lc_approx: $(addprefix $(SMITHLAB_CPP)/, \
	OptionParser.o smithlab_os.o smithlab_utils.o GenomicRegion.o) 

fastLiftOver: $(addprefix $(SMITHLAB_CPP)/, \
	OptionParser.o smithlab_os.o smithlab_utils.o GenomicRegion.o) \
	$(addprefix $(COMMON_DIR)/, MethpipeFiles.o)

%.o: %.cpp %.hpp
	$(CXX) $(CXXFLAGS) -c -o $@ $< $(INCLUDEARGS)

%: %.cpp
	$(CXX) $(CXXFLAGS) -o $@ $^ $(INCLUDEARGS) $(LIBS)

clean:
	@-rm -f $(PROGS) *.o *.so *.a *~

.PHONY: clean