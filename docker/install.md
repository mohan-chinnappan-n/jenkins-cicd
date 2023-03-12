```
docker network create jenkins
```
```
37d113c8d79cd12a209822f0ccb12be7058b9c6ccdc62e2b298725537edd703d
```

```
docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
f8ca68549edb   bridge    bridge    local
145498352d20   host      host      local
37d113c8d79c   jenkins   bridge    local
3bdfaf921867   none      null      local
```

```
docker run --name jenkins-docker --rm --detach \
  --privileged --network jenkins --network-alias docker \
  --env DOCKER_TLS_CERTDIR=/certs \
  --volume jenkins-docker-certs:/certs/client \
  --volume jenkins-data:/var/jenkins_home \
  --publish 2376:2376 \
  docker:dind --storage-driver overlay2
```
```
Unable to find image 'docker:dind' locally
dind: Pulling from library/docker
63b65145d645: Pull complete 
67fecbccebe0: Pull complete 
2b3fda0e4f2a: Pull complete 
30dc96e58339: Pull complete 
8c007c9e333b: Pull complete 
c31b9f3137a1: Pull complete 
782206789a08: Pull complete 
e415889ffe25: Pull complete 
55134767123a: Pull complete 
36af3abb7351: Pull complete 
9e414f2e72f2: Pull complete 
4ccabe0725ae: Pull complete 
ca215d26ccb7: Pull complete 
Digest: sha256:e4d776dd1e0580dfb670559d887300aa08b53b8a59f5df2d4eaace936ef4d0e9
Status: Downloaded newer image for docker:dind
58b1537f513652de9951efd03766a2c9ad853e45341a18584f39565bb4beae14
```

``` 
cat Dockerfile
```
```

FROM jenkins/jenkins:2.387.1
USER root
RUN apt-get update && apt-get install -y lsb-release
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg
RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-ce-cli
USER jenkins
RUN jenkins-plugin-cli --plugins "blueocean docker-workflow"
```

