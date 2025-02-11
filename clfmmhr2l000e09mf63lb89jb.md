---
title: "How I set up my first Hadoop / Spark cluster: Preparation"
datePublished: Thu Apr 02 2020 22:15:04 GMT+0000 (Coordinated Universal Time)
cuid: clfmmhr2l000e09mf63lb89jb
slug: how-i-set-up-my-first-hadoop-spark-cluster-preparation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1679563311820/2a7f8c03-11f9-42ee-ad6b-a70eb6769bd2.jpeg
tags: hadoop, big-data, spark, raspberry-pi

---

I’ve been envisaging setting up a cluster for Big Data practice for quite some time now. Coming from a traditional Business Intelligence background into a Software Engineering role (albeit still heavily data-related), it was only a matter of time before Big Data technologies would catch my eye.

From an outsider’s perspective, the Big Data landscape sounds like a collection of buzzwords and a myriad of products: starting from the more familiar Hadoop and going to the wide array of components that fit into that ecosystem: HDFS, Yarn, Spark, Pig, Hive, Airflow or Nifi. I’ve got to admit that some of them have really funny names, but how do they all fit into this picture?

Well, I was bound to start finding out, but this sort of thing is not something you’d pick up by watching a video tutorial. Moreover, learning something new is always exciting in the beginning but pretty discouraging when you stumble upon a roadblock. I did try setting up Hadoop at least two times before: once locally and another time using a [Cloudera Quick Start VM](https://www.cloudera.com/developers/get-started-with-hadoop-tutorial.html) . The first time I’ve given up after a few minutes trying to set up my local Java environment (I know, I know), whereas the second time I felt that given it’s a single node, sandbox setup, it wasn’t as close to the ‘real thing’ as I’d wanted.

This article, the first in a series of posts, is essentially a compilation of my travel notes on this journey. It’s not intended to be a tutorial, as I’ll be referencing other comprehensive and well-written resources that covered 90% of the way. Its purpose is to reduce the time that the reader (or future me) needs for the other 10%, or perhaps serve as a soft introduction to the topic. This has been a long introduction, so let’s get to work!

### The Preparation

Before starting to do anything, I looked at different resources available online, searching for a tutorial that would guide me along the way.

I’ve found this [**well-documented and simply outstanding series**](https://dev.to/awwsmm/building-a-raspberry-pi-hadoop-spark-cluster-8b2), written by a guy named Andrew based in Dublin, which explained everything I needed to know before starting. There were a couple of adjustments I had to make here and there.

#### Hardware

First, I wanted to go the real hardware route as opposed to setting up a fleet of VMs. So I decided to have a Raspberry Pi Cluster. I already had a [1GB Raspberry Pi 3B](https://thepihut.com/products/raspberry-pi-3-model-b-plus) (bought a couple of years ago for £35) and bought another [2GB Raspberry Pi 4B](https://thepihut.com/products/raspberry-pi-starter-kit) and [a cluster case](https://thepihut.com/products/cluster-case-for-raspberry-pi) with cooling fans. The nice thing about it: is I’ve got them delivered in under 24 hours from the UK to Bucharest. In addition to the two Pi-nodes, I will be setting up another node on my laptop, which will also be the master.

While there are better options for network performance and look ([PoE](https://en.wikipedia.org/wiki/Power_over_Ethernet)), since my devices have WiFi connectivity I’ve decided to let them communicate via wireless and be charged using standard (phone-like) chargers. Both have a 16GB microSD card as storage.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563299735/4dc89390-851c-461d-9e7e-f68e059b0ee8.png align="left")

Plan for my cluster

#### Operating system

Next, setting up the Pis. While they do come with [Noobs](https://www.raspberrypi.org/downloads/noobs/) — an easy operating system installer — which allows installing [Raspbian](https://www.raspberrypi.org/downloads/raspbian/), a Debian-based Linux which is the most popular choice for Raspberry Pis, I’ve decided to go with Ubuntu for this platform. I downloaded the [Ubuntu server image](https://ubuntu.com/download/raspberry-pi) and burned it to a microSD on my PC using an SD adapter with the [Pi Imager](https://www.raspberrypi.org/blog/raspberry-pi-imager-imaging-utility/) — a straightforward process that took about 3 minutes.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563301463/9f5b62fd-275d-4b5c-9d98-7c3d72066087.png align="left")

Raspberry Pi Imager

Then, I set up the wireless connectivity for my newly set up Raspberry Pi using the instructions [available here](https://askubuntu.com/questions/1143287/how-to-setup-of-raspberry-pi-3-onboard-wifi-for-ubuntu-server-18-04).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563303384/074ebb4b-8a0e-45d6-97f4-9b50a1e16db3.png align="left")

*/etc/netplan/50-cloud-init.yaml*

#### Hostnames

Next, I’ve set up hostnames and hosts on each machine.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563305382/b152fc24-1793-4b0d-a650-24c2e82e41f7.png align="left")

*/etc/hostname* and */etc/hosts* for one of the Pis

#### SSH

Another important step is the SSH setup. This will allow connecting to and running commands on machines in our cluster. We start with enabling SSH on the machines:

```plaintext
`sudo apt update  
sudo apt install openssh-server`
```

We can test that the service is up with:

```plaintext
sudo systemctl status ssh
```

Now, say *ubuntu* is our user and *rpi-3* is the machine we want to connect to, we could execute the following command, type in the password and be connected.

```bash
ssh ubuntu@rpi-3
```

There are a couple of more things we need to take care of. To enable passwordless login, let’s create a public-private key pair on the master:

```bash
ssh-keygen
```

This will generate a public and a private key, with the default location being ***~/.ssh***.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563307063/486cc5d6-cd13-4c16-81bb-3fe33c43d3bd.png align="left")

We’ll now append our **public key** to the slaves’ authorized\_keys

```plaintext
cat ~/.ssh/id_rsa.pub | ssh ubuntu@rpi-3 'cat >> .ssh/authorized_keys'
```

Then, on the master, we’ll set up a config file at ***~/.ssh/config*** as follows:

```bash
Host rpi-3
HostName rpi-3
User ubuntu
IdentityFile ~/.ssh/id_rsa

Host rpi-4
HostName rpi-4
User ubuntu
IdentityFile ~/.ssh/id_rsa
```

Now, connecting to another machine via SSH is as simple as:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563308601/b87febe0-bd38-4525-9400-74a10e295e24.png align="left")

#### Security and utility

The [previously referenced tutorial](https://dev.to/awwsmm/building-a-raspberry-pi-hadoop-spark-cluster-8b2) also took steps towards securing the cluster (disabling password logins, login and the potentially compromising message of the day) — important advice which I believe should be followed. Moreover, utility functions were suggested that would enable executing a command once for all machines in the cluster. For instance, I’ve added the following to my ***.bashrc*** so that one command can be issued from the master and executed on all nodes. I’ve slightly modified mine so that the *otherpis* looks up hosts that have “*rpi-*” in their name and the *clustercmd* does not execute the command on my main machine.

```plaintext
function otherpis {  
  grep "rpi-" /etc/hosts | awk '{print $2}' | grep -v $(hostname)  
}
```

```plaintext
function clustercmd {  
  for pi in $(otherpis); do ssh $pi "$@"; done  
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563309878/926b79f3-ae05-45cb-a89b-957cc9ab6fc4.png align="left")

#### Conclusion

Now that we have a working set of machines on that we can execute commands, we can proceed to set up Hadoop and Spark. I will be detailing the problems I’ve encountered in the process in an upcoming article. Thank you for reading and see you soon.

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*