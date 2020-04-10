# Adaptive City Platform Zookeeper

On the ACP Platform this repo should be installed as the `zookeeper` user.

Zookeeper is used by the Vertx real-time platform for peer discovery and synchronization.

## Installation

```
sudo adduser zookeeper
```
### Data directory
```
sudo mkdir /var/lib/zookeeper
sudo chown zookeeper:zookeeper /var/lib/zookeeper
```
### Log directory
```
sudo mkdir /var/log/zookeeper
sudo chown zookeeper:zookeeper /var/log/zookeeper
```
### Code directory

Find the latest version number via [https://zookeeper.apache.org/releases.html](https://zookeeper.apache.org/releases.html).
```
sudo mkdir /opt/zookeeper-3.6.0
sudo chown zookeeper:zookeeper /opt/zookeeper-3.6.0

sudo ln -s /opt/zookeeper-3.6.0 /opt/zookeeper

```
As user `zookeeper`:
```
ssh-keygen -t rsa -b 4096 -C "zookeeper@tfc-app6"
git clone https://github.com/AdaptiveCity/acp_zookeeper
wget -0- "https://downloads.apache.org/zookeeper/zookeeper-3.6.0/apache-zookeeper-3.6.0-bin.tar.gz"
tar -xzf "apache-zookeeper-3.6.0-bin.tar.gz" --directory /opt/zookeeper-3.6.0 --strip-components 1
```
Get the `acp_zookeeper/secrets` directory from another server.
```
cp acp_zookeeper/secrets/zoo.conf /opt/zookeeper/conf/
cp acp_zookeeper/conf/zookeeper-env.sh /opt/zookeeper/conf/
```
## Check java

```
java -version
```
If necessary see java install instructions in `acp_prod`.

## Start zookeeper
```
/opt/zookeeper/bin/zkServer.sh --config /opt/zookeeper/conf start
```
This is provided by the `acp_zookeeper/run.sh` script

## Check running zookeeper
```
echo srvr | nc localhost 2181
```
This is provided by the `acp_zookeeper/status.sh` script

## Add to crontab
```
crontab -e

@reboot /home/zookeeper/acp_zookeeper/run.sh
```
