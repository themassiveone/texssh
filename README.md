# Tex dockerized coding environment

## Motivation

Since brew and similar package managers enabled it to install any version of tex, this has been simplified a lot. Using vsCode in conjunction with tex addons like [Latex Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) is still annoying to setup, as you require tools like latexindent, which need to be installed from perl package managers. Additionally this process involves manual PATH alterations and [permission](https://stackoverflow.com/a/69396712/18392571) changes. Maybe this is due to my own mistakes, but its still not an optimal solution, as all of those systems are tightly coupled.

## Solution

Running an isolated docker container eliminates the need to install tex cli tools and other annoying configuration steps, as it allows you to run tex compilations directly on a docker using [texlive/texlive](https://hub.docker.com/r/texlive/texlive).

Running this docker by itself doesnt provide that mush interactivity though. Therefore I added openssh-server, so that one can connect to it using vsCodes [Remote SSH](https://code.visualstudio.com/docs/remote/ssh) extension.

## Getting Started

#### Create Docker

1. Install Docker on your local machine. This might be docker desktop for windows/mac or docker engine on any linux distribution
2. Pull the docker image from [Docker Hub]() using

`docker pull themassiveone/texssh:latest`

3. Run that docker image using following parameters
   ```
   docker run -d \
       --name=yourDockerName \
       -p 8022:22 \
       -v /path/to/appdata/data:/home/code \
       --restart unless-stopped \
       themassiveone/texssh:latest
   ```
   Make sure your data path already exist on your local machine.

#### Connect to your Docker Container

1. Add your tex server to your ssh config

   ```
   Host yourDockerName
   HostName localhost
   User code
   Port 8022
   ```

2. Download this [Remote SSH](https://code.visualstudio.com/docs/remote/ssh) vscode extension

3. Connect to your docker instance using Remote SSH

```
Username: code
Password: code
changing password will be implemented later
```

4. Happy tex coding
