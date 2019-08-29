FROM centos:7

MAINTAINER Stephen M. Kelly

RUN yum upgrade && \
yum install -y epel-release && \
yum install -y bind-utils \
expect \
gcc \
git \
gtk2-devel \
hdf5-devel \
hwloc \
hwloc-devel \
hwloc-gui \
libibmad \
libibumad \
libcurl \
libssh2-devel \
lua \
lua-devel \
man \
make \
man2html \
mariadb \
mariadb-devel \
mariadb-server \
munge \
munge-devel \
munge-libs \
net-tools \
ncurses-devel \
nfs-utils \
numactl \
numactl-devel \
openssh-server \
openssl-devel \
pam-devel \
perl-ExtUtils-MakeMaker \
python-pip \
readline-devel \
rpm-build \
rrdtool-devel \
wget && \
yum install -y pdsh

RUN wget https://download.schedmd.com/slurm/slurm-18.08.8.tar.bz2 && \
tar -jxvf slurm-18.08.8.tar.bz2 && \
rm -f slurm-18.08.8.tar.bz2 && \
mv /slurm-18.08.8 /root/

RUN cd /root/slurm-18.08.8 && \
./configure --disable-dependency-tracking && \
make && \
make install

RUN cp /root/slurm-18.08.8/etc/slurmdbd.service /usr/lib/systemd/system
RUN cp /root/slurm-18.08.8/etc/slurmctld.service /usr/lib/systemd/system
RUN systemctl daemon-reload && \
systemctl enable slurmdbd.service && \
systemctl enable slurmctld.service

# RUN systemctl start slurmdbd.service

ADD slurm.conf /usr/local/etc/slurm.conf
ADD slurmdbd.conf /usr/local/etc/slurmdbd.conf
RUN mkdir /var/spool/slurmd && \
chown slurm:slurm /var/spool/slurmd
RUN mkdir /var/spool/slurmctld && \
chown slurm:slurm /var/spool/slurmctld

RUN systemctl enable munge
RUN dd if=/dev/random of=/etc/munge/munge.key bs=1024 count=1
RUN chown munge:munge /etc/munge/munge.key
RUN chmod 600 /etc/munge/munge.key


RUN mkdir /etc/PDSH
RUN printf 'node00\nnode01\n' > /etc/PDSH/hosts
ENV WCOLL=/etc/PDSH/hosts

# systemctl start mariadb
# Failed to get D-Bus connection: Operation not permitted
