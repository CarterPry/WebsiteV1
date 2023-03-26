---
title: "Apache Guacamole"
date: 2022-10-09 20:55:37 +0100
description: "Manage server connections through your browser"
summary: "Managing your servers via web browser with the help of the docker container Guacamole"
tags: ["Networking", "Server-Management", "Docker"]
---

## Guacamole Docker 
Guacamole, not just a chip dip, but a docker package that's capable of server management via web browser. A friend of mine, [Zach Robinson](https://zsrobinson.com), introduced to me this little project that I wanted to try myself. I set up the docker package as well as a VNC server on a Linux Mint PC. Though Mint was used for this, this projects is also compatible with other images as well. This VNC server is what the project is surrounded with the end goal of being able to access it through something like Firefox or Brave. Though that is what I used for an example, it does take in multiple other connections to be managed by the system admin.

## What's VNC
A virtual network computing (VNC) server is a screen sharing protocol that is similar to Remote Desktop Protocol (RDP) but works differently. One of the larger differences from VNC to RDP is that VNC doesn't use a virtual session like RDP. For example VNC uses the same display as what the user would see on the actual server in front of them. If you were to use RDP on someone's computer the person in front of the actual server wouldn't see the mouse moving around but for VNC you do. I chose to indulge with this frame by frame service due to the fact that I had never actually used it before. I did feel as if it would be fun to not just work with an unknown docker project, but implement it with another unknown configuration. 

## Installing VNC
The first task at hand was to get the VNC server running on the PC. To do this, I installed the required packages and configured the required parts it needed to be active. For Linux Mint there is a good guide for setting one up [here](https://community.linuxmint.com/tutorial/view/2334)  

## Installing Guacamole
Next you would need to add docker to your system, which may vary different installation methods based on your image. Once it was installed on my PC I used the command

```json
docker pull oznu/guacamole
```

## Running the Chip Dipping Package
A way to run this service is with a few parts, with first consisting of the docker command `docker run` to start the package. 

The 2nd line specifies the port with the left listed being for the host, and the right as the container port number. 
 (I used -p 80:8080\)

The 3rd line is the location of where you want the guacamole configuration to be held, a location at your choosing 
Lastly the 4th line is the package specification. Which Docker container are you using for these commands. 

The command below is a good guideline on how it should look.

```json
docker run\
  -p (Host):(Container)\
  -v (Dedicated Config Location):/config\
  oznu/guacamole
```

After running that command with the config directory filled in, I could login to the hosting PC´s LAN IP. It was a web server being hosted with a login prompt at the front.

## Establishing Connections
The front page has default credentials with both being `guacadmin`. To change this all you would need to do was log in with the default values, and change it in the settings. In this same location you can even make other accounts with different permissions in case you wanted to share your browser project access. I personally created a new account for a custom username and password so i could delete the default login. 

Now to connect the VNC portion with this site I had to enter the right connection parameters. There are tons of options for your choosing, even with connections including SSH, RDP, Telnet and Kubernetes. For this I selected VNC, entered the hostname (the LAN IP) of the PC and the credentials of that VNC server I set (Not to confuse the creditntails I entered for Guacamole). There are more options you can fill out like load balancing or number of connections but leaving them blank is perfectly fine. There are only some required fields that would need a value. Once done, I could go back to the home page and see the new connection that is now established. I could select the connection and start using my PC through just my browser

## Outside your LAN
One of the cool things you can do is actually make it accessible from a public IP as well. Meaning you can access it from the internet from not just your home but anywhere else as well. Though it may not be fully secure, it is something interesting you can set up. You could either port forward your router to make that Docker PC accessible with the right port, or even tie it to a domain name. For instance If I decided to go through with that concept, I could type in `carterpry.com` and would be brought straight to the guacamole login page.

