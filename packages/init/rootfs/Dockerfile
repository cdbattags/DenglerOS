ARG	BASE_IMAGE=$BASE_IMAGE
FROM	$BASE_IMAGE AS rootfs

WORKDIR	/rootfs

RUN	mkdir -p \
	etc/unitfiles \
	lib/firmware \
	lib/modules \
	var/log \
	var/lib \
	proc \
	root \
	etc \
	mnt \
	dev \
	sys \
	run \
	tmp

RUN	ln -s ../tmp var/tmp
RUN	ln -s ../run var/run

RUN     ln -s /var/lib/apk var/lib/apk
RUN     ln -s /etc/apk etc/apk

RUN	apk --update --no-cache --root /rootfs --initdb add \
	busybox 
	

RUN	rm -rf \
	var/lib/apk \
	etc/apk \
	dev/* \
	etc/logrotate.d \
	etc/network \
	etc/udhcpd.conf \
	lib/apk \
	root \
	usr/etc \
	var/cache \
	var/lib/*

RUN	touch etc/resolv.conf


FROM	scratch

COPY	--from=rootfs /rootfs/ /
