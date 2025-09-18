# Standalone Makefile for OakScrpt (no CModule include)

CC        = cc
CMHG      = cmhg
LINK      = link

TARGET    = <OakScript$Dir>.OakScript

# Objects
OBJS      = o.module o.header o.engine o.core o.memory o.variables o.math o.swi o.debug o.compile o.runtime o.value o.advanced o.strings o.control_flow o.functional o.exceptions o.types o.bridge

# Libraries (stubs + kernel for RMA alloc/free)
LIBS      = C:o.stubs

# Compiler/CMHG flags
CFLAGS    = -c -depend !Depend -I,C: -apcs 3/32bit -Wcdp -throwback -fan
CMHGFLAGS = -depend !Depend -throwback

all: $(TARGET)

$(TARGET): $(OBJS)
	$(LINK) -rmf -o $(TARGET) $(OBJS) $(LIBS)

# CMHG: generate object and header (header needed by c.module)
o.header h.header: cmhg.header
	$(CMHG) $(CMHGFLAGS) cmhg.header -o o.header -d h.header

# Compile sources
o.module: c.module h.header
	$(CC) $(CFLAGS) c.module -o o.module

o.engine: c.engine h.engine
	$(CC) $(CFLAGS) c.engine -o o.engine

o.core: c.script h.engine
	$(CC) $(CFLAGS) c.script -o o.core

o.memory: c.memory
	$(CC) $(CFLAGS) c.memory -o o.memory

# New modular components
o.variables: c.variables h.variables h.engine h.memory
	$(CC) $(CFLAGS) c.variables -o o.variables



o.math: c.math h.math
	$(CC) $(CFLAGS) c.math -o o.math

o.swi: c.swi h.swi h.engine h.memory
	$(CC) $(CFLAGS) c.swi -o o.swi

o.debug: c.debug h.debug
	$(CC) $(CFLAGS) c.debug -o o.debug

o.compile: c.compile h.compile
	$(CC) $(CFLAGS) c.compile -o o.compile

o.runtime: c.runtime h.runtime h.compile
	$(CC) $(CFLAGS) c.runtime -o o.runtime

# Bridge dispatcher
o.bridge: c.bridge h.bridge h.memory h.strings
	$(CC) $(CFLAGS) c.bridge -o o.bridge

# Advanced language features
o.advanced: c.advanced h.advanced h.engine h.memory
	$(CC) $(CFLAGS) c.advanced -o o.advanced

o.strings: c.strings h.advanced h.engine h.memory h.strings
	$(CC) $(CFLAGS) c.strings -o o.strings

o.control_flow: c.control_flow h.advanced h.engine h.memory
	$(CC) $(CFLAGS) c.control_flow -o o.control_flow

o.functional: c.functional h.advanced h.engine h.memory
	$(CC) $(CFLAGS) c.functional -o o.functional

o.exceptions: c.exceptions h.advanced h.engine h.memory
	$(CC) $(CFLAGS) c.exceptions -o o.exceptions

o.value: c.value h.value h.memory
	$(CC) $(CFLAGS) c.value -o o.value

o.types: c.types h.advanced h.engine h.memory
	$(CC) $(CFLAGS) c.types -o o.types

clean:
	-wipe o.* ~C~V
	-wipe $(TARGET) ~C~V

install: $(TARGET)
	copy $(TARGET) rm.$(TARGET) ~C~V~N

# Dynamic dependencies:



o.memory:	c.memory
o.memory:	C:h.kernel
o.memory:	C:h.swis
o.memory:	h.memory
o.module:	c.module
o.module:	C:h.kernel
o.module:	C:h.swis
o.module:	h.header
o.module:	h.memory
o.module:	h.compile
o.module:	h.runtime
o.module:	h.compile
o.engine:	c.engine
o.engine:	C:h.kernel
o.engine:	h.memory
o.engine:	h.engine
o.core:	c.script
o.core:	C:h.kernel
o.core:	h.memory
o.core:	h.engine
o.core:	h.variables
o.core:	h.engine
o.core:	h.strings
o.core:	h.engine
o.core:	h.math
o.core:	h.swi
o.core:	C:h.kernel
o.core:	h.engine
o.core:	h.debug
o.core:	h.advanced
o.core:	h.engine
o.core:	h.memory
o.core:	h.value
o.core:	h.engine
o.core:	h.bridge
o.core:	h.memory
o.core:	h.strings
o.core:	h.runtime
o.core:	h.compile
o.core:	h.rt_objects
o.core:	h.bridge
o.variables:	c.variables
o.variables:	h.memory
o.variables:	h.engine
o.variables:	h.variables
o.variables:	h.engine
o.math:	c.math
o.math:	h.math
o.math:	h.engine
o.swi:	c.swi
o.swi:	C:h.kernel
o.swi:	h.memory
o.swi:	h.engine
o.swi:	h.swi
o.swi:	C:h.kernel
o.swi:	h.engine
o.swi:	h.debug
o.debug:	c.debug
o.debug:	h.debug
o.debug:	h.memory
o.debug:	h.engine
o.debug:	C:h.kernel
o.debug:	C:h.swis
o.compile:	c.compile
o.compile:	C:h.kernel
o.compile:	C:h.swis
o.compile:	h.compile
o.compile:	h.engine
o.compile:	h.memory
o.compile:	h.builtins
o.runtime:	c.runtime
o.runtime:	h.runtime
o.runtime:	h.compile
o.runtime:	h.memory
o.runtime:	h.strings
o.runtime:	h.engine
o.runtime:	h.bridge
o.runtime:	h.memory
o.runtime:	h.strings
o.runtime:	h.runtime
o.runtime:	h.rt_objects
o.runtime:	h.bridge
o.runtime:	h.engine
o.value:	c.value
o.value:	h.value
o.value:	h.engine
o.value:	h.memory
o.advanced:	c.advanced
o.advanced:	h.memory
o.advanced:	h.engine
o.advanced:	h.advanced
o.advanced:	h.engine
o.advanced:	h.memory
o.advanced:	h.value
o.advanced:	h.engine
o.strings:	c.strings
o.strings:	h.engine
o.strings:	h.memory
o.strings:	h.advanced
o.strings:	h.engine
o.strings:	h.memory
o.strings:	h.strings
o.strings:	h.engine
o.control_flow:	c.control_flow
o.control_flow:	h.advanced
o.control_flow:	h.engine
o.control_flow:	h.memory
o.control_flow:	h.memory
o.control_flow:	h.engine
o.functional:	c.functional
o.functional:	h.advanced
o.functional:	h.engine
o.functional:	h.memory
o.functional:	h.memory
o.functional:	h.engine
o.functional:	h.value
o.functional:	h.engine
o.exceptions:	c.exceptions
o.exceptions:	h.advanced
o.exceptions:	h.engine
o.exceptions:	h.memory
o.exceptions:	h.memory
o.exceptions:	h.engine
o.types:	c.types
o.types:	h.advanced
o.types:	h.engine
o.types:	h.memory
o.types:	h.memory
o.types:	h.engine
o.bridge:	c.bridge
o.bridge:	h.bridge
o.bridge:	h.memory
o.bridge:	h.strings
o.bridge:	h.engine
o.bridge:	h.runtime
o.bridge:	h.compile
o.bridge:	h.memory
o.bridge:	h.strings
o.bridge:	h.rt_objects
o.bridge:	h.bridge
o.bridge:	h.advanced
o.bridge:	h.engine
o.bridge:	h.memory
o.bridge:	h.builtins
