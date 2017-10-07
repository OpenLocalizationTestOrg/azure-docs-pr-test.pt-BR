---
title: "metadados de informações de aaaDevice em Olá solução de monitoramento remoto | Microsoft Docs"
description: "Uma descrição do hello Azure IoT pré-configurado solução de monitoramento remoto e sua arquitetura."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="23648-103">Metadados de informações de dispositivo no hello solução pré-configurada de monitoramento remoto</span><span class="sxs-lookup"><span data-stu-id="23648-103">Device information metadata in hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="23648-104">Olá solução pré-configurada de monitoramento remoto do Azure IoT Suite demonstra uma abordagem para o gerenciamento de metadados do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="23648-104">hello Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="23648-105">Este artigo descreve a abordagem de saudação esta solução usa tooenable toounderstand você:</span><span class="sxs-lookup"><span data-stu-id="23648-105">This article outlines hello approach this solution takes tooenable you toounderstand:</span></span>

* <span data-ttu-id="23648-106">Qual solução de saudação do dispositivo metadados armazena.</span><span class="sxs-lookup"><span data-stu-id="23648-106">What device metadata hello solution stores.</span></span>
* <span data-ttu-id="23648-107">Como solução Olá gerencia Olá metadados do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="23648-107">How hello solution manages hello device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="23648-108">Contexto</span><span class="sxs-lookup"><span data-stu-id="23648-108">Context</span></span>

<span data-ttu-id="23648-109">Olá monitoramento remoto pré-configurado solução usa [Azure IoT Hub] [ lnk-iot-hub] tooenable toohello de dados de toosend seus dispositivos na nuvem.</span><span class="sxs-lookup"><span data-stu-id="23648-109">hello remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] tooenable your devices toosend data toohello cloud.</span></span> <span data-ttu-id="23648-110">solução de saudação armazena informações sobre os dispositivos em três locais diferentes:</span><span class="sxs-lookup"><span data-stu-id="23648-110">hello solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="23648-111">Local</span><span class="sxs-lookup"><span data-stu-id="23648-111">Location</span></span> | <span data-ttu-id="23648-112">Informações armazenadas</span><span class="sxs-lookup"><span data-stu-id="23648-112">Information stored</span></span> | <span data-ttu-id="23648-113">Implementação</span><span class="sxs-lookup"><span data-stu-id="23648-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="23648-114">Registro de identidade</span><span class="sxs-lookup"><span data-stu-id="23648-114">Identity registry</span></span> | <span data-ttu-id="23648-115">Id do dispositivo, chaves de autenticação,estado habilitado</span><span class="sxs-lookup"><span data-stu-id="23648-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="23648-116">TooIoT interno de Hub</span><span class="sxs-lookup"><span data-stu-id="23648-116">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="23648-117">Dispositivos gêmeos</span><span class="sxs-lookup"><span data-stu-id="23648-117">Device twins</span></span> | <span data-ttu-id="23648-118">Metadados: propriedades relatadas, propriedades desejadas, marcas</span><span class="sxs-lookup"><span data-stu-id="23648-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="23648-119">TooIoT interno de Hub</span><span class="sxs-lookup"><span data-stu-id="23648-119">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="23648-120">Banco de Dados Cosmos</span><span class="sxs-lookup"><span data-stu-id="23648-120">Cosmos DB</span></span> | <span data-ttu-id="23648-121">Histórico de comandos e de métodos</span><span class="sxs-lookup"><span data-stu-id="23648-121">Command and method history</span></span> | <span data-ttu-id="23648-122">Personalizada para a solução</span><span class="sxs-lookup"><span data-stu-id="23648-122">Custom for solution</span></span> |

<span data-ttu-id="23648-123">IoT Hub inclui um [registro de identidade do dispositivo] [ lnk-identity-registry] toomanage acessar tooan IoT hub e usa [twins dispositivo] [ lnk-device-twin] toomanage metadados do dispositivo .</span><span class="sxs-lookup"><span data-stu-id="23648-123">IoT Hub includes a [device identity registry][lnk-identity-registry] toomanage access tooan IoT hub and uses [device twins][lnk-device-twin] toomanage device metadata.</span></span> <span data-ttu-id="23648-124">Também há um *registro do dispositivo* remoto específico da solução de monitoramento que armazena o histórico de comandos e de métodos.</span><span class="sxs-lookup"><span data-stu-id="23648-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="23648-125">Olá usos de solução de monitoramento remoto um [Cosmos DB] [ lnk-docdb] tooimplement de banco de dados um repositório personalizado para o histórico de comando e método.</span><span class="sxs-lookup"><span data-stu-id="23648-125">hello remote monitoring solution uses a [Cosmos DB][lnk-docdb] database tooimplement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="23648-126">Olá solução pré-configurada de monitoramento remoto mantém o registro de identidade de dispositivo de saudação em sincronia com informações de saudação no banco de dados de banco de dados do Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="23648-126">hello remote monitoring preconfigured solution keeps hello device identity registry in sync with hello information in hello Cosmos DB database.</span></span> <span data-ttu-id="23648-127">Ambos usam Olá mesmo toouniquely de id de dispositivo identificar cada dispositivo conectado tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="23648-127">Both use hello same device id toouniquely identify each device connected tooyour IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="23648-128">Metadados de dispositivo</span><span class="sxs-lookup"><span data-stu-id="23648-128">Device metadata</span></span>

