# dev-environment-vagrant
Developer Environment with Vagrant, Docker and Ansible

## What does this provide

Spin up linux development environments quickly that offers the following:
- run shell commands (installing dependencies as an example)
- use the docker provisioner if you want to make use of docker containers in your environment
- use the ansible provisioner if you want to make use of ansible playbooks to prepare your environment
- remote development on vscode

I have included a example of the shell, docker and ansible provisioner.

## Usage

Clone the repo and change to the directory:

```bash
git clone https://github.com/ruanbekker/dev-environment-vagrant
cd dev-environment-vagrant
```

Install vagrant by following their [installation documentation](https://www.vagrantup.com/docs/installation), then boot the environment using:

```bash
vagrant up
```

In this example we are using 3 provisioners for demonstration:
- shell provisioner (runs shell commands on provisioning)
- docker provisioner (runs a docker container on provisioning)
- ansible provisioner (runs a ansible playbook on provisioning)

Once the vm is booted, we can get the status:

```bash
vagrant status
```

We can ssh directly to the vm, using:

```
vagrant ssh
```

If we want to use VSCode for remote development, you can install the [Remote-SSH](https://code.visualstudio.com/docs/remote/ssh) extension if you don't have it already, then you can view the ssh config of your vm using:

```
vagrant ssh-config
```

To make things easier, we can then append the ssh config to your `~/.ssh/config` file, then we can ssh to our vm using:

```
ssh sektor
```

Or use VSCode for Remote Development, to see the instructions and screenshots, see the [VSCode Readme](README_VSCODE.md).

When making changes to your provisioner or ansible playbooks, then you can simply run:

```
vagrant provision
```

To destroy your environment:

```
vagrant destroy
```

## Project Structure

The procject structure:

```bash
.
├── README.md
├── README_VSCODE.md
├── Vagrantfile
└── ansible
    ├── inventory
    ├── playbook-no-roles.yml
    ├── playbook.yml
    └── roles
        └── website
            ├── README.md
            ├── defaults
            │   └── main.yml
            ├── files
            │   └── styles.css
            ├── handlers
            │   └── main.yml
            ├── meta
            │   └── main.yml
            ├── tasks
            │   ├── configuration.yml
            │   ├── main.yml
            │   └── setup-ubuntu.yml
            ├── templates
            │   ├── app.conf.j2
            │   ├── index.html.j2
            │   └── nginx.conf.j2
            ├── tests
            │   ├── inventory
            │   └── test.yml
            └── vars
                └── main.yml

11 directories, 20 files
```

## Example Applications

The deployed docker container can be accessed on:
- http://http://192.168.33.23:8080

The deployed website via ansible can be accessed on:
- http://192.168.33.23:8080/

## Resources

- https://github.com/AntonyLeons/Ward
- https://hub.docker.com/r/imightbebob/linux-dash