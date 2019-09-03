SHELL:=/bin/bash

setup:
	vagrant up

test:
	vagrant ssh headnode -- 'sudo su; sacctmgr -i create cluster cluster ; sacctmgr show cluster' && \
	vagrant ssh headnode -- 'sacctmgr -i create account cluster_account ; sacctmgr show account' && \
	vagrant ssh headnode -- 'sacctmgr -i create user steve account=cluster_account ; sacctmgr show user'
