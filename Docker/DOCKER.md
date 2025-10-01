### Mongo-install 
```
docker run -d --name mongodb --network my-network -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password -v mongo-data:/data/db_mongo:latest
```

### Mongo-express-install
```
docker run -d --name mongo-express --network my-network -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password -e ME_CONFIG_MONGODB_SERVER=mongodb -e ME_CONFIG_BASICAUTH_USERNAME=admin -e ME_CONFIG_BASICAUTH_PASSWORD=pass123 -p 8081:8081 mongo-express:latest
```

## If I am using bind mount volume 
- `mkdir mongo-data`
- cd  mongo-data
- pwd

```
docker run -d --name mongodb --network my-network -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password -v /home/ubuntu/mongo-data:/data/db_mongo:latest
```
