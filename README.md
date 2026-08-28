# Custom Nginx Docker Image with Docker Compose

## 📌 Task Description

Create a custom Docker image for Nginx and deploy it using Docker Compose. The deployment must use a volume bind mount at:

```text
/var/opt/nginx
```

The custom Docker image must be pushed to Docker Hub.

## 🛠️ Technologies Used

* AWS EC2
* Amazon Linux 2023
* Docker
* Docker Compose
* Docker Buildx
* Nginx
* Docker Hub
* Git & GitHub
* HTML

## 📂 Project Structure

```text
nginx-docker-task/
│
├── Dockerfile
├── docker-compose.yml
├── index.html
├── README.md
└── screenshots/
```

## 🐳 Dockerfile

The custom image is created using the official Nginx image as the base image.

```dockerfile
FROM nginx:latest

COPY index.html /usr/share/nginx/html/index.html
```

The custom HTML page is copied into the Nginx web root during image creation.

## 🐙 Docker Compose Configuration

The application is deployed using Docker Compose.

```yaml
services:
  nginx:
    build: .
    image: meghana-custom-nginx:latest
    container_name: custom-nginx
    ports:
      - "80:80"
    volumes:
      - /var/opt/nginx:/usr/share/nginx/html
    restart: unless-stopped
```

### 🔗 Volume Bind Mount

The required bind mount is:

```text
/var/opt/nginx:/usr/share/nginx/html
```

This maps the EC2 host directory:

```text
/var/opt/nginx
```

to the Nginx web root inside the container:

```text
/usr/share/nginx/html
```

## 🚀 Deployment Steps

### 1. Launch AWS EC2

An Amazon Linux 2023 EC2 instance was launched on AWS.

### 2. Install Docker

Docker was installed and configured on the EC2 instance.

### 3. Install Docker Compose

Docker Compose was installed as a Docker CLI plugin.

### 4. Create Project Directory

```bash
mkdir nginx-docker-task
cd nginx-docker-task
```

### 5. Create the Required Host Directory

```bash
sudo mkdir -p /var/opt/nginx
```

### 6. Copy Website to Bind-Mount Directory

```bash
sudo cp index.html /var/opt/nginx/
```

### 7. Build and Deploy the Custom Nginx Image

```bash
docker compose up -d --build
```

### 8. Verify Running Container

```bash
docker ps
```

The container should be running with port 80 exposed:

```text
0.0.0.0:80->80/tcp
```

### 9. Verify the Bind Mount

```bash
docker inspect custom-nginx --format '{{range .Mounts}}{{.Source}} -> {{.Destination}}{{println}}'
```

Expected output:

```text
/var/opt/nginx -> /usr/share/nginx/html
```

### 10. Test the Website

```bash
curl http://localhost
```

The website successfully returned the custom HTML content.

## 🧪 Bind Mount Verification

The bind mount was tested by modifying:

```text
/var/opt/nginx/index.html
```

The change was immediately reflected when accessing the website through Nginx.

This confirms that the Nginx container is serving the website from the host directory `/var/opt/nginx`.

## 🐳 Docker Hub

The custom Docker image was tagged as:

```text
guvimadhumn/meghana-custom-nginx:latest
```

The image was successfully pushed to Docker Hub using:

```bash
docker push guvimadhumn/meghana-custom-nginx:latest
```

Docker Hub image:

**guvimadhumn/meghana-custom-nginx**

## 🔍 Docker Image Verification

The image can be verified locally using:

```bash
docker images
```

Expected repository:

```text
guvimadhumn/meghana-custom-nginx
```

## 🌐 Application Output

The deployed website displays:

```text
Custom Nginx Docker Image

Hello from Meghana!

This Nginx website is deployed using Docker Compose.

Volume Bind Mount: /var/opt/nginx
```

The application can be accessed through the EC2 public IP:

```text
http://<EC2-PUBLIC-IP>
```

## 📸 Screenshots

The GitHub repository contains screenshots demonstrating:

1. Docker image build
2. Docker Compose deployment
3. Running Nginx container
4. `/var/opt/nginx` bind mount
5. Bind mount test output
6. Website output in browser
7. Docker Hub image push

## ✅ Task Result

The custom Nginx Docker image was successfully created and deployed using Docker Compose on AWS EC2.

The required bind mount:

```text
/var/opt/nginx
```

was successfully configured and verified.

The custom image was successfully pushed to Docker Hub.

## 🔗 Submission URLs

### GitHub Repository

```text
<GitHub-Repository-URL>
```

### Docker Hub Image

```text
https://hub.docker.com/r/guvimadhumn/meghana-custom-nginx
```

## 👩‍💻 Author

**Madhu**

DevOps / Cloud Learner
