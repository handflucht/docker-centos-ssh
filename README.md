
# General
Dockerized CentOS running a SSH-server.

You can use this container e.g. as a target for ansible.

# Build

```bash
podman build -t centos-ssh -f DOCKERFILE
```


# Run

```bash
podman run --privileged --rm -dP -v /sys/fs/cgroup:/sys/fs/cgroup:ro centos-ssh
```

# Connect

1. Get the port the service is running.
   ```bash
   podman port -l
   22/tcp -> 0.0.0.0:34505
   ```

2. Connect to the container
   ```bash
   ssh -o "StrictHostKeyChecking no" \
       -p 34505 root@127.0.0.1
   ```

3. Use password as defined in `DOCKERFILE`:  *pw*

# Ansible

If you want to process this container with ansible, add the following to the `inventory.txt`

```ini
[loc]
dockercent ansible_host=127.0.0.1 ansible_ssh_user=root ansible_ssh_pass=pw ansible_port=34505
```

Now you can provide `dockercent` as host, e.g. to the `ansible-playbook`-command. 

Also, you can start several containers, add them with a different name (e.g. `dockercent1`) and the new port and call the group `loc` to process all hosts.
