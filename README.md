# Lab02 - Docker Compose
André Banda Orbegoso
## Introducción
En esta práctica de laboratorio se configuró un entorno multicontenedor utilizando Docker Compose para desplegar una Minimal API en Node.js, replicada en 3 instancias, con una base de datos PostgreSQL con un almacenamiento persistente y una interfaz web ligera. 

Para no subir contraseñas ni datos personales al repositorio de GitHub, usamos un archivo `.env` que lee las variables, y dejamos `.env.example` de ejemplo.

---

## Instrucciones de ejecución

Primero se debe crear el archivo `.env` copiando el de ejemplo:

```bash
# Copiar variables de entorno de ejemplo
cp .env.example .env
```
| Variable | Descripción | Valor de Ejemplo |
| :--- | :--- | :--- |
| `MESSAGE` | Mensaje que devuelve la API en su respuesta | `Hola André Banda Orbegoso` |
| `POSTGRES_USER` | Usuario administrador de la base de datos | `postgres` |
| `POSTGRES_PASSWORD` | Contraseña para entrar a PostgreSQL | `contraseña_secreta` |
| `POSTGRES_DB` | Nombre de la base de datos | `lab02-bandaorbegoso` |

## Levantamiento de los contenedores
Para construir las imágenes y levantar todos los servicios en segundo plano:
```bash
docker compose up -d --build
```
Para comprobar que todos los servicios estén corriendo:
```bash
docker compose ps
```
Pruebas de la API
```bash
curl.exe -i localhost:3000 //Agrege el .exe porque de lo contrario me daba un error
curl.exe -i localhost:3001
curl.exe -i localhost:3002
```
## Redes y Volúmenes en Docker
### Tipos de Redes (Controladores de Red)  
- Bridge: Esta es la red predetermidad de Docker,p ermite la comunicación entre los contenedores en la misma máquina usando sus nombres de servicio, sin necesidad de exponerlos directamente al exterior.  

- Host: El contenedor utiliza directamente la red de la máquina física, eliminando el aislamiento de puertos.  

- Overlay: Se utiliza para conectar contenedores que se encuentran en diferentes servidores o computadoras.  

- Macvlan / Ipvlan: Asigna una dirección de red real al contenedor, haciéndolo parecer un dispositivo físico más conectado al enrutador.  

- None: Desactiva toda conexión de red en el contenedor, dejándolo completamente aislado.

### Tipos de Volúmenes
- Volúmenes con nombre: Docker gestiona de manera directa los datos en su directorio interno. La información permanece almacenada, incluso si el contenedor se apaga o se elimina.
- Bind Mounts: Establecen una conexión entre una carpeta concreta de tu ordenador y otra carpeta que se encuentra dentro del contenedor.
- tmpfs Mounts:  Conservan la información únicamente en la memoria RAM, cuando se detiene el contenedor, todo lo que tenía se elimina.

### Volúmenes y Persistencia en PostgreSQL
Se configuró un volumen administrado (**Named Volume**) para PostgreSQL en `docker-compose.yaml`.
####Justificación
- Persistencia: Mantiene intactos los datos de la base de datos al ejecutar docker compose down.
- Compatibilidad: Evita conflictos de permisos entre el sistema operativo y el contenedor.
- Rendimiento: Optimiza las operaciones de lectura y escritura recomendadas para bases de datos relacionales.

## Verificación de Persistencia
1. Inspección del volumen administrado:
```bash
docker volume ls
docker volume inspect lab02-banda-orbegoso_lab02_pgdata
```
2. Reinicio completo de la infraestructura:
```bash
docker compose down
docker compose up -d
```
3. Comprobación:
```bash
docker compose ps
```
