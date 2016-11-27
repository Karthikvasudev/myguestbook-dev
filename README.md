## Ruby development setup

#NOTE: This is the custom app repository

A repo for deploying Ruby app, with automation through Ansible and Vagrant.

## Agenda
1. To spin up an Ubuntu VM box.
2. Setting up environment for Ruby app and resolve the dependencies.
3. Provisioning ruby and redis through Ansible playbooks.
4. Finally launch the app and browse through Localhost.

## Pre-requisites:

1. A Mac or Linux Host machine (Literally a PC)
2. Install Ansible on your host (NOTE: Ansible should be 2.0 > )
3. Install some Vagrant plugins for smoother and faster development experience: `vagrant-cachier`, `vagrant-exec` and `vagrant-faster`

## File structures:

* application files are: `application.rb, boot.rb, models.rb, config.ru`
* supporting files are: `Gemfile*`, `provisioning/roles/ruby/*`, `provisioning/dev.yml`.
* Vagrant: `Vagrantfile`
* Ansible: `provisioning/*`

## Implementation

* Install Vagrant and VirtualBox
* clone this repo !!!
* Before spinning the Guest machine you should first set the environment variable on your host machine such as `DATABASE_URL='postgres://postgres:<password>@XXXXXX'` (Actual database url goes here) such a way that inline shell script will push this param to the guest machine.
* Run: `vagrant up`
* Once the box is UP then Run: `vagrant ssh -c 'cd /vagrant; bundle exec rackup -p9292 --host 0.0.0.0'` --> Binding the Guest and Host machine
* Go to `localhost:9292`, on your browser....BOOOM !! The app will appear in front of you !

## In case of errors
* Stop the VM: `vagrant halt`
* Ofcourse check the error stats and try to resolve the installation procedures !!
* Destroy the VM: `vagrant destroy`
* Start whatever you want up again
* Version the code and start the guest machine and test..
* This way devops utilized in a formal manner <code,deploy,test,repeat>

That simple!!! No burden on devs.. :-) 
