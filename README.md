# CP2 DevOps - Despliegue completo en Azure

Proyecto de despliegue de infraestructura y aplicaciones en Azure utilizando herramientas DevOps, cubriendo todo el ciclo desde la creación de recursos hasta la ejecución en Kubernetes.

---

## 🧱 Tecnologías utilizadas

- **Terraform** → Infraestructura como código en Azure
- **Ansible** → Automatización de configuración de la VM
- **Podman** → Ejecución de contenedores en la VM
- **Azure Container Registry (ACR)** → Almacenamiento de imágenes
- **Kubernetes (AKS)** → Orquestación de contenedores

---

## 🏗️ Arquitectura del proyecto

El proyecto se estructura en varias capas:

### 1. Infraestructura (Terraform)
Se crean los recursos en Azure:
- Máquina virtual Linux
- Red virtual (VNet) y reglas de seguridad (NSG)
- Azure Container Registry (ACR)
- Cluster Kubernetes (AKS)

Terraform permite reproducir el entorno de forma declarativa y versionada.

---

### 2. Construcción y almacenamiento de imágenes (ACR)
- Creación de imágenes Docker:
  - `vm-app` → usada en la VM
  - `aks-app` → usada en AKS
- Push de imágenes al ACR
- Uso del registro privado en ambos entornos (VM y AKS)

---

### 3. Configuración de la VM (Ansible)
Automatización completa de la máquina virtual:

- Instalación de dependencias:
  - Podman
  - OpenSSL
  - Apache utils (htpasswd)

- Configuración de seguridad:
  - Certificado SSL autofirmado
  - Autenticación básica

- Despliegue:
  - Contenedor Nginx desde ACR
  - Configuración HTTPS
  - Servicio systemd para persistencia

---

### 4. Despliegue en VM
- Aplicación web servida con Nginx
- Acceso mediante:
  - HTTPS
  - Autenticación básica

Se garantiza acceso seguro y persistencia del servicio.

---

### 5. AKS (Kubernetes)
Despliegue de la aplicación en cluster:

- Deployment con la imagen desde ACR
- Service para exposición externa
- Persistent Volume Claim (PVC)
- Uso de init container (busybox) para inicialización

---

## 🔐 Seguridad

- Acceso HTTPS en la VM
- Autenticación básica en Nginx
- NSG configurado con:
  - Puerto 22 (SSH)
  - Puerto 80 (AKS)
  - Puerto 443 (VM)
- Uso de ACR privado para imágenes

---

## 🔄 Flujo de despliegue

1. Terraform crea la infraestructura en Azure
2. Se construyen y suben las imágenes a ACR
3. Ansible configura la VM automáticamente
4. Podman ejecuta el contenedor en la VM
5. Kubernetes despliega la aplicación en AKS

---

## 📁 Estructura del repositorio

.
├── terraform/
├── ansible/
├── k8s/
├── images/
└── README.md

---

## ✅ Verificaciones realizadas

- Contenedor activo en VM (`podman ps`)
- Servicio systemd activo
- Acceso HTTPS funcional
- Autenticación básica operativa
- Pod en AKS en estado `Running`
- Imagen correctamente obtenida desde ACR

---

## 🚀 Resultado

- Aplicación desplegada en:
  - VM (Podman + Nginx + HTTPS + Auth)
  - AKS (Kubernetes + PVC)
- Automatización completa del despliegue
- Uso de buenas prácticas DevOps (IaC, automatización, contenedores, orquestación)

---

## 👨‍💻 Autor

**Ramiro Rodríguez Henríquez**