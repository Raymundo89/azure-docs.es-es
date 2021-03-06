---
title: Preguntas más frecuentes y problemas conocidos de Managed Service Identity (MSI) para Azure Active Directory
description: Problemas conocidos con Managed Service Identity para Azure Active Directory.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.assetid: 2097381a-a7ec-4e3b-b4ff-5d2fb17403b6
ms.service: active-directory
ms.devlang: ''
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: identity
ms.date: 12/12/2017
ms.author: daveba
ms.openlocfilehash: a50854b2e12db9a202d769f9e5feebee8e5f9395
ms.sourcegitcommit: 1362e3d6961bdeaebed7fb342c7b0b34f6f6417a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="faqs-and-known-issues-with-managed-service-identity-msi-for-azure-active-directory"></a>Preguntas más frecuentes y problemas conocidos de Managed Service Identity (MSI) para Azure Active Directory

[!INCLUDE[preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

## <a name="frequently-asked-questions-faqs"></a>Preguntas más frecuentes (P+F)

### <a name="is-there-a-private-preview-program-available-for-upcoming-msi-features-and-integrations"></a>¿Hay un programa de versión preliminar privada disponible para próximas características e integraciones de MSI?

Sí. Si desea que se le tenga en cuenta para la inscripción en el programa de versión preliminar privada, [visite nuestra página de registro](https://aka.ms/azuremsiprivatepreview).

### <a name="does-msi-work-with-azure-cloud-services"></a>¿Funciona MSI con Azure Cloud Services?

No hay planes para admitir MSI en Azure Cloud Services.

### <a name="does-msi-work-with-the-active-directory-authentication-library-adal-or-the-microsoft-authentication-library-msal"></a>¿Funciona MSI con la Biblioteca de autenticación de Active Directory (ADAL) o la Biblioteca de autenticación de Microsoft (MSAL)?

No, MSI no está integrado aún con ADAL ni con MSAL. Para obtener más información acerca de cómo obtener un token de MSI mediante el punto de conexión de REST de MSI, consulte [Uso de una identidad de servicio administrada de máquina virtual de Azure para obtener tokens](how-to-use-vm-token.md).

### <a name="what-is-the-security-boundary-of-a-managed-service-identity"></a>¿Cuál es el límite de seguridad de una identidad de servicio administrada?

El límite de seguridad de la identidad es el recurso al que está asociada. Por ejemplo, el límite de seguridad de una MSI de máquina virtual es la máquina virtual. Cualquier código que se ejecuta en esa máquina virtual puede llamar al punto de conexión de MSI y solicitar tokens. Esta experiencia es similar con otros recursos que admiten MSI.

### <a name="should-i-use-the-msi-vm-imds-endpoint-or-the-msi-vm-extension-endpoint"></a>¿Debo usar el punto de conexión IMDS de la máquina virtual con MSI o el punto de conexión de la extensión de máquina virtual con MSI?

Cuando se usa MSI con máquinas virtuales, es recomendable que use el punto de conexión MSI IMDS. Azure Instance Metadata Service es un punto de conexión REST al que pueden acceder todas las máquinas virtuales IaaS creadas a través de Azure Resource Manager. Algunas de las ventajas de usar MSI en vez de IMDS son:

1. Todos los sistemas operativos de Azure que admiten IaaS pueden usar MSI en lugar de IMDS. 
2. Ya no es necesario instalar una extensión en la máquina virtual para habilitar MSI. 
3. Los certificados que usa MSI ya no están presentes en la máquina virtual. 
4. El punto de conexión de IMDS es una dirección IP no enrutable conocida, que solo está disponible desde dentro de la máquina virtual. 

La extensión de la máquina virtual de MSI todavía se puede usar actualmente. Sin embargo, de aquí en adelante, solo podrá usar el punto de conexión de IMDS como predeterminado. La extensión de la máquina virtual de MSI pronto iniciará un plan para abandonar su uso. 

Para más información sobre Azure Instance Metada Service, consulte la [documentación de IMDS](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/instance-metadata-service)

### <a name="what-are-the-supported-linux-distributions"></a>¿Qué distribuciones de Linux son compatibles?

Todas las distribuciones de Linux compatibles con IaaS de Azure se pueden utilizar con MSI a través del punto de conexión de IMDS. 

Nota: La extensión de máquina virtual de MSI solamente admite las siguientes distribuciones de Linux:
- CoreOS Stable
- CentOS 7.1
- RedHat 7.2
- Ubuntu 15.04
- Ubuntu 16.04

Actualmente, otras distribuciones de Linux no son compatibles, por lo que existe la posibilidad de que la extensión produzca errores en ellas.

La extensión funciona en CentOS 6.9. Sin embargo, dada a la falta de compatibilidad el sistema en la 6.9, si la extensión se bloquea o se detiene, no se reiniciará automáticamente. Se reinicia cuando se reinicia la máquina virtual. Para reiniciar la extensión manualmente, consulte [¿Cómo se reinicia la extensión MSI?](#how-do-you-restart-the-msi-extension)

### <a name="how-do-you-restart-the-msi-extension"></a>¿Cómo se reinicia la extensión MSI?
Tanto en Windows como en algunas versiones de Linux, si la extensión se detiene, se puede utilizar el siguiente cmdlet para reiniciarla manualmente:

```powershell
Set-AzureRmVMExtension -Name <extension name>  -Type <extension Type>  -Location <location> -Publisher Microsoft.ManagedIdentity -VMName <vm name> -ResourceGroupName <resource group name> -ForceRerun <Any string different from any last value used>
```

Donde: 
- El nombre y tipo de la extensión para Windows es: ManagedIdentityExtensionForWindows
- El nombre y tipo de la extensión para Linux es: ManagedIdentityExtensionForLinux

## <a name="known-issues"></a>Problemas conocidos

### <a name="automation-script-fails-when-attempting-schema-export-for-msi-extension"></a>Se produce un error en el "Script de automatización" al intentar la exportación del esquema de la extensión MSI

Cuando se habilita Managed Service Identity en una máquina virtual, se muestra el siguiente error al intentar usar la característica de "Script de automatización" para la máquina virtual o su grupo de recursos:

![Error de exportación de script de automatización de MSI](../media/msi-known-issues/automation-script-export-error.png)

La extensión Managed Service Identity de la máquina virtual no admite actualmente la posibilidad de exportar su esquema a una plantilla de grupo de recursos. Como resultado, la plantilla generada no muestra los parámetros de configuración para habilitar Managed Service Identity en el recurso. Estas secciones pueden agregarse manualmente siguiendo los ejemplos de [Configuración de Managed Service Identity de una máquina virtual mediante una plantilla](qs-configure-template-windows-vm.md).

Cuando la funcionalidad de exportación de esquema está disponible para la extensión MSI de la máquina virtual, se enumerará en [Exportación de grupos de recursos que contienen extensiones de máquina virtual](../../virtual-machines/windows/extensions-export-templates.md#supported-virtual-machine-extensions).

### <a name="configuration-blade-does-not-appear-in-the-azure-portal"></a>La hoja de configuración no aparece en Azure Portal

Si la hoja de configuración de la máquina virtual no aparece en su máquina virtual, MSI todavía no se ha habilitado en el portal de su región.  Vuelva a comprobarlo más tarde.  También puede habilitar MSI para la máquina virtual con [PowerShell](qs-configure-powershell-windows-vm.md) o la [CLI de Azure](qs-configure-cli-windows-vm.md).

### <a name="cannot-assign-access-to-virtual-machines-in-the-access-control-iam-blade"></a>No se puede asignar el acceso a las máquinas virtuales en la hoja Control de acceso (IAM)

Si **Virtual Machine** no aparece en Azure Portal como una opción para **Asignar acceso a** en **Control de acceso (IAM)** > **Agregar permisos**, Managed Service Identity todavía no se ha habilitado en el portal en su región. Vuelva a comprobarlo más tarde.  Aún puede seleccionar la identidad de servicio administrada para la asignación de roles; para ello, busque la entidad de servicio de MSI.  Escriba el nombre de la máquina virtual en el campo **Seleccionar** y la entidad de servicio aparece en el resultado de la búsqueda.

### <a name="vm-fails-to-start-after-being-moved-from-resource-group-or-subscription"></a>La máquina virtual no puede iniciarse después de moverse del grupo de recursos o de la suscripción

Si mueve una máquina virtual en estado de ejecución, continúa ejecutándose durante el desplazamiento. Sin embargo, después, si la máquina virtual se detiene y se reinicia, no se podrá iniciar. Este problema se produce porque la máquina virtual no está actualizando la referencia a la identidad MSI y continúa apuntando a ella en el grupo de recursos anterior.

**Solución alternativa** 
 
Desencadene una actualización en la máquina virtual para que pueda obtener los valores correctos para la identidad MSI. Puede hacer un cambio de propiedad de máquina virtual para actualizar la referencia a la identidad MSI. Por ejemplo, puede establecer un nuevo valor de etiqueta en la máquina virtual con el siguiente comando:

```azurecli-interactive
 az  vm update -n <VM Name> -g <Resource Group> --set tags.fixVM=1
```
 
Este comando establece una nueva etiqueta "fixVM" con un valor de 1 en la máquina virtual. 
 
Al establecer esta propiedad, la máquina virtual se actualiza con el URI del recurso correcto de MSI y, a continuación, debería poder iniciar la máquina virtual. 
 
Una vez que se inicia la máquina virtual, la etiqueta puede quitarse con el comando siguiente:

```azurecli-interactive
az vm update -n <VM Name> -g <Resource Group> --remove tags.fixVM
```
