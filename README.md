# water-for-humans
A shared repo for work on the Water For Humans website refresh

## Dev Environment Setup
Download and install the following, if you don't have them already:

- Vagrant
- VirtualBox
- GitHub Client

## Basic Vagrant Commands
After cloning the repo locally, copy the vagrantfile to the root of your project folder (www). Then run `vagrant up` from a shell in this directory. Vagrant will install your LAMP components and Wordpress. Once the setup is finished, follow the directions displayed in the terminal to visit your local installation and set up Wordpress.

In order to shut down your local vagrant environment you can just run `vagrant halt` from the command line, and the virtual machine will power down. Then when you want to work again just `vagrant up` from anywhere in the project folder.