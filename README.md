# Ansible tasks for after a Kubernetes cluster has been deployed

This Ansible playbook contains tasks that retrieve the Kubernetes
configuration file and `kubectl` so you can control the Kubernetes cluster from
your computer.

# Usage
Put the host FQDN or IP address of a master system in the inventory file and
run the playbook:  

```sh
echo ec2-54-208-6-151.us-west-2.compute.amazonaws.com >> inventory
ansible-playbook playbook.yml
```

If you need to use a different key and/or user for the connection use this
command:  

```sh
ansible-playbook playbook.yml --ssh-common-args='-i /path/to/id_rsa.pub' -u user
```

If everything was successful you should be able to use the `kubectl` command to
control your cluster.

The Kubernetes configuration file may be configured to use internal IP
addresses and you should change the to use the external context.

```sh
kubectl config get-contexts  # Lists the contexts defined in the configuration.
kubectl config use-context default/ec2-54-208-6-151-us-west-2-compute-amazonaws-com:8443/system:admin
```
