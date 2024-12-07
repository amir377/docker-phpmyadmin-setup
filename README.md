
# Docker phpMyAdmin Setup

This repository provides a simple solution for deploying phpMyAdmin using Docker. It includes scripts and configuration files to automate the setup process for accessing phpMyAdmin in a Dockerized environment connected to an existing MySQL database.

## Features

1. **Quick Setup**: Deploy phpMyAdmin quickly with minimal configuration.
2. **Customizable Ports**: Access phpMyAdmin via a user-defined port.
3. **Network Integration**: Connect phpMyAdmin to your existing Docker network for seamless integration with MySQL.
4. **Environment File Support**: Configure phpMyAdmin parameters via a `.env` file.

## Prerequisites

- Docker must be installed and running on your system.
- Docker Compose must be installed.
- Git must be installed and available in your system's PATH.
  ```bash
  sudo apt install git       # For Debian/Ubuntu
  sudo yum install git       # For CentOS/RHEL
  brew install git           # For macOS
  ```
- **Linux Only**: Ensure `dos2unix` is installed to handle line ending conversions if needed.
  ```bash
  sudo apt install dos2unix
  ```

## Installation Steps

### One Command Install and Clone

#### Windows

Open PowerShell as Administrator and run:
```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass; git clone https://github.com/amir377/docker-phpmyadmin-setup; cd docker-phpmyadmin-setup; ./install.ps1
```

#### Linux/Mac

Run the following command in your terminal:
```bash
git clone https://github.com/amir377/docker-phpmyadmin-setup && cd docker-phpmyadmin-setup && dos2unix install.sh && chmod +x install.sh && ./install.sh
```

## Manual Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/amir377/docker-phpmyadmin-setup.git
   cd docker-phpmyadmin-setup
   ```

2. Place your `docker-compose.example.yaml` file in the root directory (if not already provided).

3. Run the appropriate installation script:
    - For Windows: `install.ps1`
    - For Linux/Mac: `install.sh`

4. Follow the prompts to customize your setup:
    - Container name
    - Network name
    - phpMyAdmin port
    - MySQL service name

## File Descriptions

### `install.ps1`

Automates the setup process for Windows, including:

- Generating `.env` and `docker-compose.yaml` files.
- Ensuring Docker and Docker Compose are installed.
- Creating the specified Docker network.
- Building and starting the phpMyAdmin container.

### `install.sh`

Automates the setup process for Linux/Mac, including:

- Generating `.env` and `docker-compose.yaml` files.
- Ensuring Docker and Docker Compose are installed.
- Creating the specified Docker network.
- Building and starting the phpMyAdmin container.

### `.env`

Holds configuration values for the phpMyAdmin container. Example:

```env
# PMA container settings
CONTAINER_NAME=phpmyadmin
PMA_HOST=db
PMA_PORT=80
NETWORK_NAME=general
ALLOW_HOST=0.0.0.0
```

### `docker-compose.example.yaml`

A template file for the `docker-compose.yaml` file. Placeholders are dynamically replaced with values from the `.env` file. Example:

```yaml
services:
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: ${CONTAINER_NAME}
    environment:
      PMA_HOST: ${PMA_HOST}
    ports:
      - "${ALLOW_HOST}:${PMA_PORT}:80"
    networks:
      - ${NETWORK_NAME}

networks:
  ${NETWORK_NAME}:
    external: true
```

### `docker-compose.yaml`

Generated file used to deploy the phpMyAdmin container with Docker Compose.

## Usage

### Accessing phpMyAdmin

- Access phpMyAdmin in your browser at `http://127.0.0.1:<PMA_PORT>`.
- Log in using your MySQL credentials.

### Viewing Logs

If the container fails to start, the script will display logs automatically:

```bash
docker logs <container-name>
```

### Accessing the Container Shell

If you need to access the phpMyAdmin container shell:

```bash
docker exec -it <container-name> bash
```

## Notes

- Ensure Docker is running before executing the script.
- If you encounter permission issues, run PowerShell or Bash as Administrator.
- Update the `docker-compose.example.yaml` file to suit your specific requirements.

## License

This project is licensed under the MIT License. See the LICENSE file for details.

---

Feel free to customize the script or template files to fit your specific use case!
