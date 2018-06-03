create-digitalocean-droplet
=========

A role to spin up a DigitalOcean droplet and add a DNS entry to it so that is can be accessed at a given URL (`server_fqdn` variable). The role will add the newly created server to an Ansible group titled, "new_server" which is the host value you should use for applying any additional configuration in subsequent roles of the same playbook.

Requirements
------------

You need the following items in order to use this role.
	
	* DigitalOcean account
	* API Key for your DO account stored in an environment variable called "DO_API_TOKEN"
	* The nameservers for the root domain that you are adding (server_fqdn) must be pointed to DigitalOcean's name servers
	* Your SSH Keys uploaded into your DO account and the fingerprints (MD5 hashed value) stored into the (ssh_keys) variable list

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

`host_name: "my-hostname-here"`

The hostname of your DigitalOcean droplet. This will be what is set as the hostname on the Linux VPS as well as what shows up as the name in your list of droplets.

`server_fqdn: "mysubdomain.mydomain.com"`

The domain name entry that you would like to create a DNS entry for to have it direct to this newly created DigitalOcean droplet.


`do_token: "{{ lookup('env', 'DO_API_TOKEN') }}"`

An environment variable called DO_API_TOKEN that holds the value of your DigitalOcean API key.

```
ssh_key_ids:
  - "72:aa:ae:3a:62:4d:b4:3d:6a:c5:0f:17:f8:1f:ad:d2"
  - "e4:1d:b2:d1:e1:42:c7:5c:b6:71:75:2b:f4:8d:bf:c7"
```

A list of any SSH key fingerprints that correspond to the SSH key(s) that you have uploaded to your DO account and would like to add to this droplet as it is created in order to allow access. You can find these fingerprints by going into your DO account settings, then the Security tab and either adding a SSH key and copying the fignerprint or copying a fingerprint of an already uploaded SSH key.

`droplet_size: "1gb"`

The size of the droplet that you would like to create. The default size it 1gb.

`droplet_image: "ubuntu-16-04-x64"`

The droplet image that would like to use as the base image of your newly created DigitalOcean droplet. The default image is Ubuntu 16.04 LTS (ubuntu-16-04-x64)

`region: "nyc1"`

The DigitalOcean region (data center) where you would like to create your droplet. The default is "nyc1"


Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:


	- hosts: localhost ansible_connection=local ansible_python_interpreter=python
	  vars_files:
	    - vars/main.yml
	  roles:
	    - { role: stancel.create-digitalocean-droplet }


or 


	- hosts: localhost ansible_connection=local ansible_python_interpreter=python 
	  vars:
		host_name: "my-hostname-here"
		server_fqdn: "mysubdomain.mydomain.com"
		do_token: "{{ lookup('env', 'DO_API_TOKEN') }}"
		ssh_key_ids:
		  - "72:aa:ae:3a:62:4d:b4:3d:6a:c5:0f:17:f8:1f:ad:d2" 
		droplet_size: "1gb"
		droplet_image: "ubuntu-16-04-x64"
		region: "nyc1"



License
-------

BSD

Author Information
------------------

Brad Stancel
