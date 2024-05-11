# Digital Twin Workshop

## Getting Started

1. Clone and enter the repo:
```
git clone https://github.com/model-driven-devops/digital-twin.git
cd digital-twin
```

2. Set the default environment variables:

```
. ./envvars
```

3. Create a virtual environment
- It is highly recommended that you create a virtual environment to make it easier to
install the dependencies without conflict.

```
python3 -m venv venv
. ./venv/bin/activate
```

4. Install the Python requirements via pip:

```
pip3 install -r requirements.txt
```

5. Reactivate the virtual environment
- Ensures your shell is using the newly installed ansible.

```
deactivate
. ./venv/bin/activate
```

6. Install the tooling and its Ansible dependencies via ansible-galaxy:

```
ansible-galaxy collection install -r requirements.yml
```

7. Set the following environment variables as appropriate for your environment:

```
export CML_HOST=your.cml.server
export CML_USERNAME=your_user
export CML_PASSWORD=your_pass
export CML_LAB=your_lab
export CML_VERIFY_CERT=false
```

8. Build the reference architecture in CML and start the nodes:

```
ansible-playbook cisco.cml.build -e startup=host -e wait=yes
```

9. Verify that all nodes have IP addresses:

```
ansible-playbook cisco.cml.inventory
```

10. Install NSO:
- Note: The task may fail to execute while waiting for host reachability. If so, ensure the 'sshpass' program is installed on your system.

```
ansible-playbook ciscops.mdd.nso_install
```


11. Update NSO packages:

```
ansible-playbook ciscops.mdd.nso_update_packages
```

12. Initialize NSO configuration:

```
ansible-playbook ciscops.mdd.nso_init
```

13. Add devices to NSO:

```
ansible-playbook ciscops.mdd.nso_update_devices
```

14. Get the IP address of NSO:

```
ansible-playbook cisco.cml.inventory --limit nso1
```

Browse to NSO using HTTP, the IP address of your NSO and port 8080.  Example: http://192.168.0.100:8080.  The default crendentials are ubuntu/admin.

Click on Device Manager and verify that n9kv1 and n9kv2 are configured in NSO.
