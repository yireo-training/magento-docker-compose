# Basic docker-compose for Magento

Copy files to some local folder. Navigate to folder and then run:

```bash
docker-compose up -d
docker-compose ps
```

Note that the Nginx container will fail because of a missing configuration file. First proceed with
installing Magento 2 into the `src/` folder.
