include ../../build/config.mk
include ../../build/gccconfig.mk

UHTTPD_SRC		= https://git.openwrt.org/project/uhttpd.git
UHTTPD_VER    = 51283f9f1df5dedcba35f40367ef5d4ab1a55e0b
UHTTPD_DIR		= uhttpd-src
UHTTPD_PATCHDIR = patches

all: compile

include ../../build/module.mk

$(UHTTPD_DIR)/.prepared:
	rm -rf $(UHTTPD_DIR)
	git clone $(UHTTPD_SRC) $(UHTTPD_DIR) && cd $(UHTTPD_DIR) && git checkout 51283f9 -b tmp && cd -
#	(cd $(UHTTPD_PATCHDIR); ls *.patch | sort > series) || true
#	[ -f "$(UHTTPD_PATCHDIR)/series" ] && while read patch; do \
#		patch -d $(UHTTPD_DIR) -p1 < $(UHTTPD_PATCHDIR)/$$patch; \
#	done < $(UHTTPD_PATCHDIR)/series || true
	touch $@

compile: $(UHTTPD_DIR)/.prepared
	(cd $(UHTTPD_DIR); mkdir build; cd build; cmake .. -DTLS_SUPPORT=OFF -DUBUS_SUPPORT=OFF -DUCODE_SUPPORT=OFF -DLUA_SUPPORT=OFF; make -j4)
	mkdir -p dist/usr/sbin
	cp $(UHTTPD_DIR)/build/uhttpd dist/usr/sbin

compile-all: compile

clean:
	rm -rf $(UHTTPD_DIR)
