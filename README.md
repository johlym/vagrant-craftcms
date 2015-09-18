# Vagrant-based Craft CMS Deployment

## The Purpose

For testing Craft CMS in an isolated environment on a local system. Good for pre-production work.

## System Requirements

* Vagrant
* VirtualBox

## Usage

Since this is a git repo, it's best to pull it down via git:

```git clone https://github.com/jelyman2/vagrant-craftcms && vagrant up```

I've tested this deployment on OS X. I expect Linux and Windows to be the same.

## Accessing Craft

After Vagrant finishes provisioning, browse to http://11.22.33.44.

## The Ingredient List

The Vagrantfile included in this repo will:

- Run `apt-get update`
- Install:
```
-- vim
-- curl
-- python-software-properties
-- mysql-server
-- nginx
-- php5-fpm
-- php5-mysql
-- imagemagick
-- php5-imagick
-- php5-curl
-- configure php
-- add mcrypt
-- configure nginx
-- copy Craft into `/var/www/craftcms`
```

## The Technical Stuff

- Ports (internal/external): `80:80`
- MySQL Username/Password/Database: `root`/`root`/`craft`
- Added VIM, curl, and some python to the mix to be safe.
- RAM: `2GB`

## Noteworthy

The nginx `conf` file is built to allow for url rewrites in Craft

## License

The MIT license is in effect here. Do with this repo whatever you wish. Fork the hell out of it and make it awesome!
