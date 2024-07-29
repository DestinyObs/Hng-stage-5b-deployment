# HNG Stage 5b Deployment

This repository contains an Ansible playbook to set up the environment for the HNG Stage 5b project. The playbook installs necessary packages, sets up PostgreSQL and RabbitMQ, configures Nginx, and deploys the application using PM2.

## Prerequisites

Ensure that Ansible is installed on your control node. You can install Ansible using the following steps:

### Installing Ansible

1. **Update the package list**:
   ```bash
   sudo apt update
   ```

2. **Install Ansible**:
   ```bash
   sudo apt install ansible -y
   ```

3. **Verify Ansible installation**:
   ```bash
   ansible --version
   ```

## Inventory Configuration

Create an `inventory.cfg` file in the root of the project directory. This file should contain the IP address or hostname of the target server(s).

Example `inventory.cfg`:
```ini
[hng]
your_server_ip_or_hostname ansible_user=your_username ansible_password=your_password
```

Replace `your_server_ip_or_hostname`, `your_username`, and `your_password` with your server's details.

## Running the Playbook

To run the playbook, use the following command:
```bash
ansible-playbook main.yaml -i inventory.cfg
```

## Playbook Tasks

The playbook performs the following tasks:

1. **Install Node.js and npm**:
   - Installs Node.js and npm on the target machine.

2. **Create hng user with sudo privileges**:
   - Creates a user named `hng` and adds it to the `sudo` group.

3. **Ensure /opt directory exists**:
   - Creates the `/opt` directory if it doesn't exist.

4. **Change ownership of /opt directory**:
   - Sets `hng` as the owner of the `/opt` directory.

5. **Create destination directory for cloning**:
   - Creates the `/opt/stage_5b` directory for cloning the repository.

6. **Add /opt/stage_5b as a safe directory for Git**:
   - Configures Git to treat `/opt/stage_5b` as a safe directory.

7. **Clone the DevOps branch of the repository**:
   - Clones the repository into the `/opt/stage_5b` directory.

8. **Install PostgreSQL**:
   - Installs PostgreSQL on the target machine.

9. **Ensure PostgreSQL service is running**:
   - Starts and enables the PostgreSQL service.

10. **Create PostgreSQL database**:
    - Creates a PostgreSQL database named `boilerplate_db`.

11. **Ensure /var/secrets directory exists**:
    - Creates the `/var/secrets` directory and sets appropriate permissions.

12. **Save PostgreSQL credentials**:
    - Stores PostgreSQL credentials in a file.

13. **Install RabbitMQ**:
    - Installs RabbitMQ on the target machine.

14. **Set RabbitMQ default user and password**:
    - Configures RabbitMQ user credentials.

15. **Install Nginx**:
    - Installs Nginx on the target machine.

16. **Ensure Nginx directories exist**:
    - Creates necessary Nginx directories.

17. **Configure Nginx**:
    - Sets up Nginx configuration to proxy requests to the application.

18. **Enable Nginx configuration**:
    - Enables the Nginx configuration by creating a symlink.

19. **Remove default Nginx configuration**:
    - Removes the default Nginx configuration.

20. **Restart Nginx**:
    - Restarts the Nginx service.

21. **Ensure /var/log/stage_5b directory exists**:
    - Creates the `/var/log/stage_5b` directory for logging.

22. **Set up logging for stderr and stdout**:
    - Configures rsyslog to handle application logs.

23. **Install PM2 globally**:
    - Installs PM2 globally using npm.

24. **Install NestJS CLI globally**:
    - Installs the NestJS CLI globally using npm.

25. **Install project dependencies**:
    - Installs project dependencies specified in the `package.json` file.

26. **Build the application**:
    - Builds the application using npm.

27. **Run the application in production using PM2**:
    - Starts the application with PM2, configuring logging to `/var/log/stage_5b`.

## Repository Structure

- `main.yaml`: The main Ansible playbook.
- `inventory.cfg`: Sample inventory configuration file NOt added.
- `README.md`: Documentation for the project.
