# Standalone Makefile for OakScrpt (no CModule include)

CC        = cc
CMHG      = cmhg
LINK      = link

TARGET    = <OakScript$Dir>.OakScript

# Objects
OBJS      = o.module o.header o.engine o.core o.memory o.variables o.string o.math o.swi o.debug o.compile o.runtime

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

o.string: c.string h.string
	$(CC) $(CFLAGS) c.string -o o.string

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

clean:
	-wipe o.* ~C~V
	-wipe $(TARGET) ~C~V

install: $(TARGET)
	copy $(TARGET) rm.$(TARGET) ~C~V~N

# Dynamic dependencies:

o.engine:	c.engine
o.engine:	C:h.kernel
o.engine:	h.memory
o.engine:	h.engine
o.memory:	c.memory
o.memory:	C:h.kernel
o.memory:	C:h.swis
o.memory:	h.memory
o.variables:	c.variables
o.variables:	h.memory
o.variables:	h.engine
o.variables:	h.variables
o.variables:	h.engine
o.string:	c.string
o.string:	h.string
o.string:	h.memory
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
o.core:	c.script
o.core:	C:h.kernel
o.core:	h.memory
o.core:	h.engine
o.core:	h.variables
o.core:	h.engine
o.core:	h.string
o.core:	h.math
o.core:	h.swi
o.core:	C:h.kernel
o.core:	h.engine
o.core:	h.debug
o.module:	c.module
o.module:	C:h.kernel
o.module:	C:h.swis
o.module:	h.header
o.module:	h.memory
o.module:	h.compile
o.module:	h.runtime
o.module:	h.compile
o.compile:	c.compile
o.compile:	C:h.kernel
o.compile:	C:h.swis
o.compile:	h.compile
o.compile:	h.engine
o.compile:	h.memory
o.runtime:	c.runtime
o.runtime:	h.runtime
o.runtime:	h.compile
o.runtime:	h.memory
