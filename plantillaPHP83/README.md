## Plantilla para Laravel - php 8.3 🛠️
---
[![Made by MVidales](https://img.shields.io/badge/Made%20by-MVidales-black)](https://manuelvidales.github.io/)
#### 🚀 Que incluye en la Instalacion?:

- ✅ **PHP8.3-fpm-bullseye** con paquetes de **nodejs**, **composer**.
- ✅ **nginx** version alpine como servidor Web.
- ✅ **MySQL** Base de datos principal.

> Los puertos que se Exponen se modificaron a los que son por default el WebServer "8080":80  y MySQL "3307:3306", esto para evitar conflictos si tenemos localmente corriendo los servicios.

#### Informacion:
---
Usado en la instalacion de proyecto en **[Laravel ^12](https://laravel.com/docs/12.x)** usando el Framework UI **[Filamentphp 4](https://filamentphp.com/docs/4.x/getting-started)**.

> **Nota**: los comandos para despligue de Laravel se ejecutan **manualmente**!

> **💡 Tips de Comandos**
```markdown
docker compose exec app composer install
docker compose exec app npm install
docker compose exec app npm run build # or npm run dev
docker compose exec app php artisan key:generate
docker compose exec app php artisan storage:link
docker compose exec app php artisan migrate
docker compose exec app php artisan db:seed #opcional
```
#### Saludos!
---