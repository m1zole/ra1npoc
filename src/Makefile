IGCC		= xcrun -sdk iphoneos gcc
MGCC		= xcrun -sdk macosx gcc
#DEBUGFLAG	= -DHAVE_DEBUG
MGCC_FLAGS	= -I./include -framework IOKit -framework CoreFoundation -Os -Wall $(CFLAGS) $(DEBUGFLAG)
IGCC_FLAGS	= $(MGCC_FLAGS) -DIPHONEOS_ARM
AARCH32		= -arch armv7
AARCH64		= -arch arm64

SOURCE		= \
                main.c \
                io/iousb.c \
                common/common.c \
                soc/t8010_t8015.c \
                soc/t7000_s8000.c \
                soc/s5l8960x.c

MOBJECT		= ra1npoc_macosx
IOBJECT		= ra1npoc_iphoneos
IOBJECT32	= ra1npoc_iphoneos32
IOBJECT64	= ra1npoc_iphoneos64
ICODESIGN	= ldid -S

PayloadDir	= payload/

.PHONY: all macosx iphoneos clean

all: macosx iphoneos

macosx:
	$(MGCC) $(MGCC_FLAGS) $(SOURCE) -o $(MOBJECT)

iphoneos:
	$(IGCC) $(IGCC_FLAGS) $(SOURCE) $(AARCH32) $(AARCH64) -o $(IOBJECT)
	$(ICODESIGN) $(IOBJECT)

clean:
	-$(RM) $(MOBJECT) $(IOBJECT32) $(IOBJECT64) $(IOBJECT)
