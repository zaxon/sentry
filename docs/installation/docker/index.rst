Installation w/ Docker
======================

This guide will step you through setting up your own on-premise Sentry in `Docker <https://www.docker.com/>`_.

Dependencies
------------

* `Docker version 1.10+ <https://www.docker.com/getdocker>`_

Building Container
------------------

Start by cloning or forking
`getsentry/onpremise <https://github.com/getsentry/onpremise>`_. This will act the base for your own custom Sentry.

Inside of this repository, we have a ``sentry.conf.py`` and ``config.yml`` ready for :doc:`customizing <../config>`.

.. Note:: To get started, most basic things are configurable through environment variables and won't be needed to specify in your config file, but for advanced setups, we highly recommend baking configuration inside these config files.

On top of that, we have a ``requirements.txt`` file for installing plugins.

Now we need to build our custom image. We have two ways to do this, depending on your environment. If you have a custom registry you're going to need to push to::

    REPOSITORY=registry.example.com/sentry make build push

If not, you can just build locally::

    make build

If you plan on running the dependent services in Docker as well, we support linking containers.

Running Dependent Services
--------------------------

*Running the dependent services in Docker is entirely optional*, but you may, and we fully support linking containers to get up and running quickly.

Redis
~~~~~

::

    docker run -d --name sentry-redis redis


PostgreSQL
~~~~~~~~~~

::

    docker run -d --name sentry-postgres -e POSTGRES_PASSWORD=secret -e POSTGRES_USER=sentry postgres
