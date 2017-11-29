# django-apache-virtualhost
Django and Apache - Virtual Host configuration

Django 1.11
Python 3
Apache 2


```
<VirtualHost *:80>
	DocumentRoot "/var/www/example.com"
	ServerName example.com

	# Basic configuration
	WSGIScriptAlias / /var/www/example.com/venv/wsgi.py

	# Serving files
	Alias /robots.txt /var/www/example.com/static/robots.txt
	Alias /favicon.ico /var/www/example.com/static/favicon.ico
	Alias /media/ /var/www/example.com/media/
	Alias /static/ /var/www/example.com/static/
</VirtualHost>

<IfModule mod_ssl.c>
    <VirtualHost *:443>
		DocumentRoot "/var/www/example.com"
		ServerName example.com

		# Basic configuration
		WSGIScriptAlias / /var/www/example.com/venv/wsgi.py

		# Serving files
		Alias /robots.txt /var/www/example.com/static/robots.txt
		Alias /favicon.ico /var/www/example.com/static/favicon.ico
		Alias /media/ /var/www/example.com/media/
		Alias /static/ /var/www/example.com/static/

	    SSLEngine on
	    SSLCertificateFile /etc/ssl/certs/example.com.pem
	    SSLCertificateKeyFile /etc/ssl/private/example.com.key
    </VirtualHost>
</IfModule>

# Basic configuration
WSGIPythonPath /var/www/example.com
WSGIPythonHome /var/www/example.com/venv
<Directory /var/www/example.com/venv>
    <Files wsgi.py>
        Require all granted
    </Files>
</Directory>

# Using mod_wsgi daemon mode
WSGIDaemonProcess example.com python-home=/var/www/example.com/venv python-path=/var/www/example.com
WSGIProcessGroup example.com

# Serving files
<Directory /var/www/example.com/static>
    Require all granted
</Directory>
<Directory /var/www/example.com/media>
    Require all granted
</Directory>
```
