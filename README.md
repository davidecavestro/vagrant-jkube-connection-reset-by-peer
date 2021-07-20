# vagrant-jkube-connection-reset-by-peer
Reproduces https://github.com/eclipse/jkube/issues/777


## How to run

Provision the VM with docker 1.12
```
vagrant up --provision
```
and wait until it is ready (switching to libvirt would be faster).

Then attach via ssh
```
vagrant ssh
```

Build the image
```
cd /vagrant
mvn -DskipTests clean package k8s:build
```
and obtain the "Connection reset by peer" error message.

You can check the underlying error through
```
sudo su -
journalctl -xe --no-pager
```
where you should find somethinbg like
>Error processing tar file(archive/tar: missed writing 17 bytes):
