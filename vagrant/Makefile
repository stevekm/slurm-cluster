SHELL:=/bin/bash

munge.key:
	dd if=/dev/random of=munge.key bs=1024 count=1

setup: munge.key
	vagrant up
