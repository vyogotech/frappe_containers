# Frappe v15 Container on RHEL 9

This repository contains a `Containerfile` for building an image to run Frappe v15 on a RHEL 9 base. The container includes all necessary dependencies such as Python, MariaDB, Redis, Node.js, and Nginx.

## Purpose

The purpose of this container file is to provide a consistent and reproducible environment for running Frappe v15 applications. It includes:

- Python 3.10.14
- MariaDB 10.6
- Redis
- Node.js 18
- Nginx
- Frappe v15 and ERPNext v15

## Building the Image

To build the image, follow these steps:

1. Clone the repository:
    ```sh
    git clone <repository-url>
    cd <repository-directory>
    ```

2. Build the image:
    ```sh
    podman build -t frappe-v15-rhel9 -f Containerfile.frappev15 .
    ```

## Starting the Container

To start the container, use the following command:

```sh
podman run -d --name frappe-v15-container -p 3306:3306 -p 6379:6379 -p 8000:8000 frappe-v15-rhel9
```

This command will run the container in detached mode and map the necessary ports for MariaDB, Redis, and Frappe.

## Exposed Ports

- `3306`: MariaDB
- `6379`: Redis
- `8000`: Frappe

## Services

The container includes the following services:

- MariaDB
- Redis
- Nginx
- Frappe Bench

These services are configured to start automatically when the container is launched.

## Configuration

The container uses the following configuration files:

- `frappe.conf`: Nginx configuration for Frappe
- `frappe-bench.service`: Systemd service file for Frappe Bench
- `common_site_config.json`: Common site configuration for Frappe

These files are added to the appropriate directories during the build process.

## Running Frappe Bench

The container is set up to run bench as systemctl services already. The working directory is `/home/frappe/frappe-bench`.

To interact with the Frappe Bench, you can exec into the running container:

```sh
podman exec -it frappe-v15-container /bin/bash
su frappe
bench new-site ....
```

From there, you can use the `bench` command to manage your Frappe applications.

## First time execution

Remember to secure the DB installation for the first time using the command 

`mariadb-secure-installation`

## Conclusion

This container provides a complete environment for running Frappe v15 on RHEL 9. It includes all necessary dependencies and services, making it easy to get started with Frappe development and deployment.
