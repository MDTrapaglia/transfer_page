# FileBrowser en Docker

- Puerto externo: 3050 → interno: 80.
- Datos host: `/home/mtrapaglia/Data/shared-folder` → contenedor: `/srv`.
- Usuario contenedor: `1000:1000` (mtrapaglia).
- Configuración persistente: `./data` (db) y `./config` (ajustes).

## Uso

Entra en la carpeta del compose:
```sh
cd /home/mtrapaglia/projects/upload_portal
```

Iniciar solo cuando lo necesites (daemon):
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
- Navega a `https://matiastrapaglia.space/transfer/` (proxy Nginx al contenedor en 3050; base url `/transfer`).
- Usuario activo: `mtrapaglia`
