# tjkpolisher.github.io
tjkpolisher 계정의 개인 웹사이트 구축용 리포지터리입니다.

## Docker build
[https://hub.docker.com/_/httpd](https://hub.docker.com/_/httpd)에서 httpd 도커 이미지를 pull합니다. 이후 아래 명령어를 터미널에 입력합니다.  
```Bash
$ docker build -t my-apache2 .
$ sudo docker images
```  

## Docker run
```Bash
$ sudo docker run -dit --name my-webapp -p 8081:80 my-apache2
$ sudo docker ps
```  

### Into the docker container
```Bash
$ sudo docker exec -it my-webapp bash
root@11115e4b21fd:/usr/local/apache2# ls -l
total 40
drwxr-xr-x 2 root root 4096 Oct 19 19:22 bin
drwxr-xr-x 2 root root 4096 Oct 19 19:22 build
drwxr-xr-x 2 root root 4096 Oct 19 19:22 cgi-bin
drwxr-xr-x 4 root root 4096 Oct 19 19:22 conf
drwxr-xr-x 3 root root 4096 Oct 19 19:22 error
drwxr-xr-x 1 root root 4096 Oct 20 03:15 htdocs
drwxr-xr-x 3 root root 4096 Oct 19 19:22 icons
drwxr-xr-x 2 root root 4096 Oct 19 19:22 include
drwxr-xr-x 1 root root 4096 Oct 20 03:27 logs
drwxr-xr-x 2 root root 4096 Oct 19 19:21 modules
root@11115e4b21fd:/usr/local/apache2# cd htdocs/
root@11115e4b21fd:/usr/local/apache2/htdocs# ls -l
total 96
-rw-r--r-- 1 root root    49 Oct 20 02:51 Dockerfile
-rw-r--r-- 1 root root 17128 Oct 20 02:51 LICENSE.txt
-rw-r--r-- 1 root root    84 Oct 20 02:51 LICENSE.txt:Zone.Identifier
-rw-r--r-- 1 root root  2295 Oct 20 02:51 README.md
-rw-r--r-- 1 root root  1344 Oct 20 02:51 README.txt
-rw-r--r-- 1 root root    84 Oct 20 02:51 README.txt:Zone.Identifier
drwxr-xr-x 6 root root  4096 Oct 20 02:51 assets
-rw-r--r-- 1 root root 18398 Oct 20 02:51 elements.html
-rw-r--r-- 1 root root    84 Oct 20 02:51 elements.html:Zone.Identifier
-rw-r--r-- 1 root root  5045 Oct 20 02:51 generic.html
-rw-r--r-- 1 root root    84 Oct 20 02:51 generic.html:Zone.Identifier
drwxr-xr-x 2 root root  4096 Oct 20 02:51 images
-rw-r--r-- 1 root root  7306 Oct 20 03:01 index.html
-rw-r--r-- 1 root root    84 Oct 20 02:51 index.html:Zone.Identifier
root@11115e4b21fd:/usr/local/apache2/htdocs#
```  

## Deploy production
### Deploy dev - Firebase
```Bash
$ firebase deploy
```

### Deploy stg - fly.io
```Bash
$ flyctl launch
==> Verifying app config
Validating /home/tjk/code/tjkpolisher.github.io/fly.toml
Platform: machines
✓ Configuration is valid
--> Verified app config
==> Building image
Remote builder fly-builder-ancient-fire-6017 ready
==> Building image with Docker
--> docker host: 20.10.12 linux x86_64
[+] Building 3.8s (7/7) FINISHED
 => [internal] load build definition from Dockerfile                        0.1s
 => => transferring dockerfile: 137B                                        0.1s
 => [internal] load .dockerignore                                           0.1s
 => => transferring context: 49B                                            0.1s
 => [internal] load metadata for docker.io/pierrezemb/gostatic:latest       1.3s
 => [internal] load build context                                           2.1s
 => => transferring context: 20.22MB                                        2.1s
 => [1/2] FROM docker.io/pierrezemb/gostatic@sha256:7e5718f98f2172f7c8dffd  0.2s
 => => resolve docker.io/pierrezemb/gostatic@sha256:7e5718f98f2172f7c8dffd  0.0s
 => => sha256:0cf3c901807f7df57d792cd4a926ac2eb4078eb33775 1.88MB / 1.88MB  0.1s
 => => sha256:7e5718f98f2172f7c8dffd152ef0b203873ba889c8d8 2.67kB / 2.67kB  0.0s
 => => sha256:f846dcfe68518bd5a624acb44abee440deedfca894e641b7 527B / 527B  0.0s
 => => sha256:37dd3994986381311fdfc59ea190c8e60c6c8c5a38f3cdec 915B / 915B  0.0s
 => => extracting sha256:0cf3c901807f7df57d792cd4a926ac2eb4078eb337750316d  0.1s
 => [2/2] COPY . /srv/http/                                                 0.1s
 => exporting to image                                                      0.1s
 => => exporting layers                                                     0.1s
 => => writing image sha256:814bf94d8b95fc184c0d39f093c100543e9e3a402ad5bf  0.0s
 => => naming to registry.fly.io/tjkpolisher-blog:deployment-01HDD612JXHYP  0.0s
--> Building image done
==> Pushing image to fly
The push refers to repository [registry.fly.io/tjkpolisher-blog]
a48d7c77bd45: Pushed
f347b3d1982a: Pushed
deployment-01HDD612JXHYPB7DJDF3EAW088: digest: sha256:2c8d778714879f773a4c880d28aafd1e381bfe5323026e28bd88db3c88962a37 size: 740
--> Pushing image done
image: registry.fly.io/tjkpolisher-blog:deployment-01HDD612JXHYPB7DJDF3EAW088
image size: 22 MB

Watch your deployment at https://fly.io/apps/tjkpolisher-blog/monitoring

Provisioning ips for tjkpolisher-blog
  Dedicated ipv6: 2a09:8280:1::69:8f8f
  Shared ipv4: 66.241.124.238
  Add a dedicated ipv4 with: fly ips allocate-v4

This deployment will:
 * create 2 "app" machines

No machines in group app, launching a new machine
Creating a second machine to increase service availability
Finished launching new machines
-------
NOTE: The machines for [app] have services with 'auto_stop_machines = true' that will be stopped when idling

-------

Visit your newly deployed app at https://tjkpolisher-blog.fly.dev/
```

## Load Test
The Load Test with [nGrinder](https://github.com/naver/ngrinder) was operated. It is the aim of the test to achieve TPS over 150 with stable response speed. If you'd like to see the result, you can figure it out in [this link](https://github.com/dj-twenty-six/PoC-REPORT/issues/4). Also, the configuration of the resources such as CPU and RAM restriction can be seen in `compose.yaml` file.