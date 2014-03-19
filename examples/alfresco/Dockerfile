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

# Install port scanner
RUN yum -y install nmap

# Install vim editor
RUN yum -y install vim

# Add user
RUN useradd alfresco

# Add sudo access
RUN yum -y install sudo
RUN yum -y install passwd
RUN gpasswd -a alfresco alfresco
RUN echo 'alfresco ALL=(ALL)       ALL'  >> /etc/sudoers

# Install Man pages
RUN yum -y install man

# install Java 7 SDK from AWS S3
RUN wget http://s3-eu-west-1.amazonaws.com/devops-001/rpms/jdk-7u51-linux-x64.rpm
RUN rpm -Uvh jdk-7u51-linux-x64.rpm
RUN rm jdk-7u51-linux-x64.rpm
RUN alternatives --install /usr/bin/java java /usr/java/latest/jre/bin/java 200000
RUN alternatives --install /usr/bin/javaws javaws /usr/java/latest/jre/bin/javaws 200000
RUN alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 200000
RUN alternatives --install /usr/bin/jar jar /usr/java/latest/bin/jar 200000
RUN alternatives --install /usr/bin/java java /usr/java/jdk1.7.0_45/jre/bin/java 200000
RUN alternatives --install /usr/bin/javaws javaws /usr/java/jdk1.7.0_45/jre/bin/javaws 200000
RUN alternatives --install /usr/bin/javac javac /usr/java/jdk1.7.0_45/bin/javac 200000
RUN alternatives --install /usr/bin/jar jar /usr/java/jdk1.7.0_45/bin/jar 200000
RUN alternatives --install /usr/bin/java java /usr/java/latest/bin/java 200000
RUN alternatives --install /usr/bin/javaws javaws /usr/java/latest/bin/javaws 200000
RUN alternatives --install /usr/bin/java java /usr/java/jdk1.7.0_45/jre/bin/java 200000
RUN alternatives --install /usr/bin/javaws javaws /usr/java/jdk1.7.0_45/jre/bin/javaws 200000
RUN alternatives --install /usr/bin/java java /usr/java/latest/jre/bin/java 200000 --slave /usr/share/man/man1/java.1 java.1 /usr/java/latest/man/man1/java.1
RUN alternatives --install /usr/bin/java java /usr/java/latest/jre/bin/java 200000 --slave /usr/share/man/man1/java.1 java.1 /usr/java/latest/man/man1/java.1
RUN alternatives --install /usr/bin/javaws javaws /usr/java/latest/jre/bin/javaws 200000 --slave /usr/share/man/man1/javaws.1 javaws.1 /usr/java/latest/man/man1/javaws.1
RUN alternatives --install /usr/bin/rmiregistry rmiregistry /usr/java/latest/jre/bin/rmiregistry 200000 --slave  /usr/share/man/man1/rmiregistry.1 rmiregistry.1 /usr/java/latest/man/man1/rmiregistry.1
RUN alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 200000 --slave  /usr/share/man/man1/javac.1 javac.1 /usr/java/latest/man/man1/javac.1
RUN alternatives --install /usr/bin/jar jar /usr/java/latest/bin/jar 200000 --slave  /usr/share/man/man1/jar.1 jar.1 /usr/java/latest/man/man1/jar.1
RUN alternatives --install /usr/bin/keytool keytool /usr/java/latest/jre/bin/keytool 200000 --slave /usr/share/man/man1/keytool.1 keytool.1 /usr/java/latest/man/man1/keytool.1
ENV JAVA_HOME /usr/java/default

EXPOSE 22 8080
CMD ["/run.sh"]