SHELL:=/bin/bash
ABSDIR:=$(shell python -c 'import os; print(os.path.realpath("."))')
DOCKERTAG:=stevekm:slurm-cluster
build:
	docker build -t "$(DOCKERTAG)" .

test:
	docker run --privileged --cap-add SYS_ADMIN -p 8080:8080 --rm -ti "$(DOCKERTAG)" bash
# -v "$(ABSDIR)":/staging
# --privileged
