.. _BasicUsageAnchor:

.. index:: Basic Usage

.. _basic usage:

===========
Basic Usage
===========

Once Docker is installed, you can now run a *Flare Linux* container. It is possible to run the container in
live or test modes.

.. index:: Live mode

---------------------
Flare Linux Live Mode
---------------------

When running Flare Linux in live mode, you will run a node on the Songbird Network (Canary).

Songbird Network
----------------

.. note:: You must be whitelisted by Flare in order to connect to the live network. Please see the `Flare website <https://flare.xyz/putting-songbird-in-flight/>`_.

Open a Bash or a ZSH terminal (Mac or Linux), or a Powershell CLI (Windows), and enter the following
command in the terminal, and wait for the server to finish bootstrapping (might take some time)::

    $ docker run -dit --rm -e FLARE_BIND_ADDRESS=0.0.0.0 -p 9650:9650 --name my_flare_server asclinux/flarelinux:1.0.0 flare --songbird

To check the state of the 'C' chain, you can watch the logs of the server with this command, from inside
the container::

    $ docker exec -it my_flare_server /bin/bash

You will then get a command-line interface similar to this one:

.. image:: /images/basic_usage01.png

Then, from inside the container::

    # tail -f /home/flareuser/.flare/logs/C.log

You should then see the Songbird node's logs, like so:

.. image:: /images/basic_usage02.png

.. index:: Test mode

---------------------
Flare Linux Test Mode
---------------------

When running Flare Linux in test mode, you will either connect to the Coston network (test network),
or use a local test network.

Coston Network
--------------

Open a Bash or a ZSH terminal (Mac or Linux), or a Powershell CLI (Windows), and enter the following
command in the terminal, and wait for the server to finish bootstrapping (might take a few minutes)::

    $ docker run -dit --rm -e FLARE_BIND_ADDRESS=0.0.0.0 -p 9650:9650 --name my_flare_server asclinux/flarelinux:1.0.0 flare --coston

To check the state of the 'C' chain, you can watch the logs of the server with this command from inside
the container::

    $ docker exec -it my_flare_server /bin/bash

Then, from inside the container::

    # tail -f /home/flareuser/.flare/logs/C.log

You can also run the server in interactive mode by removing the 'd' option, like so::

    $ docker run -it --rm -e FLARE_BIND_ADDRESS=0.0.0.0 -p 9650:9650 --name my_flare_server asclinux/flarelinux:1.0.0 flare --coston

Local Network
--------------

If you prefer, you can run a local Flare node, by running the following command instead::

    $ docker run -it --rm -e FLARE_BIND_ADDRESS=127.0.0.1 -p 9650:9650 --name my_flare_server asclinux/flarelinux:1.0.0 flare

---------------------------
Start Testing the Flare API
---------------------------

Use `Postman <https://www.postman.com/>`_ to start querying your server's API: `VIDEO TUTORIAL <https://youtu.be/NPvu6xJ7tsk?t=2447>`_,

.. note:: Make sure the "C" chain is bootstrapped, before making other queries!

-----------------------
Stopping the Flare Node
-----------------------

To stop the Flare server, please enter the following command (or press `Ctrl+C` in interactive mode)::

    $ docker rm -f my_flare_server

