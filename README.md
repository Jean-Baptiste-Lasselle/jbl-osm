# jbl-osm
pour reprendre une idée placée dans un glaçon


## Pour le faire fondre

[Source](https://stackoverflow.com/questions/45494746/docker-compose-volumes-from-usage-example)


As documentation said volumes if you are in version 3 you can use The top-level volumes to define a named volume as db-data ee code below and you can reference it in every services something like this:
```yaml
version: "3"

services:

  web:
    nginx:alpine
    ports:
    - "80:80"

  postgres:
    image: postgres:9.4
    volumes:
      - db-data:/var/lib/db

  backup:
    image: postgres:9.4
    volumes:
      - db-data:/var/lib/backup/data

  redis:
    image: redis
    ports:
      - "6379:6379"
    volumes:
      - ./data:/data

volumes:
  db-data:

    version 2.0:
```
volumes_from allow you mount all data or volume from another service or container, you have to specify the access level how documentation said volumes from in your code you can use something like this:
```yaml
version: "2"

services:
  web:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes_from:
      - redis:rw
  postgres:
    image: postgres:9.4
    volumes:
      - /data/webapp
  backup:
    image: postgres:9.4
    volumes:
      - /var/lib/backup/data

  redis:
    image: redis
    ports:
      - "6379:6379"
    volumes:
      - /data/db
```
To code above reddis define a volume services and then you can use in another container for example web with volumes_from look like web service use that volume service specify access level to read and write
