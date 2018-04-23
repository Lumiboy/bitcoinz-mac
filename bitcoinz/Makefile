
target_name ?= bitcoinz

include ../Makefile.build

BITCOINZ_VERSION=master

bitcoinz_clone:
	if [ ! -d "bitcoinz_$(BITCOINZ_VERSION)" ]; then git clone -b $(BITCOINZ_VERSION) https://github.com/Lumiboy/bitcoinz.git bitcoinz_$(BITCOINZ_VERSION); fi

bitcoinz_config:
	$(call patchme,bitcoinz_$(BITCOINZ_VERSION))

bitcoinz_build:
	( cd bitcoinz_$(BITCOINZ_VERSION); \
		LIBTOOLIZE=glibtoolize ./zcutil/build.sh --disable-libs; \
	)

bitcoinz_install:
	rm -rf tmp
	mkdir -p tmp
	mkdir -p ${BSPINSTALL}/usr/local
	make DESTDIR=${BSPROOT}/bitcoinz/tmp -C bitcoinz_$(BITCOINZ_VERSION) install
	cp -af ${BSPROOT}/bitcoinz/tmp${BSPROOT}/bitcoinz/bitcoinz_$(BITCOINZ_VERSION)/depends/*/* ${BSPINSTALL}/usr/local
# install bitcoinz init script
	cp -a files/* ${BSPINSTALL}/usr/local/bin

bitcoinz_uninstall:
	make -C bitcoinz_$(BITCOINZ_VERSION) uninstall

bitcoinz_clean:
	if [ -f "bitcoinz_$(BITCOINZ_VERSION)/Makefile" ]; then make -C bitcoinz_$(BITCOINZ_VERSION) distclean; fi

bitcoinz_distclean:
	rm -rf bitcoinz_$(BITCOINZ_VERSION)
