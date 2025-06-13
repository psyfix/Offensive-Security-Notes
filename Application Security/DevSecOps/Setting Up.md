###### Setting up GitLab and a GitRunner
```
#Tutorial
https://www.youtube.com/watch?v=Y0qT6MCnRG0

#Create docker volume to map to drive.
docker volume create gitlab-runner-config

#Create docker container gitlab-runner map volume to drive and pull latest image.
docker run -d --name gitlab-runner --dns 8.8.8.8 --restart always -v /var/run/docker.sock:/var/run/docker.sock -v gitlab-runner-config:/etc/gitlab-runner gitlab/gitlab-runner:latest

#Register Runner
docker run --rm -it -v gitlab-runner-config:/etc/gitlab-runner gitlab/gitlab-runner:latest register

#Errors
Can't resolve docker host: 
- Try check DNS configuration
- Try check the docker config.toml file "volumes = ["/var/run/docker.sock:/var/run/docker.sock", "/cache"]"

Can't upload ar

```
##### Vulnerable Apps
These are repositories you can import into GitLab or what ever CI/CD platform to use for testing pipelines.
```
#Python
https://github.com/NetSPI/django.nV
```
ddd
