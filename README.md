# IP Quail #

## Like ipchicken but shorter ##

I wanted to make my own ipchicken type site, so I came up with this.

Uses:

*	Bootstrap: http://getbootstrap.com/
*	Funny bird from: http://pixabay.com/en/animals-baby-face-cartoon-birds-37395/

## Setup with NGINX ##


```
map $http_user_agent $myindex {
  default /index.html;
  ~curl /ip.html;
}

# Redirect everything to the secure site.
server {
	listen 206.220.196.21:80 accept_filter=httpready;
	listen [2604:4280:6865:6e63:686d:616e:3231:22]:80 ipv6only=on accept_filter=httpready;

	server_name ipquail.com www.ipquail.com 4.ipquail.com 6.ipquail.com;
	root /usr/local/www/ipquail;

	access_log /var/log/nginx/ipquail_com_access.log;
	error_log /var/log/nginx/ipquail_com_error.log;

	ssi on;

	location = / { rewrite ^ $myindex; }
}

```
