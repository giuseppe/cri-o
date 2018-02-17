src = $(wildcard *.c)
obj = $(src:.c=.o)

override LIBS += $(shell pkg-config --libs glib-2.0) ../crun/libcrun.a ../crun/libocispec/libocispec.a -lyajl -lselinux -lsystemd -lseccomp -lcap
override CFLAGS += -std=c99 -Os -Wall -Wextra $(shell pkg-config --cflags glib-2.0) -I ../crun -I ../crun/src -I ../crun/libocispec/src

conmon: $(obj) ../crun/libcrun.a
	$(CC) -o ../bin/$@ $^ $(CFLAGS) $(LIBS)

../crun/libcrun.a: ../crun/config.status
	$(MAKE) -C ../crun

../crun/config.status: ../crun/configure
	(cd ../crun; ./configure)

../crun/configure:
	(cd ../crun; ./autogen.sh)

.PHONY: clean
clean:
	rm -f $(obj) ../bin/conmon
