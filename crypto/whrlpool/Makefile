#
# crypto/whrlpool/Makefile
#

DIR=	whrlpool
TOP=	../..
CC=	cc
CPP=	$(CC) -E
INCLUDES=
CFLAG=-g
MAKEFILE=	Makefile
AR=		ar r

WP_ASM_OBJ=wp_block.o

CFLAGS= $(INCLUDES) $(CFLAG)
ASFLAGS= $(INCLUDES) $(ASFLAG)
AFLAGS= $(ASFLAGS)

GENERAL=Makefile

LIB=$(TOP)/libcrypto.a
LIBSRC=wp_dgst.c wp_block.c
LIBOBJ=wp_dgst.o $(WP_ASM_OBJ)

SRC= $(LIBSRC)

HEADER= wp_locl.h

ALL=    $(GENERAL) $(SRC) $(HEADER)

top:
	(cd ../..; $(MAKE) DIRS=crypto SDIRS=$(DIR) sub_all)

all:	lib

lib:	$(LIBOBJ)
	$(AR) $(LIB) $(LIBOBJ)
	$(RANLIB) $(LIB) || echo Never mind.
	@touch lib

wp-mmx.s:	asm/wp-mmx.pl ../perlasm/x86asm.pl
	$(PERL) asm/wp-mmx.pl $(PERLASM_SCHEME) $(CFLAGS) $(PROCESSOR) > $@

wp-x86_64.s: asm/wp-x86_64.pl
	$(PERL) asm/wp-x86_64.pl $(PERLASM_SCHEME) > $@

$(LIBOBJ): $(LIBSRC)

files:
	$(PERL) $(TOP)/util/files.pl Makefile >> $(TOP)/MINFO

tags:
	ctags $(SRC)

tests:

lint:
	lint -DLINT $(INCLUDES) $(SRC)>fluff

update: depend

depend:
	@[ -n "$(MAKEDEPEND)" ] # should be set by upper Makefile...
	$(MAKEDEPEND) -- $(CFLAG) $(INCLUDES) $(DEPFLAG) -- $(PROGS) $(LIBSRC)

dclean:
	$(PERL) -pe 'if (/^# DO NOT DELETE THIS LINE/) {print; exit(0);}' $(MAKEFILE) >Makefile.new
	mv -f Makefile.new $(MAKEFILE)

clean:
	rm -f *.s *.o *.obj lib tags core .pure .nfs* *.old *.bak fluff

# DO NOT DELETE THIS LINE -- make depend depends on it.

wp_block.o: ../../include/openssl/e_os2.h ../../include/openssl/opensslconf.h
wp_block.o: ../../include/openssl/whrlpool.h wp_block.c wp_locl.h
wp_dgst.o: ../../include/openssl/e_os2.h ../../include/openssl/opensslconf.h
wp_dgst.o: ../../include/openssl/whrlpool.h wp_dgst.c wp_locl.h
