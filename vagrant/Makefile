SHELL:=/bin/bash

munge.key:
	dd if=/dev/random of=munge.key bs=1024 count=1

setup: munge.key
	vagrant up && \
	vagrant ssh headnode -- -t 'sinfo; \
	sudo -E env "PATH=/usr/local/bin/:$PATH" scontrol update nodename=node00 state=resume; \
	sudo -E env "PATH=/usr/local/bin/:$PATH" scontrol update nodename=node01 state=resume; \
	sinfo' && \
	sleep 5 && \
	vagrant ssh headnode -- -t 'sinfo'

sinfo:
	vagrant ssh headnode -- -t 'sinfo'

debug:
	vagrant ssh headnode -- -t 'sudo cat /var/log/slurmctld.log'
	vagrant ssh headnode -- -t 'sudo scontrol show node'
	vagrant ssh node00 -- -t 'sudo cat /var/log/slurmd.log'
	vagrant ssh node01 -- -t 'sudo cat /var/log/slurmd.log'
