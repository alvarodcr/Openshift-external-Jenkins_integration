# Openshift-external-Jenkins_integration

## TODO

1. Ficheros microservicios para crear un entorno de pruebas
2. Integración CI/CD con Jenkins sobre un Docker local.
3. Integración de algún tipo de monitorización.


# Pre-requisitos para entornos Windows 10/11

1. Instalación y configuración de minikube: [Minishift QuickStart OKD 3.11](https://docs.okd.io/3.11/minishift/getting-started/quickstart.html)
2. Instalación de docker desktop: [Docker Desktop](https://docs.docker.com/desktop/install/windows-install/)

## Minishift

Minishift es un cluster basado en OKD de un solo nodo, con esta herramienta simularemos un cluster de OCP, es necesario configurar un entorno virtual con Hyper-V o con VirtualBox.
En mi caso lo he realizado con Hyper-V, para activar la feature en Windows ejecutar:

[Enable-hyper-v](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)

`$ Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All`

Encontrarás mas información de como configurar Minishift en este enlace [hyper-v driver](https://docs.okd.io/3.11/minishift/getting-started/setting-up-virtualization-environment.html#setting-up-hyper-v-driver).

Adaptar los nucleos y la memoria asignada, según disponibilidad del equipo.

## Docker Desktop

Se utilizará Docker para levantar Jenkins y otros servicios con los que queramos simular una infraestructura de servicios independientes pero que esten integrados con 
el cluster de OCP:

[Instalación de Docker en entornos Windows](https://docs.docker.com/desktop/install/windows-install/)

De forma alternativa se puede valorar usar [Podman](https://podman.io/whatis.html).
