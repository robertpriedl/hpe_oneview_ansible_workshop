
# Welcome to Red Hat / HPE Server Provisioning

## Introduction

This Playbooks will add the Server to OneView, a genreated Profile with OneView.
Then a Playbook will prepare an ISO File with the given vars for an unattended ESXi Installation.
A last Playbook will remove the Serverprofile and the Server Hardware from OneView, to make it prepared for delivery.

## Prereqs:

| Topic   | Exercises  | 
|---|---|
| **BastionHost** : The installed Bastionhost with webserver and ESXi Iso under /tmp. Beware of the iso directory - my iso dir has the name "iso" not "isos"!|  |
| **Inventory** : The Host file with the supporting server and the target servers. The name and the Ilo Vars are required for installing. The IP of the target Server is required for static IP. The ilo_pw is the password of the "Administrator" of the ILO interface and is documented on a lable on the Server itself| |
| **group_vars** : Here are all required vars for the server deployment. For production it should be one group_var per customer and a "all" group for generic settings. Also the host specific vars should be in the host_vars or in the inventory file |  |
| **-** : -| -- |


