# [Documentación de Cloud Services](index.md)

# Información general
## [¿Qué es Cloud Services?](cloud-services-choose-me.md)
## [Archivos de configuración y empaquetado de un servicio en la nube](cloud-services-model-and-package.md)

# Introducción
## [Servicio en la nube de .NET de ejemplo](cloud-services-dotnet-get-started.md)
## [Servicio en la nube de Python para Visual Studio de ejemplo](cloud-services-python-ptvs.md)
## [Configuración de un clúster HPC híbrido con Microsoft HPC Pack](cloud-services-setup-hybrid-hpcpack-cluster.md)

# Procedimientos
## Plan
### [Tamaños de máquina virtual](cloud-services-sizes-specs.md)
### [Actualizaciones](cloud-services-update-azure-service.md)

## Desarrollo
### [Creación de roles de trabajo y web de PHP](../cloud-services-php-create-web-role.md)
### [Compilación e implementación de una aplicación de Node.js](cloud-services-nodejs-develop-deploy-app.md)
### [Compilación de una aplicación web Node.js con Express](cloud-services-nodejs-develop-deploy-express-app.md)
### Storage y Visual Studio
#### [Blob Storage y servicios conectados](../visual-studio/vs-storage-cloud-services-getting-started-blobs.md)
#### [Queue Storage y servicios conectados](../visual-studio/vs-storage-cloud-services-getting-started-queues.md)
#### [Table Storage y servicios conectados](../visual-studio/vs-storage-cloud-services-getting-started-tables.md)
### [Configuración de reglas de tráfico para un rol](cloud-services-enable-communication-role-instances.md)
### [Control de eventos de ciclo de vida de servicio en la nube](cloud-services-role-lifecycle-dotnet.md)
### [Socket.io (Node.js)](cloud-services-nodejs-chat-app-socketio.md)
### [Uso de Twilio para realizar una llamada telefónica (.NET)](../partner-twilio-cloud-services-dotnet-phone-call-web-role.md)

### Configuración de las tareas de inicio
#### [Creación de tareas de inicio](cloud-services-startup-tasks.md)
#### [Tareas de inicio comunes](cloud-services-startup-tasks-common.md)
#### [Uso de una tarea para instalar .NET en un rol de servicio en la nube](cloud-services-dotnet-install-dotnet.md)

### Configuración de Escritorio remoto
#### [Portal](cloud-services-role-enable-remote-desktop-new-portal.md)
#### [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
#### [Visual Studio](cloud-services-role-enable-remote-desktop-visual-studio.md)

## Implementación
### [Creación e implementación de un servicio en la nube en el portal](cloud-services-how-to-create-deploy-portal.md)
### [Creación de un contenedor de servicios en la nube vacío en PowerShell](cloud-services-powershell-create-cloud-container.md)
### [Configuración de un nombre de dominio personalizado](cloud-services-custom-domain-name-portal.md)
### [Conexión a un controlador de dominio personalizado](cloud-services-connect-to-custom-domain.md)

## Administración de servicios
### [Tareas comunes de administración](cloud-services-how-to-manage-portal.md)
### [Configuración de un servicio en la nube](cloud-services-how-to-configure-portal.md)
### [Administración de un servicio en la nube con Azure Automation](automation-manage-cloud-services.md)
### [Configuración de escalado automático](cloud-services-how-to-scale-portal.md)
### [Uso de Python para administrar recursos de Azure](cloud-services-python-how-to-use-service-management.md)
### [Mitigación de ejecución especulativa](mitigate-se.md)

### [Revisiones del SO invitado](cloud-services-guestos-msrc-releases.md)
### Retirada de SO invitado
#### [Directiva de retirada](cloud-services-guestos-retirement-policy.md)
#### [Aviso de retirada de la familia 1](cloud-services-guestos-family1-retirement.md)
### [Novedades de la versión del SO invitado](cloud-services-guestos-update-matrix.md)
### [Hoja de referencia rápida de XPath de configuración de rol de Cloud Services](cloud-services-role-config-xpath.md)

