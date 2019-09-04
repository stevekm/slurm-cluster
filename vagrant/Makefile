SHELL:=/bin/bash

munge.key:
	dd if=/dev/random of=munge.key bs=1024 count=1

# initial setup and provisioning of the VMs
setup: munge.key
	vagrant up && \
	vagrant ssh headnode -- -t 'sinfo; \
	sudo -E env "PATH=/usr/local/bin/:$$PATH" scontrol update nodename=node00 state=resume; \
	sudo -E env "PATH=/usr/local/bin/:$$PATH" scontrol update nodename=node01 state=resume; \
	sinfo' && \
	sleep 5 && \
	vagrant ssh headnode -- -t 'sinfo'

# Run this after running 'vagrant reload'
# also required to re-sync changes to the VM /vagrant/ dir from host;
# https://stackoverflow.com/questions/40972345/vagrant-synced-folders-not-working-real-time-on-virtualbox
# https://www.vagrantup.com/docs/synced-folders/rsync.html
reload:
	vagrant ssh headnode -- -t 'sudo systemctl start munge; \
	sleep 1; \
	sudo systemctl status munge; \
	sleep 1; \
	sudo systemctl start mariadb; \
	sleep 1; \
	sudo systemctl status mariadb; \
	sleep 1; \
	sudo systemctl start slurmdbd; \
	sleep 1; \
	sudo systemctl status slurmdbd; \
	sleep 1; \
	sudo systemctl start slurmctld; \
	sleep 1; \
	sudo systemctl status slurmctld; \
	' && \
	vagrant ssh node00 -- -t 'sudo systemctl start munge; \
	sleep 1; \
	sudo systemctl status munge; \
	sleep 1; \
	sudo systemctl start slurmd; \
	sleep 1; \
	sudo systemctl status slurmd; \
	' && \
	vagrant ssh node01 -- -t 'sudo systemctl start munge; \
	sleep 1; \
	sudo systemctl status munge; \
	sleep 1; \
	sudo systemctl start slurmd; \
	sleep 1; \
	sudo systemctl status slurmd; \
	' && \
	vagrant ssh headnode -- -t 'sinfo; \
	sudo -E env "PATH=/usr/local/bin/:$$PATH" scontrol update nodename=node00 state=resume; \
	sudo -E env "PATH=/usr/local/bin/:$$PATH" scontrol update nodename=node01 state=resume; \
	sleep 5; \
	sinfo'

# check the cluster status
sinfo:
	vagrant ssh headnode -- -t 'sinfo'

# submit a test job long enough to watch it in sinfo
test:
	vagrant ssh headnode -- -t "sbatch /vagrant/job.sh; sleep 1; sinfo; squeue"

debug:
	vagrant ssh headnode -- -t 'sudo cat /var/log/slurmctld.log'
	vagrant ssh headnode -- -t 'sudo scontrol show node'
	vagrant ssh node00 -- -t 'sudo cat /var/log/slurmd.log'
	vagrant ssh node01 -- -t 'sudo cat /var/log/slurmd.log'
