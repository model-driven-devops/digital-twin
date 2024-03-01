# Digital Twin Workshop

## Getting Started

First, clone and enter the repo:
```
git clone https://github.com/model-driven-devops/digital-twin.git
cd digital-twin
```

Set the default environment variables:

```
. ./envvars
```

Next, it is highly recommended that you create a virtual environment to make it easier to
install the dependencies without conflict:

```
python3 -m venv venv
. ./venv/bin/activate
```

Next, install the Python requirements via pip:
```
pip3 install -r requirements.txt
```

Reactivate virtual environment to ensure your shell is using the newly installed ansible.  
```
deactivate
. ./venv/bin/activate
```

To install the tooling and its Ansible dependencies, use ansible-galaxy:

```
ansible-galaxy collection install -r requirements.yml
```

Set the following environment variables as appropriate for your environment:

```
export CML_HOST=your.cml.server
export CML_USERNAME=your_username
export CML_PASSWORD=your_password
export CML_LAB=your_lab_name
export CML_VERIFY_CERT=false
```

Built the reference architecture in CML and start the nodes:

```
ansible-playbook cisco.cml.build -e startup=host -e wait=yes
```

Verify that all nodes have IP addresses:

```
ansible-playbook cisco.cml.inventory
```

Install NSO:

```
ansible-playbook ciscops.mdd.nso_install
```

Update NSO packages:

```
ansible-playbook ciscops.mdd.nso_update_packages
```

Initialize NSO configuration:

```
ansible-playbook ciscops.mdd.nso_init
```

Add devices to NSO:

```
ansible-playbook ciscops.mdd.nso_update_devices
```

Get the IP address of NSO:

```
ansible-playbook cisco.cml.inventory --limit nso1
```

Browse to NSO using HTTP, the IP address of your NSO and port 8080.  Example: http://192.168.0.100:8080.  The default crendentials are ubuntu/admin.

Click on Device Manager and verify that n9kv1 and n9kv2 are configured in NSO.