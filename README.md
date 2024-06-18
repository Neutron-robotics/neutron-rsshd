# neutron-rsshd

[![Docker Image Version (tag latest semver)](https://img.shields.io/docker/v/hugoperier/rsshd?sort=semver)](https://hub.docker.com/r/hugoperier/rsshd)

A minimal Docker container derived from [efrecon/rsshd](https://github.com/efrecon/rsshd) designed to maintain connections to remote servers hidden behind NATed networks. This lightweight image simplifies the creation of reverse SSH tunnels between your server (neutron-robotics.com) and client devices not directly accessible from the internet.

## Features

* **Dockerized sshd:** Based on Alpine Linux for a small footprint.
* **Reverse SSH Tunneling:** Securely connect to devices behind NAT.
* **Environment Variable Configuration:** Customize behavior with ROOT_PASSWORD, NEUTRON_PASSWORD, KEYS, and LOCAL variables.

## How It Works

1. Remote servers initiate reverse SSH tunnels to the host running this Docker container.
2. You can then log into the remote servers through the reverse tunnels, using the host as a gateway.

## Usage

### 1. Build the Docker Image

```bash
docker build -t hugoperier/neutron-rsshd:latest .
```

### 2. Push the Image to Docker Hub (Optional)

```bash
docker push docker push hugoperier/neutron-rsshd:latest
```

### 3. Deploy with Docker Compose

```bash
docker-compose up -d
```

## Environment Variables

* **ROOT_PASSWORD:** The password for the 'root' user within the container. If not provided, a random password will be generated on startup.
* **NEUTRON_PASSWORD:** The password for the 'neutron' user, used exclusively for establishing reverse SSH tunnels. This user has no shell access or other permissions.
* **KEYS:** (Internal) The location where host keys are stored.
* **LOCAL:** Set to '1' to restrict access to tunnels from outside the container. Default is '0' (tunnels accessible from outside).

### Security Notice

**Keep the ROOT_PASSWORD secret!** This password grants direct SSH access to the container and potentially the entire network connected to it.

## Additional Notes

* Make sure to adjust the port range in the `docker-compose.yml` file to fit your requirements.
* For detailed configuration and troubleshooting, refer to the original [rsshd documentation](https://github.com/efrecon/rsshd).

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