```
docker build -t myjenkins-blueocean:2.387.1-1 .
[+] Building 42.9s (10/10) FINISHED                                                                                                                    
 => [internal] load build definition from Dockerfile                                                                                              0.0s
 => => transferring dockerfile: 602B                                                                                                              0.0s
 => [internal] load .dockerignore                                                                                                                 0.0s
 => => transferring context: 2B                                                                                                                   0.0s
 => [internal] load metadata for docker.io/jenkins/jenkins:2.387.1                                                                                1.0s
 => [1/6] FROM docker.io/jenkins/jenkins:2.387.1@sha256:0944e18261a6547e89b700cec432949281a7419a6165a3906e78c97efde3bc86                         11.1s
 => => resolve docker.io/jenkins/jenkins:2.387.1@sha256:0944e18261a6547e89b700cec432949281a7419a6165a3906e78c97efde3bc86                          0.0s
 => => sha256:a56533012712c1db623da3e5e9c2d0276301c82db0a2e7a82debfb57e5d916f2 8.93MB / 8.93MB                                                    0.3s
 => => sha256:c09d5e9e1188f3fff7a4f8c3c7c330fde5184cba1c6f0c92526b8b7bd0ac7c26 51.63MB / 51.63MB                                                  3.4s
 => => sha256:0944e18261a6547e89b700cec432949281a7419a6165a3906e78c97efde3bc86 2.36kB / 2.36kB                                                    0.0s
 => => sha256:32fb02163b6bb519a30f909008e852354dae10bdfd6b34190dbdfe8f15403ea0 55.05MB / 55.05MB                                                  2.6s
 => => sha256:005fcb5c3017ef120d0d9d8d8925e9248ff6e2cf2b5e18b527b01459c7b2b3f4 2.77kB / 2.77kB                                                    0.0s
 => => sha256:d5ed2ceef0ec08e9044ebb39812f211d64dbcdfce775cc6b0460ca289193416f 13.13kB / 13.13kB                                                  0.0s
 => => sha256:7936e107ffe73b406a0d02edf9bb02b983534d803bb06fd03dc38dac4b6cfe2a 1.24kB / 1.24kB                                                    0.4s
 => => sha256:3ca683058265b99b65bbc69b9e8fa4c46e830db35aad614706200e6cf0c30d8a 189B / 189B                                                        0.5s
 => => sha256:c2ecd304b4b84ef6154bd85e13360f0b015e39057a329698617ce0a53ed6cf32 98.12MB / 98.12MB                                                  4.7s
 => => extracting sha256:32fb02163b6bb519a30f909008e852354dae10bdfd6b34190dbdfe8f15403ea0                                                         2.4s
 => => sha256:be3512d810d65f00f28af0885e2f30833263ee061528e20c7fee21664f1572b8 202B / 202B                                                        2.8s
 => => sha256:56b37d7c2a7a3c93fd013cb1ad5652f8cea3910ecc0274d73064bba27ab57864 5.84MB / 5.84MB                                                    3.4s
 => => sha256:99ed1e723e52507ce2d615e1682d673c3ffcec5f5b68c266db70d829ef4be208 76.93MB / 76.93MB                                                  5.8s
 => => sha256:256db5485b1399ecbd58c2558388fc9a4ff1caaaeacbdfe23127c7f13b1ee98b 1.93kB / 1.93kB                                                    3.5s
 => => sha256:ee8c7eaf5e6bd8c45e503756da48e80137def6765017148ce9f2af66ce97244b 1.17kB / 1.17kB                                                    3.7s
 => => sha256:509f66c2f3174642f0eb3e3b2e8a70da698f613042ec65f525c476afe0b6b7d5 374B / 374B                                                        3.9s
 => => sha256:820296a845d636be13276fdf3bdae7fdf2ac00d401182632d1ab450e26353674 271B / 271B                                                        4.1s
 => => extracting sha256:c09d5e9e1188f3fff7a4f8c3c7c330fde5184cba1c6f0c92526b8b7bd0ac7c26                                                         2.0s
 => => extracting sha256:a56533012712c1db623da3e5e9c2d0276301c82db0a2e7a82debfb57e5d916f2                                                         0.2s
 => => extracting sha256:7936e107ffe73b406a0d02edf9bb02b983534d803bb06fd03dc38dac4b6cfe2a                                                         0.0s
 => => extracting sha256:3ca683058265b99b65bbc69b9e8fa4c46e830db35aad614706200e6cf0c30d8a                                                         0.0s
 => => extracting sha256:c2ecd304b4b84ef6154bd85e13360f0b015e39057a329698617ce0a53ed6cf32                                                         0.6s
 => => extracting sha256:be3512d810d65f00f28af0885e2f30833263ee061528e20c7fee21664f1572b8                                                         0.0s
 => => extracting sha256:56b37d7c2a7a3c93fd013cb1ad5652f8cea3910ecc0274d73064bba27ab57864                                                         0.1s
 => => extracting sha256:99ed1e723e52507ce2d615e1682d673c3ffcec5f5b68c266db70d829ef4be208                                                         1.6s
 => => extracting sha256:256db5485b1399ecbd58c2558388fc9a4ff1caaaeacbdfe23127c7f13b1ee98b                                                         0.0s
 => => extracting sha256:ee8c7eaf5e6bd8c45e503756da48e80137def6765017148ce9f2af66ce97244b                                                         0.0s
 => => extracting sha256:509f66c2f3174642f0eb3e3b2e8a70da698f613042ec65f525c476afe0b6b7d5                                                         0.0s
 => => extracting sha256:820296a845d636be13276fdf3bdae7fdf2ac00d401182632d1ab450e26353674                                                         0.0s
 => [2/6] RUN apt-get update && apt-get install -y lsb-release                                                                                    6.7s
 => [3/6] RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc   https://download.docker.com/linux/debian/gpg                           0.7s
 => [4/6] RUN echo "deb [arch=$(dpkg --print-architecture)   signed-by=/usr/share/keyrings/docker-archive-keyring.asc]   https://download.docker  0.2s
 => [5/6] RUN apt-get update && apt-get install -y docker-ce-cli                                                                                  8.9s
 => [6/6] RUN jenkins-plugin-cli --plugins "blueocean docker-workflow"                                                                           13.5s
 => exporting to image                                                                                                                            0.8s
 => => exporting layers                                                                                                                           0.8s
 => => writing image sha256:fd428091db2d8149ed7ce13d7fe3ccd7d412e87a121f4a6850ec0cfd0ed91ce2                                                      0.0s
 => => naming to docker.io/library/myjenkins-blueocean:2.387.1-1                                                                                  0.0s

Use 'docker scan' to run Snyk tests against images to find vulnerabilities and learn how to fix them
```

