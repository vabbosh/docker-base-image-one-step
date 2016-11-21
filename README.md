# docker-base-image-one-step
This contains the contents of the repo - docker-base-image-one-step provided by the WP team. 

I unzipped the docker-base-image-one-step.git.tar.gz and it resulted in this directory - "docker-base-image-one-step.git" being created.

I created a new directory and cloned the docker-base-image-one-step.git repository.

I changed the remote repo to a repo in our organization
git remote set-url origin https://github.com/containers-a8/docker-base-image-one-step.git

Pushed the contents of the local repo to the new remote repo (our github repo)
git push origin master

Create the base image using the Dockefile-centos instead of the default Dockerfile (which uses RHEL)
