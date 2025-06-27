### Example: Delete Nginx access logs older than 30 days
```
find /var/log/nginx -type f -name "access.log-*.gz" -mtime +30 -exec rm {} \;
```
Explanation:\
find /var/log/nginx: Specifies the directory to search.\
-type f: Limits the search to regular files.\
-name "access.log-*.gz": Matches log files with a specific naming pattern (e.g., rotated and compressed Nginx access logs).\
-mtime +30: Finds files that were last modified more than 30 days ago.\
-exec rm {} \;: Executes the rm command on each found file. {} is a placeholder for the filename, and \; terminates the exec command.

###  Truncating Log Files (Clearing Contents)
```
# Empty the syslog file
sudo truncate -s 0 /var/log/syslog
```
explanation:\
truncate: The command specifically designed for changing the size of a file.\
-s 0: Sets the size of the file to 0 bytes, effectively emptying it.

```
# Or using redirection (another common method)
sudo > /var/log/syslog
```
explanation:
```
>: This is a shell redirection operator. When used alone like this, it redirects the standard output of a command to a file.
```