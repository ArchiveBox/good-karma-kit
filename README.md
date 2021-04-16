<div align="center">

<h1>The Good Karma Kit</h1>

<img src="https://user-images.githubusercontent.com/511499/114660274-03b9dc00-9cc3-11eb-9db2-19ff3817d5f9.png" width="300px"/><br/>
<i><b>A Docker Compose project to run on servers with spare CPU, disk, and bandwidth.</b><br/>Help the world by contributing your unused computing power to good causes.</i>

</div>

## Quickstart

1. Download [`docker-compose.yml`](https://github.com/pirate/good-karma-kit/blob/main/docker-compose.yml) into an empty directory (or clone this repo)
2. Edit the `docker-compose.yml` file to fill in config vars, tune resource limits, or comment out containers you don't want to run
3. Download the most recent images and start the containers
```bash
mkdir -p data
docker-compose pull
docker-compose up <servicename>  # start them one at a time
docker-compose up                # or all at once
```
4.  Finish setting up some projects through their respective web dashboards exposed on localhost (see below)


Next steps: Check the status of everything
```bash
docker-compose ps
apt install ctop && ctop
```
Or use the web dashboard / publics leaderboards for each service.

*See the notes below for more info on each container, what it does, and what companies it's affiliated with.*

## Caveats

The nature of most of these containers is that you're contributing resources to the public or to specific causes running on the public internet.
Unless otherwise specified or restricted to 127.0.0.1 in the compose file, all ports should be made available to the public internet.
Make sure you understand the risks involved with exposing your machine to WAN. It may be worth running this in an isolated VM on an isolated subnet if it's on your home or corporate network.

Two containers need access to `/var/run/docker.sock` to function: `watchtower` (the autoupdater), and `zimfarm` (which uses it to spawn containers for its sub-tasks). Both are optional and can be commented out, just make sure to update the containers yourself semi-regularly if you disable the `watchtower`.

Not all the containers are not-for-profit, some either reward you with cryptocurrency, or are affiliated with for-profit entities. Each container is marked below with its non-profit/for-profit status.

If there are too many containers for your liking, the top-3 high-impact and easy-to-run ones are:

- ⭐️  `archivewarrior`
- ⭐️  `boinc`
- ⭐️  `tor`

## Contents

---

### Autoupdater

#### watchtower

`image: containrrr/watchtower`

> Automatically update & restart docker containers when they have new versions available. (open source helper container)

[https://containrrr.dev/watchtower/](https://containrrr.dev/watchtower/)  
[https://github.com/containrrr/watchtower](https://github.com/containrrr/watchtower)

Notes: requires access to system docker socket, and will autoupdate *all* running containers on the host unless scoped with [labels](https://github.com/ArchiveBox/good-karma-kit/issues/1).

---

### Distributed networking projects

#### tor ⭐️

`image: thetorproject/obfs4-bridge:latest`

> Run a relay node for the Tor onion routing netowrk that helps people use the internet with as much privacy as possible. (501(c)(3) US nonprofit)

[https://www.torproject.org/](https://www.torproject.org/)  
[https://hub.docker.com/r/thetorproject/obfs4-bridge](https://hub.docker.com/r/thetorproject/obfs4-bridge)

Notes: don't worry, this is just a relay node, not an entry/exit node. Police wont come bashing down your door, this is safe to run on a home network.

#### i2p

`image: divax/i2p:i2p-tor`

> Run a relay node for the i2p routing network (similar to Tor). (501(c)(3) US nonprofit)

[https://geti2p.net/en/](https://geti2p.net/en/)  
[https://hub.docker.com/r/divax/i2p](https://hub.docker.com/r/divax/i2p)


---

### Distributed computing projects

#### boinc ⭐️

`image: ghcr.io/linuxserver/boinc`

> Help contribute CPU and GPU power to a wide variety of scientific research projects, including protein folding, alien signal detection, and more! (operated not-for-profit by UC Berkeley and funded by the NSF)

[https://boinc.berkeley.edu/](https://boinc.berkeley.edu/)  
[https://hub.docker.com/r/linuxserver/boinc](https://hub.docker.com/r/linuxserver/boinc)
    
Notes: if you have a GPU, it will help computations greatly, please uncomment the /dev/dri line.


#### foldingathome

`image: ghcr.io/linuxserver/foldingathome`

> Help contribute CPU power to solve protein folding problems in bioscience, crucial to the development of vacienes and our understanding of molecular biology and mechanics. (operated by a research group at Washington University in Saint Louis, a 501(c)(3) non-profit) 

[https://foldingathome.org/](https://foldingathome.org/)  
[https://hub.docker.com/r/linuxserver/foldingathome](https://hub.docker.com/r/linuxserver/foldingathome)


---

### Internet Archiving projects

#### archivewarrior ⭐️

`image: atdr.meo.ws/archiveteam/warrior-dockerfile:latest` or `archiveteam/warrior-dockerfile`

> Help contribute CPU and bandwidth to archive parts of the internet automatically before they go down. Has helped save large swaths of the internet from going dark forever by adding them to Archive.org. (operated by an open-source collective, not-for-profit)

[https://warrior.archiveteam.org/](https://warrior.archiveteam.org/)  
[https://hub.docker.com/r/archiveteam/warrior-dockerfile/](https://hub.docker.com/r/archiveteam/warrior-dockerfile/)

#### zimfarm

`image: openzim/zimfarm-worker-manager`

> Help contribute CPU and bandwidth to *archive* large content collections for offline use in areas with limited internet. Helps many communities access things like Wikipedia, Project Gutenberg, and more. (operated by the Swiss non-profit Kiwix/OpenZIM)

[https://github.com/openzim/zimfarm](https://github.com/openzim/zimfarm)  
[https://hub.docker.com/r/openzim/zimfarm-worker-manager](https://hub.docker.com/r/openzim/zimfarm-worker-manager)
    
Notes: this one requires a static IP and >1TB of monthly network transfer available! You must [contact Kiwix to get your worker set up](https://github.com/openzim/zimfarm/blob/master/workers/README.md#zimfarm-workers), and get your static IP whitelisted.

#### kiwix

`image: kiwix/kiwix-serve:latest`

> Help contribute bandwidth and disk to *serve* large content collections to users in areas with limited or censored internet. This is the server for the content that `zimfarm` archives. (operated by the Swiss non-profit Kiwix/OpenZIM)

[https://www.kiwix.org/en/](https://www.kiwix.org/en/)  
[https://hub.docker.com/r/kiwix/kiwix-serve](https://hub.docker.com/r/kiwix/kiwix-serve)

Notes: this one requires you download some ZIM archives to serve into `./data/kiwix`, get those from here: [https://wiki.kiwix.org/wiki/Content_in_all_languages](https://wiki.kiwix.org/wiki/Content_in_all_languages)

#### archivebox

`image: archivebox/archivebox:latest`

> Use ArchiveBox as a tool to archive sites you care about for offline visiting or rehosting after they go down. (open source project, not-for-profit)

[https://archivebox.io](https://archivebox.io)  
[https://hub.docker.com/r/archivebox/archivebox/](https://hub.docker.com/r/archivebox/archivebox/)
    
Notes: this one is empty by default, add some sites to archive or crawl regulary using the web UI or CLI.

#### pywb

`image: webrecorder/pywb:latest`

> Use PYWB as a tool to archive sites you care about for offline visiting or rehosting after they go down. (open source project, not-for-profit, affiliated with Rhizome/Webrecorder)

[https://github.com/webrecorder/pywb](https://github.com/webrecorder/pywb)  
[https://hub.docker.com/r/webrecorder/pywb](https://hub.docker.com/r/webrecorder/pywb)
    
Notes: this one is empty by default, add some sites to archive or crawl regulary using the web UI or CLI.

---

### Distribued storage projects

(these serve assets to the public, 

#### ipfs

`image: ipfs/go-ipfs:latest`

> Run a storage node (free/not-for-profit) on the IPFS distributed storage network and pin files you care about to help serve them to others. (operated by Protocol Labs Inc., a for-profit 💰 US company)

[https://ipfs.io](https://ipfs.io)  
[https://hub.docker.com/r/ipfs/go-ipfs](https://hub.docker.com/r/ipfs/go-ipfs)


#### storj

`image: storjlabs/storagenode:latest`

> Run a storage node (for profit) on the Storj distributed storage network, automatically contribute your storage space and bandwidth and earn cryptocurrency in return. (operated by Storj Labs Inc., a for-profit 💰 US company)

[https://www.storj.io/](https://www.storj.io/)  
[https://hub.docker.com/r/storjlabs/storagenode](https://hub.docker.com/r/storjlabs/storagenode)

Notes: 💰 This one earns you money for your storage! Set up your `WALLET` address for payouts.

#### sia

(OPTIONAL, commented out by default)

`image: nebulouslabs/sia`

> Run a storage node (free/not-for-profit) on the Sia distributed storage network. (technically operated by Sia Foundation, a 501(c)(3) US nonprofit, but helps serve Skynet, their for-profit 💰 entity)

[https://sia.tech/](https://sia.tech/)  
[https://hub.docker.com/r/nebulouslabs/sia](https://hub.docker.com/r/nebulouslabs/sia)

#### Transmission

(OPTIONAL, commented out by default)

`image: linuxserver/transmission`

> Seed files to the public via BitTorrent (e.g. linux ISOs, Archive.org collections, etc.). This starts empty by default, you have to add content yourself.

(OPTIONAL)
```yaml
image: linuxserver/transmission
ports:
    - 127.0.0.1:9091:9091
    - 0.0.0.0:51413:51413
    - 0.0.0.0:51413:51413/udp
environment:
    - USER=squash
    - PASS=NfC6r47FA8J2K
volumes:
    - ./data/transmission/files:/data
    - ./data/transmission:/config
```

---


## Contribute

Contributions, corrections, and documentation improvements are welcome! Please open an issue or PR to suggest a fix or a new container addition.
