#  Container Project Management 

Author: Darrell D, Feb 2026

<img src="./media/alienplanet.png" style="width:600px" alt="abstract alien planet" >
<div class="clear"></div>

## Why

As a learner I am building new projects often; it is helpful if they are self 
documented and reproducible.

## What podman gives you

A container that is independent of the host system, which allows you to build,
run and deploy consistently.

## What mise gives you

> toml with bash run blocks avoids mixed language code for the most part

Mise is way to group and label a series of tasks, make a clear menu of those tasks, and
provide you with feedback on each step. It can also act as a general purpose version
manager, though, it is only used as a runner here.

> if a line from a run block returns non 0, the run block stops, that is 
> why false on a line by itself disables a task.
> Also, if you don't care if a command succeeds you can append || true


> You may end up recreating containers over top of existing mount, so
> mkdir will fail, but we don't want the script to abort

## What it looks like

> devcontainers, the vscode / github codespaces containerized form are better than no containers, 
> 
> but vscode obfuscates folder paths for your mount point (deep in ~.local) and 
> a container image is created for every project, which pollutes your image directory, it
> also uses unrelated name, that is super annoying because you are correlating the 
> stupid names with my stupid brain is incredible irritation

So what I've done here is each project starts in a folder with 
the mise.toml file, which provides tasks for creating and using a container.
The container will have a name the same as the project. There is a user 
inside the container with the same name as your current user on the host.
The project files will be mounted in a folder called mount, and when you 
enter the container that folder becomes your home folder inside the container.

You can work on your project files from outside the container in the mount folder,
but you should build, run, deploy etc from the container to get a clean room.

## Steps

0. Install Mise and Podman, refer to podman.mise.toml

1. create a folder for your project hello
```
mkdir hello
cd hello
```

2. Place mise.toml Container Manager script inside the project folder
```
wget https://raw.githubusercontent.com/dirtslayer/project/refs/heads/main/mise.toml
```

3. Review mise.toml
    - remove false's at start of run section to enable task
    - add your tooling to the PACKAGES variable in the setup-container task

4. mise run, to show task menu

5. steps in order of: 90, 99 from the mise.toml will create and setup your container

    > the container will have the same name as your project

6. disable steps 90,91,99 in the mise.toml 

7. mise run, 01 to work on your project

8. mise run, 02 to update / install software inside container

9. enjoy not having to use devcontainers!

10. Star The Repo

Link: [project repo](https://github.com/dirtslayer/project)

11. Create an Issue, Create a PR

This scaffold is for Debian host and arch container.
One could create other similar variations, like arch as a host with an alpine container.

## My First PeerTube

<div style="position: relative; padding-top: 56.25%;"><iframe title="Using Podman and Mise to containerize projects" width="100%" height="100%" src="https://video.mycrowd.ca/videos/embed/eYMKFAYkAEjRBxDX8FrhR2" allow="fullscreen" sandbox="allow-same-origin allow-scripts allow-popups allow-forms" style="border: 0px; position: absolute; inset: 0px;"></iframe></div>