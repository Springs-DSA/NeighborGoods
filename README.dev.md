# NeighborGoods Development Setup

## Prerequisites
- Docker
- Docker Compose
- Git

## Getting Started

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd neighborgoods
   ```

2. Start the development server:
   ```bash
   docker compose up --build
   ```

3. Access the application:
   - Web Interface: http://localhost:8080
   - Proxy Service: http://localhost:7156

## Development Notes

- The application code is mounted at `/app` inside the container
- Changes to Python files will require a container restart: `docker compose restart`
- Data is persisted in the `neighborgoods_data` Docker volume
- Logs can be viewed with: `docker compose logs -f`

## Common Tasks

### Rebuilding the Container
```bash
docker compose build --no-cache
```

### Resetting Data
```bash
docker compose down -v
docker compose up --build
```

### Accessing the Container Shell
```bash
docker compose exec neighborgoods /bin/bash
```

## Troubleshooting

1. If port 8080 is in use:
   - Edit docker-compose.yml and change the port mapping
   - Example: `"8081:80"`

2. If changes aren't reflecting:
   - Ensure files are being mounted correctly
   - Restart the container: `docker compose restart`

3. Permission issues:
   - The container runs as the epicyon user
   - Ensure local files are readable by the container user

## Development Environment

The development setup includes:
- Live code mounting for quick development
- Persistent data volume for maintaining state
- Python output unbuffered for immediate logging
- Exposed ports 8080 (web) and 7156 (proxy)
- Automatic container restart on failure

## Data Persistence

The setup uses a named Docker volume (`neighborgoods_data`) to persist data between container restarts. This includes:
- User data
- Configuration files
- Uploaded media

To completely reset your development environment, you can remove this volume using:
```bash
docker compose down -v
