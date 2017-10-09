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
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="4998c-103">Entender e usar os SDKs do Azure IoT</span><span class="sxs-lookup"><span data-stu-id="4998c-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="4998c-104">Há três categorias de SDK para trabalhar com o Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="4998c-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="4998c-105">**Dispositivo SDKs** permitem que você toobuild aplicativos que são executados em seus dispositivos IoT.</span><span class="sxs-lookup"><span data-stu-id="4998c-105">**Device SDKs** enable you toobuild apps that run on your IoT devices.</span></span> <span data-ttu-id="4998c-106">Esses aplicativos enviar hub de IoT tooyour telemetria e, opcionalmente, recebem mensagens de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4998c-106">These apps send telemetry tooyour IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="4998c-107">**Serviço SDKs** habilitar você toomanage seu hub IoT e, opcionalmente, enviar mensagens tooyour IoT dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4998c-107">**Service SDKs** enable you toomanage your IoT hub, and optionally send messages tooyour IoT devices.</span></span>

* <span data-ttu-id="4998c-108">**Borda de IoT do Azure** permite que você toobuild dispositivos de tooenable gateways que não use um dos protocolos Olá suportada ou quando precisar de mensagens tooprocess na borda da saudação.</span><span class="sxs-lookup"><span data-stu-id="4998c-108">**Azure IoT Edge** enables you toobuild gateways tooenable devices that don't use one of hello supported protocols, or when you need tooprocess messages on hello edge.</span></span>

<span data-ttu-id="4998c-109">SDKs são fornecidos toosupport várias linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="4998c-109">SDKs are provided toosupport multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="4998c-110">SDKs do dispositivo IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="4998c-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="4998c-111">Olá SDKs de dispositivo do Microsoft Azure IoT contêm código que facilita a criação de dispositivos e aplicativos que se conectam tooand são gerenciados pelos serviços do Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4998c-111">hello Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect tooand are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="4998c-112">Olá seguintes SDKs de dispositivo IoT do Azure estão disponível toodownload do GitHub:</span><span class="sxs-lookup"><span data-stu-id="4998c-112">hello following Azure IoT device SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="4998c-113">[Dispositivo SDK do dispositivo IoT do Azure para C][lnk-c-device-sdk] gravado em ANSI C (C99) para portabilidade e compatibilidade ampla da plataforma.</span><span class="sxs-lookup"><span data-stu-id="4998c-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="4998c-114">Há duas bibliotecas de cliente de dispositivo para C, hello baixo nível **iothub_client** e hello **serializador**.</span><span class="sxs-lookup"><span data-stu-id="4998c-114">There are two device client libraries for C, hello low-level **iothub_client** and hello **serializer**.</span></span>
* <span data-ttu-id="4998c-115">[SDK do dispositivo IoT do Azure para .NET][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="4998c-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="4998c-116">[SDK do dispositivo IoT do Azure para Java][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="4998c-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="4998c-117">[SDK do dispositivo IoT do Azure para Node.js][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="4998c-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="4998c-118">[SDK do dispositivo IoT do Azure para Python][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="4998c-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="4998c-119">Consulte arquivos Leiame de saudação em repositórios de GitHub Olá para obter informações sobre como usar o idioma e binários de tooinstall de gerenciadores de pacotes específicos de plataforma e dependências em seu computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="4998c-119">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="4998c-120">Compatibilidade de plataforma do sistema operacional e hardware</span><span class="sxs-lookup"><span data-stu-id="4998c-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="4998c-121">Para obter mais informações sobre a compatibilidade do SDK com dispositivos de hardware específicos, consulte Olá [Azure Certified para catálogo de dispositivo IoT][lnk-certified].</span><span class="sxs-lookup"><span data-stu-id="4998c-121">For more information about SDK compatibility with specific hardware devices, see hello [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="4998c-122">SDKs do serviço IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="4998c-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="4998c-123">serviço de Azure IoT Olá SDKs contêm código toofacilitate criação de aplicativos que interagem diretamente com segurança e dispositivos de toomanage de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4998c-123">hello Azure IoT service SDKs contain code toofacilitate building applications that interact directly with IoT Hub toomanage devices and security.</span></span>

<span data-ttu-id="4998c-124">Olá seguintes SDKs do serviço de Azure IoT são toodownload disponível do GitHub:</span><span class="sxs-lookup"><span data-stu-id="4998c-124">hello following Azure IoT service SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="4998c-125">[SDK de serviço do Azure IoT para .NET][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="4998c-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="4998c-126">[SDK de serviço do Azure IoT para Node.js][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="4998c-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="4998c-127">[SDK de serviço do Azure IoT para Java][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="4998c-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="4998c-128">[SDK de serviço IoT do Azure para Python][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="4998c-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="4998c-129">[SDK de serviço do Azure IoT para C][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="4998c-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="4998c-130">Consulte arquivos Leiame de saudação em repositórios de GitHub Olá para obter informações sobre como usar o idioma e binários de tooinstall de gerenciadores de pacotes específicos de plataforma e dependências em seu computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="4998c-130">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="4998c-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="4998c-131">Azure IoT Edge</span></span>

<span data-ttu-id="4998c-132">Borda de IoT do Azure contém Olá infraestrutura e módulos toocreate IoT soluções de gateway.</span><span class="sxs-lookup"><span data-stu-id="4998c-132">Azure IoT Edge contains hello infrastructure and modules toocreate IoT gateway solutions.</span></span> <span data-ttu-id="4998c-133">Você pode estender o cenário de ponta a ponta do IoT borda toocreate gateways tooany personalizada.</span><span class="sxs-lookup"><span data-stu-id="4998c-133">You can extend IoT Edge toocreate gateways tailored tooany end-to-end scenario.</span></span>

<span data-ttu-id="4998c-134">Baixe o [Azure IoT Edge][lnk-iot-edge] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="4998c-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="4998c-135">Documentação de referência online de API</span><span class="sxs-lookup"><span data-stu-id="4998c-135">Online API reference documentation</span></span>

<span data-ttu-id="4998c-136">Olá, lista a seguir contém links documentação de referência de API tooonline para dispositivo IoT do Azure, serviço e bibliotecas de gateway:</span><span class="sxs-lookup"><span data-stu-id="4998c-136">hello following list contains links tooonline API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="4998c-137">[Internet das Coisas (IoT) .NET][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="4998c-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="4998c-138">[REST do Hub IoT][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="4998c-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="4998c-139">[SDK do dispositivo IoT do Azure para C][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="4998c-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="4998c-140">[SDK do dispositivo IoT do Azure para Java][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="4998c-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="4998c-141">[SDK de serviço do Azure IoT para Java][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="4998c-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="4998c-142">[SDK do dispositivo IoT do Azure para Node.js][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="4998c-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="4998c-143">[SDK de serviço do Azure IoT para Node.js][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="4998c-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="4998c-144">[Azure IoT Edge][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="4998c-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="4998c-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4998c-145">Next steps</span></span>

<span data-ttu-id="4998c-146">Outros tópicos de referência neste Guia do desenvolvedor do Hub IoT incluem:</span><span class="sxs-lookup"><span data-stu-id="4998c-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="4998c-147">[Pontos de extremidade do Hub IoT][lnk-devguide-endpoints]</span><span class="sxs-lookup"><span data-stu-id="4998c-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="4998c-148">[Linguagem de consulta do Hub IoT para dispositivos gêmeos, trabalhos e roteamento de mensagens][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="4998c-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="4998c-149">[Cotas e limitações][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="4998c-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="4998c-150">[Suporte ao MQTT do Hub IoT][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="4998c-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

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
