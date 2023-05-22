# The data folder

Container state will be automatically stored in this folder, with one subfolder per container (as configured by the `volumes:` sections in the `docker-compose.yml` file).

(Depending on your host OS and Docker setup, you may need to manually `chown` this folder to have `777` permissions so that containers using weird UIDs can still create their data folders within.)

You must create this folder manually if you downloaded the `docker-compose.yml` file.

```bash
# cd good-karma-kit
# nano docker-compose.yml

mkdir ./data
chmod 777 ./data
ls -lah ./data
```

<br/>

You can also clone the entire repo in order to not have to make the folder manually.

```bash
# git clone https://github.com/ArchiveBox/good-karma-kit
# cd good-karma-kit

ls -lah ./data
```
