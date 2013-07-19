Ceph 5-Minute Quickstart Playbook
=================================

* Requires Ansible 1.2
* Expects Ubuntu Server 12.04+

Ceph
----

_"Ceph is a distributed object store and file system designed to provide excellent performance, reliability and scalability."_

[Ceph Architecture](http://ceph.com/docs/master/architecture/) (ceph.com)

Introduction
------------

These playbooks will configure a pair of servers to function as a basic Ceph server and client following the 5-Minute Quick Start Guide found here: http://ceph.com/docs/next/start/quick-start/

**Note:** The preferred method for deploying Ceph is now ceph-deploy. This playbook uses the old method, mkcephfs.

Getting Started
---------------

Just update the included 'hosts' file with appropriate address and connection information for the ceph-client and ceph-server aliases.

    [ceph-quickstart]
    ceph-client
    ceph-server

With that done, use the following command to deploy the nodes:

    ansible-playbook -i hosts ceph-quickstart.yml

Successful deployment can be verified with the ansible command line.

    ansible ceph-client -i hosts -a "ceph health"

Which should return the following:

    ceph-client | success | rc=0 >>
    HEALTH_OK

Background
----------

I've been wanting to get my feet wet with Ansible, Ceph and Github, this is the first result. There's surely room for improvement.

Building these playbooks was an interesting learning experience and exposed me to a number of ansible modules and features.

**Modules**

* apt
* apt_key
* command
* copy
* file
* fetch
* shell
* template

**Features**

* Using with_items to iterate.
* Roles.
* Jinja2 templating and accessing facts from other hosts.

Improvements
------------

* mkcephfs is has been outmoded by ceph-deploy which is surely an easier way to get started with Ceph. 
* The shell + fetch + copy + file routine for moving the ceph.keyring to the client could certainly be simplified and the fetched keyring must be cleaned from ansible admin client manually.
* Mixing group_vars and roles with specific host references doesn't seem like a good idea.  This set of files started as a single monolithic playbook, but I wanted to toy with creating a directoy structure in line with best practices.
