.. _ConfigurationAnchor:

.. index:: Configuration

.. _configuration:

=============
Configuration
=============

The Flare Linux Docker image allows for runtime configuration. You can do so by passing in environment
variables to the container on startup, or by sharing configuration files with the container that is
running the Flare server nodes.

---------------------
Environment Variables
---------------------

You can set some environment variables in order to change the default values of the Flare server nodes
at runtime.

You can do so by adding the 'e' option as often as you need to, like so::

    $ docker run -it --rm -p 9650:9650 --name my_flare_server -e FLARE_BIND_ADDRESS="0.0.0.0" asclinux/flarelinux:1.0.0-rc2 flare --songbird

Here is a complete list of all environment variables that will be taken into account by the Flare Linux
container at runtime:

.. list-table:: Environment Variables
   :widths: 40 60
   :header-rows: 1

   * - Variable
     - Description
   * - FLARE_BIND_ADDRESS
     - Bind the Flare server to a specified network address

-------------------
Configuration Files
-------------------

It is also possible to configure the Flare Linux container at runtime by sharing configuration files.

You can do so by adding the 'v' option as often as you need to, like so::

    $ docker run -it --rm -p 9650:9650 --name my_flare_server -v ${PWD}/chain_apis.json:/home/flare/conf/songbird/chain_apis.json asclinux/flarelinux:1.0.0-rc2 flare --songbird

Here is an example of what the `chain_apis.json` might look like:

.. code-block:: json

    {
        "LTC": [
            {
                "api": "https://litecoin.flare.network/",
                "auth": "basic",
                "u": "public",
                "p": "gA4Yv3cnuXrIvP_7VIZjW1yliZ9GAclj1Td6tRITc6s="
            },
            {
                "api": "https://litecoin-0.flare.network/",
                "auth": "basic",
                "u": "public",
                "p": "gA4Yv3cnuXrIvP_7VIZjW1yliZ9GAclj1Td6tRITc6s="
            }
        ],
        "XRP": [
            {
                "api": "https://xrpl.flare.network/"
            },
            {
                "api": "https://xrpl-1.flare.network/"
            }
        ]
    }
