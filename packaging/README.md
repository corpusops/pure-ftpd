# CorpusOps ppa upgrade workflow
## INSTALL
```sh
sudo apt-get install devscripts debhelper dh-systemd dput python-paramiko python-scp/xenial python3-paramiko python3-scp
git clone https://github.com/corpusops/pure-ftpd.git pure-ftpdp/pure-ftpd
cd pure-ftpdp/pure-ftpd
git remote add upstream https://github.com/jedisct1/pure-ftpd
git fetch --all
git fetch --all --tags
```

## Refresh stable
```sh
git checkout master
git pull origin
git fetch grke
git rebase -i upstream/<tag>
packaging/sync_debian.sh
```

## Test build in docker
```sh
docker build -t pure-ftpdp  -f packaging/Dockerfile .
docker run --name=pure-ftpdp1 --rm -v /src_real -ti pure-ftpdp bash
```
