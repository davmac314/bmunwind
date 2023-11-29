CXXOBJS=libunwind.o
COBJS=UnwindLevel1.o UnwindLevel1-gcc-ext.o
SOBJS=UnwindRegistersSave.o UnwindRegistersRestore.o

# default, should be overridden:
OUTDIR=.

LIBUNWIND_CPPFLAGS ::= -I../include -D_LIBUNWIND_IS_BAREMETAL -D_LIBUNWIND_IS_NATIVE_ONLY -DNDEBUG \
         -D_LIBUNWIND_HAS_NO_THREADS -D_LIBUNWIND_NO_HEAP -D_LIBUNWIND_REMEMBER_STACK_ALLOC

all: $(CXXOBJS) $(COBJS) $(SOBJS)
	ar r $(OUTDIR)/libunwind.a $(CXXOBJS) $(COBJS) $(SOBJS)

$(CXXOBJS): %.o: %.cpp
	$(CXX) $(CXXPPFLAGS) $(LIBUNWIND_CPPFLAGS) $(CXXFLAGS) -c $< -o $@

# Note that _Unwind_RaiseException must be built with unwind tables (-funwind-tables)
$(COBJS): %.o: %.c
	$(CC) $(CPPFLAGS) $(LIBUNWIND_CPPFLAGS) $(CFLAGS) -funwind-tables -c $< -o $@
	
$(SOBJS): %.o: %.S
	$(CC) $(CPPFLAGS) $(LIBUNWIND_CPPFLAGS) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(COBJS) $(CXXOBJS) $(SOBJS)
