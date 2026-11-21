all: info/init_ok
	dab bootstrap
	# systemd-resolved is Priority: important in noble but optional in
	# noble-updates, so dab no longer selects it; install it explicitly to keep
	# the same package set and resolver setup as ubuntu-24.04-standard_24.04-2.
	dab install systemd-resolved
	# Ubuntu's ssl-cert ships ssl-cert.service, which creates the snakeoil
	# key-pair on first boot when the key is missing. Do not ship the pair
	# generated at build time: pve-container would otherwise add its own
	# one-shot regeneration unit, and both make-ssl-cert runs race for the
	# debconf lock on first boot (one of the two units fails).
	dab exec sh -c 'rm -f /etc/ssl/private/ssl-cert-snakeoil.key /etc/ssl/certs/ssl-cert-snakeoil.pem; find /etc/ssl/certs -lname ssl-cert-snakeoil.pem -delete'
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
