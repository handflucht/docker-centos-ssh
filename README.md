
# General
A simple CentOS running an SSH-server.

You can use this container e.g. as an target for ansible.

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
