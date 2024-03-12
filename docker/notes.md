# Docker

Docker aims to solve operating system & machine based dependencies.

## What is Docker

Docker is a software that can create containers, which store every single thing a project needs, to run.
Not just the code and its dependencies but a common OS as well.

## Isn't it just a VM?

Both containers and VMs provide isolated environments, but containers are a lot, but containers are a lot lighter than VMs
VMs contain an entire functioning operating system, whereas a container will only contain things it needs & nothing more
making it faster to create & easier to replicate.

VMs are basically tricked by the host system to act as if they are running on their own hardware.
A container shares compute & kernel with the host system and only emulates a minimal file system

## What is a container?

A container is a sandboxed process running on a host machine that is isolated from all other processes running on that host machine. That isolation leverages kernel namespaces and cgroups, features that have been in Linux for a long time. Docker makes these capabilities approachable and easy to use. To summarize, a container:

- Is a runnable instance of an image. You can create, start, stop, move,
  or delete a container using the Docker API or CLI.
- Can be run on local machines, virtual machines, or deployed to the cloud.
- Is portable (and can be run on any OS).
- Is isolated from other containers and runs its own software, binaries, configurations, etc.

If you're familiar with chroot, then think of a container as an extended version of chroot.
The filesystem comes from the image. However, a container adds additional
isolation not available when using chroot.

## What is an Image

A running container uses an isolated filesystem. This isolated filesystem is provided by an image,
and the image must contain everything needed to run an application - all dependencies, configurations, scripts, binaries, etc.
The image also contains other configurations for the container, such as environment variables, a default command to run,
and other metadata.

## Docker build command

The docker build command uses the Dockerfile to build a new image. You might have noticed that Docker downloaded a lot of "layers". This is because you instructed the builder that you wanted to start from the node:18-alpine image. But, since you didn't have that on your machine, Docker needed to download the image.

After Docker downloaded the image, the instructions from the Dockerfile copied in your application and used yarn to install your application's dependencies. The CMD directive specifies the default command to run when starting a container from this image.

Finally, the -t flag tags your image. Think of this as a human-readable name for the final image. Since you named the image getting-started, you can refer to that image when you run a container.

The . at the end of the docker build command tells Docker that it should look for the Dockerfile in the current directory.

## Docker run command

The -d flag (short for --detach) runs the container in the background. This means that Docker starts your container and returns you to the terminal prompt. You can verify that a container is running by viewing it in Docker Dashboard under Containers, or by running docker ps in the terminal.

The -p flag (short for --publish) creates a port mapping between the host and the container.
The -p flag takes a string value in the format of HOST:CONTAINER, where HOST is the address on the host, and CONTAINER is the port
on the container. The command publishes the container's port 3000 to 127.0.0.1:3000 (localhost:3000) on the host.
Without the port mapping, you wouldn't be able to access the application from the host.

## Remove old container

To remove a container, you first need to stop it. Once it has stopped, you can remove it.
You can remove the old container using the CLI or Docker Desktop's graphical interface.
Choose the option that you're most comfortable with.

```
docker ps
```

```
docker stop <container-id>
```

```
docker rm <container-id>
```

You can stop and remove a container in a single command by adding the `force` flag to the docker `rm` command.
For example: `docker rm -f <the-container-id>`

## Docker Volumes

With the previous experiment, you saw that each container starts from the image definition each time it starts.
While containers can create, update, and delete files, those changes are lost when you remove the container and
Docker isolates all changes to that container. With volumes, you can change all of this.

Volumes provide the ability to connect specific filesystem paths of the container back to the host machine.
If you mount a directory in the container, changes in that directory are also seen on the host machine. If you mount that same directory across container restarts, you'd see the same files.

There are two main types of volumes.

Anonymous volumes:
Anonymous volumes are created automatically by Docker when you mount a directory or file from the host machine
into a container. Anonymous volumes are not named and cannot be reused.

Named volumes:
Named volumes are created and managed by the user.
They are named and can be reused by multiple containers.

## Docker Bind Mounts

A bind mount is another type of mount, which lets you share a directory from the
host's filesystem into the container. When working on an application, you can use a
bind mount to mount source code into the container.
The container sees the changes you make to the code immediately, as soon as you save a file.
This means that you can run processes in the container that
watch for filesystem changes and respond to them.

### Run your app in a development container

```bash
docker run -dp 127.0.0.1:3000:3000 \
    -w /app --mount type=bind,src="$(pwd)",target=/app \
    node:18-alpine \
    sh -c "yarn install && yarn run dev"
```

The following is a breakdown of the command:

1. `-dp 127.0.0.1:3000:3000`- same as before. Run in detached (background) mode and create a port mapping
2. `-w /app - sets the "working directory"` or the current directory that the command will run from
3. `--mount type=bind,src="$(pwd)",target=/app` - bind mount the current directory from the host into the /app directory in the container
4. `node:18-alpine` - the image to use. Note that this is the base image for your app from the Dockerfile
5. `sh -c "yarn install && yarn run dev"` - the command. You're starting a shell using sh (alpine doesn't have bash)
   and running yarn install to install packages and then running yarn run dev to start the development server.
   If you look in the package.json, you'll see that the dev script starts nodemon.

## Muti Container Apps

The following are a few reasons to run the container separately:

There's a good chance you'd have to scale APIs and front-ends differently than databases.
Separate containers let you version and update versions in isolation.
While you may use a container for the database locally, you may want to use a managed service for the database in production. You don't want to ship your database engine with your app then.
Running multiple processes will require a process manager (the container only starts one process), which adds complexity to container startup/shutdown.

## Docker compose

Docker Compose is a tool that helps you define and share multi-container applications.
With Compose, you can create a YAML file to define the services and with a single command,
you can spin everything up or tear it all down.

The big advantage of using Compose is you can define your application stack in a file,
keep it at the root of your project repository (it's now version controlled), and easily enable someone
else to contribute to your project. Someone would only need to clone your repository and start the
app using Compose. In fact, you might see quite a few projects on GitHub/GitLab doing exactly this now.
