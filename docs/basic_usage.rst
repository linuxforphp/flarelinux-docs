.. _BasicUsageAnchor:

===========
Basic Usage
===========

Once Docker is installed, you can now run a *Flare Linux* container. It is possible to run the container in
live or test modes.

.. index:: Live mode

---------------------
Flare Linux Live Mode
---------------------

Flare Linux Live mode will be available soon.

.. index:: Test mode

---------------------
Flare Linux Test Mode
---------------------

When running Flare Linux in test mode, you can run the node on the Coston network (test network), or
on your local network only.

Coston Network
--------------

Open a Bash or a ZSH terminal (Mac or Linux), or a Powershell CLI (Windows), and enter the following
command in the terminal, and wait for the server to finish bootstrapping (approx. 5 minutes)::

    $ docker run -it --rm -p 9650:9650 --name my_flare_server asclinux/flarelinux:1.0.0-rc1 flare --coston

You will then get a command-line interface similar to this one:

.. image:: /images/basic_usage01.png

You can run the server in detached mode by adding the 'd' option, like so::

    $ docker run -dit --rm -p 9650:9650 --name my_flare_server asclinux/flarelinux:1.0.0-rc1 flare --coston

You can change the version of the Flare server node, by adding a Git commit hash to end of the command, like so::

    $ docker run -it --rm -p 9650:9650 --name my_flare_server asclinux/flarelinux:1.0.0-rc1 flare --coston e9ca17eace0

Local Network
--------------

If you prefer, you can run a local Flare node, by running the following command instead::

    $ docker run -it --rm -p 9650:9650 --name my_flare_server asclinux/flarelinux:1.0.0-rc1 flare --local

---------------------------
Start testing the Flare API
---------------------------

Use `Postman <https://www.postman.com/>`_ to start querying your server's API: `VIDEO TUTORIAL <https://youtu.be/NPvu6xJ7tsk?t=2447>`_,

.. note:: Make sure the "P" and "C" chains are bootstrapped, before making other queries!

-------------------------------
Validate a real XRP transaction
-------------------------------

Open ANOTHER Bash or a ZSH terminal (Mac or Linux), or ANOTHER Powershell CLI (Windows), and enter
the following command::

    $ docker exec -it my_flare_server /bin/bash

Once you are inside the Docker container, enter these commands to validate an XRP transaction::

    $ cd /root/flare/client
    $ $( ./bridge.sh xrp ) &
    $ node --no-warnings prove xrp FFB44382D074CB37B63AC9D3EB2D829C1D1FE4D54DC1A0BCC1D23BAE18D53272 2>/dev/null

After you are done testing, you can exit the container by typing ``exit``.

To stop the Flare server, please enter the following command::

    $ docker stop my_flare_server
