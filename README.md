# Proyecto Final Bootcamp: Análisis de Negocio DVD Rental (Pagila)

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![Metabase](https://img.shields.io/badge/Metabase-509EE3?style=for-the-badge&logo=metabase&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=sql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

## Tabla de Contenidos
- [Descripción del Proyecto](#descripción-del-proyecto)
- [Tech Stack](#tech-stack)
- [Instalación y Setup](#instalación-y-setup)
- [Metodología y Arquitectura](#metodología-y-arquitectura)
- [Resultados y Dashboard](#resultados-y-dashboard)
- [Estructura del Repositorio](#estructura-del-repositorio)
- [Conclusión](#conclusión)

Este repositorio contiene el Trabajo Final del Bootcamp de Data Analytics, enfocado en la simulación de un proceso de Business Intelligence completo: desde la ingesta de una base de datos transaccional hasta la visualización de indicadores clave para la toma de decisiones.

## Descripción del Proyecto
El objetivo principal fue transformar datos crudos de una empresa de alquiler de películas (base de datos Pagila, similar a Blockbuster) en información estratégica.

A través de este proyecto, se simula el rol de un Data Engineer/Analyst para responder preguntas de negocio como:

¿Qué tiendas generan más ingresos?

¿Cuáles son las películas más rentables?

¿Quiénes son los mejores clientes?

¿Existe estacionalidad en las ventas?

## Tech Stack

- **Motor de Base de Datos:** PostgreSQL
- **Gestión de BD:** pgAdmin 4
- **Lenguaje de Consulta:** SQL (DML & DDL)
- **Visualización:** Metabase
- **Documentación:** Markdown & PDF
- **Containerización:** Docker & Docker Compose

## Instalación y Setup

### Prerrequisitos
- Docker y Docker Compose instalados
- Git para clonar el repositorio

### Pasos de instalación

1. **Clonar el repositorio:**
```bash
git clone <url-del-repositorio>
cd pagila-analytics
```

2. **Levantar los servicios con Docker:**
```bash
docker-compose up -d
```

3. **Acceder a pgAdmin:**
   - URL: http://localhost:5050
   - Usuario: admin@admin.com
   - Contraseña: root

4. **Configurar la base de datos:**
   - Los datos de Pagila se cargan automáticamente al levantar los contenedores
   - En pgAdmin, conectar al servidor PostgreSQL:
     - Host: pagila (nombre del contenedor)
     - Puerto: 5432
     - Usuario: postgres
     - Contraseña: 123456

5. **Conectar Metabase:**
   - URL: http://localhost:3000
   - Configurar conexión a PostgreSQL:
     - Host: localhost
     - Puerto: 5432
     - Base de datos: postgres
     - Usuario: postgres
     - Contraseña: 123456

## Metodología y Arquitectura
El proyecto se dividió en 4 etapas clave:

1. Análisis del Modelo Transaccional
Se exploró la base de datos Pagila (modelo en 3ra Forma Normal) para entender las relaciones entre las 15+ tablas originales (rental, payment, inventory, etc.).


2. Diseño del Modelo Analítico (Esquema Estrella)
Para optimizar las consultas de reporte, se desnormalizó la base de datos creando un esquema analytics con la siguiente estructura:

Tabla de Hechos (Fact Table):


fact_rentals: Centraliza cada transacción de alquiler, unificando fechas, montos y claves foráneas.

Dimensiones (Dimensions):


dim_customer: Datos descriptivos de clientes.


dim_film: Títulos, categorías y ratings.


dim_store: Ubicación geográfica (País/Ciudad).


dim_staff: Información de empleados.


dim_date: Dimensión temporal para análisis de series de tiempo.

3. Proceso ETL (SQL)
Se desarrollaron scripts SQL para la extracción, transformación y carga de datos. Se utilizaron técnicas como:

JOINs para unificar tablas dispersas.

Conversión de tipos de datos (CAST).

Limpieza de datos (filtrado de tiendas sin actividad).

4. Visualización y Dashboarding
Se conectó la base de datos analítica a Metabase para crear un dashboard interactivo. Se implementaron:

Filtros Dinámicos: Por rango de fechas, categoría de película y tienda (País).

Consultas SQL Nativas: Uso de variables ({{variable}}) para dar interactividad a los gráficos.

## Resultados y Dashboard
El dashboard final permite monitorear la salud del negocio en tiempo real a través de múltiples vistas interactivas.

### Vista General (KPIs)
Métricas principales que encabezan el reporte:

- **Ingresos Totales:** US$22,961.92
- **Cantidad de Alquileres:** 5,505 transacciones
- **Ticket Promedio:** US$4.17

### Secciones del Análisis

#### 1. Tendencias de Negocio
Análisis temporal que muestra la evolución mensual de ingresos y patrones estacionales:

- Pico de ventas en julio (US$4,000+)
- Estacionalidad clara con mayor actividad en verano
- Análisis por categorías de películas

#### 2. Rankings y Performance
Top performers del negocio:

- **Top 10 Clientes:** Liderado por Diane Collins y Marcia Dean
- **Top Películas:** "Dogma Family" y "Harry Idaho" como más rentables
- **Rendimiento de Empleados:** Warner Hudson como top performer

#### 3. Segmentación Geográfica
Mapa interactivo de ventas por país:

- Distribución entre EE.UU. (23.0k) y China (23.4k+)
- Análisis de performance por tienda y ubicación

## Estructura del Repositorio

```
pagila-analytics/
├── docker-compose.yml          # Configuración de servicios
├── pagila-schema.sql          # Esquema original de Pagila
├── pagila-schema-jsonb.sql    # Esquema optimizado con JSONB
├── pagila-data.sql           # Datos de prueba
├── restore-pagila-data-jsonb.sh # Script de restauración
├── pgadmin/                  # Configuración de pgAdmin
│   ├── pgadmin_pass         # Credenciales
│   └── pgadmin_servers.json # Configuración de servidores
└── README.md                # Este archivo
```

### Archivos principales:
- **`/sql`:** Scripts de creación del esquema analítico y consultas de Metabase
- **`/docs`:** Documentación del proyecto
  - `Informe_Final.pdf`: Análisis detallado de negocio y diccionario de datos
  - `Presentacion.pdf`: Diapositivas de la defensa del proyecto
- **`/img`:** Capturas de pantalla del proceso y dashboards

## Conclusión
Este proyecto demuestra cómo una arquitectura de datos bien diseñada facilita el análisis exploratorio. La implementación del esquema estrella y los filtros dinámicos permite a los gerentes pasar de datos crudos a insights accionables en segundos.

### Logros principales:
- Transformación exitosa de un modelo transaccional a analítico
- Dashboard interactivo con KPIs en tiempo real
- Identificación de patrones estacionales y top performers
- Arquitectura escalable usando Docker y tecnologías open source

---

**Autor:** Lucrecia Concatti - 2025  
**Bootcamp:** Data Analytics  
**Tecnologías:** PostgreSQL | Metabase | Docker | SQL