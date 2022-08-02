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
#### apply configuration that was just written to /etc/sysctl.conf
```
sudo sysctl -p
```