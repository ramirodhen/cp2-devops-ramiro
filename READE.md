# CP2 DevOps - Despliegue completo en Azure

Proyecto de despliegue de infraestructura y aplicaciones en Azure utilizando herramientas DevOps.

---

## 🧱 Tecnologías utilizadas

- **Terraform** → Infraestructura como código (Azure)
- **Ansible** → Configuración automática de la VM
- **Podman** → Contenedores en la máquina virtual
- **Azure Container Registry (ACR)** → Registro de imágenes
- **Kubernetes (AKS)** → Orquestación de contenedores

---

## 🏗️ Arquitectura del proyecto

El proyecto se divide en varias capas:

### 1. Infraestructura (Terraform)
- Creación de recursos en Azure:
  - Máquina virtual Linux
  - Red virtual y NSG
  - Azure Container Registry
  - Cluster AKS

---

### 2. Configuración de la VM (Ansible)
- Instalación de:
  - Podman
  - OpenSSL
  - Apache utils (htpasswd)
- Generación de:
  - Certificado SSL autofirmado
  - Autenticación básica
- Despliegue de contenedor Nginx

---

### 3. Contenedor en VM
- Aplicación web servida con Nginx
- Acceso mediante:
  - HTTPS
  - Autenticación básica

---

### 4. AKS (Kubernetes)
- Deployment de la aplicación
- Service para exposición externa
- PVC para almacenamiento persistente
- Uso de imagen desde ACR

---

## 🔐 Seguridad

- Acceso HTTPS en la VM
- Autenticación básica en Nginx
- NSG configurado con:
  - Puerto 22 (SSH)
  - Puerto 80 (AKS)
  - Puerto 443 (VM)

---

## 📁 Estructura del repositorio

.
├── terraform/
├── ansible/
├── k8s/
├── images/
└── README.md

---

## 🚀 Resultado

- Aplicación desplegada en:
  - VM (Podman + Nginx + HTTPS + Auth)
  - AKS (Kubernetes + PVC)
- Automatización completa del despliegue
- Uso de buenas prácticas DevOps

---

## 👨‍💻 Autor

**Ramiro Rodríguez Henríquez**
