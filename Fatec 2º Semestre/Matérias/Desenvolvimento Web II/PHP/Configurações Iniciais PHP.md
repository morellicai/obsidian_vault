# Configurações principais do sistema com PHP

- Para as configurações básicas do PHP, é usado um arquivo chamado `php.ini`, que conterá todos as configurações importantes para a engrenagem de interpretação do PHP
	- Esse arquivo no arch linux está no diretório:
	- `/etc/php/php.ini`
	- Junto dele temos outros arquivos que compõem o trabalho da compilação para navegadores web através de um servidor. Temos o `php-fmp.conf` e o `php-fpm.d`
		- É necessário procurar mais para entender como eles funcionam
- Para o servidor web neste computador, estou usando o servidor de proxy reverso nginx. As configurações são essas:

```nginx
server{
	listen 8000;
	server_name localhost;
	root /home/morelli/Documentos/Estudos/php/;

	index barra.php index.html index.htm;
	
	location /{
		try_files $uri $uri/ =404;
	}
	location ~ \.php$ {
    include fastcgi_params;
    fastcgi_pass unix:/run/php-fpm/php-fpm.sock;
    fastcgi_index barra.php; # Use barra.php como index padrão para PHP
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    fastcgi_split_path_info ^(.+\.php)(/.+)$;
}

	location /phpmyadmin/ {
		alias /usr/share/webapps/phpMyAdmin/;
		index index.php index.html index.htm;
		location ~ ^/phpmyadmin/(.+\.php)$ {
			include fastcgi_params;
			fastcgi_pass unix:/run/php-fpm/php-fpm.sock;
			fastcgi_param SCRIPT_FILENAME $request_filename;
		}
	}
}
```

- Não irei entrar a fundo a respeito das configurações, pois ainda é necessário entender muita coisa a respeito do nginx. Existirá um estudo anotado somente sobre ele futuramente.