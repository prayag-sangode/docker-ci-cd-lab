# Docker CI Lab

Builds an Nginx Docker image with custom `index.html` and pushes it to Docker Hub using GitHub Actions on every push to `main`.

**Setup:**  
- Create Docker Hub repo (`prayag/gitlab-ci-demo`)  
- Add GitHub Secrets: `DOCKER_USERNAME` & `DOCKER_PASSWORD` (token)

**Usage:**  
```bash
git add . && git commit -m "CI workflow" && git push origin main
docker pull prayag/gitlab-ci-demo:latest
docker run -d -p 8080:80 prayag/gitlab-ci-demo:latest
````

Open `http://localhost:8080` to see the webpage.

```
```