```
docker container ls
```

```
CONTAINER ID   IMAGE         COMMAND                  CREATED         STATUS         PORTS                              NAMES
58b1537f5136   docker:dind   "dockerd-entrypoint.…"   2 minutes ago   Up 2 minutes   2375/tcp, 0.0.0.0:2376->2376/tcp   jenkins-docker
```

```
docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.387.1-1
```

```
docker ps
```

```
CONTAINER ID   IMAGE                           COMMAND                  CREATED         STATUS         PORTS                                              NAMES
c5ea234eee86   myjenkins-blueocean:2.387.1-1   "/usr/bin/tini -- /u…"   2 minutes ago   Up 2 minutes   0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp   jenkins-blueocean
58b1537f5136   docker:dind                     "dockerd-entrypoint.…"   4 minutes ago   Up 4 minutes   2375/tcp, 0.0.0.0:2376->2376/tcp                   jenkins-docker
```

## Getting initialAdminPassword
```
docker exec c5ea234eee86  cat /var/jenkins_home/secrets/initialAdminPassword
```
```
600755197d9642a08d03aa294fb82344
```

## bash into docker container
```
docker exec -it c5ea234eee86   bash
```

```
jenkins@c5ea234eee86:~$ ls -l
total 112
-rw-r--r--   1 jenkins jenkins  1663 Mar 12 13:29 config.xml
-rw-r--r--   1 jenkins jenkins  5316 Mar 12 13:28 copy_reference_file.log
-rw-r--r--   1 jenkins jenkins   156 Mar 12 13:28 hudson.model.UpdateCenter.xml
-rw-r--r--   1 jenkins jenkins   370 Mar 12 13:28 hudson.plugins.git.GitTool.xml
-rw-------   1 jenkins jenkins  1680 Mar 12 13:28 identity.key.enc
-rw-r--r--   1 jenkins jenkins     7 Mar 12 13:34 jenkins.install.InstallUtil.lastExecVersion
-rw-r--r--   1 jenkins jenkins     7 Mar 12 13:34 jenkins.install.UpgradeWizard.state
-rw-r--r--   1 jenkins jenkins   179 Mar 12 13:34 jenkins.model.JenkinsLocationConfiguration.xml
-rw-r--r--   1 jenkins jenkins   171 Mar 12 13:28 jenkins.telemetry.Correlator.xml
drwxr-xr-x   3 jenkins jenkins  4096 Mar 12 13:51 jobs
drwxr-xr-x   4 jenkins jenkins  4096 Mar 12 14:33 logs
-rw-r--r--   1 jenkins jenkins   907 Mar 12 13:28 nodeMonitors.xml
drwxr-xr-x   2 jenkins jenkins  4096 Mar 12 13:28 nodes
drwxr-xr-x 114 jenkins jenkins 24576 Mar 12 13:33 plugins
-rw-r--r--   1 jenkins jenkins   129 Mar 12 13:54 queue.xml
-rw-r--r--   1 jenkins jenkins    64 Mar 12 13:28 secret.key
-rw-r--r--   1 jenkins jenkins     0 Mar 12 13:28 secret.key.not-so-secret
drwx------   2 jenkins jenkins  4096 Mar 12 13:53 secrets
drwxr-xr-x   2 jenkins jenkins  4096 Mar 12 13:33 updates
drwxr-xr-x   2 jenkins jenkins  4096 Mar 12 13:28 userContent
drwxr-xr-x   3 jenkins jenkins  4096 Mar 12 13:33 users
drwxr-xr-x  11 jenkins jenkins  4096 Mar 12 13:28 war
drwxr-xr-x   3 jenkins jenkins  4096 Mar 12 13:53 workspace
jenkins@c5ea234eee86:~$ pwd
/var/jenkins_home
jenkins@c5ea234eee86:~$ python3
Python 3.9.2 (default, Feb 28 2021, 17:03:44) 
[GCC 10.2.1 20210110] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> exit()
```


