# OpenMRS to OMOP ETL Workgroup Database

This repository contains a Docker setup for a pre-configured OpenMRS database with 250 sample patients, ready for use in the OpenMRS to OMOP ETL Workgroup.

## Prerequisites

### Installing Docker

<details>
<summary>mac OS</summary>


1. **Manual Installation:**
   - Download Docker Desktop from [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
   - Install and launch Docker Desktop
   - Ensure Docker is running (you should see the Docker icon in your menu bar)
2. Or ** Using Homebrew:**
   ```bash
   brew install --cask docker
   ```
   Then launch Docker Desktop from Applications.
</details>

<details>
<summary>Windows</summary>

1. Download Docker Desktop from [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
2. Install and launch Docker Desktop
3. Ensure WSL 2 is enabled if prompted
</details>

<details>
<summary>Linux (Ubuntu/Debian)</summary>


```bash
# Update package index
sudo apt-get update

# Install prerequisites
sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release

# Add Docker's official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Add Docker repository
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

# Start Docker service
sudo systemctl start docker
sudo systemctl enable docker

# Add your user to docker group (optional, to avoid sudo)
sudo usermod -aG docker $USER
```

</details>

## Quick Start

### 1. Clone the Repository or just click code > download zip option in the repo
```bash
git clone https://github.com/jayasanka-sack/etl-deep-dive-omrs-db
cd etl-deep-dive-omrs-db
```

### 2. Start the Database Container
```bash
docker compose up -d
```

This command will:
- Pull the MariaDB 10.11.7 image
- Create and start a container with the OpenMRS database
- Initialize the database with 250 sample patients
- Make the database accessible on port 3307

### 3. Verify the Container is Running
```bash
docker compose ps
```

You should see the `db` service running with status "Up".

### 4. Check Container Logs (Optional)
```bash
docker compose logs db
```

## Database Connection Details

- **Host:** `localhost` (or `127.0.0.1`)
- **Port:** `3307`
- **Database:** `openmrs`
- **Username:** `openmrs`
- **Password:** `openmrs`
- **Root Password:** `openmrs`


## Container Management

### Stop the Container
```bash
docker compose down
```

### Stop and Remove Data Volumes
```bash
docker compose down -v
```

## Database Features

- **MariaDB 10.11.7** with UTF-8 support
- **250 pre-loaded patients** with realistic medical data
- **OpenMRS-compatible schema** ready for ETL development
- **Persistent data storage** using Docker volumes
- **Health checks** to ensure database availability

## Troubleshooting

### Port Already in Use
If port 3307 is already in use, you can modify the port mapping in `docker-compose.yml`:
```yaml
ports:
  - "3308:3306"  # Change 3307 to any available port
```

### Container Won't Start
1. Check if Docker is running: `docker --version`
2. Check container logs: `docker compose logs db`
3. Ensure no other services are using the required ports

### Database Connection Issues
1. Verify the container is running: `docker compose ps`
2. Check the health status: `docker compose ps --format "table {{.Name}}\t{{.Status}}"`
3. Ensure you're using the correct port (3307)

