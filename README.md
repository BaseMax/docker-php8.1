# Docker-PHP 8.1

![Docker](https://img.shields.io/docker/pulls/basemax/docker-php8.1) ![License](https://img.shields.io/github/license/BaseMax/docker-php8.1)

A production-ready Dockerfile for PHP 8.1 tailored specifically for WordPress or other PHP-based systems. This image includes a wide range of essential PHP extensions and tools like SourceGuardian and ionCube, widely used in the WordPress ecosystem.

## Features

- **PHP Version**: 8.1 (FPM Alpine)
- **Extensions**:
  - Core PHP extensions: `bcmath`, `bz2`, `calendar`, `curl`, `exif`, `fileinfo`, `ftp`, `gd`, `gettext`, `imagick`, `imap`, `intl`, `ldap`, `mbstring`, `mcrypt`, `memcached`, `mongodb`, `mysqli`, `opcache`, `pdo`, `pdo_mysql`, `redis`, `soap`, `sodium`, `sysvsem`, `sysvshm`, `xmlrpc`, `xsl`, `zip`
  - Advanced debugging tools: `xdebug`
  - Profiling support: `xhprof`
- **PHP Encryption Support**:
  - ionCube Loader
  - SourceGuardian
- **Additional Tools**:
  - [Composer](https://getcomposer.org/)
  - [WP-CLI](https://wp-cli.org/)
- **Optimizations**:
  - OPCache configuration for performance
- **Base OS**: Alpine Linux (lightweight and secure)

## Installation

### Prerequisites

- [Docker](https://www.docker.com/products/docker-desktop) installed on your system.

### Pull the Image

Pull the pre-built image from Docker Hub (replace `your-dockerhub-repo` with your repository, if published):

```bash
# Pull the image
docker pull basemax/docker-php8.1
```

---

## Usage

### Basic Usage

Run the container:

```bash
docker run -d \
  -v $(pwd):/var/www/html \
  -p 9000:9000 \
  --name php-fpm-basemax \
  basemax/docker-php8.1
```

### Docker Compose Example

Here’s an example `docker-compose.yml` file for use with this Docker image and Nginx:

```yaml
services:
  php:
    image: basemax/docker-php8.1
    volumes:
      - .:/var/www/html
    ports:
      - "9000:9000"

  nginx:
    image: nginx:alpine
    volumes:
      - .:/var/www/html
      - ./nginx.conf:/etc/nginx/conf.d/default.conf
    ports:
      - "8080:80"
    depends_on:
      - php
```

Start the services:

```bash
docker-compose up -d
```

### OPCache Configuration

The Dockerfile includes optimized OPCache settings. If you need to modify them, edit the configuration file located in `/usr/local/etc/php/conf.d/docker-php-ext-opcache.ini`.

## PHP Tools

### Composer

Composer is pre-installed and available globally.

```bash
composer --version
```

### WP-CLI

WP-CLI is pre-installed for managing WordPress installations.

```bash
wp --info
```

### SourceGuardian and ionCube Loader

These popular encryption tools are included and pre-configured.

## Example for WordPress Setup

### Step 1: Create a `docker-compose.yml` file

Use the Docker Compose example above and adjust paths as needed.

### Step 2: Download WordPress
Download WordPress to your project directory:

```bash
curl -O https://wordpress.org/latest.tar.gz
```

### Step 3: Start the Environment

Run the containers:

```bash
docker-compose up -d
```

Access your WordPress site at `http://localhost:8080`.

## Customization

### Adding More Extensions

Use the `install-php-extensions` script to install additional extensions:

```Dockerfile
RUN install-php-extensions <extension-name>
```

### Changing User Permissions

By default, the `www-data` user and group IDs are set to `1000` for compatibility with host systems. Adjust as needed:

```bash
usermod -u <UID> www-data
groupmod -g <GID> www-data
```

## Support

For issues or feature requests, please open an issue on the [GitHub repository](https://github.com/BaseMax/docker-php8.1/issues).

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request.

## Disclaimer

This image is provided as-is without warranty. Please test thoroughly before using in production environments.

## License

This project is licensed under the [MIT License](LICENSE).

https://github.com/mlocati/docker-php-extension-installer
