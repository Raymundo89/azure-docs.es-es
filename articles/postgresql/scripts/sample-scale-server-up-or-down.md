---
title: 'Script de la CLI de Azure: escala de Azure Database for PostgreSQL'
description: 'Ejemplo de script de la CLI de Azure: escalado del servidor de Azure Database for PostgreSQL (Base de datos de Azure para PostgreSQL) a un nivel de rendimiento diferente después de consultar las métricas.'
services: postgresql
author: rachel-msft
ms.author: raagyema
manager: kfile
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 04/05/2018
ms.openlocfilehash: ff740bf22b745e3f9e00ccbdb40c5e4d5948fb41
ms.sourcegitcommit: 5b2ac9e6d8539c11ab0891b686b8afa12441a8f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a>Supervisión y escalado de un solo servidor PostgreSQL mediante la CLI de Azure
Este script de la CLI de ejemplo escala un solo servidor de Azure Database for PostgreSQL (Base de datos de Azure para PostgreSQL) a un nivel de rendimiento diferente después de consultar las métricas. 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Si decide ejecutar la CLI localmente, este artículo necesita la CLI de Azure versión 2.0 o posterior. Ejecute `az --version` para comprobar la versión. Consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli) para instalar o actualizar su versión.

## <a name="sample-script"></a>Script de ejemplo
En este script de ejemplo, va a modificar las líneas resaltadas para actualizar el nombre de usuario administrador y la contraseña a los suyos propios. Reemplace el identificador de suscripción usado en los comandos `az monitor` por su propio identificador de suscripción.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=18-19 "Create and scale Azure Database for PostgreSQL.")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación
Use el comando siguiente para quitar el grupo de recursos y todos los recursos asociados a él después de ejecutarse el script de ejemplo. 
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete the resource group.")]

## <a name="script-explanation"></a>Explicación del script
Este script usa los comandos que se describen en la tabla siguiente:

| **Comando** | **Notas** |
|---|---|
| [az group create](/cli/azure/group#az_group_create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az postgres server create](/cli/azure/postgres/server#az_postgres_server_create) | Crea un servidor PostgreSQL que hospeda las bases de datos. |
| [az monitor metrics list](/cli/azure/monitor/metrics#az_monitor_metrics_list) | Especifica el valor de métrica de los recursos. |
| [az group delete](/cli/azure/group#az_group_delete) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |

## <a name="next-steps"></a>Pasos siguientes
- Para más información sobre la CLI de Azure, vea la [documentación de la CLI de Azure](/cli/azure).
- Pruebe otros scripts adicionales: [Ejemplos de la CLI de Azure para Azure Database for PostgreSQL](../sample-scripts-azure-cli.md).
- Para más información sobre el escalado, vea [Niveles de servicio](../concepts-service-tiers.md) y [Unidades de Compute y Storage](../concepts-compute-unit-and-storage.md).
