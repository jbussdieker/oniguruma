## Makefile.am for Oniguruma
encdir    = $(top_srcdir)/enc
sampledir = $(top_srcdir)/sample
libname = libonig.la

#AM_CFLAGS = -DNOT_RUBY
AM_CFLAGS =
INCLUDES  = -I$(top_srcdir) -I$(includedir)

SUBDIRS = . sample

include_HEADERS = oniguruma.h oniggnu.h onigposix.h
lib_LTLIBRARIES = $(libname)

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = libonig.pc

libonig_la_SOURCES = regint.h regparse.h regenc.h st.h \
	regerror.c regparse.c regext.c regcomp.c regexec.c reggnu.c \
	regenc.c regsyntax.c regtrav.c regversion.c st.c \
	regposix.c regposerr.c \
	$(encdir)/unicode.c $(encdir)/ascii.c $(encdir)/utf8.c \
	$(encdir)/utf16_be.c $(encdir)/utf16_le.c \
	$(encdir)/utf32_be.c $(encdir)/utf32_le.c \
	$(encdir)/euc_jp.c $(encdir)/sjis.c $(encdir)/iso8859_1.c \
	$(encdir)/iso8859_2.c  $(encdir)/iso8859_3.c \
	$(encdir)/iso8859_4.c  $(encdir)/iso8859_5.c \
	$(encdir)/iso8859_6.c  $(encdir)/iso8859_7.c \
	$(encdir)/iso8859_8.c  $(encdir)/iso8859_9.c \
	$(encdir)/iso8859_10.c $(encdir)/iso8859_11.c \
	$(encdir)/iso8859_13.c $(encdir)/iso8859_14.c \
	$(encdir)/iso8859_15.c $(encdir)/iso8859_16.c \
	$(encdir)/euc_tw.c $(encdir)/euc_kr.c $(encdir)/big5.c \
	$(encdir)/gb18030.c $(encdir)/koi8_r.c $(encdir)/cp1251.c

libonig_la_LDFLAGS = -version-info $(LTVERSION)

EXTRA_DIST = HISTORY README.ja index.html index_ja.html \
	doc/API doc/API.ja doc/RE doc/RE.ja doc/FAQ doc/FAQ.ja \
	win32/Makefile win32/config.h win32/testc.c \
	$(encdir)/koi8.c $(encdir)/mktable.c \
	$(sampledir)/encode.c $(sampledir)/listcap.c $(sampledir)/names.c \
	$(sampledir)/posix.c $(sampledir)/simple.c $(sampledir)/sql.c \
	$(sampledir)/syntax.c $(srcdir)/libonig.pc.in

bin_SCRIPTS = onig-config

onig-config: onig-config.in

dll:
	$(CXX) -shared -Wl,--output-def,libonig.def -o libonig.dll *.o \
	$(LIBS)
	strip libonig.dll

# Ruby TEST
rtest:
	$(RUBYDIR)/ruby -w -Ke $(srcdir)/test.rb

# character-types-table source generator
mktable: $(encdir)/mktable.c $(srcdir)/regenc.h
	$(CC) -I$(top_srcdir) -o mktable $(encdir)/mktable.c


# TEST
TESTS = testc testp testcu

check_PROGRAMS = testc testp testcu

atest: testc testp testcu
	@echo "[Oniguruma API, ASCII/EUC-JP check]"
	@$(top_builddir)/testc  | grep RESULT
	@echo "[POSIX API, ASCII/EUC-JP check]"
	@$(top_builddir)/testp  | grep RESULT
	@echo "[Oniguruma API, UTF-16 check]"
	@$(top_builddir)/testcu | grep RESULT

testc_SOURCES = testc.c
testc_LDADD = libonig.la

testp_SOURCES = testc.c
testp_LDADD = libonig.la
testp_CFLAGS = -DPOSIX_TEST

testcu_SOURCES = testu.c
testcu_LDADD = libonig.la


#testc.c: $(srcdir)/test.rb $(srcdir)/testconv.rb
#	ruby -Ke $(srcdir)/testconv.rb < $(srcdir)/test.rb > $@

#testu.c: $(srcdir)/test.rb $(srcdir)/testconvu.rb
#	ruby -Ke $(srcdir)/testconvu.rb $(srcdir)/test.rb > $@

#win32/testc.c: $(srcdir)/test.rb $(srcdir)/testconv.rb
#	ruby -Ke $(srcdir)/testconv.rb -win < $(srcdir)/test.rb | nkf -cs > $@

## END OF FILE
