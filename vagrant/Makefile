SHELL:=/bin/bash

munge.key:
	dd if=/dev/random of=munge.key bs=1024 count=1

setup: munge.key
	vagrant up && \
	vagrant ssh headnode -- -t 'sinfo; \
	sudo -E env "PATH=/usr/local/bin/:$PATH" scontrol update nodename=node00 state=resume; \
	sudo -E env "PATH=/usr/local/bin/:$PATH" scontrol update nodename=node01 state=resume; \ sinfo'
