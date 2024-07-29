# HNG Stage 5B Deployment

## Overview

This project is an Ansible playbook to automate the deployment and configuration of the Stage 5B boilerplate application on an Ubuntu 22.04 server. The playbook performs the following tasks:

- Creates a user named `hng` with sudo privileges
- Clones the specified GitHub repository into `/opt/stage_5b`
- Installs PostgreSQL and saves the admin credentials
- Installs RabbitMQ and sets the default user password
- Configures Nginx to reverse proxy the application
- Sets up logging for stderr and stdout
- Installs necessary Node.js packages and runs the application

## Prerequisites

Ensure you have the following installed on your local machine:

- Ansible (installation instructions provided below)
- Git

## Installation

### Installing Ansible

To install Ansible, follow these steps:

1. Update your package index:

    ```bash
    sudo apt update
    ```

2. Install Ansible:

    ```bash
    sudo apt install ansible -y
    ```

3. Verify the installation:

    ```bash
    ansible --version
    ```

## Usage

### Preparing the Inventory

Create an `inventory.cfg` file in the same directory as `main.yaml` with the following content:

```ini
[hng]
localhost
```
## Running the Playbook
To run the playbook, navigate to the directory containing main.yaml and inventory.cfg, and execute the following command:

```
ansible-playbook main.yaml -i inventory.cfg -b
```

