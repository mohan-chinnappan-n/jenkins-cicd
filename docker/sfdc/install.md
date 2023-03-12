## Build Docker image

```
docker build -t docker-agent-sfdx .
```

```
[+] Building 160.6s (15/15) FINISHED                                                                                                                                                      
 => [internal] load build definition from Dockerfile                                                                                                                                 0.0s
 => => transferring dockerfile: 557B                                                                                                                                                 0.0s
 => [internal] load .dockerignore                                                                                                                                                    0.0s
 => => transferring context: 2B                                                                                                                                                      0.0s
 => [internal] load metadata for docker.io/jenkins/agent:alpine-jdk11                                                                                                                0.9s
 => [ 1/11] FROM docker.io/jenkins/agent:alpine-jdk11@sha256:fdf4d5e79b3645be5779130bf3239cf9344b5b1929d538b7d2980be8868550f6                                                        0.0s
 => CACHED [ 2/11] RUN apk add python3                                                                                                                                               0.0s
 => CACHED [ 3/11] RUN apk add py3-pip                                                                                                                                               0.0s
 => [ 4/11] RUN apk add  vim                                                                                                                                                         1.4s
 => [ 5/11] RUN apk add nodejs                                                                                                                                                       1.3s
 => [ 6/11] RUN apk add npm                                                                                                                                                          1.0s 
 => [ 7/11] RUN apk add yarn                                                                                                                                                         0.8s 
 => [ 8/11] RUN npm install --global sfdx-cli@latest                                                                                                                                30.6s 
 => [ 9/11] RUN apk add jq                                                                                                                                                           0.9s 
 => [10/11] RUN  echo 'y' |  sfdx plugins:install sfdx-mohanc-plugins                                                                                                               63.6s 
 => [11/11] RUN  echo 'y' |  sfdx plugins:install sfdx-git-delta                                                                                                                    38.8s 
 => exporting to image                                                                                                                                                              21.2s 
 => => exporting layers                                                                                                                                                             21.1s 
 => => writing image sha256:5d988bfa62b447ffe80a0421417b9f6329656f4d78722ea65969d32cdc13b5d4                                                                                         0.0s 
 => => naming to docker.io/library/docker-agent-sfdx 
 ```

 ## run the image
 ```
 docker run -it --entrypoint bash   --name  docker-agent-sfdx-app docker-agent-sfdx 
```
```
 17ded65a422c:~$ sfdx plugins
sfdx-git-delta 5.13.3
sfdx-mohanc-plugins 0.0.343

 ```

 ```
 exit
 ```

 ## Publish this image : 5d988bfa62b447ffe80a0421417b9f6329656f4d78722ea65969d32cdc13b5d4   

 ```
 docker tag 5d988bfa62b447ffe80a0421417b9f6329656f4d78722ea65969d32cdc13b5d4    mohanchinnappan/mc-sfdx 
```
```
docker images
```

```
REPOSITORY                       TAG            IMAGE ID       CREATED          SIZE
mohanchinnappan/mc-sfdx          latest         5d988bfa62b4   24 minutes ago   1.51GB
myjenkins-blueocean              2.387.1-1      fd428091db2d   4 hours ago      805MB
docker                           dind           c365741dcfc2   4 days ago       311MB
alpine/socat                     latest         f0bbf8a4f6a0   2 weeks ago      8.5MB
```

### Push
```
docker push   mohanchinnappan/mc-sfdx 
```
```
Using default tag: latest
The push refers to repository [docker.io/mohanchinnappan/mc-sfdx]
3c3548e6efa9: Pushed 
c991a1b7df1a: Pushed 
018486e93789: Pushed 
96d7750030cc: Pushed 
17ec9d53bd65: Pushed 
cc4f6cce9ed0: Pushed 
e5fc35b10359: Pushed 
26cde4efb06b: Pushed 
a91d2cf08b0f: Pushed 
0970af15e418: Pushed 
5f70bf18a086: Mounted from mohanchinnappan/jupyter-rust 
639d13e0e024: Mounted from jenkins/agent 
b910852e976b: Mounted from jenkins/agent 
bc4c636cd02f: Mounted from jenkins/agent 
99b5df13238c: Mounted from jenkins/agent 
10009e9661e3: Mounted from jenkins/agent 
abc8eda4da3a: Mounted from jenkins/agent 
591e5beaaae8: Mounted from jenkins/agent 
a34e3a797aad: Mounted from jenkins/agent 
7cd52847ad77: Mounted from jenkins/agent 
latest: digest: sha256:cf4b1d93c8833298cec8fa5897d22ede339b53193a606c69448ac8ee76a0c90b size: 4532
```

