include ../Flags.mk

DIRS=hotcrp

INCLUDE_PATHS +=
LIB_PATHS +=
LIBS = -lhotcrppol -lqapla
EXTRA_STATIC_LIBS = -lmysqlparser -lm -lantlr3c -lmysqlclient -lz
EXTRA_DYNAMIC_LIBS = -lpthread -lrt -ldl

# == test ==
TEST_SRC=\
				 testlexer.c	\
				 refmon.c	\
				 latency.c

TEST_BIN=$(TEST_SRC:.c=)

%: %.c
	$(CXX) $(CXXFLAGS) `mysql_config --cxxflags` $< -o $@ $(LIB_PATHS) \
		-Wl,-Bstatic $(LIBS) $(EXTRA_STATIC_LIBS)	\
		-Wl,-Bdynamic $(CLIBS) $(EXTRA_DYNAMIC_LIBS)

all: dir src libs libso

dir:
	for d in $(DIRS); do	\
		$(MAKE) -C $$d;	\
	done

src: test

test: cleantest $(TEST_BIN)

cleantest:
	rm -f $(TEST_BIN)

clean:
	for d in $(DIRS); do	\
		$(MAKE) -C $$d $@;	\
	done
	rm -f *.o

distclean: clean cleantest

.PHONY: all clean test cleantest src libs libso distclean