## Administración de certificados
### [Cloud Services y certificados de administración](cloud-services-certs-create.md)
### [Configuración de SSL](cloud-services-configure-ssl-certificate-portal.md)

## Supervisión
### [Supervisión de los servicios en la nube](cloud-services-how-to-monitor.md)
### [Uso de contadores de rendimiento](diagnostics-performance-counters.md)
### [Comprobación del rendimiento](../vs-azure-tools-performance-profiling-cloud-services.md)
#### [Realice la prueba con el generador de perfiles de Visual Studio](cloud-services-performance-testing-visual-studio-profiler.md)
### Habilitación de diagnósticos
#### [Azure PowerShell](cloud-services-diagnostics-powershell.md)
#### [.NET](cloud-services-dotnet-diagnostics.md)
#### [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)
### [Almacenamiento y visualización de los datos de diagnóstico en Azure Storage](../monitoring-and-diagnostics/azure-diagnostics-storage.md?toc=%2fazure%2fcloud-services%2ftoc.json )
### [Seguimiento de un servicio en la nube con Diagnósticos](cloud-services-dotnet-diagnostics-trace-flow.md)

## Solución de problemas
### Depurar 
#### [Opciones para un servicio en la nube](../vs-azure-tools-debugging-cloud-services-overview.md)
#### [Servicio en la nube local con Visual Studio](../vs-azure-tools-debug-cloud-services-virtual-machines.md)
#### [Servicio en la nube publicado con Visual Studio](../vs-azure-tools-intellitrace-debug-published-cloud-services.md)
### [Error de asignación de servicio en la nube](cloud-services-allocation-failures.md)
### [Causas comunes del reciclaje de roles del servicio en la nube](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md)
### [El tamaño de la carpeta TEMP predeterminada es demasiado pequeño para el rol](cloud-services-troubleshoot-default-temp-folder-size-too-small-web-worker-role.md)
### [Problemas comunes de implementación](cloud-services-troubleshoot-deployment-problems.md)
### [Error al iniciar el rol](cloud-services-troubleshoot-roles-that-fail-start.md)
### [Guía de recuperación](cloud-services-disaster-recovery-guidance.md)
### P+F de Cloud Services
#### [Preguntas más frecuentes sobre la disponibilidad de aplicaciones y servicios](cloud-services-application-and-service-availability-faq.md)
#### [Preguntas más frecuentes sobre la configuración y administración](cloud-services-configuration-and-management-faq.md)
#### [Preguntas más frecuentes sobre conectividad y redes](cloud-services-connectivity-and-networking-faq.md)
#### [Preguntas más frecuentes sobre la implementación](cloud-services-deployment-faq.md)

# Referencia
## [Ejemplos de código](https://azure.microsoft.com/resources/samples/?service=cloud-services)
## [Esquema XML de .csdef](schema-csdef-file.md)
### [Esquema LoadBalancerProbe](schema-csdef-loadbalancerprobe.md)
### [Esquema WebRole](schema-csdef-webrole.md)
### [Esquema WorkerRole](schema-csdef-workerrole.md)
### [Esquema NetworkTrafficRules](schema-csdef-networktrafficrules.md)
## [Esquema XML de .cscfg](schema-cscfg-file.md)
### [Esquema de rol](schema-cscfg-role.md)
### [Esquema de NetworkConfiguration](schema-cscfg-networkconfiguration.md)
## [REST](/rest/api/compute/cloudservices/)

# Recursos
## [Azure Roadmap](https://azure.microsoft.com/roadmap/?category=compute)
## [Ruta de aprendizaje](https://azure.microsoft.com/documentation/learning-paths/cloud-services/)
## [Foro de MSDN](https://social.msdn.microsoft.com/Forums/en-us/home?forum=windowsazuredevelopment)
## [Precios](https://azure.microsoft.com/pricing/details/cloud-services/)
## [Calculadora de precios](https://azure.microsoft.com/pricing/calculator/)
## [Actualizaciones del servicio](https://azure.microsoft.com/updates/?product=cloud-services&updatetype=&platform=)
## [Vídeos](https://azure.microsoft.com/documentation/videos/index/?services=cloud-services)
