# LAMP + Java, NodeJS, and MongoDB

The purpose of this project is to have a development environment up and running in the quickest amount of time.

## Dependencies

* Vagrant (1.22+)
* VirtualBox (4.2+)
* Ruby (1.87+)

## Installation

Once all dependencies have been installed, run `./setup.rb` to initialize the vagrant environment.

The script will do the following:

1. Configure your shared directory.
1. Update any attached submodules (cookbooks)
1. Install dependent vagrant plugins.
1. Initialize vagrant VM with a non-NFS shared directory for initial installation.
1. Reboot with NFS engaged.

## Working with the Environment

The vagrant development environment can be run and shutdown with the `vagrant` command from the onboarding directory.

#### Bring the box up

`vagrant up`

#### Bring the box up without NFS shared directories

`NFS=0 vagrant up`

#### Shutdown the box

`vagrant halt`

#### Reload the box

`vagrant reload`

See `vagrant -h` for complete information.

## Possible Issues

* If there's a problem mounting the NFS shared directory, this can sometimes happen the first time you try the NFS mount. Retry the vagrant up. If it is still a problem, you can execute the vagrant commands without the NFS mount: `NFS=0 vagrant up`.