<span data-ttu-id="23648-129">IoT Hub mantém um [duas dispositivo] [ lnk-device-twin] para cada dispositivo simulado e físico conectado tooa remota de solução de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="23648-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected tooa remote monitoring solution.</span></span> <span data-ttu-id="23648-130">solução de saudação usa dispositivo twins toomanage Olá metadados associados a dispositivos.</span><span class="sxs-lookup"><span data-stu-id="23648-130">hello solution uses device twins toomanage hello metadata associated with devices.</span></span> <span data-ttu-id="23648-131">Duas um dispositivo é um documento JSON mantido pelo IoT Hub e solução de saudação usa Olá API de Hub IoT toointeract com twins de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="23648-131">A device twin is a JSON document maintained by IoT Hub, and hello solution uses hello IoT Hub API toointeract with device twins.</span></span>

<span data-ttu-id="23648-132">Um dispositivo gêmeo armazena três tipos de metadados:</span><span class="sxs-lookup"><span data-stu-id="23648-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="23648-133">*Relatado propriedades* são enviadas tooan IoT hub por um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="23648-133">*Reported properties* are sent tooan IoT hub by a device.</span></span> <span data-ttu-id="23648-134">No hello remota de solução de monitoramento, dispositivos simulados enviam propriedades relatadas na inicialização e na resposta muito**alterar o estado do dispositivo** comandos e métodos.</span><span class="sxs-lookup"><span data-stu-id="23648-134">In hello remote monitoring solution, simulated devices send reported properties at start-up and in response too**Change device state** commands and methods.</span></span> <span data-ttu-id="23648-135">Você pode exibir propriedades relatadas no hello **lista de dispositivos** e **detalhes do dispositivo** no portal de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="23648-135">You can view reported properties in hello **Device list** and **Device details** in hello solution portal.</span></span> <span data-ttu-id="23648-136">As propriedades relatadas são somente leitura.</span><span class="sxs-lookup"><span data-stu-id="23648-136">Reported properties are read only.</span></span>
- <span data-ttu-id="23648-137">*Propriedades desejadas* são recuperadas do hub IoT de saudação pelos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="23648-137">*Desired properties* are retrieved from hello IoT hub by devices.</span></span> <span data-ttu-id="23648-138">É responsabilidade de saudação do hello dispositivo toomake alterar qualquer configuração necessária no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="23648-138">It is hello responsibility of hello device toomake any necessary configuration change on hello device.</span></span> <span data-ttu-id="23648-139">Também é responsabilidade de saudação do hub de toohello back Olá dispositivo tooreport Olá alteração como uma propriedade relatada.</span><span class="sxs-lookup"><span data-stu-id="23648-139">It is also hello responsibility of hello device tooreport hello change back toohello hub as a reported property.</span></span> <span data-ttu-id="23648-140">Você pode definir um valor de propriedade desejado por meio do portal de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="23648-140">You can set a desired property value through hello solution portal.</span></span>
- <span data-ttu-id="23648-141">*Marcas* só existem em duas de dispositivo hello e nunca são sincronizadas com um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="23648-141">*Tags* only exist in hello device twin and are never synchronized with a device.</span></span> <span data-ttu-id="23648-142">Você pode definir valores de marca no portal de solução hello e usá-los quando você filtrar Olá lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="23648-142">You can set tag values in hello solution portal and use them when you filter hello list of devices.</span></span> <span data-ttu-id="23648-143">solução de Olá também usa um toodisplay de ícone marca tooidentify Olá para um dispositivo no portal de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="23648-143">hello solution also uses a tag tooidentify hello icon toodisplay for a device in hello solution portal.</span></span>

