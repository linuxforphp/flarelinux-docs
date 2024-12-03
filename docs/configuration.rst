.. _ConfigurationAnchor:

.. index:: Configuration

.. _configuration:

=============
Configuration
=============

The Flare Linux Docker image allows for runtime configuration. You can do so by passing in environment
variables to the container on startup, or by sharing files with the container that is running the
Flare server nodes.

---------------------
Environment Variables
---------------------

You can set some environment variables in order to change the default values of the Flare server nodes
at runtime.

You can do so by adding the 'e' option as often as you need to, like so::

    $ docker run -it --rm -p 9650:9650 --name my_flare_server -e FLARE_BIND_ADDRESS="0.0.0.0" asclinux/flarelinux:1.1.6-1.9.1 flare --flare-coston1

Here is a complete list of all environment variables that will be taken into account by the Flare Linux
container at runtime:

.. list-table:: Environment Variables
   :widths: 40 60
   :header-rows: 1

   * - Variable
     - Description
   * - FLARE_BIND_ADDRESS
     - Bind the Flare server to a specified network interface

-------------
Sharing Files
-------------

It is also possible to share files with the Flare Linux container at runtime.

You can do so by adding the 'v' option as often as you need to, like so::

    $ docker run -it --rm -p 9650:9650 --name my_flare_server -v ${PWD}/.flare:/home/flareuser/.flare asclinux/flarelinux:1.1.6-1.9.1 flare --flare-coston1

------------------------------
Installing Additional Software
------------------------------

You can install additional software by using the lfphp-get utility.

For example, to install the Ethereum tools, you can run the following command, from inside the container::

    # lfphp-get ethereum-utils

For more information on this utility, please see the `Linux for PHP Documentation <https://linux-for-php-documentation.readthedocs.io/en/latest/advanced_features.html#package-installation-using-the-lfphp-get-command>`_.