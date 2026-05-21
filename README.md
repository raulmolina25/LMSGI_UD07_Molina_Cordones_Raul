# LMSGI_UD07_Molina_Cordones_Raul

# Manual de Explotación ERP - WillmanTech S.L. (ISO 26514)

## Arquitectura del Sistema

El ERP se despliega en alta disponibilidad lógica mediante microservicios con Docker Compose.

## Guía de Instalación y Reinstalación

Necesitas crear un archivo con este nombre y insertar el siguiente codigo:
docker-compose.yml  

services:
  odoo:
    image: odoo:latest
    container_name: odoo
    restart: unless-stopped
    depends_on:
      - db
    ports:
      - "8200:8069"
    volumes:
      - odoo-data:/var/lib/odoo
      - ./config:/etc/odoo
      - ./addons:/mnt/extra-addons
    environment:
      - HOST=db
      - USER=odoo
      - PASSWORD=odoo
    command: odoo -d odoo --db_user=odoo --db_password=odoo -i base

  db:
    image: postgres:16.0
    container_name: db
    restart: unless-stopped
    environment:
      - POSTGRES_DB=odoo
      - POSTGRES_PASSWORD=odoo
      - POSTGRES_USER=odoo
      - PGDATA=/var/lib/postgresql/data/pgdata
    volumes:
      - db-data:/var/lib/postgresql/data

volumes:
  odoo-data:
  db-data:



## Seguridad y Control de Acceso

Administrador: Permisos de Lectura, Escritura y Ejecucion(7). Acceso total
Contable: Permisos de Solo Lectura(4)
Comercial: Permisos de Lectura y Escritura(6)


## Flujo Operativo de Facturación e Informes

Arriba a la izquierda le das a Facturación - Nuevo  
Seleccionas el cliente, los productos, el precio, la cantidad y todos los datos que te pidan y sean necesarios  
Cuando lo hayas completado todo presionar Confirmar  
ejemplo:  
<img width="1247" height="667" alt="image" src="https://github.com/user-attachments/assets/212c8a4f-dd19-4de6-9348-c86ceb3b245b" />