## socat container 
- proxy the connection between Jenkins master container and localhost

```


Jenkins Docker Plugin Configuration when running jenkins as container

1) First Install Docker Plugin

2) Go to Manage Jenkins -> System Configuration -> Scroll down to botton -> Add Cloud -> Docker

3) If you are running jenkins as container, in the docker host uri field you have to enter unix or tcp address of the docker host. But since you are running jenkins as container, the container cant reach docker host unix port

4) So we have to run another container that can mediate between docker host and jenkins container. It will publish docker host's unix port as its tcp port. Follow the instructions to create socat container https://hub.docker.com/r/alpine/socat/

5)After the creating socat container, you can go back the docker configuration in jenkins and enter tcp://socat-container-ip:2375

6) Test Connection should succeed now

```
```
docker run -d --restart=always -p 127.0.0.1:2400:2375 --network jenkins -v /var/run/docker.sock:/var/run/docker.sock alpine/socat tcp-listen:2375,fork,reuseaddr unix-connect:/var/run/docker.sock
```
```
b643f2a82b31e1f2ac9e5261badbb65d13447b94a92eaa0bb34202a9148f39b4


```

```
 docker container ls
```
```
CONTAINER ID   IMAGE                           COMMAND                  CREATED              STATUS              PORTS                                              NAMES
b643f2a82b31   alpine/socat                    "socat tcp-listen:23…"   About a minute ago   Up About a minute   127.0.0.1:2400->2375/tcp                           silly_hopper
c5ea234eee86   myjenkins-blueocean:2.387.1-1   "/usr/bin/tini -- /u…"   3 hours ago          Up 12 minutes       0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp   jenkins-blueocean
58b1537f5136   docker:dind                     "dockerd-entrypoint.…"   3 hours ago          Up 3 hours          2375/tcp, 0.0.0.0:2376->2376/tcp                   jenkins-docker


```

```
docker inspect b643f2a82b31e1f2ac9e5261badbb65d13447b94a92eaa0bb34202a9148f39b4 | grep IPAddress
```

```
"SecondaryIPAddresses": null,
            "IPAddress": "",
                    "IPAddress": "172.18.0.4",
```

```

docker ps
```

```
CONTAINER ID   IMAGE                           COMMAND                  CREATED         STATUS          PORTS                                              NAMES
b643f2a82b31   alpine/socat                    "socat tcp-listen:23…"   2 minutes ago   Up 2 minutes    127.0.0.1:2400->2375/tcp                           silly_hopper
c5ea234eee86   myjenkins-blueocean:2.387.1-1   "/usr/bin/tini -- /u…"   3 hours ago     Up 13 minutes   0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp   jenkins-blueocean
58b1537f5136   docker:dind                     "dockerd-entrypoint.…"   3 hours ago     Up 3 hours      2375/tcp, 0.0.0.0:2376->2376/tcp                   jenkins-docker
```

```

docker inspect  silly_hopper 
```

