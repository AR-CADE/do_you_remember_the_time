
MODULE_NAME = CPUfreq
MODULE_VERSION = "1.0.0"
MODULE_COMPAT_VERSION = "1.0.0"
MODULE_START = _$(MODULE_NAME)_start
MODULE_DEPENDENCIES = 

BUNDLE_NAME = $(MODULE_NAME)
BUNDLE_EXEC = $(BUNDLE_NAME)
BUNDLE_LIBS = 
BUNDLE_INFO      = 
BUNDLE_ID      =  com.boot.CPU.CPU_ENV.cpufreq
BUNDLE_COPYRIGHT = Copyright 2010,2011 valv, cparm . All rights reserved.
BUNDLE_LICENCE   = 
BUNDLE_VERSION   = 0.1
BUNDLE_ICON      =
BUNDLE_SHORT_VERSION = 1
BUNDLE_CLASS = CPU_ENV
BUNDLE_CLASS_PROVIDER = CPU
DIR = CPUfreq

include ../../MakePaths.dir

OBJROOT=../../../obj/i386/modules/$(DIR)
SYMROOT=../../../sym/i386/modules/
DSTROOT=../../../dst/i386/modules/


UTILDIR = ../../util
LIBSADIR = ../../libsa
LIBSAIODIR = ../../libsaio
BOOT2DIR = ../../boot2
INCLUDE = ../include

INSTALLDIR = $(DSTROOT)/System/Library/Frameworks/System.framework/Versions/B/PrivateHeaders/standalone

OPTIM = -Os -Oz
DEBUG = -DNOTHING
CFLAGS	= $(RC_CFLAGS) $(OPTIM) $(MORECPP)  -g -Wall -fstack-protector-all \
    -D__ARCHITECTURE__=\"i386\"  \
    $(DEBUG) \
    -fno-builtin $(OMIT_FRAME_POINTER_CFLAG) \
    -mpreferred-stack-boundary=2 -fno-align-functions \
    -march=pentium4 -msse2 -mfpmath=sse -msoft-float -fno-common -msoft-float -mstackrealign

DEFINES=
CONFIG = hd
INC = -I. -I.. -I$(SYMROOT) -I$(UTILDIR) -I$(LIBSADIR) -I$(LIBSAIODIR) -I$(BOOT2DIR)
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

CPUfreq_OBJS = CPUfreq.o stack_protector.o


SFILES =
CFILES = 
HFILES = 
EXPORTED_HFILES =
INSTALLED_HFILES =
OTHERFILES = Makefile
ALLSRC =  $(SFILES) $(CFILES) \
	$(HFILES) $(OTHERFILES)
DIRS_NEEDED = $(OBJROOT) $(SYMROOT)

all embedtheme: ${CPUfreq_OBJS} bundle


bundle: 
	ld  \
	-undefined dynamic_lookup \
	-alias $(MODULE_START) start \
	-dylib -read_only_relocs suppress \
	-S -x -Z -dead_strip_dylibs \
	-no_uuid \
	-current_version $(MODULE_VERSION) -compatibility_version $(MODULE_COMPAT_VERSION) \
	-final_output $(MODULE_NAME) \
	-macosx_version_min 10.6 \
	$(OBJROOT)/stack_protector.o $(OBJROOT)/CPUfreq.o -o $(SYMROOT)/$(BUNDLE_EXEC)
	@rm -rf $(SYMROOT)/$(BUNDLE_NAME).bundle	
	@mkdir $(SYMROOT)/$(BUNDLE_NAME).bundle	
	@mkdir $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents	
	@mkdir $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/MacOS	
	@mkdir $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/Resources	
	@mkdir $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/PlugIns	
	@mv $(SYMROOT)/$(BUNDLE_EXEC) $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/MacOS	
	@#mv $(SYMROOT)/$(SYMBOLS_BUNDLE_LIBS) $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/PlugIns	
	
	@defaults write $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/Info "CFBundleGetInfoString" '$(BUNDLE_INFO)'	
	@defaults write $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/Info "NSHumanReadableCopyright" '$(BUNDLE_COPYRIGHT)'	
	@defaults write $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/Info "CFBundleShortVersionString" '$(BUNDLE_SHORT_VERSION)'	
	@defaults write $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/Info "CFBundleIconFile" '$(BUNDLE_ICON)'	
	@defaults write $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/Info "CFBundleVersion" '$(BUNDLE_VERSION)'	
	@defaults write $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/Info "CFBundlePackageType" 'BNDL'	
	@defaults write $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/Info "CFBundleInfoDictionaryVersion" '6.0'	
	@defaults write $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/Info "CFBundleName" '$(BUNDLE_NAME)'	
	@defaults write $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/Info "CFBundleIdentifier" '$(BUNDLE_ID)'
	@defaults write $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/Info "NSPrincipalClass" '$(BUNDLE_CLASS)'

	@defaults write $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/Info "CFBundleExecutable" '$(BUNDLE_EXEC)'	
	@defaults write $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/Info "IOClass" '$(BUNDLE_CLASS)'	
	@defaults write $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/Info "IOProviderClass" '$(BUNDLE_CLASS_PROVIDER)'	
	@plutil -convert xml1 $(SYMROOT)/$(BUNDLE_NAME).bundle/Contents/Info.plist


	
stack_protector.o: 	
	$(CC) $(CPPFLAGS) $(CFLAGS) $(DEFINES) -c "$(LIBSAIODIR)/stack_protector.c" $(INC) -o "$(OBJROOT)/stack_protector.o"
        
CPUfreq.o: 	
	$(CC) $(CPPFLAGS) $(CFLAGS) $(DEFINES) -c "CPUfreq.c" $(INC) -o "$(OBJROOT)/CPUfreq.o"

include ../../MakeInc.dir

# dependencies
-include $(OBJROOT)/Makedep
