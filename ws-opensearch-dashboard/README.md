# Whale Sentinel OpenSearch Dashboard

This repository contains the Docker Compose setup for running OpenSearch and OpenSearch Dashboards, which are used for managing and visualizing data in the Whale Sentinel project.

---

## Prerequisites

1. **Docker**: Ensure Docker is installed on your system. You can download it from [Docker's official website](https://www.docker.com/).
2. **Docker Compose**: Ensure Docker Compose is installed. It is typically bundled with Docker Desktop.

---

## Services

### 1. **OpenSearch Dashboards**
- **Image**: `opensearchproject/opensearch-dashboards:latest`
- **Container Name**: `opensearch-dashboards`
- **Port**: `5601` (accessible at `http://localhost:5601`)
- **Environment Variables**:
  - `OPENSEARCH_HOSTS`: Specifies the OpenSearch instance to connect to (`https://ws-opensearch-db:9200`).

### 2. **OpenSearch Database**
- **Image**: `opensearchproject/opensearch:latest`
- **Container Name**: `opensearch-db`
- **Ports**:
  - `9200`: OpenSearch API (accessible at `http://localhost:9200`).
  - `9600`: OpenSearch performance monitoring.
- **Environment Variables**:
  - `discovery.type`: Set to `single-node` for local development.
  - `plugins.security.disabled`: Set to `"false"` to enable security.
  - `OPENSEARCH_INITIAL_ADMIN_PASSWORD`: Set the initial admin password for OpenSearch.

---

## Network

- **Network Name**: `whale-sentinel-controller-network`
- **Driver**: `bridge`
- **Subnet**: `172.24.0.0/16`

---

## Usage

### 1. **Create new docker-compose**
```
cp docker-compose.example.yml docker-compose.yml
```

### 2. **Start the Services**
Run the following command to start the services:
```bash
docker-compose -f docker-compose.yml up -d
```

### 3. **Stop the Services**
To stop the services, run:
```bash
docker-compose -f docker-compose.yml down
```

### 4. **Access OpenSearch Dashboards**
Open your web browser and go to `http://localhost:5601` to access OpenSearch Dashboards.

### 5. **Access OpenSearch API**
You can access the OpenSearch API at `http://localhost:9200`.

---

## Configuration

OpenSearch Dashboards

- The OPENSEARCH_HOSTS environment variable specifies the OpenSearch instance that Dashboards will connect to. Update it if your OpenSearch instance is hosted elsewhere.

OpenSearch

- The OPENSEARCH_INITIAL_ADMIN_PASSWORD environment variable sets the initial admin password. Replace your-opensearch-password with a secure password.
Notes

---

## Troubleshooting

OpenSearch Dashboards Not Connecting:

- Ensure the OPENSEARCH_HOSTS variable in the docker-compose.example.yml file points to the correct OpenSearch instance.

Port Conflicts:

- If ports 5601, 9200, or 9600 are already in use, update the ports section in the docker-compose.example.yml file.

Logs:

- View logs for debugging:

```bash
docker logs opensearch-db
docker logs opensearch-dashboards
```

---

# License

This setup uses the OpenSearch and OpenSearch Dashboards images provided by the OpenSearch Project. For more information, visit OpenSearch.

---

## Notes

- Ensure that the ports `5601`, `9200`, and `9600` are not in use by other applications on your host machine.
- For production deployments, consider using Docker volumes for data persistence and configuring backups for the OpenSearch database.
- Security: By default, security is enabled for OpenSearch. Ensure you configure the appropriate credentials for production environments.
- Local Development: This setup is optimized for local development. For production, consider using a multi-node OpenSearch cluster and enabling TLS.


