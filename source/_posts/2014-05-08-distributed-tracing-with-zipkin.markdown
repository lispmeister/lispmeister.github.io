---
layout: post
title: "Distributed Tracing with Zipkin"
date: 2014-05-08 18:35
comments: true
categories: [distributed, tracing, Docker, Cassandra, Zipkin, programming, design]
---
{% img right /images/2014/05/zipkin-docker-small.png 400 339 'Distributed Tracing with Zipkin' 'Distributed Tracing with Zipkin' %}

Instead of parsing log file entries we now send tracing messages to a
Zipkin collector. To make initial development easier we containerized
a fully working Zipkin environment. All you need is `Virtualbox` and
`boot2docker` to boot Zipkin and run the demo Scala code.

All Docker images needed for Zipkin are registered as trusted builds
with the Docker.io index. To give it a spin you can just checkou the
Scala / Akka demo project and deploy the images. If you're curious the
Docker project shows how to setup and link containers.

Below you'll find instructions on how to test the Zipkin containers
with a Scala / Akka project running locally on your OSX host.

You first need to install VirtualBox.
<https://www.virtualbox.org/wiki/Downloads>

Information on running Docker on OSX can be found here:
<http://docs.docker.io/installation/mac/>

You need to have the Homebrew package manager installed:
<http://brew.sh/>

You need to install `boot2docker`:

    brew update
    brew install boot2docker
    brew install docker
    
Once boot2docker is installed boot the VM for the first time:

    export DOCKER_HOST=tcp://127.0.0.1:4243
    boot2docker init
    boot2docker start

When booting the images via boot2docker on OSX you will need to make
sure the guest VM ports are forwarded. Here's an example that forwards
the relevant ports for the Zipkin services:

    # vm must be powered off 
    boot2docker stop
    # collector
    VBoxManage modifyvm "boot2docker-vm" --natpf1 "tcp-port9410,tcp,127.0.0.1,9410,,9410"
    VBoxManage modifyvm "boot2docker-vm" --natpf1 "udp-port9410,udp,127.0.0.1,9410,,9410"
    VBoxManage modifyvm "boot2docker-vm" --natpf1 "tcp-port9900,tcp,127.0.0.1,9900,,9900"
    # query
    VBoxManage modifyvm "boot2docker-vm" --natpf1 "tcp-port9411,tcp,127.0.0.1,9411,,9411"
    # web
    VBoxManage modifyvm "boot2docker-vm" --natpf1 "tcp-port8080,tcp,127.0.0.1,8080,,8080"
    # cassandra
    VBoxManage modifyvm "boot2docker-vm" --natpf1 "tcp-port7000,tcp,127.0.0.1,7000,,7000"
    VBoxManage modifyvm "boot2docker-vm" --natpf1 "tcp-port7001,tcp,127.0.0.1,7001,,7001"
    VBoxManage modifyvm "boot2docker-vm" --natpf1 "tcp-port9042,tcp,127.0.0.1,9042,,9042"
    VBoxManage modifyvm "boot2docker-vm" --natpf1 "tcp-port9160,tcp,127.0.0.1,9160,,9160"
    # start VM
    boot2docker start

## Install and Boot Zipkin

Clone the demo project:

    git clone https://github.com/lispmeister/psychic-octo-bear.git zipkin-tracing-demo
    cd zipkin-tracing-demo

Now you're ready to deploy the Docker images for Zipkin.
The images are all registered at
<https://index.docker.io/u/lispmeister/>
and will be downloaded automatically.

    bin/deploy-zipkin.sh

This will fetch the Docker images from the Docker.io index and start
the containers. Downloading the Docker images will take a while. Be
patient. Once the images are downloaded the deploy script will start
the containers. Wait until the CPU load is below 40% again. Booting
Cassandra in the container can take quite a while.

If you want to trace code that runs on the host you will need to
expose and forward the collector port as shown in deploy.sh.

Once the containers are running you can connect to the collector on
port 9410 via akka-tracing or other libraries that support Zipkin tracing.
<https://github.com/levkhomich/akka-tracing>

## Install SBT

You need to have `sbt` installed.

    brew install sbt

## Run the demo
The demo creates ten Put requests that flow through the Web,
Service, S3 actors. The flows into and out of the actors are traced
using the Akka Tracing library which implements a Scala interface for
the Twitter Zipkin distributed tracing tool.

    sbt run

## Inspect the Trace
Open a browser to the local Zipkin web instance at this address:

<http://127.0.0.1:8080/>

## Links:

- [Scala / Akka Demo Project](https://github.com/lispmeister/psychic-octo-bear)
- [Docker container with Zipkin](https://github.com/lispmeister/docker-zipkin)




  
