# Proyecto de Integración Continua (CI) - Poli

![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python&logoColor=white)
![Django](https://img.shields.io/badge/Django-4.2+-092E20?logo=django&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-4169E1?logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?logo=docker&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-CI-D24939?logo=jenkins&logoColor=white)
![Travis CI](https://img.shields.io/badge/Travis_CI-Cloud-3EAAAF?logo=travis-ci&logoColor=white)
![Codeship](https://img.shields.io/badge/Codeship-Pro-004B66?logo=codeship&logoColor=white)

Este repositorio contiene la infraestructura dockerizada para el ecosistema de Integración Continua (CI) Multi-Plataforma. El diseño implementa una arquitectura multi-contenedor aislada, lo que garantiza la paridad entre entornos de desarrollo y producción, eliminando los clásicos conflictos de dependencias locales (*"en mi máquina sí funciona"*), y establece pipelines declarativos compatibles simultáneamente con herramientas Self-Hosted y SaaS en la nube.

---

## Arquitectura del Proyecto

El sistema se compone de **tres servicios independientes** que coexisten dentro de una red interna virtual aislada creada automáticamente por Docker Compose. Esto permite que se comuniquen entre sí utilizando resolución de nombres nativa sin necesidad de IPs estáticas.

1. **`backend-app` (Servicio Backend):** Desarrollado en **Django (Python 3.12)**. Escucha internamente en el puerto `8000` y está expuesto hacia la máquina host a través del puerto **`8080`** para evitar colisiones con procesos locales persistentes o memoria caché del puerto estándar.
2. **`base-de-datos` (Servicio Base de Datos):** Motor relacional **PostgreSQL 15**. Escucha y expone el puerto estándar `5432` y maneja la persistencia de datos solicitada en los requerimientos del proyecto.
3. **`jenkins` (Orquestador CI Local):** Servidor de automatización autohospedado `jenkins:lts`. Mapeado estratégicamente al puerto **`8081`** del host para evitar colisiones con otros servidores locales, y equipado con un volumen persistente (`jenkins_data`) para proteger su configuración de pipelines.

---

##  Ecosistema de Integración Continua (CI/CD)

El proyecto está diseñado para ser agnóstico a la plataforma de ejecución. En la raíz del repositorio se encuentran los archivos de configuración para tres auditores distintos:

* **Jenkins (`Jenkinsfile`):** Pipeline declarativo estructurado en 4 etapas (*Preparation, Build, Test, Deploy*) diseñado para ejecutarse en el orquestador local.
* **Travis CI (`.travis.yml`):** Configuración en la nube que provisiona un entorno Python 3.9 con servicios de Docker para compilar y validar la infraestructura remotamente ante cada evento en GitHub.
* **Codeship Pro (`codeship-services.yml` y `codeship-steps.yml`):** Topología dividida que respeta el estándar estricto de contenedores de Codeship, replicando la red local en sus servidores para ejecutar comandos de validación en entornos aislados.

---

##  Requisitos Previos

Antes de proceder con el despliegue, asegúrese de tener instalado y activo en el sistema operativo:
* **Docker Desktop** (o Rancher Desktop) con el Docker Engine corriendo.
* **Git** (para la gestión del flujo del repositorio).

---

## Guía de Despliegue Paso a Paso

Siga estos comandos secuenciales en la terminal para clonar, construir y ejecutar la infraestructura completa sin inconvenientes:

### 1. Clonar el repositorio de forma local
```bash
git clone [https://github.com/HANNS-01/Proyecto-CI-Poli.git](https://github.com/HANNS-01/Proyecto-CI-Poli.git)
cd Proyecto-CI-Poli
