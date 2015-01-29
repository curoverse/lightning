Lightning
=========

How to Set-up a local lightning cluster:
=======================
## Notes:
* This will **not** populate the database with a tile library or population. These capabilities are under development.
* An official Curoverse/Arvados docker image is in development.

## Procedure:
1.	Install docker (https://docs.docker.com/installation/)

2.	Start a Container running postgres (named base-postgres):

		$ sudo docker run --name base-postgres -e POSTGRES_USER=lightning -e POSTGRES_PASSWORD=mypassword -d postgres

3.	Pull sguthrie/lightning (you can also build it user the Dockerfile in experimental/pylightweb)

		$ sudo docker pull sguthrie/lightning

4.  Link the base-postgres with lightning:

		$ sudo docker run --name lightning -it --link base-postgres:postgres sguthrie/lightning /bin/bash

5.	Pull the most recent version of lightning from github

		/home/lightning/lightning/experimental/pylightweb/lightning# git pull

6.	Migrate the lightning tables into postgres:

		/home/lightning/lightning/experimental/pylightweb/lightning# python manage.py migrate

7.	That's it! You can test the installation using:

		/home/lightning/lightning/experimental/pylightweb/lightning# python manage.py test tile_library
