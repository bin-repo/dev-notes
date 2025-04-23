# docker-dockerfile

Dockerfile 参考指南

## `FROM <image>`

- Defines a base for your image.
- 引用基础镜像

## `RUN <command>`

- Executes any commands in a new layer on top of the current image and commits the result.
- RUN also has a shell form for running commands.
- 构建镜像时执行的命令

## `CMD <command>`

- Lets you define the default program that is run once you start the container based on this image.
- Each Dockerfile only has one CMD, and only the last CMD instance is respected when multiple exist.
- 镜像容器启动时一次性执行的默认命令

## `USER <user:group> 或 <UID:GID>`

- Sets the user name (or UID) and optionally the user group (or GID).
- 切换当前用户及组

## `WORKDIR <directory>`

- Sets the working directory for any `RUN`, `CMD`, `ENTRYPOINT`, `COPY`, and `ADD` instructions that follow it in the Dockerfile.
- 切换当前工作目录

## `COPY [--chown=user:group] <src> <dest>`

- Copies new files or directories from 'src' and adds them to the filesystem of the container at the path 'dest'.
- 复制文件/目录到镜像

## `ADD [--chown=user:group] <src> <dest>`

- Copies new files, directories or remote file URLs.
- 复制文件/目录/网络资源到镜像

## `ARG <Key=Value>`

- Declare the variables.
- 定义构建镜像过程引用的参数

## `ENV <key=value>`

- Sets the environment variable and will persist when a container is run from the resulting image.
- 定义环境变量，镜像和容器均有效

## `LABEL <key=value key=value ...>`

- Adds metadata to image
- 添加镜像元数据

## `EXPOSE <port/protocl ...>`

- the container listens on the specified network ports at runtime.
- 定义容器运行时对外端口

## `ENTRYPOINT ["exec", "param1", "param2"]`

- configure a container that will run as an executable.
- 配置为可执行容器

## `VOLUME ["/data"]`

- creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers.
- 定义挂载点，用于挂载主机或其他容器数据卷
