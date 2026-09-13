# Laboratorio 02
Hoy utilizaremos docker compose para poder desplegar su trabajo. Servicio web y una
base de datos
## Stack
API
- Minimal API
- Debe retornar un mensaje incluyendo mi nombre
- Docker
- docker run -d --rm -p 3000:3000 nmatsui/hello-world-api. 8c446d43dfc9
focused_wilson
docker run -d --rm -p 3001:3000 nmatsui/hello-world-api sweet_sammet
BD
- PostgreSQL
- $ docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d
postgres
# Indicaciones
## Comandos
```bash
docker compose up -d
```
## Configuración por entorno
```
MESSAGE=<Colocar nombre>
```
# Creditos
- Banda Orbegoso André Alejandro
# ETC