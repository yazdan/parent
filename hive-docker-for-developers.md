در این نوشته کوتاه سعی می‌شود که معرفی کوتاهی از [داکر] برای توسعه دهندگان آورده شود. [داکر] به عنوان یک ابزار مدرن جهت اجرای نرم‌افزارها در محیط توسعه و عملیاتی معرفی شده و مواردی که [داکر] باعث بهبود روند آنها می‌شود آورده می‌شود.

#معرفی داکر



## مفاهیم مختلف داکر

    Docker client: this is what's running in our machine. It's the docker binary that we'll be interfacing with whenever we open a terminal and type $ docker pull or $ docker run. It connects to the docker daemon which does all the heavy-lifting, either in the same host (in the case of Linux) or remotely (in our case, interacting with our VirtualBox VM).
    Docker daemon: this is what does the heavy lifting of building, running, and distributing your Docker containers.
    Docker Images: docker images are the blueprints for our applications. Keeping with the container/lego brick analogy, they're our blueprints for actually building a real instance of them. An image can be an OS like Ubuntu, but it can also be an Ubuntu with your web application and all its necessary packages installed.
    Docker Container: containers are created from docker images, and they are the real instances of our containers/lego bricks. They can be started, run, stopped, deleted, and moved.
    Docker Hub (Registry): a Docker Registry is a hosted registry server that can hold Docker Images. Docker (the company) offers a public Docker Registry called the Docker Hub which we'll use in this tutorial, but they offer the whole system open-source for people to run on their own servers and store images privately.


#مشکلاتی که حل می‌کند
    Consistent development environments for your entire team. All developers use the same OS, same system libraries, same language runtime, no matter what host OS they are using (even Windows if you can believe it).
    The development environment is the exact same as the production environment. Meaning you can deploy and it will “just work”.
    If you’re having a hard time building something (by build, I mean compile), build it inside Docker. This primarily applies to developers using MacOS and Windows.
    You only need Docker to develop. You don’t need to install a bunch of language environments on your machine. Want to run a Ruby script but don’t have Ruby installed? Run it in a Ruby Docker image.
    Can use multiple language versions without having to resort to all the hackarounds for your language (python, python, ruby, ruby, java, node). Want to run your Python program in Python 3, but only have Python 2 installed? Run it using Python 3 image. Want to compile your Java program with Java 1.6 instead of the 1.7 that’s installed on your machine? Compile it in a Java 1.6 Docker image.
    Deployment is easy. If it runs in your container, it will run on your server just the same. Just package up your code and deploy it on a server with the same image or push a new Docker image with your code in it and run that new image.
    Can still use your favorite editor/IDE as you normally do. No need for running a VM in VirtualBox and SSHing in and developing from the shell just so you can build/run on a Linux box.

#امکانات داکر

پورت
لینک
ولیوم
compose


