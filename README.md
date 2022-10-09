## Jenkins declarative Pipeline
### Docker image
Jenkins server
```bash
docker pull jenkins/jenkins:alpine
docker run -p 8080:8080 -p 50000:50000 --restart=on-failure jenkins/jenkins:alpine
```
