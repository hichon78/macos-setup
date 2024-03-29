# MacOS Setup with Ansible and Bash

This repository contains a collection of bash scripts and ansible playbooks to setup a new Mac OS from scratch. The intent of this is to get as much of the configuration and installation steps done using a no touch approach. There will be a few manual steps after completion, but not much.

## Getting Started

There are some shell scripts in `/bin` that can be used to abstract start up. These shell scripts provide a simpler method to get started. Supported operations are described below.

### backup

There's a backup script that will pull files such as ssh, zsh, and other configuration settings from your home directory into this repo for saving. I added this here because I always forgot to backup my home directory configs.

````
./bin/backup
````

### bootstrap

Before we can actually run ansible, we need to setup our runtime which requires various software to be installed. We can just setup ansible directly, but it's better to do it correctly via the right package managers. The bootstrap is meant to only deploy the basic minimum, however it does quite a bit:

- Install XCode
- Install Rosetta2
- Install Homebrew
- Install asdf via Homebrew
- Install poetry via Homebrew
- Install python via asdf
- Install direnv via asdf
- Create virtualenv
- Upgrade pip

````
./bin/run --bootstrap
````

Once `direnv` is installed, you can simply do `run --bootstrap` from the root of the project. Once the system is bootstrapped. run the following to enter the virtual environment:

````
poet
````

### clean

If you need to `start over` and wipe your system. There is a clean flag operation that can be executed to remove the core software

- Remove Homebrew
- Remove asdf

Note - some fo the applications installed by homebrew will not be removed.

````
./bin/run --clean
````

### Run

The main installation and configuration is done via ansible. I could have stayed pure bash, but it's easier to maintain the configuration in ansible. This portion of the execution will:

- Install and configure oh-my-zsh
- Install homebrew taps, casks, and packages
- Install additional asdf plugins 
- Install Apple store software
- Install vscode and configure it

If you want to remove/add/modify the various packages, simply do so within `./vars` there's a yaml configuration for each of the `components` that is fairly self explanatory.
