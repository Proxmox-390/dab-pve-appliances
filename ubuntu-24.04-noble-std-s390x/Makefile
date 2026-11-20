all: info/init_ok
	dab bootstrap
	# systemd-resolved is Priority: important in noble but optional in
	# noble-updates, so dab no longer selects it; install it explicitly to keep
	# the same package set and resolver setup as ubuntu-24.04-standard_24.04-2.
	dab install systemd-resolved
	###
	# NOTE: zstd appliances are only supported on PVE >= 7.0, take care on upload!
	###
	dab finalize --compressor zstd-max

info/init_ok: dab.conf
	dab init
	touch $@

.PHONY: clean
clean:
	dab clean
	rm -f *~

.PHONY: dist-clean
dist-clean:
	dab dist-clean
	rm -f *~
