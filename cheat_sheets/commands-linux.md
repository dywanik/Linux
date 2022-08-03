# Cheat sheet for some usefull Linux commands
## apt-get
#### list installed packages (use ```| grep something``` if you look for a particular package)
```
apt list --installed
```
#### show available versions of a package
```
apt list -a <package>
```
## system
#### status of a service with full description (use with left/right buttons to scroll horizontally)
```
sudo systemctl status <service> -l
```
#### apply configuration that was just written to unit file (/etc/sysctl.conf)
```
sudo sysctl -p
```
#### reload daemons, i.e., after changing configuration
```
sudo systemctl daemon-reload
```
#### make directory with whole patch
```
mkdir -p /full/path/i/want/to/be/created
```
