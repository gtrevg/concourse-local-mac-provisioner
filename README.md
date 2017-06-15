# Overview

This tool deploys a concourse server, linux worker, and mac worker onto a target mac. It will also install any missing dependencies that are necessary for deploying concourse onto the target machine.

# Motivation

1. Projects often need a quick and simple CI setup.
1. We would like to use concourse in our projects more often.
1. The default concourse docker images do not allow iOS tests to be run. This tool includes a mac worker to address this need.

# Usage

There are two machine entities involved when using this tool: the control machine, and the target machine. They can be the same machine, or two separate machines.

The control machine can be thought of as the machine initiating provisioning, and the target machine is the machine that you would like to deploy concourse onto. 

You will need sudo access either way, and you will also need ssh access to the target machine if it is not localhost.

This tool requires the following packages installed on the control machine in order to run:
  * [ansible](http://docs.ansible.com/ansible/)

It also requires the following packages to be installed on the target machine:
  * [virtualbox](https://www.virtualbox.org/)
  * [xcode command line tools](https://developer.apple.com/xcode/)

----

**Examples**:

*Control machine deploys to itself (aka deploy to localhost)*

```
git clone https://github.com/pivotal-tokyo/concourse-local-mac-provisioner

cd concourse-local-mac-provisioner/ansible

./run-concourse-mac-provisioner.sh localhost

# Concourse is now running at http://localhost:8000
```

*Control machine deploys to target machine (e.g. sushi.foobar.com)*

```
git clone https://github.com/pivotal-tokyo/concourse-local-mac-provisioner

cd concourse-local-mac-provisioner/ansible

./run-concourse-mac-provisioner.sh sushi.foobar.com

# Concourse is now running at http://sushi.foobar.com:8000
```

## Logs

Logs can be accessed on the target machine as follows:

  * Nginx
    * Standard Output Log: /var/log/nginx/access.log
    * Standard Error Log: /var/log/nginx/error.log
  * Concourse Mac Worker
    * Standard Output Log: /var/log/concourse/mac-worker-stdout.log
    * Standard Error Log: /var/log/concourse/mac-worker-stderr.log
  * Concourse Web
    * docker logs docker_concourse-web_1
  * Concourse PostgresDB
    * docker logs docker_concourse-db_1
  * Concourse Linux Worker
    * docker logs docker_concourse-worker_1
  

## Errata

  * The virtualbox installation cannot yet be automated because it uses an interactive installer.
  * Xcode must be downloaded from the MacOS App Store.

# License

MIT License