# Supported tags
-   [`1.9.5`, `1.9.5-r2`, `latest` (*[1.9.5-r2/Dockerfile](https://github.com/gkweb76/dnscrypt-proxy/blob/master/1.9.5-r2/Dockerfile)*)]



# What is DNSCrypt proxy
[DNSCrypt proxy](https://dnscrypt.info/) is a DNS resolver using DNScrypt protocol, which works with encrypted DNS requests to DNSCrypt enabled servers.  
![](https://dnscrypt.info/_nuxt/img/dnscrypt.cd47d19.png)



# Why using this image ?
This image is a vanilla DNSCrypt proxy software without any additional packages installed. This enables you to run it concurrently with the DNS caching service of your choice (e.g Unbound).  

This image is based on [Alpine Linux](https://alpinelinux.org/) and therefore is built with [LibreSSL](https://www.libressl.org/), which is a more secure fork of OpenSSL made by the [OpenBSD](https://www.openbsd.org/) team. Also Alpine Linux is generally immune to vulnerabilities targetting components not installed in this Operating System, such as: bash (e.g. Shellshock vulnerability), OpenSSL (e.g. Heartbleed vulnerability), glibc (e.g Ghost vulnerability). Also, Alpine Linux has a much smaller image size compared to other OS thanks to less packages installed by default and not relying on glibc, providing faster image download, and reduced attack surface, hence better security.

![](https://wiki.alpinelinux.org/w/resources/assets/alogo.png)



# Maintained by
Guillaume Kaddouch  
Blog: [https://networkfilter.blogspot.com/](https://networkfilter.blogspot.com/)  
Twitter: [@gkweb76](https://twitter.com/gkweb76)  
Github: [gkweb76](https://github.com/gkweb76/)  



# How to use this image from command line
Start your container with the local port of your choice:  
`docker container run --rm --read-only=true --name dnscrypt-proxy \`  
`-e LOCAL_IP=0.0.0.0 -e LOCAL_PORT=53 -e SERVER=dnscrypt.eu-dk gkweb76/dnscrypt-proxy`  


# Docker compose example  
`version: "3.5"`  
  
`services:`  
&nbsp;&nbsp;  `dnscrypt:`  
&nbsp;&nbsp;  `image: gkweb76/dnscrypt-proxy:latest`  
&nbsp;&nbsp;  `container_name: dnscrypt-proxy`  
&nbsp;&nbsp;  `read_only: yes`  
&nbsp;&nbsp;  `networks:`  
&nbsp;&nbsp;&nbsp;&nbsp;  `- dnscrypt`  
&nbsp;&nbsp;    `environment:`  
&nbsp;&nbsp;&nbsp;&nbsp;  `- LOCAL_IP=0.0.0.0 # host IP`  
&nbsp;&nbsp;&nbsp;&nbsp;  `- LOCAL_PORT=53 # container port`  
&nbsp;&nbsp;&nbsp;&nbsp;  `- SERVER=dnscrypt.eu-dk`  
&nbsp;&nbsp;    `volumes:`   
&nbsp;&nbsp;&nbsp;&nbsp;      `- /etc/localtime:/etc/localtime:ro # keep container clock in sync with host`  
&nbsp;&nbsp;    `restart: "unless-stopped"`  
  
`# Networks declaration`  
`networks:`  
&nbsp;&nbsp;  `dnscrypt:` 
    
If you need help with your compose file, check the official [documentation](https://docs.docker.com/compose/compose-file/).  


# Tested on

[Ubuntu](https://www.ubuntu.com/) 18.04 LTS and Docker 18.04.0 CE (Community Edition).

# License

MIT License
