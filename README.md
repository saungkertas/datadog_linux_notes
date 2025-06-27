# datadog_linux_notes


### Setting API_KEY and install
```
DD_API_KEY=<dd_api_key> DD_SITE="<region>.datadoghq.com" bash -c "$(curl -L https://install.datadoghq.com/scripts/install_script_agent7.sh)"
```

### Enable Log
```
nano /etc/datadog-agent/datadog.yaml
logs_enabled: true
```

### Active log for any connector available
[activate everything log under  /etc/datadog-agent/conf.d/]

example:  /etc/datadog-agent/conf.d/nginx.d/conf.yaml

### check who own the access for these directories
```
ls -ld /var/log/nginx/
ls -ld /var/log/
ls -ld /var/
```

### give access to dd-agent
```
sudo usermod -a -G <owner group> dd-agent
sudo usermod -a -G <owner group> dd-agent
```

### Grant read access to others (less secure)
```
sudo chmod o+r /var/log/nginx/access.log
sudo chmod o+x /var/log/nginx/
sudo chmod o+x /var/log/
```

### Enable Access Control Lists 
```
sudo apt install acl 
sudo setfacl -m u:dd-agent:r /var/log/nginx/access.log
sudo setfacl -m u:dd-agent:rx /var/log/nginx/ 
sudo setfacl -m u:dd-agent:rx /var/log/ 
```

### Verify
```
getfacl /var/log/nginx/access.log
```

### Make sure all log is covered
```
datadog-agent configcheck
```

### Change config with log level debug or trace
```
sudo nano /etc/datadog-agent/datadog.yaml
log_level: DEBUG
logs_enabled: true
```

### restart datadog if using vm
```
sudo systemctl restart datadog-agent
```

### restart datadog if using docker/container:
```
service datadog-agent restart
```

### using these metrics by default dashboard
```
system.cpu.usage
system.mem.used
system.disk.in_use
system.net.bytes_rcvd
system.load.1
```