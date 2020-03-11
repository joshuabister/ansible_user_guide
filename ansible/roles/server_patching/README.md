Server Patching
=========

# server_patching/README.md
Set repositories, patches and versions

See the examples below for variable arrangement


Requirements
------------

Role Variables
--------------

repositories:
  - name: docker
    description: docker official repo
    file: docker_repos
    baseurl: "https://download.docker.com/linux/centos/docker-ce.repo"
    gpgcheck: true
    gpgkey: "https://download.docker.com/linux/centos/gpg"
  - name: epel
    description: epel
    file: extras
    baseurl: "https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm"
    gpgcheck: true
    gpgkey: "/etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7"
packages:
  - package\_name: docker
    package\_version: 1.8.0

Dependencies
------------

Example Playbook
----------------

- hosts: servers
  tasks:
    - name: install packages to specified version
      include_role:
        - name: jbister.server_patching

License
-------

MIT

Author Information
------------------

Joshua Bister
jbister@redhat.com