- [mohanchinnappan/mc-sfdxDocker Image url](https://hub.docker.com/repository/docker/mohanchinnappan/mc-sfdx/general)




## Run it
```
docker run -it --entrypoint bash    mohanchinnappan/mc-sfdx  


```

```
9900abaf79d2:~$ sfdx plugins
sfdx-git-delta 5.13.3
sfdx-mohanc-plugins 0.0.343

python3 
Python 3.10.10 (main, Feb  9 2023, 02:08:14) [GCC 12.2.1 20220924] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> exit()

9900abaf79d2:~$ pwd
/home/jenkins


9900abaf79d2:~$ vim
9900abaf79d2:~$ java --version
openjdk 11.0.18 2023-01-17
OpenJDK Runtime Environment Temurin-11.0.18+10 (build 11.0.18+10)
OpenJDK 64-Bit Server VM Temurin-11.0.18+10 (build 11.0.18+10, mixed mode)



```


```
docker ps       
```

```
CONTAINER ID   IMAGE                           COMMAND                  CREATED          STATUS          PORTS                                              NAMES
bd6b56f8666f   mohanchinnappan/mc-sfdx         "bash"                   36 seconds ago   Up 35 seconds                                                      reverent_beaver
b643f2a82b31   alpine/socat                    "socat tcp-listen:23…"   2 hours ago      Up 2 hours      127.0.0.1:2400->2375/tcp                           silly_hopper
c5ea234eee86   myjenkins-blueocean:2.387.1-1   "/usr/bin/tini -- /u…"   5 hours ago      Up 2 hours      0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp   jenkins-blueocean
58b1537f5136   docker:dind                     "dockerd-entrypoint.…"   5 hours ago      Up 5 hours      2375/tcp, 0.0.0.0:2376->2376/tcp                   jenkins-docker
```


## Running build on this 


```
 Started by user Mohan Chinnappan
Running as SYSTEM
Building remotely on docker-node-sfdx-00006mp66sdok on docker (docker-node-sfdx) in workspace /home/jenkins/workspace/HelloWorldPython
The recommended git tool is: NONE
No credentials specified
Cloning the remote Git repository
Cloning repository https://github.com/mohan-chinnappan-n/jenkins-cicd
 > git init /home/jenkins/workspace/HelloWorldPython # timeout=10
Fetching upstream changes from https://github.com/mohan-chinnappan-n/jenkins-cicd
 > git --version # timeout=10
 > git --version # 'git version 2.38.4'
 > git fetch --tags --force --progress -- https://github.com/mohan-chinnappan-n/jenkins-cicd +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git config remote.origin.url https://github.com/mohan-chinnappan-n/jenkins-cicd # timeout=10
 > git config --add remote.origin.fetch +refs/heads/*:refs/remotes/origin/* # timeout=10
Avoid second fetch
 > git rev-parse refs/remotes/origin/main^{commit} # timeout=10
Checking out Revision b34f09b31c3cc64d716a6e9ff613e7b71de5fe4c (refs/remotes/origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f b34f09b31c3cc64d716a6e9ff613e7b71de5fe4c # timeout=10
Commit message: "init"
 > git rev-list --no-walk b34f09b31c3cc64d716a6e9ff613e7b71de5fe4c # timeout=10
[HelloWorldPython] $ /bin/sh -xe /tmp/jenkins15310274698032643005.sh
+ python3 py/hw.py
Hello World!
Finished: SUCCESS

```




