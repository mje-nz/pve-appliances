BASEDIR:=$(shell dab basedir)

all: info/init_ok
	# Update version
	sed -i "s/Version: .*/Version: $$(date '+%Y.%m.%d')/" dab.conf
	# Set up container with as little as DAB will allow pre-installed
	dab bootstrap --minimal
	# Remove unnecessary packages
	dab exec apt-get remove -y postfix vim-common vim-tiny
	# Clear out documentation and locale files
	# (rm with a wildcard needs bash and I can't be bothered figuring out the right quotes)
	dab exec find /usr/share/doc -mindepth 1 -delete
	dab exec find /usr/share/locale -mindepth 1 -delete
	dab exec find /usr/share/man -mindepth 1 -delete
	# Build into image
	dab finalize

info/init_ok: dab.conf
	dab init && touch $@

.PHONY: clean
clean:
	dab clean
	rm -f *~

.PHONY: dist-clean
dist-clean:
	dab dist-clean
	rm -f *~
