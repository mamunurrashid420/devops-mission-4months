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
### Multi-stage Docker 
The idea is to separate build-time dependencies (compilers, SDKs, tools) from runtime dependencies, so the final image stays small, secure, and clean.
## Why do we need it:
1. Small final image size:
    - you might need compilers `node-modules` in your build time but you don't need it in your runtime
    - But in production, you only need the compiled output.
    - Multi-stage removes unnecessary stuff → final image is lightweight
2. Security:
    - Build tools, compilers, and secrets stay in the build stage.
    - Final image has only what’s needed to run → reduces attack surface
3. Faster build & deployment:
    - Smaller images are faster to push/pull.
    - Faster CI/CD pipelines and deployments.
### 🔹 Multi-Stage Build Examples
#### Golang app
```
# ---- Build Stage ----
FROM golang:1.21 AS builder

WORKDIR /app
COPY . .

# Build the binary
RUN go build -o myapp main.go

# ---- Runtime Stage ----
FROM alpine:3.18
WORKDIR /app
COPY --from=builder /app/myapp .

ENTRYPOINT ["./myapp"]
```
#### React/Next.js frontend with Nginx
```Dockerfile
# ---- Build Stage ----
FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# ---- Runtime Stage ----
FROM nginx:alpine
COPY --from=builder /app/build /usr/share/nginx/html
```
### Deep Dive Concepts
- Named Stages
    - AS builder lets you reference the stage later:
```
COPY --from=builder /app/build /usr/share/nginx/html
```
- Target Builds

    - You can build only up to a specific stage:
```
docker build --target builder -t myapp-builder .
```
## Witout Muti-stage
```
FROM node:latest
WORKDIR /app
COPY package*.json ./
RUN npm install 
COPY . .
RUN npm run build 
EXPOSE 3000 
CMD ["npm","run","start'] 
```

### multi-stage
```
FROM node:alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM node:alpine AS production
WORKDIR /app
COPY --from=builder /app/build /app/build
RUN npm install -g serve
EXPOSE 3000
CMD["serve","-s","build","-l","3000"]