```json
[
    {
        "Id": "b643f2a82b31e1f2ac9e5261badbb65d13447b94a92eaa0bb34202a9148f39b4",
        "Created": "2023-03-12T16:08:27.933374909Z",
        "Path": "socat",
        "Args": [
            "tcp-listen:2375,fork,reuseaddr",
            "unix-connect:/var/run/docker.sock"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 8609,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2023-03-12T16:08:28.362760818Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:f0bbf8a4f6a0e25e06fe69c284e6e0494948e8de21ef933d72732b7858da3110",
        "ResolvConfPath": "/var/lib/docker/containers/b643f2a82b31e1f2ac9e5261badbb65d13447b94a92eaa0bb34202a9148f39b4/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/b643f2a82b31e1f2ac9e5261badbb65d13447b94a92eaa0bb34202a9148f39b4/hostname",
        "HostsPath": "/var/lib/docker/containers/b643f2a82b31e1f2ac9e5261badbb65d13447b94a92eaa0bb34202a9148f39b4/hosts",
        "LogPath": "/var/lib/docker/containers/b643f2a82b31e1f2ac9e5261badbb65d13447b94a92eaa0bb34202a9148f39b4/b643f2a82b31e1f2ac9e5261badbb65d13447b94a92eaa0bb34202a9148f39b4-json.log",
        "Name": "/silly_hopper",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": [
                "/var/run/docker.sock:/var/run/docker.sock"
            ],
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "jenkins",
            "PortBindings": {
                "2375/tcp": [
                    {
                        "HostIp": "127.0.0.1",
                        "HostPort": "2400"
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "always",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "private",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": null,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/ac59c4bb642c204d52676ea5a3f38ab123aa55c28e7c4d32885c29798685bf6c-init/diff:/var/lib/docker/overlay2/33c335c0d0c0267bc8a0de4b181fa6a67212ef993d5b23cc2d932eccd87da979/diff:/var/lib/docker/overlay2/0b76f458f2092bfa7d73629e242e320299fb159448bf52a18647959f1637387c/diff",
                "MergedDir": "/var/lib/docker/overlay2/ac59c4bb642c204d52676ea5a3f38ab123aa55c28e7c4d32885c29798685bf6c/merged",
                "UpperDir": "/var/lib/docker/overlay2/ac59c4bb642c204d52676ea5a3f38ab123aa55c28e7c4d32885c29798685bf6c/diff",
                "WorkDir": "/var/lib/docker/overlay2/ac59c4bb642c204d52676ea5a3f38ab123aa55c28e7c4d32885c29798685bf6c/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [
            {
                "Type": "bind",
                "Source": "/var/run/docker.sock",
                "Destination": "/var/run/docker.sock",
                "Mode": "",
                "RW": true,
                "Propagation": "rprivate"
            }
        ],
        "Config": {
            "Hostname": "b643f2a82b31",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "2375/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "tcp-listen:2375,fork,reuseaddr",
                "unix-connect:/var/run/docker.sock"
            ],
            "Image": "alpine/socat",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "socat"
            ],
            "OnBuild": null,
            "Labels": {}
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "a818d2616cbaced18798c777a02b95d53c16765842f392151d39272ed0e4be37",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "2375/tcp": [
                    {
                        "HostIp": "127.0.0.1",
                        "HostPort": "2400"
                    }
                ]
            },
            "SandboxKey": "/var/run/docker/netns/a818d2616cba",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "",
            "Gateway": "",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "",
            "IPPrefixLen": 0,
            "IPv6Gateway": "",
            "MacAddress": "",
            "Networks": {
                "jenkins": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": [
                        "b643f2a82b31"
                    ],
                    "NetworkID": "37d113c8d79cd12a209822f0ccb12be7058b9c6ccdc62e2b298725537edd703d",
                    "EndpointID": "08bc7021dd48b6993f51b08a0d0e9333276c64311b4487361b02c476a3a1e3f9",
                    "Gateway": "172.18.0.1",
                    "IPAddress": "172.18.0.4",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:12:00:04",
                    "DriverOpts": null
                }
            }
        }
    }
]
```

### Running docker-agent-sfdx

```
 docker build -t docker-agent-sfdx .

 ```


