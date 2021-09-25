
# Welcome to Red Hat / HPE Server Provisioning

## Introduction

This Playbooks will add the Server to OneView, a genreated Profile with OneView.
Then a Playbook will prepare an ISO File with the given vars for an unattended ESXi Installation.
A last Playbook will remove the Serverprofile and the Server Hardware from OneView, to make it prepared for delivery.

## Prereqs:

| Topic   | Description  | 
|---|---|
| **BastionHost** : | The installed Bastionhost with webserver and ESXi Iso under /tmp. Beware of the iso directory - my iso dir has the name "iso" not "isos"! |
| **Inventory** : | The Host file with the supporting server and the target servers. The name and the Ilo Vars are required for installing. The IP of the target Server is required for static IP. The ilo_pw is the password of the "Administrator" of the ILO interface and is documented on a lable on the Server itself. The host specific vars should be here in the inventory file, or under the host_vars |
| **group_vars** : | Here are all required vars for the server deployment. For production it should be one group_var per customer and a "all" group for generic settings. |
| **-** : -| -- |

## Playbooks:

| Playbook   | Description |
|---|---|
|**hps-addServerHardware.yml**| Add the Server hardware to Oneview. You need the OneView Credentials, the ILO Credentials are in the hosts_var or in the inventory file. Use vault vars for production.|
|**hps-deployServerProfile.yml**| Deploy a custom Serverprofile to the Server Hardware. It is a yaml code in the playbook, it should be handled separate with own var files in the future |
|**hps-getServerProfileFacts.yml**| Get the Serverprofile Facts from OneView. Its quite easier to configure the Server Profile in yaml, when you have a working Profile for copy-pasting. You'll find the Profile Facts under the ESXi host Facts|
|**hps-removeServerHardware.yml**| Remove the Serverprofile from the Serverhardware under OneView and Delete the Serverhardware from OneView. So the Server will be prepared for delivery. |
|**vmware_iso_boot**| Boot the created ISO and install ESXi unattended. A Task will wait for the Server, when the ESXi IP is answering on port 80|
|**vmware_iso_cleanup.yml**| Clean up the working dir with the temporary mounted iso files. Also it cleanup the ISO files on the bastion_host webserver directory |
|**vmware_iso_prep**| Create a unattended ESXi install ISO file with templating a ks.cfg file and configuring the ISO. After all it will be copied to the bastion_server to the iso directory for further use. |
