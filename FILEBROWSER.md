# FileBrowser en Docker

- Puerto expuesto: `${FILEBROWSER_BIND_IP:-127.0.0.1}:${FILEBROWSER_PORT:-3050}` → contenedor `80` (solo loopback por defecto).
- Datos host: `${FILEBROWSER_ROOT:-/home/mtrapaglia/Data/shared-folder}` → contenedor: `/srv`.
- Usuario contenedor: `1000:1000` (mtrapaglia).
- Configuración persistente: `./data` (db, sin versionar) y `./config` (ajustes).

## Preparación (seguridad)

1) Copia `.env.example` a `.env` y ajusta bind/puerto/carpeta si lo necesitas.
2) Rota credenciales filtradas: elimina o mueve el contenido de `./data` para regenerar la base de datos y crea un administrador nuevo:
```sh
docker compose run --rm filebrowser filebrowser users add <usuario> <password> --perm.admin --database /database/filebrowser.db
```
   - Para cambiar la clave de un usuario existente, usa `users update` en lugar de `users add`.

## Uso

Entra en la carpeta del compose:
```sh
cd /home/mtrapaglia/projects/upload_portal
```

Arrancar (solo cuando lo necesites):
```sh
docker compose up -d
```

Detener y eliminar contenedor para liberar RAM y cerrar acceso:
```sh
docker compose down
```

Ver estado (encendido/apagado):
```sh
docker compose ps
```

Acceso web:
- Navega a `https://matiastrapaglia.space/transfer/` (proxy Nginx al contenedor en el puerto interno 80; base url `/transfer`).
