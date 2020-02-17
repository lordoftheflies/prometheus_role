---
title: 'Ansible Role: Prometheus'
description: 'Quickstart and examples for demonstrating the Prometheus role capabilities.'
comments: true
feedback: true
---

# Ansible Role: Prometheus

Self-managing role for maintain **Prometheus** instance/cluster. The role
including automation scripts to the whole operation lifecycle.

```plantuml
@startuml
(*) --> ===b===
===b=== --> "Install\nPrometheus\nservers"
===b=== --> "Rollback previous\nhealthy state"
if "Is deployment\nsuccessfully finished?" then
-> [Success] operate
-> monitor
--> ===e===
else
--> [Fail] troubleshooting
if "Is problem solved?" then
-> [yes] ===e===
else
-> [no] "Rollback previous\nhealthy state"
"Rollback previous\nhealthy state" --> ===e===
===e=== --> (*)
@enduml
```

```plantuml
@startuml
actor "Operator" as o
node "Workstation" <<Controller>> as w {
  component "Ansible 2.9+" as a
  component "Python 3.4+" as p
  artifact "Summarized\nError Log" as e
  artifact "Summarized\nConsole Log" as c
}
cloud "Nodes" as n {
  node "Prometheus #1" <<Node>> as p1
  node "Prometheus #2" <<Node>> as p2
  node "Prometheus #3" <<Node>> as p3
}
o -r-> a: Login as\nAnsible\nuser
p -d-> p1: SSH
p -d-> p2: SSH
p -d-> p3: SSH
a -> p
a -u-> e
a -u-> c
@enduml
```

## Status

[![Build Status](https://travis-ci.org/lordoftheflies/prometheus_role.svg?branch=master)](https://travis-ci.org/lordoftheflies/prometheus_role)

## Description

The `prometheus_role` is an Ansible role used to setup and maintain production grade services,
including the whole operation lifecycle.

## Roadmap

* [ROADMAP.md](ROADMAP.md)

## References

* [docs.ansible.com](https://docs.ansible.com/)
* [On Ansible Galaxy](https://galaxy.ansible.com/lordoftheflies/prometheus_role)

## Requirements

### Production

* Ansible

### For Local Testing

* [Vagrant](https://www.vagrantup.com/) - (Tested using version 2.1.1)
* Vagrant plugins:
  * [vagrant-disksize (0.1.2)](https://github.com/lordoftheflies/vagrant-disksize)
  * [vagrant-libvirt](https://github.com/lordoftheflies/vagrant-libvirt)
  * vai (0.9.3) - For testing with multiple vms [vagrant-plugin-vai](https://github.com/lordoftheflies/vagrant-plugin-vai)
  * [vagrant-vbguest (0.15.2) - Recommended vagrant-vbguest](https://github.com/lordoftheflies/vagrant-vbguest)
* [Virtual Box](https://www.virtualbox.org/)
  * Tested using Version 5.2.14 r123301 (Qt5.6.1)

## Variables

### defaults/main.yml

* [defaults/main.yml](defaults/main.yml) contains all of the required variables.

### project_name/site.yml example

* [example_prometheus_role.yml](files/example_site.yml) may contain an example entry.

## Testing

To test with all VM's defined in Vagrantfile run the following:

```shell
cd roles/prometheus_role
vagrant up
```

To run on a specific VM's
```shell
vagrant up xenial
```

### VM's tested with Vagrant and Virtualbox

pass, fail, untested, unsupported


| OS | Version | Distribution | Supported [^1](#) | Results  |
| :--- | :---: | :---: | :---: | :---: |


## Authors

- [László Hegedűs](mailto:lordoftheflies)

## License: [MIT](https://tldrlegal.com/license/mit-license)

* prometheus_role generated using [ansible_collection_skeleton](https://github.com/lordoftheflies/ansible_collection_skeleton)
