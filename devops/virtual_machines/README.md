## Introduction
We use Vagrant to build and develop the digital collections infrastructure. Vagrant is a tool by which we can build a virtual server with a few commands. It harnesses both VirtualBox as well as bash, so both are necessary on your hosting machine. In Windows, you can install and configure mobaxterm to provide the requisite bash environment.

## Installing Virtual Machines (for Development)
After installing VirtualBox, Vagrant, and bash (if it's not already on your computer), clone one of the virtual machine repositories such as [fedora-stack-prod] (https://github.com/WSULib/fedora-stack-prod). Then navigate to the folder in your terminal, unzip the downloads.zip folder, and run the command ```vagrant up```. This should start the process of building your virtual machine on your computer. The process will take a while (10-15~ minutes). When finished, type in ```vagrant ssh``` to remote into the virtual machine and start your development work.

## Installing Virtual Machines (for Production)
Similar to the development installation process outlined above, installing for production involves the use of the same virtual machine codebase (master branch). Assuming a base Ubuntu server has been created for you with admin privileges, login to this blank remote server via ssh. Then, clone the virtual machine repository such as [fedora-stack-prod] (https://github.com/WSULib/fedora-stack-prod). Run the ./prebuild.sh script. This will download the sensitive configuration files found in our fedora-stack-downloads repository. Then, notice that with the fedora-stack-prod build instructions found on the Github README.md, there are additional configuration steps including building a file in config/envvars. Finally run ./bash_install.sh to activate the installation process. You'll notice this installation process is purely a bash affair with no use of Vagrant; however, it uses the same provisioning files as the Vagrant development install. Follow any prompts that might appear, and when finished, you will have a base production machine. Check security rules and other settings when finished...although those should have already been set in the base image and configuration steps above.


## Starting and Stopping
### Vagrant
When building a virtual machine for develop, you can harness the power of Vagrant to control the installation process.  The following commands are useful to know:

```vagrant up``` -- start the installation process

```vagrant halt``` -- stop the current virtual machine

```vagrant destroy -f``` -- destroy (forcefully with no prompts) the existing virtual machine

You can essentially build and rebuild at will with Vagrant. Just remember that builds do take time (10-15~ minutes). Consult [Vagrant documentation] (https://www.vagrantup.com/docs/cli/) for further commands.

When building a production machine, you lack the fine grained control afforded by the Vagrant-mediated development process. The installation process for production is controlled by an uber-bash script. The two commands you need to know to for handling the production installation:

```./bash_install.sh``` -- start the installation process

```Ctrl+C``` -- kill the installation script

There is no way currently to rollback changes. Due the minimalist approach of building production, all testing should be done in development to ensure a successful production build.

## Troubleshooting

## :tomato:ToDo
* Troubleshooting section
