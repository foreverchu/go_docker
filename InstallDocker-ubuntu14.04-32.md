1.
Ubuntu 14.04 版本系统中已经自带了 Docker 包，可以直接安装。

$ sudo apt-get update
$ sudo apt-get install -y docker.io
$ sudo ln -sf /usr/bin/docker.io /usr/local/bin/docker
$ sudo sed -i '$acomplete -F _docker docker' /etc/bash_completion.d/docker.io
安装之后启动 Docker 服务。

$ sudo service docker start





-------------------------------------------------------------------





下载镜像 sudo docker pull ubuntu:12.04  该命令实际上相当于 $ sudo docker pull registry.hub.docker.com/ubuntu:12.04 命令，即从注册服务器 registry.hub.docker.com 中的 ubuntu 仓库来下载标记为 12.04 的镜像。

创建容器 sudo sudo docker run -t -i ubuntu:12.04 /bin/bash
-t 选项让Docker分配一个伪终端（pseudo-tty）并绑定到容器的标准输入上， -i 则让容器的标准输入保持打开


列出镜像 sudo docker images

列出容器 sudo docker ps -a

进入容器 sudo docker attach <container_id> 只能进入启动到容器，不然需要现启动，再进入

清除容器 sudo docker rm $(sudo docker ps -a -q)


启动已终止容器： docker start <CONTAINER_ID>





---------------------------------



Docker 仓库

仓库是集中存放镜像文件的场所。有时候会把仓库和仓库注册服务器（Registry）混为一谈，并不严格区分。实际上，仓库注册服务器上往往存放着多个仓库，每个仓库中又包含了多个镜像，每个镜像有不同的标签（tag）。

仓库分为公开仓库（Public）和私有仓库（Private）两种形式。

最大的公开仓库是 Docker Hub，存放了数量庞大的镜像供用户下载。 国内的公开仓库包括 Docker Pool 等，可以提供大陆用户更稳定快速的访问。

当然，用户也可以在r地网络内创建一个私有仓库。

当用户创建了自己的镜像之后就可以使用 push 命令将它上传到公有或者私有仓库，这样下次在另外一台机器上使用这个镜像时候，只需要从仓库上 pull 下来就可以了。

*注：Docker 仓库的概念跟 Git 类似，注册服务器可以理解为 GitHub 这样的托管服务。





Docker 镜像

Docker 镜像就是一个只读的模板。

例如：一个镜像可以包含一个完整的 ubuntu 操作系统环境，里面仅安装了 Apache 或用户需要的其它应用程序。

镜像可以用来创建 Docker 容器。

Docker 提供了一个很简单的机制来创建镜像或者更新现有的镜像，用户甚至可以直接从其他人那里下载一个已经做好的镜像来直接使用。

*注 : 下载ubuntu 32位镜像 m.blog.csdn.net/blog/zqxnum1/42063521 。 然后执行sudo cat ubuntu-14.04-x86-minimal.tar.gz | sudo docker import - ubuntu  。通过sudo docker images 就能看到了











Docker 容器

Docker 利用容器来运行应用。

容器是从镜像创建的运行实例。它可以被启动、开始、停止、删除。每个容器都是相互隔离的、保证安全的平台。

可以把容器看做是一个简易版的 Linux 环境（包括root用户权限、进程空间、用户空间和网络空间等）和运行在其中的应用程序。

*注：镜像是只读的，容器在启动的时候创建一层可写层作为最上层。





---

### 显示镜像信息：

cat /var/lib/docker/repositories |python -mjson.tool

或者docker images


---

exit 退出容器

docker start启动关闭的容器



