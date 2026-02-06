## Plantilla para Laravel - php 8.2 🛠️
---
[![Made by MVidales](https://img.shields.io/badge/Made%20by-MVidales-black)](https://manuelvidales.github.io/)
#### 🚀 Que incluye en la Instalacion?:

- ✅ **PHP8.2-fpm-bullseye** con paquetes de **nodejs**, **composer**.
- ✅ **driver ODBC de Microsoft** agregado al Dockefile en extensiones de PHP.
- ✅ **nginx** version alpine como servidor Web.
- ✅ **MySQL** Base de datos Versión LTS.

> Los puertos que se Exponen se modificaron a los que son por default el WebServer "8009":80  y MySQL "3307:3306", esto para evitar conflictos si tenemos localmente corriendo los servicios.

#### Informacion:
Usado en la instalacion de proyecto en **[Laravel ^12](https://laravel.com/docs/12.x)** basado con el paquete **[Oficial Laravel Livewire Starter Kit](https://laravel.com/starter-kits)**, usando una conexion de Base de Datos Secundaria de SQL Server, con los [Drivers oficiales de Microsoft de PHP8.2](https://learn.microsoft.com/en-us/sql/connect/php/installation-tutorial-linux-mac?view=sql-server-ver17) en la imagen que genera el archivo Dockerfile.

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