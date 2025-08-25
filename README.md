# Docker CI/CD Lab

Builds a custom Nginx Docker image with `index.html`, pushes it to Docker Hub, and deploys it to an EC2 instance via GitHub Actions.

---

## Prerequisites

- Docker installed locally
- GitHub & Docker Hub accounts
- AWS EC2 instance (Ubuntu) with public IP
- GitHub repo with `.github/workflows/docker-ci-cd.yml`

---

## GitHub Secrets

- `DOCKER_USERNAME` & `DOCKER_PASSWORD` (Docker Hub)
- `EC2_HOST`, `EC2_USER`, `EC2_SSH_KEY` (EC2 access)

---

## Dockerfile

```dockerfile
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
````

`index.html`:

```html
<h1>Hello from GitHub Actions CI/CD</h1>
```

---

## Usage

Push changes to GitHub:

```bash
git add . && git commit -m "Add CI/CD workflow" && git push origin main
```

The workflow builds & pushes the image, then deploys it to EC2.
Verify manually:

```bash
docker pull prayags/gitlab-ci-cd-demo:latest
docker run -d -p 80:80 --name gitlab-ci-cd-demo prayags/gitlab-ci-cd-demo:latest
```

Open in browser: `http://<EC2_PUBLIC_IP>`

---

## Cleanup

```bash
docker stop gitlab-ci-cd-demo
docker rm gitlab-ci-cd-demo
docker system prune -af
docker volume prune -f
```

---

**Outcome:** Automated Docker CI/CD pipeline with EC2 deployment and live Nginx container.



If you want, I can make an **even one-screen version** perfect for students or lab manuals. Do you want me to do that?
```
