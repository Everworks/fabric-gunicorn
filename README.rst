fabric-gunicorn
===============

Control your gunicorn process with fabric.

Install
-------

The installation is thanks to the Python Package Index and `pip <http://www.pip-installer.org/>`_ really simple.

::

   $ pip install fabric-gunicorn


First steeps
------------

Add ``import fabric_gunicorn as gunicorn`` to your new or existing fabfile.py. After this you should go in your termianl and run ``fab -l`` in your project directory. You will see something like this:

::

    $ fab -l
    Available commands:
    
        gunicorn.start
        gunicorn.status
        gunicorn.stop

Befor you can start a gunicorn process on your server you must set the gunicorn_wsgi_app env variable. Edit your fabfile.py and add something like: ``env.gunicorn_wsgi_app = 'hello.wsgi:app'``. The default workdir is the home directory of the connected user. You can also change this path with the env variable ``env.remote_workdir``.

Normaly you shoudl now able to run ``fab gunicorn.start`` and the gunicorn server shoudl start on your remote machine. Gunicorn must be installed.

Configuration
-------------

fabric-gunicorn take all configuration from the fabric env variable. For gunicorn I added some variables:

env.remote_workdir
  This is normaly your project path.

env.virtualenv_dir
  If you want to use a virtualenv than you can here define the path to your 
  env directory.

env.gunicorn_wsgi_app
  There you set your wsgi app import path.
  Example: ``mydjangoproject.wsgi:application``
  
env.gunicorn_bind
  Define on which port or socket gunicorn should bind.
  Default: ``127.0.0.1:8000``

env.gunicorn_pidfile
  The path for the pidfile of the gunicorn master process.
  Default: ``remote_workdir/gunicorn.pid``

env.django_settings_module
  This is special for django to set the DJANGO_SETTINGS_MODULE path.
  Example: ``mydjangoproject.settings``