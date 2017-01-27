Links:
- [Apache HTTP Server Version 2.4 Documentation](http://httpd.apache.org/docs/2.4/)
- [Oracle Docs: Apache Web Server](https://docs.oracle.com/cd/E53394_01/html/E54831/gnvhs.html)

# Apache on Oracle Solaris
- By default apache22 is installed but disabled. One can check using either of the following:
```
svcs *apache*       # Or:
svcs http
```
- Can install newer version then enable the server.
```
pkg install web/server/apache-24
svcadm -v enable /network/http:apache24
```
- Alternately can install a Apache webserver with MySQL and PHP:
```
pkg install group/feature/amp
```
- Verify that webserver works by opening: `http://localhost:80` in browser.

# Configuration of Apache
- Configuration is stored in the `/etc/apache2/2.2/httpd.conf` file.
- By default, web pages are served from `/var/apache2/2.2/htdocs` folders.

## Edit `/etc/apache2/2.2/httpd.conf`
- Can edit `DocumentRoot` to point to another directory.
- Make sure to change the <Directory ""> to point to the same DocumentRoot
- Also need to make sure that the directory it points into to has execute permissions, otherwise others won't be able to read the files within the directory.
