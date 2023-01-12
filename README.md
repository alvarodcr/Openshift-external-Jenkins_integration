# OCP_LAB

## Pre requisites Windows environment

1. Instalación y configuración de minikube: [Minishift QuickStart OKD 3.11](https://docs.okd.io/3.11/minishift/getting-started/quickstart.html)
2. Instalación de docker desktop: [Docker Desktop](https://docs.docker.com/desktop/install/windows-install/)

## Minikube

Minishift es un cluster basado en OKD de un solo nodo, con esta herramienta simularemos un cluster de OCP, es necesario configurar un entorno virtual con Hyper-V o con VirtualBox.
En mi caso lo he realizado con Hyper-V, para activar la feature en Windows ejecutar:

[enable-hyper-v](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)

`Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All`

Encontrarás como configurar minishift en ente enlace [hyper-v driver](https://docs.okd.io/3.11/minishift/getting-started/setting-up-virtualization-environment.html#setting-up-hyper-v-driver)

Adaptar los nucleos y la memoria asignada, según disponibilidad del equipo.

## Docker Desktop

Se utilizará Docker para levantar Jenkins y otros servicios con los que queramos simular una infraestructura de servicios independientes pero que esten integrados con 
el cluster de OCP.
