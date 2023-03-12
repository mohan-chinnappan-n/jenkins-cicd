# Running HelloWorkPython

```
Started by user Mohan Chinnappan

Running as SYSTEM

Building in workspace /var/jenkins_home/workspace/HelloWorldPython

The recommended git tool is: NONE

No credentials specified

Cloning the remote Git repository

Cloning repository https://github.com/mohan-chinnappan-n/jenkins-cicd

 > git init /var/jenkins_home/workspace/HelloWorldPython # timeout=10

Fetching upstream changes from https://github.com/mohan-chinnappan-n/jenkins-cicd

 > git --version # timeout=10

 > git --version # 'git version 2.30.2'

 > git fetch --tags --force --progress -- https://github.com/mohan-chinnappan-n/jenkins-cicd +refs/heads/*:refs/remotes/origin/* # timeout=10

 > git config remote.origin.url https://github.com/mohan-chinnappan-n/jenkins-cicd # timeout=10

 > git config --add remote.origin.fetch +refs/heads/*:refs/remotes/origin/* # timeout=10

Avoid second fetch

 > git rev-parse refs/remotes/origin/main^{commit} # timeout=10

Checking out Revision b34f09b31c3cc64d716a6e9ff613e7b71de5fe4c (refs/remotes/origin/main)

 > git config core.sparsecheckout # timeout=10

 > git checkout -f b34f09b31c3cc64d716a6e9ff613e7b71de5fe4c # timeout=10

Commit message: "init"

First time build. Skipping changelog.

[HelloWorldPython] $ /bin/sh -xe /tmp/jenkins1846208202096239518.sh

+ python3 py/hw.py

Hello World!

Finished: SUCCESS
```

![Python Hello World](img/jenkins-cicd-1.webm.gif)
