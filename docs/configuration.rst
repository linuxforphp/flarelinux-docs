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

    $ docker run -it --rm -p 9650:9650 --name my_flare_server -e FLARE_BIND_ADDRESS="0.0.0.0" asclinux/flarelinux:1.1.6-1.11.0 flare --flare-coston1

Here is a complete list of all environment variables that will be taken into account by the Flare Linux
container at runtime:

.. list-table:: Environment Variables
   :widths: 40 60
   :header-rows: 1

   * - Variable
     - Description
   * - FLARE_BOOTSTRAP_IPS
     - IP address of the peer used to connect to the rest of the network for bootstrapping. By default, the bootstrap details are programmatically retrieved from the Flare bootstrap nodes upon startup. This is the recommended approach as the bootstrap node's IP can rotate.
   * - FLARE_BOOTSTRAP_IDS
     - Node ID of the peer used to connect to the rest of the network for bootstrapping. In the run command above, the bootstrap details are programmatically retrieved from the Flare bootstrap nodes upon startup. This is the recommended approach as the bootstrap node's ID can rotate.
   * - FLARE_HTTP_HOST
     - IP address that the node will use on the network to allow connections from other machines. Otherwise, only connections from localhost are accepted.
   * - FLARE_HTTP_PORT
     - The port through which the node will listen to API requests. The default value is 9650.
   * - FLARE_ALLOWED_HOSTS
     - Bind the Flare node to specified virtual host names for API requests (default: localhost, or * if FLARE_BIND_ADDRESS is set to 0.0.0.0).
   * - FLARE_DATA_DIR
     - Directory where the data files are stored, including the LevelDB database files (--db-dir). The default is '/home/flareuser/.flare' within the container. This directory can be shared with the host computer (please see the 'Sharing Files' section).
   * - FLARE_PUBLIC_IP
     - IP address that the node will publish as its remote IP address on the network.
   * - FLARE_BIND_ADDRESS
     - Bind the Flare node to a specified network interface. Use "0.0.0.0" to allow connections from any machine (FLARE_ALLOWED_HOSTS will be set to '*'), or to a specific IP address. Otherwise, only connections from localhost or HTTP_FLARE_HOST are accepted. This variable overrides FLARE_HTTP_HOST.

.. note:: To use a custom C chain configuration file (config.json), the file needs to be shared with the Flare Linux container, in the /home/flareuser/.flare/configs/chains/C directory.

-------------
Sharing Files
-------------

It is also possible to share files with the Flare Linux container at runtime.

You can do so by adding the 'v' option as often as you need to, like so::

    $ docker run -it --rm -p 9650:9650 --name my_flare_server -v ${PWD}/.flare:/home/flareuser/.flare asclinux/flarelinux:1.1.6-1.11.0 flare --flare-coston1

------------------------------
Installing Additional Software
------------------------------

You can install additional software by using the lfphp-get utility.

For example, to install the Ethereum tools, you can run the following command, from inside the container::

    # lfphp-get ethereum-utils

For more information on this utility, please see the `Linux for PHP Documentation <https://linux-for-php-documentation.readthedocs.io/en/latest/advanced_features.html#package-installation-using-the-lfphp-get-command>`_.