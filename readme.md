packages used:
  - pymongo
  - requests
  - flask

docker-compose.yml:
```yml
version: "3.3"

services:
  mongo:
    image: mongo
    restart: unless-stopped
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: supersecretpassword
      MONGO_INITDB_DATABASE: shortner
  frontend:
    image: xedom/short.octafox.it
    restart: unless-stopped
    depends_on:
      - mongo
    environment:
      MONGODB_URI: mongodb://root:supersecretpassword@mongo:27017/
      MONGODB_DB: shortner
      DOMAIN_NAME: "http://localhost:8001"
    ports:
      - "8001:8001"
```
