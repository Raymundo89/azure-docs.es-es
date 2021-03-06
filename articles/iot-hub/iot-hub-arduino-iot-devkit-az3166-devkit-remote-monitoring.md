---
title: 'IoT DevKit en la nube: conexión de IoT MXChip DevKit a Azure IoT Hub | Microsoft Docs'
description: En este tutorial aprenda cómo enviar el estado de los sensores de IoT DevKit AZ3166 a Azure IoT Suite para su supervisión y visualización.
services: iot-hub
documentationcenter: ''
author: liydu
manager: timlt
tags: ''
keywords: ''
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2018
ms.author: liydu
ms.openlocfilehash: b288595ca06c3a3cccb72082658f1927f2ae558a
ms.sourcegitcommit: 20d103fb8658b29b48115782fe01f76239b240aa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2018
---
# <a name="connect-mxchip-iot-devkit-to-azure-iot-suite-for-remote-monitoring"></a>Conexión de MXChip IoT DevKit a Azure IoT Suite para la supervisión remota

En este tutorial, aprenderá a ejecutar una aplicación de ejemplo en DevKit para enviar datos de sensor a Azure IoT Suite.

[MXChip IoT DevKit](https://aka.ms/iot-devkit) es una placa integral compatible de Arduino con periféricos y sensores varios. Se puede desarrollar para ella con la [extensión de Visual Studio Code para Arduino](https://aka.ms/arduino). Incluye un [catálogo de proyectos](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) cada vez mayor que sirve de guía para crear prototipos de soluciones de Internet de las cosas (IoT) que aprovechen los servicios de Microsoft Azure.

## <a name="what-you-need"></a>Lo que necesita

Siga la [Guía de introducción](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started) para:

* Conexión de DevKit con Wi-Fi
* Preparación del entorno de desarrollo

Una suscripción de Azure activa. Si no tiene una, puede registrarse a través de uno de estos dos métodos:

* Active una [cuenta de Microsoft Azure de prueba de 30 días gratis](https://azure.microsoft.com/en-us/free/)
* Reclame su [crédito de Azure](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) si es suscriptor de MSDN o Visual Studio

## <a name="create-an-azure-iot-suite"></a>Creación de una instancia de Azure IoT Suite

1. Vaya a [sitio de Azure IoT Suite](https://www.azureiotsuite.com/) y haga clic en **Crear una solución nueva**.
  ![Selección del tipo de instancia Azure IoT Suite](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-solution-types.png)
  > [!WARNING]
  > De forma predeterminada, este ejemplo crea una instancia de S2 IoT Hub después de crear una instancia de IoT Suite. Si no esta instancia de IoT Hub no se utiliza con un gran número de dispositivos, se recomienda cambiar de S2 a S1 y eliminar la instancia de IoT Suite para poder eliminar también la de IoT Hub cuando ya no la necesite. 

2. Seleccione **Supervisión remota**.

3. Escriba un nombre para la solución, seleccione una suscripción y una región y después haga clic en **Crear solución**. La solución puede tardar varios minutos en aprovisionar.
  ![Creación de la solución](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-new-solution.png)

4. Una vez completado el aprovisionamiento, haga clic en **Iniciar**. Algunos dispositivos simulados se crean para la solución durante el proceso de aprovisionamiento. Haga clic en **DISPOSITIVOS** para revisarlos. ![Panel](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-new-solution-created.png)
  ![consola](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-console.png)

5. Haga clic en **AGREGAR UN DISPOSITIVO**.

6. Haga clic en **Añadir nuevo** para **Dispositivo personalizado**.
  ![Incorporación de un nuevo dispositivo](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-add-new-device.png)

7. Haga clic en **Permitirme definir mi propio Id. de dispositivo**, escriba `AZ3166`y, a continuación, haga clic en **Crear**.
  ![Creación de un dispositivo con identificador](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/azure-iot-suite-new-device-configuration.png)

8. Tome nota del **nombre de host de IoT Hub** y haga clic en **Listo**.

## <a name="open-the-remotemonitoring-sample"></a>Apertura del ejemplo de RemoteMonitoring

1. Desconecte el DevKit del equipo, si está conectado.

2. Inicie VS Code.

3. Conecte el DevKit al equipo. Código de VS detecta automáticamente el DevKit y abre las páginas siguientes:
  * Página de introducción del DevKit.
  * Ejemplos de Arduino: ejemplos prácticos para empezar a trabajar con DevKit.

4. Expanda la sección de la izquierda **EJEMPLOS DE ARDUINO**, vaya a **Ejemplos para MXCHIP AZ3166 > AzureIoT** y seleccione **RemoteMonitoring**. Se abre una nueva ventana de VS Code que contiene la carpeta de proyecto.
  > [!NOTE]
  > Si cierra el panel, puede volver a abrirlo. Utilice `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) para abrir la paleta de comandos, escriba **Arduino** y, a continuación, busque y seleccione **Arduino: ejemplos** .

## <a name="provision-required-azure-services"></a>Aprovisionamiento de los servicios de Azure necesarios

En la ventana de la solución, ejecute la tarea mediante `Ctrl+P` (macOS: `Cmd+P`) escribiendo `task cloud-provision`en el cuadro de texto proporcionado:

En el terminal de VS Code, una línea de comandos interactiva le guía durante el aprovisionamiento de los servicios de Azure necesarios:

![Aprovisionamiento de los recursos de Azure](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/provision.png)

## <a name="build-and-upload-the-device-code"></a>Creación y carga del código del dispositivo

1. Use `Ctrl+P` (macOS: `Cmd + P`) y escriba **task config-device-connection**.

2. El terminal le pregunta si desea usar la cadena de conexión que se recupera en el paso `task cloud-provision`. También podría introducir su propia cadena de conexión de dispositivo, haciendo clic en "Create New..." (Crear nuevo...)

3. El terminal le pide que especifique el modo de configuración. Para ello, mantenga presionado el botón A, y presione y suelte el botón de restablecimiento. La pantalla muestra el identificador de DevKit y "Configuration" (Configuración).
  ![Entrada de cadena de conexión](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/config-device-connection.png)

4. Después de que `task config-device-connection` termine, haga clic en `F1` para cargar los comandos VS Code y seleccione `Arduino: Upload`, a continuación, VS Code inicia la comprobación y la carga del boceto de Arduino: ![Comprobación y carga del boceto de Arduino](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/arduino-upload.png)

El DevKit se reinicia y comienza a ejecutar el código.

## <a name="test-the-project"></a>Prueba del proyecto

Cuando se ejecuta la aplicación de ejemplo, DevKit envía datos de sensor vía Wi-Fi a la instancia de Azure IoT Suite. Para ver el resultado, siga estos pasos:

1. Vaya a Azure IoT Suite y haga clic en **PANEL**.

2. En la consola de solución de Azure IoT Suite, verá el estado del sensor de DevKit.

![Datos del sensor de Azure IoT Suite](media/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring/sensor-status.png)

## <a name="change-device-id"></a>Cambio del identificador del dispositivo

Puede cambiar el identificador del dispositivo en IoT Hub siguiendo [esta guía](https://microsoft.github.io/azure-iot-developer-kit/docs/customize-device-id/). Y si desea cambiar el valor codificado de forma rígida **AZ3166** para personalizar el identificador de dispositivo en el código, [aquí](https://github.com/Microsoft/devkit-sdk/blob/master/AZ3166/src/libraries/AzureIoT/examples/RemoteMonitoring/RemoteMonitoring.ino#L23) tiene la línea de código que puede modificar.

## <a name="problems-and-feedback"></a>Problemas y comentarios

Si tiene algún problema, acuda a [P+F](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/), o también puede ponerse en contacto con nosotros a través de los siguientes canales:

* [Gitter.im](http://gitter.im/Microsoft/azure-iot-developer-kit)
* [Stackoverflow](https://stackoverflow.com/questions/tagged/iot-devkit)

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido cómo conectar un dispositivo de DevKit a Azure IoT Suite y visualizar los datos de sensor, aquí tiene los siguientes pasos sugeridos:

* [Información general de Azure IoT Suite](https://docs.microsoft.com/azure/iot-suite/)
* [Connect an MXChip IoT DevKit device to your Microsoft IoT Central application](https://docs.microsoft.com/en-us/microsoft-iot-central/howto-connect-devkit) (Conectar un dispositivo MXChip IoT DevKit a una aplicación de Microsoft IoT Central)
