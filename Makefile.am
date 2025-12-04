# $Id$

bin_PROGRAMS=lookbusy
man_MANS=man/lookbusy.1
lookbusy_SOURCES=src/lb.c

EXTRA_DIST=$(man_MANS)

all-local: lookbusy
	@mkdir -p targets
	@cp lookbusy targets/

clean-local:
	rm -rf targets
