# Openshift-external-Jenkins_integration
<br />

# Pre-requisitos para entornos Windows 10/11

1. Instalación y configuración de [Minishift QuickStart OKD 3.11](https://docs.okd.io/3.11/minishift/getting-started/quickstart.html).
2. Instalación de [Podman Desktop](https://github.com/containers/podman/blob/main/docs/tutorials/podman-for-windows.md).

<br />

## 1. Minishift

Minishift es un cluster basado en OKD con un solo nodo, con esta herramienta simularemos un cluster de OCP, es necesario configurar un entorno virtual con Hyper-V o con VirtualBox.
En mi caso lo he realizado con Hyper-V, para activar la feature en Windows ejecutar ([enable-hyper-v](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)):


`$ Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All`

Encontrarás mas información de como configurar Minishift en este enlace [hyper-v driver](https://docs.okd.io/3.11/minishift/getting-started/setting-up-virtualization-environment.html#setting-up-hyper-v-driver).

Adaptar los nucleos y la memoria asignada, según disponibilidad del equipo.

<br />

## 2. Podman Desktop

Se utilizará [Podman](https://podman.io/whatis.html) para levantar Jenkins de forma externa (tambien es posble [instalarlo](https://cloud.redhat.com/blog/deploy-jenkins-pipelines-in-openshift-4-with-openshift-container-storage-4) dentro del cluster):

[Instalación de Podman en entornos Windows](https://github.com/containers/podman/blob/main/docs/tutorials/podman-for-windows.md)

<br />
<br />

# Levantar y configurar el entorno


## 3. Ejecutar Minishift

Una vez descargado y configurado ejecutar:

`$ minishift start`

![1-hyper-v.png](https://github.com/VictorGil-Ops/Openshift-external-Jenkins_integration/blob/main/images/1-hyper-v.png)

<br />

## 4. Crear contenedor de Jenkins

4.1 Construcción del contenedor:

`$ podman build .`

`$ podman volume create jenkins-data`

`$ podman container run --name jenkins --rm --detach \
--privileged --publish 8080:8080 \
--publish 50000:50000 --volume jenkins-data:/var/jenkins_home \
--volume jenkins-docker-certs:/certs/client:ro docker.io/jenkins/jenkins`

4.2 Obtención del token:

`$ podman ps`

`$ podman exec -it <CONTAINER ID> cat /var/jenkins_home/secrets/initialAdminPassword`

4.3 Ir a http://localhost:8080 y desbloquear Jenkins con el token obtenido:

![2-jenkins-unlock.png](https://github.com/VictorGil-Ops/Openshift-external-Jenkins_integration/blob/main/images/2-jenkins-unlock.png)

4.4 Instalar los plugins recomendados:

![3-customize-jenkins.png](https://github.com/VictorGil-Ops/Openshift-external-Jenkins_integration/blob/main/images/3-customize-jenkins.png)

4.5 Crear usuario:

![4-crear-usuario-jenkins.png](https://github.com/VictorGil-Ops/Openshift-external-Jenkins_integration/blob/main/images/4-crear-usuario-jenkins.png)

<br />

# Instalar jenkins-client-plugin

Instalar plugin desde Panel de Control > Administrar Jenkins > Plugins:

![5-ocp-client-plugin.png](https://github.com/VictorGil-Ops/Openshift-external-Jenkins_integration/blob/main/images/5-ocp-client-plugin.png)

Ir a Panel de Control > Administrar Jenkins > System > OpenShift Client Plugin y configurar el cluster Minishift:

![6-ocp-client-config.png](https://github.com/VictorGil-Ops/Openshift-external-Jenkins_integration/blob/main/images/6-ocp-client-config.png)

![7-ocp-client-config.png](https://github.com/VictorGil-Ops/Openshift-external-Jenkins_integration/blob/main/images/7-ocp-client-config.png)

Configurar el token

![8-ocp-client-config.png](https://github.com/VictorGil-Ops/Openshift-external-Jenkins_integration/blob/main/images/8-ocp-client-config.png)

![9-ocp-client-config.png](https://github.com/VictorGil-Ops/Openshift-external-Jenkins_integration/blob/main/images/9-ocp-client-config.png)

