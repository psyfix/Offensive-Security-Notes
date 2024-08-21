###### Setting up GitLab and a GitRunner
```
https://www.youtube.com/watch?v=KgddhbgdHEA
https://www.youtube.com/watch?v=Y2k2R9A6UbQ

sudo curl -L --output /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/biniaries/gitlab-runner-linux-amd64
sudo chmod +x /usr/local/bin/gitlab-runner
sudo useradd --comment 'Gitlab Runner Docker' --create-home gitlab-runner-docker --shell /bin/bash
sudo gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner



docker volume create gitlab-runner-config
docker run -d --name gitlab-runner --restart always -v /var/run/docker.sock:/var/run/docker.sock -v gitlab-runner-config:/etc/gitlab-runner gitlab/gitlab-runner:latest
```
##### Vulnerable Apps
These are repositories you can import into GitLab or what ever CI/CD platform to use for testing pipelines.
```
#Python
https://github.com/NetSPI/django.nV
```

