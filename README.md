<div align="center">

<h1>The Good Karma Kit</h1>

<img src="https://user-images.githubusercontent.com/511499/114660274-03b9dc00-9cc3-11eb-9db2-19ff3817d5f9.png" width="300px"/><br/>
<i><b>A Docker Compose project to run on servers with spare CPU, disk, and bandwidth.</b><br/>Help the world by contributing your unused computing power to good causes.</i>

</div>

## Quickstart

1. Download [`docker-compose.yml`](https://github.com/pirate/good-karma-kit/blob/main/docker-compose.yml) into an empty directory (or clone this repo)
2. Edit the `docker-compose.yml` file to fill in config vars, tune resource limits, or comment out containers you don't want to run
3. Start the containers with `docker-compose up`
4. Finish setting up some projects through their respective web dashboards exposed on localhost (see below)

```bash
curl -O https://raw.githubusercontent.com/ArchiveBox/good-karma-kit/main/docker-compose.yml
# edit docker-compose.yml to fill in config, tune limits, or disable containers

mkdir -p data
docker-compose up
```

<br/>
<div align="center">
<img width="22%" src="https://user-images.githubusercontent.com/511499/115007022-897e8880-9e77-11eb-9f99-4ed39b7110f1.png" align="top"/>
<img width="22%" src="https://user-images.githubusercontent.com/511499/115006794-458b8380-9e77-11eb-8106-abfcca5b82b5.png" align="top"/>
<img width="22%" src="https://user-images.githubusercontent.com/511499/115006828-4f14eb80-9e77-11eb-96ef-527751d0f170.png" align="top"/>
<img width="22%" src="https://user-images.githubusercontent.com/511499/115006790-42909300-9e77-11eb-9d72-15bc186a2158.png" align="top"/>
</div>


Next steps: Check the status of everything using `htop`
```bash
docker-compose ps
htop
```
Or use the web dashboards / leaderboards for each service listed below.

## Overview

Have some space computing power and want to donate it to a good cause? How about 10+ good causes at once?

> ♻️   put an under-utilized system to good use  
> 🚲  use as much or as little CPU/RAM/DISK as you want  
> ✨  100% more soul warming than mining  
> 📈  geek out over your CPU/disk/bandwidth stats on the leaderboards

This is a collection of containers that all contribute to public-good projects:

- networks: Tor, i2p
- computing: boinc, foldingathome
- archiving: archivewarrior, zimfarm, kiwix, archivebox, pywb
- storage: ipfs, storj, transmission

This v1 list was started by the [ArchiveBox](https://archivebox.io) project, but it's open to contributions.

<small>We've added the 501(c)/non-profit status of each cause below, so you can filter out for-profit ones if you don't want to participate in those (e.g. Storj/IPFS/etc.).</small>

---


## Caveats

The nature of most of these containers is that you're contributing resources to the public or to specific causes running on the public internet.
Unless otherwise specified or restricted to 127.0.0.1 in the compose file, all ports should be made available to the public internet.
Make sure you understand the risks involved with exposing your machine to WAN. It may be worth running this in an isolated VM on an isolated subnet if it's on your home or corporate network.

Two optional containers need access to `/var/run/docker.sock`: `watchtower` (uses it to update the other containers), and `zimfarm` (uses it to fork worker containers for its sub-tasks). Make sure to update the containers yourself semi-regularly if you disable the `watchtower`.

Not all the containers are not-for-profit, some either reward you with cryptocurrency, or are affiliated with for-profit entities. Each container is marked below with its non-profit/for-profit status.

If there are too many containers for your liking, the top-3 high-impact and easy-to-run ones are:

- ⭐️  `archivewarrior`
- ⭐️  `boinc`
- ⭐️  `tor`

## Contents

---

<br/>

### Autoupdater

<br/>

#### watchtower

`image: containrrr/watchtower`

> Automatically update & restart docker containers when they have new versions available. (open source helper container)

*(commented out by default, but highly recommended to enable it by uncommenting)*

[https://containrrr.dev/watchtower/](https://containrrr.dev/watchtower/)  
[https://github.com/containrrr/watchtower](https://github.com/containrrr/watchtower)

Notes: needs access `docker.sock` to work, but can be disabled if you regularly udpate the containers yourself by hand

<br/>

---

<br/>

### Distributed networking projects

<br/>

#### tor ⭐️

`image: thetorproject/obfs4-bridge:latest`

> Run a relay node for the Tor onion routing network that helps people use the internet with as much privacy as possible. (501(c)(3) US nonprofit)

[https://www.torproject.org/](https://www.torproject.org/)  
[https://hub.docker.com/r/thetorproject/obfs4-bridge](https://hub.docker.com/r/thetorproject/obfs4-bridge)

Notes: Does not run a guard/exit node, only a [middle relay](https://community.torproject.org/relay/types-of-relays/) node

<br/>

#### i2p

`image: geti2p/i2p`

> Run a relay node for the i2p routing network (similar to Tor). (501(c)(3) US nonprofit)

[https://geti2p.net/en/](https://geti2p.net/en/)

[https://geti2p.net/en/download/docker](https://geti2p.net/en/download/docker)

<br/>

---

<br/>

### Distributed computing projects

<br/>

#### boinc ⭐️

`image: ghcr.io/linuxserver/boinc`

> Help contribute CPU and GPU power to a wide variety of scientific research projects, including protein folding, alien signal detection, and more! (operated not-for-profit by UC Berkeley and funded by the NSF)

[https://boinc.berkeley.edu/](https://boinc.berkeley.edu/)  
[https://hub.docker.com/r/linuxserver/boinc](https://hub.docker.com/r/linuxserver/boinc)
    
Notes: if you have a GPU, it will help computations greatly, please uncomment the /dev/dri line.

<br/>

#### foldingathome

`image: ghcr.io/linuxserver/foldingathome`

> Help contribute CPU power to solve protein folding problems in bioscience, crucial to the development of vacienes and our understanding of molecular biology and mechanics. (operated by a research group at Washington University in Saint Louis, a 501(c)(3) non-profit) 

[https://foldingathome.org/](https://foldingathome.org/)  
[https://hub.docker.com/r/linuxserver/foldingathome](https://hub.docker.com/r/linuxserver/foldingathome)

<br/>

---

<br/>

### Internet Archiving projects

<br/>

#### archivewarrior ⭐️

`image: atdr.meo.ws/archiveteam/warrior-dockerfile:latest`

> Help contribute CPU and bandwidth to archive parts of the internet automatically before they go down. Has helped save large swaths of the internet from going dark forever by adding them to Archive.org. (operated by an open-source collective, not-for-profit)

[https://warrior.archiveteam.org/](https://warrior.archiveteam.org/)  
[https://github.com/ArchiveTeam/warrior-dockerfile](https://github.com/ArchiveTeam/warrior-dockerfile)

<br/>

#### zimfarm

`image: openzim/zimfarm-worker-manager`

> Help contribute CPU and bandwidth to *archive* large content collections for offline use in areas with limited internet. Helps many communities access things like Wikipedia, Project Gutenberg, and more. (operated by the Swiss non-profit Kiwix/OpenZIM)

[https://github.com/openzim/zimfarm](https://github.com/openzim/zimfarm)  
[https://hub.docker.com/r/openzim/zimfarm-worker-manager](https://hub.docker.com/r/openzim/zimfarm-worker-manager)
    
Notes: this one requires a static IP and >1TB of monthly network transfer available! You must [contact Kiwix to get your worker set up](https://github.com/openzim/zimfarm/blob/master/workers/README.md#zimfarm-workers), and get your static IP whitelisted.

<br/>

#### kiwix

`image: kiwix/kiwix-serve:latest`

> Help contribute bandwidth and disk to *serve* large content collections to users in areas with limited or censored internet. This is the server for the content that `zimfarm` archives. (operated by the Swiss non-profit Kiwix/OpenZIM)

[https://www.kiwix.org/en/](https://www.kiwix.org/en/)  
[https://hub.docker.com/r/kiwix/kiwix-serve](https://hub.docker.com/r/kiwix/kiwix-serve)

Notes: this one requires you download some ZIM archives to serve into `./data/kiwix`, get those from here: [https://wiki.kiwix.org/wiki/Content_in_all_languages](https://wiki.kiwix.org/wiki/Content_in_all_languages)

<br/>

#### archivebox

`image: archivebox/archivebox:latest`

> Use ArchiveBox as a tool to archive sites you care about for offline visiting or rehosting after they go down. (open source project, not-for-profit)

[https://archivebox.io](https://archivebox.io)  
[https://hub.docker.com/r/archivebox/archivebox/](https://hub.docker.com/r/archivebox/archivebox/)
    
Notes: this one is empty by default, add some sites to archive or crawl regulary using the web UI or CLI.

<br/>

#### pywb

`image: webrecorder/pywb:latest`

> Use PYWB as a tool to archive sites you care about for offline visiting or rehosting after they go down. (open source project, not-for-profit, affiliated with Rhizome/Webrecorder)

[https://github.com/webrecorder/pywb](https://github.com/webrecorder/pywb)  
[https://hub.docker.com/r/webrecorder/pywb](https://hub.docker.com/r/webrecorder/pywb)
    
Notes: this one is empty by default, add some sites to archive or crawl regulary using the web UI or CLI.

<br/>

#### mwmbl

Docker image is built from the official [git repository](https://github.com/mwmbl/crawler-script/)

> [Mwmbl](https://github.com/mwmbl/mwmbl) is a non-profit, open source search engine where the community determines the rankings. We aim to be a replacement for commercial search engines such as Google and Bing.

[https://github.com/mwmbl/mwmbl](https://github.com/mwmbl/mwmbl)

<br/>

---

<br/>

### Distribued storage projects

(these serve assets to the public, 

<br/>

#### ipfs

`image: ipfs/go-ipfs:latest`

> Run a storage node (free/not-for-profit) on the IPFS distributed storage network and pin files you care about to help serve them to others. (operated by Protocol Labs Inc., a for-profit 💰 US company)

[https://ipfs.io](https://ipfs.io)  
[https://hub.docker.com/r/ipfs/go-ipfs](https://hub.docker.com/r/ipfs/go-ipfs)

<br/>

#### storj

`image: storjlabs/storagenode:latest`

> Run a storage node (for profit) on the Storj distributed storage network, automatically contribute your storage space and bandwidth and earn cryptocurrency in return. (operated by Storj Labs Inc., a for-profit 💰 US company)

[https://www.storj.io/](https://www.storj.io/)  
[https://hub.docker.com/r/storjlabs/storagenode](https://hub.docker.com/r/storjlabs/storagenode)

Notes: 💰 This one (optionally) earns you money for your storage. Set the `WALLET` to your address if you want payouts.

<br/>

#### Transmission

`image: linuxserver/transmission`

> Seed files to the public via BitTorrent (e.g. linux ISOs, Archive.org collections, etc.). This starts empty by default, you have to add content yourself.

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

<br/>

Notes: some networks don't like BitTorrent traffic, make sure your provider allows it.

<br/>

---

<br/>

## Contribute

Contributions, corrections, and documentation improvements are welcome! Please open an issue or PR to suggest a fix or a new container addition.
