all: info/init_ok
	# s390-tools (Priority: important on s390x only) and sysconfig-hardware
	# (standard) manage CCW/zFCP/DASD hardware, which a container never sees.
	# Excluding them keeps the package set equal to the amd64 template; their
	# dependencies drop out with them since nothing else pulls them in.
	dab bootstrap --exclude s390-tools,sysconfig-hardware
	echo "disable systemd-networkd-wait-online.service" >00-pve-template.preset
	dab cp 00-pve-template.preset /etc/systemd/system-preset/00-pve-template.preset
	rm 00-pve-template.preset
	dab install \
	    ifupdown2 \
	    isc-dhcp-client \
	    ;
	# NOTE: zstd appliances are only supported on PVE >= 7.0, take care on upload!
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
