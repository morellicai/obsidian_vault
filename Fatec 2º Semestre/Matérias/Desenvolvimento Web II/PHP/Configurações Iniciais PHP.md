/

## Iniciando php

É necessário alguns comandos para iniciar o php no linux. 
```bash
sudo systemctl start nginx
sudo systemctl start php-fpm
# Se for utilizar o banco de dados também
sudo systemctl start mariadb
```
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

-  **Listen, server_name, root**: Considero o cabeçalho da configuração. Ele define bastante coisas
	- **Listen**: Serve para configurar a porta de rede que o servidor vai estar ouvindo. Neste caso, utilizei a porta padrão da web para não precisar passar a porta na url
	- **Server_name**: ali é como vou digitar meu servidor para localizar minha aplicação web. Como estou usando uma aplicação caseira, não preciso que ninguém veja, então estou utilizando um `loopback` para servir. localhost é o DNS que dei ao meu ip de loopback
	- **root**: é onde o nginx vai procurar minha aplicação. Tudo que eu inserir dentro do diretório php, ele vai me servir como uma rota na web. Ficando assim a URL `http://localhost/projCalendario/calendario.php'
		- Perceba que é apenas o que vem a frente do diretório `php`. Dentro desse diretório, tenho um outro diretório que se chama projCalendario e um programa em php chamado calendário. 
- **Index**: Indico para o nginx qual deve ser o nome do arquivo principal no diretório. No meu caso, eu nomeei como barra. E está servindo uma aplicação que mostra as informações do php
- **Locations**: Os locations são algumas rotas que precisamos construir para poder acessar o sistema.
	- **.\php**: Aqui é onde está definido as configurações basicas para o acesso a todos os meus programas que estão escrito dentro do diretório `php`.
		- Ainda não sei explicar tudo, mas em algum momento vou deixar aqui as explicações completas kkkk
	- **/phpmyadmin/**: É uma aplicação php para administrar o banco de dados mySQL de forma mais visual. É como uma pagina administradora. Como é um programa a parte, preciso passar ele também aqui nas rotas para acessar ele como `localhost/phpmyadmin/ 
		- Lembrando que essa rota não se encontra no diretório `php`, ele é uma aplicação instalada no meu sistema