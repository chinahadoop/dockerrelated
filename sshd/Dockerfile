# sshd
#
# VERSION               0.0.2

FROM centos:6.6
MAINTAINER Sven Dowideit <SvenDowideit@docker.com>

RUN yum clean all && yum install -y openssh-server openssh-clients
RUN mkdir /var/run/sshd
RUN echo 'root:chinahadoop' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
RUN echo "/etc/init.d/sshd start" >> /etc/rc.local
RUN echo "/bin/bash" >> /etc/rc.local

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
