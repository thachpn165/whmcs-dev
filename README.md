# WHMCS Docker Development Environment

This repository provides a ready-to-use Docker-based development environment for [WHMCS](https://www.whmcs.com/). It includes pre-configured containers for Nginx, PHP-FPM, and MariaDB, making it easy to get started with WHMCS development on your local machine.

## Project Structure

```
.
├── docker-compose.yml      # Docker Compose configuration
├── nginx/
│   ├── conf.d/
│   │   └── default.conf    # Nginx virtual host configuration (HTTP/HTTPS)
│   └── certs/              # SSL certificates (self-signed by default)
├── php/
│   └── custom.ini          # Custom PHP configuration
├── whmcs/                  # Place your WHMCS source code here
└── .gitignore
```

## Services

- **nginx**: Serves as the web server, configured for both HTTP (port 280) and HTTPS (port 2443). Uses configs from `nginx/conf.d` and SSL certs from `nginx/certs`.
- **php**: Runs PHP-FPM 8.2 (Bitnami), with custom settings and extensions enabled via `php/custom.ini`.
- **mariadb**: Provides a MariaDB 10.6 database with default credentials for development.

## Usage

### 1. Clone the Repository

```bash
git clone <this-repo-url>
cd whmcs-dev
```

### 2. Add WHMCS Source Code

Place your WHMCS files inside the `whmcs/` directory.

### 3. Start the Environment

```bash
docker-compose up -d
```

- Nginx will be available at [http://localhost:280](http://localhost:280) and [https://localhost:2443](https://localhost:2443).
- MariaDB will be accessible internally as `mariadb` with:
  - Database: `whmcs`
  - User: `whmcs_user`
  - Password: `whmcs_pass`
  - Root Password: `whmcs_root_pass`

### 4. Customization

- **Nginx**: Edit `nginx/conf.d/default.conf` for server settings.
- **PHP**: Edit `php/custom.ini` to change PHP extensions or settings.
- **SSL**: Replace the self-signed certificates in `nginx/certs` as needed.

### 5. Stopping the Environment

```bash
docker-compose down
```

## Notes

- This setup is intended for development only. Do not use the default credentials or self-signed certificates in production.
- Make sure to place valid WHMCS files in the `whmcs/` directory before starting the containers. 