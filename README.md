tutum-centos
============

Simple CentOS docker image with SSH access


Usage
-----

To create the image `tutum/centos`, execute the following commands on the tutum-centos folder:

	docker build -t tutum/centos:6.4 6.4/


Running tutum/centos
--------------------

Run a container from the image you created earlier binding it to port 2222 in all interfaces:

	sudo docker run -d -p 0.0.0.0:2222:22 tutum/centos:6.4

The first time that you run your container, a random password will be generated
for user `root`. To get the password, check the logs of the container by running:

	docker logs <CONTAINER_ID>

You will see an output like the following:

	========================================================================
	You can now connect to this CentOS container via SSH using:

	    ssh -p <port> root@<host>
	and enter the root password 'U0iSGVUCr7W3' when prompted

	Please remember to change the above password as soon as possible!
	========================================================================

In this case, `U0iSGVUCr7W3` is the password allocated to the `root` user.

Done!


Setting a specific password for the root account
------------------------------------------------

If you want to use a preset password instead of a random generated one, you can
set the environment variable `ROOT_PASS` to your specific password when running the container:

	docker run -d -p 0.0.0.0:2222:22 -e ROOT_PASS="mypass" tutum/centos:6.4

