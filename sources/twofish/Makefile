OS=$(shell uname -s)
MACHINE=$(shell uname -m)
MACHINE_STD=$(patsubst i%86,x86,$(MACHINE))
ifeq ($(OS),Linux)
	LIBEXT=so
endif
ifeq ($(OS),Darwin)
	LIBEXT=dylib
endif

TCLINCLUDEFLAG=$(shell grep 'TCL_INCLUDE_SPEC' /usr/lib/tclConfig.sh | cut -d= -f2 )
TCLSTUBLIBFLAG=$(shell grep 'TCL_STUB_LIB_FLAG' /usr/lib/tclConfig.sh | cut -d= -f2 )
CFLAGS+=-Wall -O1

.PHONY: all
all: libtwofish-$(OS)-$(MACHINE_STD).$(LIBEXT)
libtwofish-$(OS)-$(MACHINE_STD).$(LIBEXT): twofish.c
	gcc $(CFLAGS) -shared -fPIC -o $@ -DUSE_TCL_STUBS $(TCLINCLUDEFLAG) $(TCLSTUBLIBFLAG) $<

.PHONY: clean
clean:
	rm -f libtwofish-$(OS)-$(MACHINE_STD).$(LIBEXT)
