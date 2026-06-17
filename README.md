# Devops-Back

Backend de la aplicación **Tienda de Alimentos para Perritos**, desarrollado con Node.js y Express.

## Descripción

Este servicio expone una API REST para realizar operaciones CRUD sobre los productos almacenados en una base de datos MySQL.

Las operaciones disponibles incluyen:

* Obtener productos
* Crear productos
* Actualizar productos
* Eliminar productos

## Tecnologías utilizadas

* Node.js
* Express.js
* MySQL
* Docker
* Amazon ECR
* Amazon ECS Fargate
* GitHub Actions
* AWS Auto Scaling

## Arquitectura

Frontend → Backend API → MySQL

### Servicios AWS utilizados

* Amazon ECS Fargate para ejecución de contenedores.
* Amazon ECR para almacenamiento de imágenes Docker.
* GitHub Actions para integración y despliegue continuo (CI/CD).
* Auto Scaling para escalamiento automático basado en utilización de CPU.

## Construcción de la imagen Docker

```bash
docker build -t tienda-backend .
```

## Ejecución local

```bash
docker run -d -p 3001:3001 tienda-backend
```

## Variables de entorno

El backend utiliza variables de entorno para conectarse a la base de datos:

```env
DB_HOST=xxxx
DB_USER=xxxx
DB_PASSWORD=xxxx
DB_NAME=tienda_perritos
DB_PORT=3306
PORT=3001
```

## Endpoints principales

### Obtener productos

```http
GET /api/productos
```

### Crear producto

```http
POST /api/productos
```

### Actualizar producto

```http
PUT /api/productos/:id
```

### Eliminar producto

```http
DELETE /api/productos/:id
```

## Pipeline CI/CD

Cada vez que se realiza un push a la rama `main`:

1. GitHub Actions construye una nueva imagen Docker.
2. La imagen se publica en Amazon ECR.
3. Amazon ECS actualiza automáticamente el servicio Backend.
4. Se realiza un nuevo despliegue sin intervención manual.

## Escalamiento automático

El servicio Backend utiliza Auto Scaling configurado con:

* Mínimo: 1 tarea
* Máximo: 3 tareas
* Métrica: CPU Utilization
* Objetivo: 50%

## Autor

Nicolás Silva Figueroa
Dylan Monroy Sanhueza

Ingeniería en Informática
