---
title: "Olá aaaUnderstand SDKs do Azure IoT | Microsoft Docs"
description: "Guia do desenvolvedor - informações sobre e links toohello SDKs vários para o dispositivo e o serviço do IoT do Azure que você pode usar toobuild aplicativos de dispositivos e aplicativos de back-end."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: c5c9a497-bb03-4301-be2d-00edfb7d308f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e319451ca97876666e1c011ee0e1a73d0a0f1ed1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a>Entender e usar os SDKs do Azure IoT

Há três categorias de SDK para trabalhar com o Hub IoT:

* **Dispositivo SDKs** permitem que você toobuild aplicativos que são executados em seus dispositivos IoT. Esses aplicativos enviar hub de IoT tooyour telemetria e, opcionalmente, recebem mensagens de seu hub IoT.

* **Serviço SDKs** habilitar você toomanage seu hub IoT e, opcionalmente, enviar mensagens tooyour IoT dispositivos.

* **Borda de IoT do Azure** permite que você toobuild dispositivos de tooenable gateways que não use um dos protocolos Olá suportada ou quando precisar de mensagens tooprocess na borda da saudação.

SDKs são fornecidos toosupport várias linguagens de programação.

## <a name="azure-iot-device-sdks"></a>SDKs do dispositivo IoT do Azure

Olá SDKs de dispositivo do Microsoft Azure IoT contêm código que facilita a criação de dispositivos e aplicativos que se conectam tooand são gerenciados pelos serviços do Azure IoT Hub.

Olá seguintes SDKs de dispositivo IoT do Azure estão disponível toodownload do GitHub:

* [Dispositivo SDK do dispositivo IoT do Azure para C][lnk-c-device-sdk] gravado em ANSI C (C99) para portabilidade e compatibilidade ampla da plataforma. Há duas bibliotecas de cliente de dispositivo para C, hello baixo nível **iothub_client** e hello **serializador**.
* [SDK do dispositivo IoT do Azure para .NET][lnk-dotnet-device-sdk]
* [SDK do dispositivo IoT do Azure para Java][lnk-java-device-sdk]
* [SDK do dispositivo IoT do Azure para Node.js][lnk-node-device-sdk]
* [SDK do dispositivo IoT do Azure para Python][lnk-python-device-sdk]

> [!NOTE]
> Consulte arquivos Leiame de saudação em repositórios de GitHub Olá para obter informações sobre como usar o idioma e binários de tooinstall de gerenciadores de pacotes específicos de plataforma e dependências em seu computador de desenvolvimento.
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a>Compatibilidade de plataforma do sistema operacional e hardware

Para obter mais informações sobre a compatibilidade do SDK com dispositivos de hardware específicos, consulte Olá [Azure Certified para catálogo de dispositivo IoT][lnk-certified].

## <a name="azure-iot-service-sdks"></a>SDKs do serviço IoT do Azure

serviço de Azure IoT Olá SDKs contêm código toofacilitate criação de aplicativos que interagem diretamente com segurança e dispositivos de toomanage de IoT Hub.

Olá seguintes SDKs do serviço de Azure IoT são toodownload disponível do GitHub:

* [SDK de serviço do Azure IoT para .NET][lnk-dotnet-service-sdk]
* [SDK de serviço do Azure IoT para Node.js][lnk-node-service-sdk]
* [SDK de serviço do Azure IoT para Java][lnk-java-service-sdk]
* [SDK de serviço IoT do Azure para Python][lnk-python-service-sdk]
* [SDK de serviço do Azure IoT para C][lnk-c-service-sdk]

> [!NOTE]
> Consulte arquivos Leiame de saudação em repositórios de GitHub Olá para obter informações sobre como usar o idioma e binários de tooinstall de gerenciadores de pacotes específicos de plataforma e dependências em seu computador de desenvolvimento.

## <a name="azure-iot-edge"></a>Azure IoT Edge

Borda de IoT do Azure contém Olá infraestrutura e módulos toocreate IoT soluções de gateway. Você pode estender o cenário de ponta a ponta do IoT borda toocreate gateways tooany personalizada.

Baixe o [Azure IoT Edge][lnk-iot-edge] no GitHub.

## <a name="online-api-reference-documentation"></a>Documentação de referência online de API

Olá, lista a seguir contém links documentação de referência de API tooonline para dispositivo IoT do Azure, serviço e bibliotecas de gateway:

* [Internet das Coisas (IoT) .NET][lnk-dotnet-ref]
* [REST do Hub IoT][lnk-rest-ref]
* [SDK do dispositivo IoT do Azure para C][lnk-c-ref]
* [SDK do dispositivo IoT do Azure para Java][lnk-java-ref]
* [SDK de serviço do Azure IoT para Java][lnk-java-service-ref]
* [SDK do dispositivo IoT do Azure para Node.js][lnk-node-ref]
* [SDK de serviço do Azure IoT para Node.js][lnk-node-service-ref]
* [Azure IoT Edge][lnk-gateway-ref]

## <a name="next-steps"></a>Próximas etapas

Outros tópicos de referência neste Guia do desenvolvedor do Hub IoT incluem:

* [Pontos de extremidade do Hub IoT][lnk-devguide-endpoints]
* [Linguagem de consulta do Hub IoT para dispositivos gêmeos, trabalhos e roteamento de mensagens][lnk-devguide-query]
* [Cotas e limitações][lnk-devguide-quotas]
* [Suporte ao MQTT do Hub IoT][lnk-devguide-mqtt]

<!-- Links and images -->

[lnk-c-device-sdk]: https://github.com/Azure/azure-iot-sdk-c
[lnk-c-service-sdk]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_service_client
[lnk-dotnet-device-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-java-device-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device
[lnk-dotnet-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-java-service-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/service
[lnk-node-device-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/device
[lnk-node-service-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/service
[lnk-python-device-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device
[lnk-python-service-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/service
[lnk-certified]: https://catalog.azureiotsuite.com/
[lnk-iot-edge]: https://github.com/Azure/iot-edge

[lnk-dotnet-ref]: https://docs.microsoft.com/dotnet/api/microsoft.azure.devices
[lnk-c-ref]: https://azure.github.io/azure-iot-sdk-c/index.html
[lnk-java-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.device
[lnk-node-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-rest-ref]: https://docs.microsoft.com/rest/api/iothub/
[lnk-java-service-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth
[lnk-node-service-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-gateway-ref]: http://azure.github.io/iot-edge/api_reference/c/html/

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
