---
title: Uso de reproductores existentes para reproducir el contenido - Azure | Microsoft Docs
description: En este tema se enumeran los reproductores existentes que puede usar para reproducir el contenido.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: a64d32747371aab2bd927e53c5d43e30de9108f9
ms.sourcegitcommit: e221d1a2e0fb245610a6dd886e7e74c362f06467
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2018
---
# <a name="playing-your-content-with-existing-players"></a>Reproducción de contenido con existentes
Azure Media Services admite muchos formatos de streaming populares como Smooth Streaming, HTTP Live Streaming y MPEG-Dash. Este tema remite a reproductores existentes que puede usar para probar sus transmisiones.

### <a name="the-azure-portal-media-services-content-player"></a>Reproductor del contenido de Media Services de Azure Portal
**Azure Portal** proporciona un reproductor de contenido que puede usar para probar el vídeo.

Haga clic en el vídeo deseado (asegúrese de que se ha [publicado](media-services-portal-publish.md)) y haga clic en el botón **Reproducir** situado en la parte inferior del portal.

Se aplican algunas consideraciones:

* El **REPRODUCTOR DE CONTENIDO DE SERVICIOS MULTIMEDIA** reproduce desde el extremo de streaming predeterminado. Si desea reproducir desde un extremo de streaming que no esté predeterminado, use otro reproductor. Por ejemplo, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a>Azure Media Player
Use [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) para reproducir el contenido (libre o protegido) en cualquiera de los siguientes formatos:

* Smooth Streaming
* MPEG DASH
* HLS
* MP4 progresivo

### <a name="flash-player"></a>Flash Player
#### <a name="aes-encrypted-with-token"></a>Cifrado de AES con token
[http://aestoken.azurewebsites.net](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a>Reproductores de Silverlight
#### <a name="monitoring"></a>Supervisión
[http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a>PlayReady con token
[http://sltoken.azurewebsites.net](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a>Reproductores DASH
[http://dashplayer.azurewebsites.net](http://dashplayer.azurewebsites.net)

[http://dashif.org](http://dashif.org)

### <a name="other"></a>Otros
Para probar las direcciones URL de HLS también puede utilizar:

* **Safari** en un dispositivo iOS o
* **3ivx HLS Player** en Windows.

## <a name="developing-video-players"></a>Desarrollo de reproductores de vídeo
Para obtener información sobre cómo desarrollar sus propios reproductores, consulte [Desarrollo de reproductores de vídeo](media-services-develop-video-players.md)

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Media Services
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
