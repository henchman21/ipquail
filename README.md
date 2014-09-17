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

server {
	listen 199.202.21.19:80; 
	listen [2604:4280:d000:11::19]:80;

	server_name ipquail.com 4.ipquail.com 6.ipquail.com www.ipquail.com;
	root /var/www/ipquail;

	charset utf-8;

	access_log /var/log/nginx/ipquail_com_access.log;
	error_log /var/log/nginx/ipquail_com_error.log;

	ssi on;

	location = / { rewrite ^ $myindex; }

	location /ip/api/v1.0/ {
		try_files $uri $uri/ $uri.html =404;
		add_header 'Access-Control-Allow-Origin' '*';
		add_header 'Access-Control-Allow-Methods' 'GET';
		add_header 'Access-Control-Allow-Headers' 'X-Requested-With,Accept,Content-Type,Origin';
	}

}

```
