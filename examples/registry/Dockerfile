FROM centos:6.4
MAINTAINER Phillip Read <phillip.read@gmail.com>

# Install packages and set up sshd
RUN yum -y install openssh-server
RUN ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_dsa_key && ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key && sed -i "s/#UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config && sed -i "s/UsePAM.*/UsePAM no/g" /etc/ssh/sshd_config

# Add scripts
RUN rpm -i http://dl.fedoraproject.org/pub/epel/6/x86_64/pwgen-2.06-5.el6.x86_64.rpm
ADD set_root_pw.sh /set_root_pw.sh
ADD run.sh /run.sh
RUN chmod +x /*.sh

# Install the EPEL Repository
RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm

# Install Git
RUN yum -y install git

# Install Subversion client
RUN yum -y install subversion

# Install the required RPMs
RUN yum -y install python-setuptools python-gevent python-gunicorn python-flask \ 
 python-werkzeug python-urllib3 python-six python-ordereddict python-chardet \
 python-backports-ssl_match_hostname python-backports python-requests \
 python-redis python-blinker python-yaml python-simplejson pyliblzma \
 python-backports-lzma

# Install the required RPMs
RUN easy_install rsa
RUN easy_install pyasn1
 
# Change our working directory
RUN cd /var/opt

# Clone the docker-registry git repository
RUN git clone https://github.com/dotcloud/docker-registry.git

# Change our working directory
RUN cd docker-registry

# Modify the config_sample.yml file for local usage
RUN cp config/config_sample.yml config/config.yml

# Create our registry directory (make sure you have enough space here)
RUN mkdir /tmp/registry
RUN chmod 777 /tmp/registry

# Let’s start the registry
RUN cd /var/opt/docker-registry
RUN gunicorn --access-logfile - --log-level debug --debug \
 -b 0.0.0.0:8000 -c config/gunicorn_config.py \
 -w 1 wsgi:application
 
EXPOSE 22
CMD ["/run.sh"]
