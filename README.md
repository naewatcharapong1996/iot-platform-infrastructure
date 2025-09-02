# Factory Platform - Authentication Infrastructure

A Docker-based Zitadel authentication service for the Factory Platform IoT management system.

## 🚀 Quick Start

### Prerequisites

- Docker Desktop installed and running
- Git installed

### Setup & Run

1. **Clone and navigate to the project**:

   ```bash
   git clone <your-repo-url>
   cd iot-platform-infrastructure
   ```

2. **Start the services**:

   ```bash
   docker-compose up -d
   ```

3. **Wait for initialization** (first startup takes 2-3 minutes)

4. **Access Zitadel Console**:
   - URL: http://localhost:8080/ui/console
   - Login: `admin@factory-platform.localhost`
   - Password: `P@ssw0rd`

## 🔧 Services

| Service             | URL                              | Purpose            |
| ------------------- | -------------------------------- | ------------------ |
| **Zitadel Console** | http://localhost:8080/ui/console | Admin interface    |
| **Zitadel API**     | http://localhost:8080            | Authentication API |
| **PostgreSQL**      | localhost:5432                   | Database           |

## 📋 Verification

Check if all services are running:

```bash
# View service status
docker-compose ps

# Check Zitadel health
curl http://localhost:8080/debug/ready

# View logs (if needed)
docker-compose logs zitadel
```

## 🛠 Configuration

The setup uses the following key configuration:

- **Organization**: Factory Platform
- **External Domain**: localhost
- **Database**: PostgreSQL 17 Alpine
- **TLS**: Disabled for local development

## 🔑 Default Credentials

- **Admin User**: admin@factory-platform.localhost
- **Password**: P@ssw0rd
- **Database**: postgres/postgres

## 📁 Project Structure

```
iot-platform-infrastructure/
├── docker-compose.yml    # Main Docker Compose configuration
├── .env                  # Environment variables
├── .env.example         # Environment template
└── README.md            # This file
```

## 🚦 Management Commands

```bash
# Start services
docker-compose up -d

# Stop services
docker-compose down

# View logs
docker-compose logs -f zitadel

# Restart services
docker-compose restart

# Clean up (removes all data)
docker-compose down -v
```

## 🔄 Next Steps

1. **Create Applications**: Use the console to create frontend/backend applications
2. **Configure OIDC**: Set up OAuth2/OIDC clients for your applications
3. **Brand Customization**: Apply factory-themed branding
4. **User Management**: Create additional users and organizations

## 🌐 External Access

For production deployment or external access, you'll need to:

1. Set `ZITADEL_EXTERNAL_DOMAIN` to your actual domain
2. Set `ZITADEL_EXTERNAL_SECURE=true` for HTTPS
3. Configure proper SSL certificates
4. Update redirect URLs in your applications

## 🐛 Troubleshooting

### Services won't start

- Ensure Docker Desktop is running
- Check if ports 8080, 5432 are available
- Verify .env file has correct 32-character master key

### Can't access console

- Wait for full initialization (2-3 minutes on first run)
- Check `docker-compose logs zitadel` for errors
- Verify health endpoint: `curl http://localhost:8080/debug/ready`

### Login issues

- Use full login format: `admin@factory-platform.localhost`
- Check if user exists: Connect to PostgreSQL and run:
  ```sql
  SELECT * FROM projections.login_names3;
  ```

## 📚 Documentation

- [Zitadel Documentation](https://zitadel.com/docs)
- [Docker Compose Guide](https://zitadel.com/docs/self-hosting/deploy/compose)
- [OIDC Configuration](https://zitadel.com/docs/guides/integrate/oauth-oidc)
