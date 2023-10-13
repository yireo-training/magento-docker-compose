# Basic docker-compose for Magento

Copy files to some local folder. Navigate to folder and then run:

```bash
docker-compose up -d
docker-compose ps

mkdir -p src/
```

Note that the Nginx container will fail because of a missing configuration file. First proceed with
installing Magento 2 into the `src/` folder.

## Install Magento 2 sources into src/
Login into the PHP-FPM container (assuming that the name of the PHP-FPM container is `magento-docker-compose_php-fpm_1`):
```bash
docker exec -it magento-docker-compose_php-fpm_1 bash
```

Within the PHP-FPM container, run the following:
```bash
cd /var/www/html/
composer create-project --repository-url=https://repo.mage-os.org/ mage-os/project-community-edition .
```

## Fix Nginx configuration
Next, fix the Nginx configuration (on your host):
```bash
cd src/
cp nginx.conf.sample nginx.conf
docker-compose up -d
docker-compose ps
```

## Magento database configuration

