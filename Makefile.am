AUTOMAKE_OPTIONS = foreign dist-zip

lib_LTLIBRARIES = librdata.la

librdata_la_SOURCES = \
	src/CKHashTable.c \
	src/rdata_bits.c \
	src/rdata_error.c \
	src/rdata_io_unistd.c \
	src/rdata_parser.c \
	src/rdata_read.c \
	src/rdata_write.c

librdata_la_LIBADD =
librdata_la_CFLAGS = -Os -Wall -Wstrict-prototypes
librdata_la_LDFLAGS = @EXTRA_LDFLAGS@

if HAVE_BZIP2
librdata_la_LIBADD += -lbz2
librdata_la_CFLAGS += -DHAVE_BZIP2
endif

if HAVE_ZLIB
librdata_la_LIBADD += -lz
librdata_la_CFLAGS += -DHAVE_ZLIB=1
endif

if HAVE_APPLE_COMPRESSION
librdata_la_LIBADD += -lcompression
librdata_la_CFLAGS += -DHAVE_APPLE_COMPRESSION=1
else
if HAVE_LZMA
librdata_la_LIBADD += -llzma
librdata_la_CFLAGS += -DHAVE_LZMA=1
endif
endif

include_HEADERS = src/rdata.h

noinst_HEADERS = \
	 src/CKHashTable.h \
	 src/rdata_bits.h \
	 src/rdata_internal.h \
	 src/rdata_io_unistd.h \
	 src/test/test_buffer.h \
	 src/test/test_buffer_io.h

check_PROGRAMS = test_rdata

test_rdata_SOURCES = \
     src/test/test_buffer.c \
     src/test/test_buffer_io.c \
     src/test/test_rdata.c

test_rdata_LDADD = librdata.la

TESTS = test_rdata

if HAVE_FUZZER
noinst_PROGRAMS = fuzz_rdata

fuzz_rdata_SOURCES = src/fuzz/fuzz_rdata.c
fuzz_rdata_LDADD = librdata.la -lstdc++ -lFuzzer
fuzz_rdata_CFLAGS = -g -Wall @EXTRA_WARNINGS@ -Werror -pedantic-errors -std=c99 @SANITIZERS@
endif
