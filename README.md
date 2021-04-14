<div align="center">

# The Good Karma Kit

> A Docker Compose project to run on servers with spare CPU, RAM, and bandwidth to help the world.

<img src="https://user-images.githubusercontent.com/511499/114660274-03b9dc00-9cc3-11eb-9db2-19ff3817d5f9.png" width="400px"/>

</div>

Contribute your unused computing power to good causes.

1. Download [`docker-compose.yml`](https://github.com/pirate/good-karma-kit/blob/main/docker-compose.yml) into an empty directory
2. `mkdir data`
3. `docker-compose up`
4. Finish setting up projects through their respective web dashboards exposed on localhost

You can also comment out any containers you don't want to run in the compose file.

Unless otherwise specified or restricted to 127.0.0.1 in the compose file, all ports should be made available to the public internet.
The nature of most of these containers is that you're contributing resources to the public or to specific causes running on the public internet,
so make sure you understand the risks involved with exposing your machine to WAN. It may be worth running this in an isolated VM on an isolated subnet if it's on your home or corporate network.

## Contents

---

### Autoupdater

#### watchtower

`image: containrrr/watchtower`

Automatically updates & restarts the containers when they have new versions available 

https://containrrr.dev/watchtower/  
https://github.com/containrrr/watchtower

Notes: requires access to system docker socket, and will autoupdate *all* running containers on the host unless scoped with labels.

---

### Distributed networking projects

#### tor

`image: thetorproject/obfs4-bridge:latest`

https://www.torproject.org/  
https://hub.docker.com/r/thetorproject/obfs4-bridge


#### i2p

`image: divax/i2p:i2p-tor`

https://geti2p.net/en/  
https://hub.docker.com/r/divax/i2p

---

### Distribued storage projects

#### ipfs

`image: ipfs/go-ipfs:latest`

https://ipfs.io  
https://hub.docker.com/r/ipfs/go-ipfs


#### storj

`image: storjlabs/storagenode:latest`

https://www.storj.io/  
https://hub.docker.com/r/storjlabs/storagenode

Notes: 💰 This one earns you money for your storage! Set up your `WALLET` address for payouts.

#### sia

`image: nebulouslabs/sia`

https://sia.tech/  
https://hub.docker.com/r/nebulouslabs/sia

---

### Distributed computing projects

#### boinc

`image: ghcr.io/linuxserver/boinc`

https://boinc.berkeley.edu/  
https://hub.docker.com/r/linuxserver/boinc
    
Notes: if you have a GPU, it will help computations greatly, please uncomment the /dev/dri line.


#### foldingathome

`image: ghcr.io/linuxserver/foldingathome`

https://foldingathome.org/  
https://hub.docker.com/r/linuxserver/foldingathome

---

### Internet Archiving projects

#### archivewarrior

`image: archiveteam/warrior-dockerfile`

http://warrior.archiveteam.org/  
https://hub.docker.com/r/archiveteam/warrior-dockerfile/


#### zimfarm

`image: openzim/zimfarm-worker-manager`

https://github.com/openzim/zimfarm  
https://hub.docker.com/r/openzim/zimfarm-worker-manager
    
Notes: this one requires a static IP! You must contact Kiwix to get your worker set up, and get your static IP whitelisted.

#### kiwix

`image: kiwix/kiwix-serve:latest`

https://www.kiwix.org/en/  
https://hub.docker.com/r/kiwix/kiwix-serve
    
Notes: this one requires you download some ZIM archives to serve into `./data/kiwix`, get those from here: https://wiki.kiwix.org/wiki/Content_in_all_languages

#### archivebox

`image: archivebox/archivebox:latest`

https://archivebox.io  
https://hub.docker.com/r/archivebox/archivebox/
    
Notes: this one is empty by default, add some sites to archive or crawl regulary using the web UI or CLI.

#### pywb

`image: webrecorder/pywb:latest`

https://github.com/webrecorder/pywb  
https://hub.docker.com/r/webrecorder/pywb
    
Notes: this one is empty by default, add some sites to archive or crawl regulary using the web UI or CLI.

---

## Contribute

Contributions are welcome! Please open an issue or PR to suggest a new container be added to the bundle.
