
# Setup Docker Para Projetos Laravel (Renato Magalhães)

### Passo a passo
Clone Repositório
```sh
git clone https://github.com/renatomagalhaes/setup-docker-laravel.git
```


Clone os Arquivos do Laravel
```sh
git clone https://github.com/laravel/laravel.git example-project
```


Copie os arquivos docker-compose.yml, Dockerfile e o diretório docker/ para o seu projeto
```sh
cp -r setup-docker-laravel/* example-project/
```


Crie o Arquivo .env
```sh
cd example-project/
cp .env.example .env
```


Atualizar as variáveis de ambiente do arquivo .env
```dosini
APP_NAME=Projeto
APP_URL=http://localhost:8080

DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=database
DB_USERNAME=root
DB_PASSWORD=root

CACHE_DRIVER=redis
QUEUE_CONNECTION=redis
SESSION_DRIVER=redis

REDIS_HOST=redis
REDIS_PASSWORD=null
REDIS_PORT=6379
```


Suba os containers do projeto
```sh
docker-compose up -d
```


Acessar o container
```sh
docker-compose exec project_x bash
```


Instalar as dependências do projeto
```sh
composer install
```


Gerar a key do projeto Laravel
```sh
php artisan key:generate
```


Acessar o projeto
[http://localhost:8080](http://localhost:8080)


Em produção é recomendado não expor a porta mysql, remova do arquivo docker-compose.yml
```dosini
ports: 
  - 3388:3306
```


Se alterar o nome project_x no arquivo docker-compose.yml, não esqueça de alterar o nome no arquivo docker/nginx/laravel.conf
```dosini
fastcgi_pass project_x:9000;
```