<span data-ttu-id="23648-144">Exemplo relatado propriedades dos dispositivos Olá simulado incluem fabricante, modelo, latitude e longitude.</span><span class="sxs-lookup"><span data-stu-id="23648-144">Example reported properties from hello simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="23648-145">Lista de retorno também Olá dispositivos simulada dos métodos com suporte como uma propriedade relatada.</span><span class="sxs-lookup"><span data-stu-id="23648-145">Simulated devices also return hello list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="23648-146">Olá dispositivo simulado código só usa Olá **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** Olá de tooupdate propriedades desejadas relatado propriedades enviadas de volta tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="23648-146">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="23648-147">Todas as outras solicitações de alteração de propriedade desejadas são ignoradas.</span><span class="sxs-lookup"><span data-stu-id="23648-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="23648-148">Um documento JSON de metadados do dispositivo informações armazenado no banco de dados Cosmos DB do registro de dispositivo de Olá tem Olá estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="23648-148">A device information metadata JSON document stored in hello device registry Cosmos DB database has hello following structure:</span></span>

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> <span data-ttu-id="23648-149">Informações de dispositivo também podem incluir metadados toodescribe Olá telemetria Olá dispositivo envia tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="23648-149">Device information can also include metadata toodescribe hello telemetry hello device sends tooIoT Hub.</span></span> <span data-ttu-id="23648-150">solução de monitoramento remoto Olá usa essa toocustomize de metadados de telemetria como painel Olá exibe [telemetria dinâmica][lnk-dynamic-telemetry].</span><span class="sxs-lookup"><span data-stu-id="23648-150">hello remote monitoring solution uses this telemetry metadata toocustomize how hello dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="23648-151">Ciclo de vida</span><span class="sxs-lookup"><span data-stu-id="23648-151">Lifecycle</span></span>

<span data-ttu-id="23648-152">Quando você cria primeiro um dispositivo no portal de solução hello, solução de saudação cria uma entrada de saudação comando de toostore de banco de dados do banco de dados do Cosmos e histórico de método.</span><span class="sxs-lookup"><span data-stu-id="23648-152">When you first create a device in hello solution portal, hello solution creates an entry in hello Cosmos DB database toostore command and method history.</span></span> <span data-ttu-id="23648-153">Neste ponto, a solução de Olá também cria uma entrada para o dispositivo de saudação no registro de identidade do dispositivo hello, que gera Olá chaves Olá dispositivo usa tooauthenticate com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="23648-153">At this point, hello solution also creates an entry for hello device in hello device identity registry, which generates hello keys hello device uses tooauthenticate with IoT Hub.</span></span> <span data-ttu-id="23648-154">Ele também cria um dispositivo gêmeo.</span><span class="sxs-lookup"><span data-stu-id="23648-154">It also creates a device twin.</span></span>

<span data-ttu-id="23648-155">Quando um dispositivo conectado pela primeira solução toohello, ele envia propriedades relatadas e uma mensagem de informações do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="23648-155">When a device first connects toohello solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="23648-156">Olá informou valores de propriedade são salvas automaticamente em duas de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="23648-156">hello reported property values are automatically saved in hello device twin.</span></span> <span data-ttu-id="23648-157">Olá relatado propriedades incluem o fabricante do dispositivo hello, número do modelo, número de série e uma lista de métodos com suporte.</span><span class="sxs-lookup"><span data-stu-id="23648-157">hello reported properties include hello device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="23648-158">mensagem de informações de dispositivo de saudação inclui a lista de saudação de comandos Olá Olá dispositivo dá suporte à incluindo informações sobre quaisquer parâmetros de comando.</span><span class="sxs-lookup"><span data-stu-id="23648-158">hello device information message includes hello list of hello commands hello device supports including information about any command parameters.</span></span> <span data-ttu-id="23648-159">Quando a solução Olá recebe essa mensagem, ele atualiza informações do dispositivo Olá no banco de dados de banco de dados do Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="23648-159">When hello solution receives this message, it updates hello device information in hello Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a><span data-ttu-id="23648-160">Exibir e editar informações de dispositivo no portal de solução de saudação</span><span class="sxs-lookup"><span data-stu-id="23648-160">View and edit device information in hello solution portal</span></span>

<span data-ttu-id="23648-161">lista de dispositivos no portal de solução Olá Olá exibe Olá seguintes propriedades de dispositivo como colunas por padrão: **Status**, **DeviceId**, **fabricante**, **Número modelo**, **número de série**, **Firmware**, **plataforma**, **processador**e  **Instalado RAM**.</span><span class="sxs-lookup"><span data-stu-id="23648-161">hello device list in hello solution portal displays hello following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="23648-162">Você pode personalizar colunas Olá clicando **editor coluna**.</span><span class="sxs-lookup"><span data-stu-id="23648-162">You can customize hello columns by clicking **Column editor**.</span></span> <span data-ttu-id="23648-163">Olá propriedades do dispositivo **Latitude** e **Longitude** da unidade local Olá Olá mapa do Bing no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="23648-163">hello device properties **Latitude** and **Longitude** drive hello location in hello Bing Map on hello dashboard.</span></span>

