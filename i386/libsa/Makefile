
DIR = libsa
include ../MakePaths.dir

UTILDIR = ../util
LIBSAIODIR = ../libsaio
INSTALL_SA_DIR = $(DSTROOT)/System/Library/Frameworks/System.framework/Versions/B/PrivateHeaders/standalone
INSTALL_MD_DIR = $(DSTROOT)/System/Library/Frameworks/System.framework/Versions/B/PrivateHeaders/machdep/i386

OPTIM = -Os -Oz
CFLAGS	= $(RC_CFLAGS) $(OPTIM) $(MORECPP)  -g -Wall -fno-stack-protector \
	      -fno-builtin -static $(OMIT_FRAME_POINTER_CFLAG) \
          -march=pentium4 -msse2 -msoft-float  -ffreestanding -DBOOT_CORE -mpreferred-stack-boundary=2 -fno-align-functions -mfpmath=sse -Werror
GFLAGS	= 
INC = -I. -I$(SYMROOT) -I$(UTILDIR) -I$(LIBSAIODIR)
ifneq "" "$(wildcard /bin/mkdirs)"
  MKDIRS = /bin/mkdirs
else
  MKDIRS = /bin/mkdir -p
endif
AS = as
LD = ld
# LIBS= -lc_static
LIBS=

VPATH = $(OBJROOT):$(SYMROOT)

SA_OBJS = __bzero.o ffs.o qdivrem.o umoddi3.o udivdi3.o divdi3.o moddi3.o printf.o \
	string.o strtol.o \
	setjmp.o qsort.o efi_tables.o jemalloc.o sbrk.o ctype.o __printf.o    

SFILES = setjmp.s __bzero.s ffs.s
CFILES = qdivrem.c umoddi3.c udivdi3.c divdi3.c moddi3.c printf.c zalloc.c \
	string.c strtol.c \
	qsort.c efi_tables.c sbrk.c ctype.c __printf.c

HFILES = memory.h
EXPORTED_HFILES = libsa.h memory.h
INSTALLED_SA_HFILES = libsa.h
OTHERFILES = Makefile
ALLSRC =  $(SFILES) $(CFILES) $(HFILES) $(OTHERFILES)
LIBS = libsa.a
DIRS_NEEDED = $(OBJROOT) $(SYMROOT)

CFLAGS += -DSAFE_MALLOC #if zalloc

HFILES = memory.h
EXPORTED_HFILES = libsa.h memory.h
INSTALLED_SA_HFILES = libsa.h
OTHERFILES = Makefile
ALLSRC =  $(SFILES) $(CFILES) $(HFILES) $(OTHERFILES)
LIBS = libsa.a
DIRS_NEEDED = $(OBJROOT) $(SYMROOT)

CFLAGS += -DSAFE_MALLOC

all embedtheme: $(DIRS_NEEDED) $(LIBS)

libsa.a: $(SA_OBJS)
	rm -f $(SYMROOT)/$(@F)
	ar q $(SYMROOT)/$(@F) $^
	ranlib $(SYMROOT)/$(@F)

$(INSTALL_SA_DIR) $(INSTALL_MD_DIR):
	$(MKDIRS) $@

installhdrs:: $(INSTALL_SA_DIR) $(INSTALL_MD_DIR)
	cp $(INSTALLED_SA_HFILES) $(INSTALL_SA_DIR)

include ../MakeInc.dir

# dependencies
-include $(OBJROOT)/Makedep
