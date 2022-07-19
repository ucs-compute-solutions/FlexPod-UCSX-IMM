# Cisco Intersight Managed Mode setup using Ansible

 This is repository contains Ansible playbooks to configure  Cisco UCS in Intersight Managed Mode (IMM). This repository can be used for setting up UCS in following Cisco Validated Design (CVD): https://www.cisco.com/c/en/us/td/docs/unified_computing/ucs/UCS_CVDs/flexpod_xseries_vmware_7u2.html (with minor changes). For configuring the remaing components of the FlexPod, following repository can be utilized: https://github.com/ucs-compute-solutions/FlexPod-UCSM-M6. In near future, a combined repository will be developed to configure all the components at the same time.

# Intersight Setup Requirement

The playbooks in this repository perform following functions:

1. Create various pools required to setup a Server Profile Template
2. Create various policies required to setup a Server Profile Template
3. Create iSCSI and/or FC Server Profile Templates

After successfully executing the playbooks, 1 or many server profiles can easily derived and attached to the compute node from Intersight dashboard.

NOTE: The addition of UCS to Intersight Account or configuration of Domain Profile to setup UCS is not part of this repository and will have to be performed manually. The playbooks assume an organization has already been setup under Intersight account as covered in the Cisco Validated Design.


# Execution Package Requirement

To execute the ansible playbooks for configuring IMM, a linux based system will need to be setup with ansible and following Ansible package needs to be installed:

https://galaxy.ansible.com/cisco/intersight?extIdCarryOver=true&sc_cid=701f2000001OH7YAAW

You might already have this collection installed. 

To check whether it is installed, run: ansible-galaxy collection list

To install it, use: ansible-galaxy collection install cisco.intersight.

# Intersight Access Requirement

To execute the playbooks against your Intersight account, you need to complete following additional steps of creating an API key and saving the Secrets_File:

https://community.cisco.com/t5/data-center-and-cloud-documents/intersight-api-overview/ta-p/3651994

The API key and Secrets_Filename information is added to the group_vars/all.yml. The default Secrets_File value in all.yml assumes Secrets_File was copied to the same folder/directory where Ansible Playbooks were cloned (alongside inventory file).


# Setting up Variables

All the variables used in this framework are defined in the following locations:

1. Variable that require customer inputs are part of group_vars/all.yml
2. Variable that do not typically require customer input (e.g. descriptions etc.) are present under role_name/defauls/main.yml.

NOTE: All pools and policies created using these playbooks are tagged with user_defined_prefix and "ansible" to easily filter the configuration.

# Post Configuration Tasks

Execution of the playbooks in these repositories sets up Server Profile Template. After successfully executing the playbooks, one or more server profiles can easily derived and attached to the compute node from Intersight dashboard. KVM mounted DVD option is available to install OS to these newly derived servers.


# Playbook Execution Commands - Summary

1. Setup various pools: "ansible-playbook ./create_pools.yml -i inventory"
2. Setup various policies: "ansible-playbook ./create_server_policies.yml -i inventory"
3. Setup Server Profile Template(s): "ansible-playbook ./create_server_profile_template.yml -i inventory"

