# Dockerfile – Golang Multi-Stage Build

I created this Dockerfile to containerize a Go-based microservice (`product-catalog`) in a clean, efficient, and production-ready way using a multi-stage build. Worked inside the `ultimate-devops-project-demo/src/product-catalog` directory because its `README.md` provides build and operational instructions relevant for DevOps engineers. These include how to compile the Go binary, set environment variables, and run the service locally or inside a container.


### Goals:

- Automate the build process using Docker
- Keep the final image small and secure using Alpine
- Standardize how the service is built and run across environments
- Follow DevOps best practices and enable CI/CD integration

---
## Step-by-Step Summary with Commands

### 1. Connected to the EC2 instance
`ssh -i /home/shellesty/devops-demo.pem ubuntu@public-ip`

Used the .pem file to SSH into the EC2 instance.
### 2. Navigated to the Go application directory (which contains DevOps instructions)

`cd ultimate-devops-project-demo/src/product-catalog`

This folder contains the Go code and a README.md with the required instructions for building and running the service.
### 3. Removed existing Dockerfile and binary

`rm -rf Dockerfile
rm -rf product-catalog`

Cleaned up any old Dockerfile and compiled binaries to start fresh.
### 4. Created a new Dockerfile

`vim Dockerfile`

Opened the file to write the Dockerfile using a multi-stage build approach.
### 5. Wrote Dockerfile script and built the Docker image
Dockerfile content:
```Bash
FROM golang:1.22-alpine AS builder

WORKDIR /usr/src/app

COPY . .

RUN go mod download

RUN go build -o product-catalog .

FROM alpine AS release

WORKDIR /usr/src/app

COPY ./products ./products
COPY --from=builder /usr/src/app/product-catalog ./

ENV PRODUCT_CATALOG_PORT 8088
ENTRYPOINT ["./product-catalog"]
```

This Dockerfile compiles the Go binary in a separate build stage and copies it into a minimal Alpine runtime image.
Build command:

`docker build -t shellesty/product-catalog:v1 .`

Built the Docker image and tagged it with version v1.
### 6. Verified image creation
```bash
docker images
docker images | grep shellesty
```

Checked that the image was created successfully.
### 7. Ran the container

`docker run shellesty/product-catalog:v1`

Initial run failed due to missing the PRODUCT_CATALOG_PORT environment variable, which was required by the Go service.
### 8. Built and ran updated container with environment variable fixed

`docker build -t shellesty/product-catalog:v2 .
docker run shellesty/product-catalog:v2`

Tagged the updated image as v2 after adding ENV PRODUCT_CATALOG_PORT 8088 in the Dockerfile to resolve the fatal error.
Expected output:
```bash
time="2025-06-17T22:59:44Z" level=info msg="Loaded 10 products"
time="2025-06-17T22:59:44Z" level=info msg="Product Catalog gRPC server started on port: 8088"
```

This confirms that the binary ran correctly inside the container — Dockerfile build and execution was successful.
