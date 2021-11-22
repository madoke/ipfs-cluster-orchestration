# IPFS Cluster Orchestration

A collection of ansible playbooks to build an IPFS cluster setup with TLS termination for the Gateway, UI and HTTP API.

## Playbooks

- `ipfs-cluster.yml`: Installs and configures the `ipfs` and `ipfs-cluster` daemons
- `certbot.yml`: Installs and configures TLS certificates for any number of hosts
- `nginx.yml`: Installs and configures nginx
- `nginx-config.yml`: Creates the virtual hosts on nginx to expose the HTTP Gateway and the Web UI
- `main.yml`: Executes all of the above playbooks in sequence

## Setting up

- Configure the hostnames/addresses for all the nodes in the cluster in `env/ipfs/hosts.yml` (replace `ipfs-node-x` with your values)
- Generate an IPFS Secret and replace the placeholders in `env/ipfs/host_vars/**.yml` as well as `env/ipfs/group_vars/ipts_cluster.yml` with your values. (Refer to [Ansible IPFS Cluster](https://github.com/hsanjuan/ansible-ipfs-cluster) for info on how to get those values)
- Add any number of users to the variable `ipfs_cluster_restapi_users` in `env/ipfs/group_vars/ipts_cluster.yml` 
- Replace the value in `env/ipfs/group_vars/all/common.yml` with your domain name for the TLS certificate.
- Create a new file in `env/ipfs/group_vars/all` and declare the `ipfs_nginx_htpasswd`, `ipfs_nginx_username` and `ipfs_nginx_password` with values of your choosing. make sure to add that file to gitignore

## How to run

### Installing everyting in one go

```bash
ansible-playbook -i env/ipfs-cluster main.yml
```

### Running specific playbooks

```bash
ansible-playbook -i env/ipfs-cluster main.yml --tags nginx
```