![Editor de colunas na lista de dispositivos][img-device-list]

<span data-ttu-id="23648-165">Em Olá **detalhes do dispositivo** painel no portal de solução hello, você pode editar as propriedades desejadas e marcas (relatado propriedades são somente leitura).</span><span class="sxs-lookup"><span data-stu-id="23648-165">In hello **Device Details** pane in hello solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![Painel de detalhes do dispositivo][img-device-edit]

<span data-ttu-id="23648-167">Você pode usar tooremove um dispositivo do portal de solução de saudação de sua solução.</span><span class="sxs-lookup"><span data-stu-id="23648-167">You can use hello solution portal tooremove a device from your solution.</span></span> <span data-ttu-id="23648-168">Quando você remover um dispositivo, solução de Olá remove a entrada do dispositivo de saudação do registro de identidade e, em seguida, exclui duas de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="23648-168">When you remove a device, hello solution removes hello device entry from identity registry and then deletes hello device twin.</span></span> <span data-ttu-id="23648-169">solução Olá também remove o dispositivo de toohello relacionados de informações do banco de dados de banco de dados do Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="23648-169">hello solution also removes information related toohello device from hello Cosmos DB database.</span></span> <span data-ttu-id="23648-170">Antes de remover um dispositivo, você deverá desabilitá-lo.</span><span class="sxs-lookup"><span data-stu-id="23648-170">Before you can remove a device, you must disable it.</span></span>

![Remover o dispositivo][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="23648-172">Processamento de mensagens de informações de dispositivo</span><span class="sxs-lookup"><span data-stu-id="23648-172">Device information message processing</span></span>

<span data-ttu-id="23648-173">As mensagens de informações sobre um dispositivo enviadas por um dispositivo são diferentes das mensagens de telemetria.</span><span class="sxs-lookup"><span data-stu-id="23648-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="23648-174">Mensagens de informações do dispositivo incluem comandos Olá a que um dispositivo pode responder e qualquer histórico de comandos.</span><span class="sxs-lookup"><span data-stu-id="23648-174">Device information messages include hello commands a device can respond to, and any command history.</span></span> <span data-ttu-id="23648-175">IoT Hub em si não tem conhecimento de metadados de saudação contido em uma mensagem de informações do dispositivo e processos Olá mensagem de saudação mesma forma que processa qualquer mensagem do dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="23648-175">IoT Hub itself has no knowledge of hello metadata contained in a device information message and processes hello message in hello same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="23648-176">Na solução de monitoramento remoto de saudação um [Azure Stream Analytics] [ lnk-stream-analytics] trabalho (ASA) lê mensagens de saudação do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="23648-176">In hello remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads hello messages from IoT Hub.</span></span> <span data-ttu-id="23648-177">Olá **DeviceInfo** análise de fluxo de trabalho filtros para mensagens que contêm **"ObjectType": "DeviceInfo"** e encaminha-toohello **EventProcessorHost** host instância que é executado em um trabalho da web.</span><span class="sxs-lookup"><span data-stu-id="23648-177">hello **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them toohello **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="23648-178">Lógica em Olá **EventProcessorHost** instância usa o registro de banco de dados do Cosmos Olá dispositivo id toofind Olá para Olá dispositivo e atualização Olá registro específico.</span><span class="sxs-lookup"><span data-stu-id="23648-178">Logic in hello **EventProcessorHost** instance uses hello device id toofind hello Cosmos DB record for hello specific device and update hello record.</span></span>

> [!NOTE]
> <span data-ttu-id="23648-179">Uma mensagem de informações de dispositivo é uma mensagem padrão do dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="23648-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="23648-180">solução de saudação faz distinção entre mensagens de informações de dispositivo e telemetria por meio de consultas ASA.</span><span class="sxs-lookup"><span data-stu-id="23648-180">hello solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23648-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="23648-181">Next steps</span></span>

<span data-ttu-id="23648-182">Agora você terminou a aprender como você pode personalizar soluções Olá pré-configurados, você pode explorar alguns dos Olá outros recursos e capacidades de soluções do IoT Suite pré-configurado hello:</span><span class="sxs-lookup"><span data-stu-id="23648-182">Now you've finished learning how you can customize hello preconfigured solutions, you can explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="23648-183">[Visão geral da solução pré-configurada de manutenção preditiva][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="23648-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="23648-184">[Perguntas frequentes sobre o IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="23648-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="23648-185">[Segurança de IoT da saudação de plano de fundo para cima][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="23648-185">[IoT security from hello ground up][lnk-security-groundup]</span></span>

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
