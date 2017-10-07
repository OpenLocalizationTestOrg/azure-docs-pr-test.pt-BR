---
title: twins de dispositivo do Azure IoT Hub aaaUnderstand | Microsoft Docs
description: "Guia do desenvolvedor - usar dispositivo twins toosynchronize os dados de estado e a configuração entre os dispositivos e o IoT Hub"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="92541-103">Entender e usar dispositivos gêmeos no Hub IoT</span><span class="sxs-lookup"><span data-stu-id="92541-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="92541-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="92541-104">Overview</span></span>
<span data-ttu-id="92541-105">*Dispositivos gêmeos* são documentos JSON que armazenam informações do estado do dispositivo (metadados, configurações e condições).</span><span class="sxs-lookup"><span data-stu-id="92541-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="92541-106">IoT Hub mantém duas um dispositivo de cada dispositivo que você se conecte tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="92541-106">IoT Hub persists a device twin for each device that you connect tooIoT Hub.</span></span> <span data-ttu-id="92541-107">Este artigo descreve:</span><span class="sxs-lookup"><span data-stu-id="92541-107">This article describes:</span></span>

* <span data-ttu-id="92541-108">Olá estrutura de duas de dispositivo Olá: *marcas*, *desejado* e *relatado propriedades*, e</span><span class="sxs-lookup"><span data-stu-id="92541-108">hello structure of hello device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="92541-109">operações de saudação que aplicativos de dispositivo e de back-end pode executar em twins de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92541-109">hello operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="92541-110">Atualmente, twins de dispositivo são acessíveis somente de dispositivos que se conectam tooIoT Hub usando o protocolo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="92541-110">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="92541-111">Consulte toohello [suporte MQTT] [ lnk-devguide-mqtt] artigo para obter instruções sobre como tooconvert existente dispositivo aplicativo toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="92541-111">Refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

### <a name="when-toouse"></a><span data-ttu-id="92541-112">Quando toouse</span><span class="sxs-lookup"><span data-stu-id="92541-112">When toouse</span></span>
<span data-ttu-id="92541-113">Use os dispositivos gêmeos para:</span><span class="sxs-lookup"><span data-stu-id="92541-113">Use device twins to:</span></span>

* <span data-ttu-id="92541-114">Armazenar os metadados específicos do dispositivo na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="92541-114">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="92541-115">Por exemplo, Olá local de implantação de uma máquina de vendas.</span><span class="sxs-lookup"><span data-stu-id="92541-115">For example, hello deployment location of a vending machine.</span></span>
* <span data-ttu-id="92541-116">Relate informações de estado atual, como recursos disponíveis e condições do aplicativo do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92541-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="92541-117">Por exemplo, um dispositivo está conectado tooyour IoT hub via celular ou Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="92541-117">For example, a device is connected tooyour IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="92541-118">Sincronize o estado de saudação de fluxos de trabalho de longa duração entre o aplicativo de dispositivo e aplicativo de back-end.</span><span class="sxs-lookup"><span data-stu-id="92541-118">Synchronize hello state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="92541-119">Por exemplo, quando Olá solução novamente final Especifica Olá novo tooinstall de versão de firmware e relatórios de aplicativos de dispositivo Olá Olá várias fases do processo de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="92541-119">For example, when hello solution back end specifies hello new firmware version tooinstall, and hello device app reports hello various stages of hello update process.</span></span>
* <span data-ttu-id="92541-120">Consultar os metadados, a configuração ou o estado do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92541-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="92541-121">Consulte também[orientação de comunicação do dispositivo para nuvem] [ lnk-d2c-guidance] para obter orientação sobre como usar propriedades relatadas, mensagens de dispositivo para nuvem ou carregamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="92541-121">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="92541-122">Consulte também[orientação de comunicação de nuvem para dispositivo] [ lnk-c2d-guidance] para obter orientação sobre como usar as propriedades desejadas, métodos diretos ou mensagens de nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92541-122">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="92541-123">Dispositivos gêmeos</span><span class="sxs-lookup"><span data-stu-id="92541-123">Device twins</span></span>
<span data-ttu-id="92541-124">Dispositivos gêmeos armazenam informações relacionadas ao dispositivo que:</span><span class="sxs-lookup"><span data-stu-id="92541-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="92541-125">Termina de dispositivo e de volta pode usar a configuração e as condições de dispositivo toosynchronize.</span><span class="sxs-lookup"><span data-stu-id="92541-125">Device and back ends can use toosynchronize device conditions and configuration.</span></span>
* <span data-ttu-id="92541-126">back-end de solução Olá use tooquery e operações de execução longa de destino.</span><span class="sxs-lookup"><span data-stu-id="92541-126">hello solution back end can use tooquery and target long-running operations.</span></span>

<span data-ttu-id="92541-127">ciclo de vida de saudação de duas um dispositivo é vinculado correspondente toohello [identidade do dispositivo][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="92541-127">hello lifecycle of a device twin is linked toohello corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="92541-128">Os dispositivos gêmeos são criados e excluídos implicitamente quando uma nova identidade de dispositivo é criada ou excluída no Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="92541-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="92541-129">Um dispositivo gêmeo é um documento JSON que inclui:</span><span class="sxs-lookup"><span data-stu-id="92541-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="92541-130">**Marcas**.</span><span class="sxs-lookup"><span data-stu-id="92541-130">**Tags**.</span></span> <span data-ttu-id="92541-131">Uma seção do documento JSON Olá Olá back-end solução pode ler e gravar.</span><span class="sxs-lookup"><span data-stu-id="92541-131">A section of hello JSON document that hello solution back end can read from and write to.</span></span> <span data-ttu-id="92541-132">Marcas não são visíveis toodevice aplicativos.</span><span class="sxs-lookup"><span data-stu-id="92541-132">Tags are not visible toodevice apps.</span></span>
* <span data-ttu-id="92541-133">**Propriedades desejadas**.</span><span class="sxs-lookup"><span data-stu-id="92541-133">**Desired properties**.</span></span> <span data-ttu-id="92541-134">Usada junto com a configuração do dispositivo toosynchronize propriedades relatado ou condições.</span><span class="sxs-lookup"><span data-stu-id="92541-134">Used along with reported properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="92541-135">Propriedades desejadas só podem ser definidas pela solução de saudação volta final e podem ser lido pelo aplicativo de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="92541-135">Desired properties can only be set by hello solution back end and can be read by hello device app.</span></span> <span data-ttu-id="92541-136">aplicativo de dispositivo Olá também pode ser notificado em tempo real de alterações em Propriedades de saudação desejada.</span><span class="sxs-lookup"><span data-stu-id="92541-136">hello device app can also be notified in real time of changes in hello desired properties.</span></span>
* <span data-ttu-id="92541-137">**Propriedades reportadas**.</span><span class="sxs-lookup"><span data-stu-id="92541-137">**Reported properties**.</span></span> <span data-ttu-id="92541-138">Usada junto com a configuração do dispositivo toosynchronize propriedades desejadas ou condições.</span><span class="sxs-lookup"><span data-stu-id="92541-138">Used along with desired properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="92541-139">Propriedades relatadas só pode ser definidas por aplicativo para dispositivo hello e podem ser leitura e consultadas pelo back-end de solução hello.</span><span class="sxs-lookup"><span data-stu-id="92541-139">Reported properties can only be set by hello device app and can be read and queried by hello solution back end.</span></span>

<span data-ttu-id="92541-140">Além disso, raiz de saudação do documento JSON Olá dispositivo duas contém propriedades somente leitura de saudação de identidade de dispositivo correspondente Olá armazenados em Olá [registro identidade][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="92541-140">Additionally, hello root of hello device twin JSON document contains hello read-only properties from hello corresponding device identity stored in hello [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="92541-141">saudação de exemplo a seguir mostra uma documento JSON de duas do dispositivo:</span><span class="sxs-lookup"><span data-stu-id="92541-141">hello following example shows a device twin JSON document:</span></span>

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

<span data-ttu-id="92541-142">Na raiz do objeto hello, é Olá propriedades do sistema e objetos de contêiner para `tags` e `reported` e `desired` propriedades.</span><span class="sxs-lookup"><span data-stu-id="92541-142">In hello root object, are hello system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="92541-143">Olá `properties` contêiner contém alguns elementos somente leitura (`$metadata`, `$etag`, e `$version`) descrito no hello [dispositivo duas metadados] [ lnk-twin-metadata] e [ Simultaneidade otimista] [ lnk-concurrency] seções.</span><span class="sxs-lookup"><span data-stu-id="92541-143">hello `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in hello [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="92541-144">Exemplo da propriedade reportada</span><span class="sxs-lookup"><span data-stu-id="92541-144">Reported property example</span></span>
<span data-ttu-id="92541-145">No exemplo anterior de saudação, duas de dispositivo Olá contém um `batteryLevel` propriedade é relatada pelo aplicativo de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="92541-145">In hello previous example, hello device twin contains a `batteryLevel` property that is reported by hello device app.</span></span> <span data-ttu-id="92541-146">Essa propriedade torna possível tooquery e operar em dispositivos com base no nível de bateria relatado última hello.</span><span class="sxs-lookup"><span data-stu-id="92541-146">This property makes it possible tooquery and operate on devices based on hello last reported battery level.</span></span> <span data-ttu-id="92541-147">Outros exemplos incluem hello dispositivo app reporting recursos do dispositivo ou opções de conectividade.</span><span class="sxs-lookup"><span data-stu-id="92541-147">Other examples include hello device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="92541-148">Propriedades relatadas simplificam cenários onde o back-end de solução hello está interessada em Olá conhecido último valor de uma propriedade.</span><span class="sxs-lookup"><span data-stu-id="92541-148">Reported properties simplify scenarios where hello solution back end is interested in hello last known value of a property.</span></span> <span data-ttu-id="92541-149">Use [mensagens de dispositivo para nuvem] [ lnk-d2c] se back-end de solução Olá precisa tooprocess telemetria do dispositivo no formulário de saudação de sequências de eventos de marca, como a série temporal.</span><span class="sxs-lookup"><span data-stu-id="92541-149">Use [device-to-cloud messages][lnk-d2c] if hello solution back end needs tooprocess device telemetry in hello form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="92541-150">Exemplo da propriedade desejada</span><span class="sxs-lookup"><span data-stu-id="92541-150">Desired property example</span></span>
<span data-ttu-id="92541-151">No exemplo anterior de saudação, Olá `telemetryConfig` duas dispositivo desejado e relatadas propriedades são usadas pelo back-end de solução hello e configuração de telemetria de Olá Olá dispositivo aplicativo toosynchronize para este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92541-151">In hello previous example, hello `telemetryConfig` device twin desired and reported properties are used by hello solution back end and hello device app toosynchronize hello telemetry configuration for this device.</span></span> <span data-ttu-id="92541-152">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="92541-152">For example:</span></span>

1. <span data-ttu-id="92541-153">back-end de solução Olá define a propriedade de saudação desejada com o valor de configuração de saudação desejada.</span><span class="sxs-lookup"><span data-stu-id="92541-153">hello solution back end sets hello desired property with hello desired configuration value.</span></span> <span data-ttu-id="92541-154">Aqui é parte de saudação do documento hello com o conjunto de propriedades de saudação desejado:</span><span class="sxs-lookup"><span data-stu-id="92541-154">Here is hello portion of hello document with hello desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="92541-155">aplicativo de dispositivo de saudação é notificado sobre alteração de Olá imediatamente se conectado, ou em Olá primeiro se reconectar.</span><span class="sxs-lookup"><span data-stu-id="92541-155">hello device app is notified of hello change immediately if connected, or at hello first reconnect.</span></span> <span data-ttu-id="92541-156">Olá aplicativo de dispositivo reporta configuração Olá atualizado (ou uma condição de erro usando Olá `status` propriedade).</span><span class="sxs-lookup"><span data-stu-id="92541-156">hello device app then reports hello updated configuration (or an error condition using hello `status` property).</span></span> <span data-ttu-id="92541-157">Aqui está parte Olá Olá relatado propriedades:</span><span class="sxs-lookup"><span data-stu-id="92541-157">Here is hello portion of hello reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="92541-158">back-end de solução Olá pode acompanhar Olá resultados da operação de configuração de saudação em vários dispositivos, por [consultando] [ lnk-query] twins do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92541-158">hello solution back end can track hello results of hello configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="92541-159">trechos de código anteriores Hello são exemplos, otimizado para legibilidade, de uma maneira tooencode uma configuração de dispositivo e seu status.</span><span class="sxs-lookup"><span data-stu-id="92541-159">hello preceding snippets are examples, optimized for readability, of one way tooencode a device configuration and its status.</span></span> <span data-ttu-id="92541-160">IoT Hub não impõe um esquema específico para duas de dispositivo de saudação desejado e relatado propriedades em twins de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="92541-160">IoT Hub does not impose a specific schema for hello device twin desired and reported properties in hello device twins.</span></span>
> 
> 

<span data-ttu-id="92541-161">Você pode usar operações de execução longa toosynchronize twins como atualizações de firmware.</span><span class="sxs-lookup"><span data-stu-id="92541-161">You can use twins toosynchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="92541-162">Para obter mais informações sobre como toouse propriedades toosynchronize e rastrear uma operação de longa duração em todos os dispositivos, consulte [uso desejado dispositivos de tooconfigure propriedades][lnk-twin-properties].</span><span class="sxs-lookup"><span data-stu-id="92541-162">For more information on how toouse properties toosynchronize and track a long running operation across devices, see [Use desired properties tooconfigure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="92541-163">Operações de back-end</span><span class="sxs-lookup"><span data-stu-id="92541-163">Back-end operations</span></span>
<span data-ttu-id="92541-164">back-end de solução Olá opera em duas de dispositivo hello usando Olá operações atômicas, expostas por meio de HTTP a seguir:</span><span class="sxs-lookup"><span data-stu-id="92541-164">hello solution back end operates on hello device twin using hello following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="92541-165">**Recuperar dispositivo gêmeo por id**. Essa operação retorna Olá dispositivo duas documento, inclusive as marcas e desejado, relatado e as propriedades do sistema.</span><span class="sxs-lookup"><span data-stu-id="92541-165">**Retrieve device twin by id**. This operation returns hello device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="92541-166">**Atualizar parcialmente o dispositivo gêmeo**.</span><span class="sxs-lookup"><span data-stu-id="92541-166">**Partially update device twin**.</span></span> <span data-ttu-id="92541-167">Esta operação permite marcas de Olá Olá solução back-end toopartially atualização ou as propriedades desejadas em duas um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92541-167">This operation enables hello solution back end toopartially update hello tags or desired properties in a device twin.</span></span> <span data-ttu-id="92541-168">atualização parcial Olá é expressa como um documento JSON que adiciona ou atualiza qualquer propriedade.</span><span class="sxs-lookup"><span data-stu-id="92541-168">hello partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="92541-169">Propriedades definidas muito`null` são removidos.</span><span class="sxs-lookup"><span data-stu-id="92541-169">Properties set too`null` are removed.</span></span> <span data-ttu-id="92541-170">Olá exemplo a seguir cria uma nova propriedade desejada com o valor `{"newProperty": "newValue"}`, substitui o valor existente de saudação do `existingProperty` com `"otherNewValue"`e remove `otherOldProperty`.</span><span class="sxs-lookup"><span data-stu-id="92541-170">hello following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites hello existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="92541-171">Nenhuma outra alteração é feitas tooexisting desejado propriedades ou marcas:</span><span class="sxs-lookup"><span data-stu-id="92541-171">No other changes are made tooexisting desired properties or tags:</span></span>
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. <span data-ttu-id="92541-172">**Substituir propriedades desejadas**.</span><span class="sxs-lookup"><span data-stu-id="92541-172">**Replace desired properties**.</span></span> <span data-ttu-id="92541-173">Esta operação habilita Olá solução back-end toocompletely substituir todas as propriedades desejadas existentes e substituir por um novo documento JSON para `properties/desired`.</span><span class="sxs-lookup"><span data-stu-id="92541-173">This operation enables hello solution back end toocompletely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="92541-174">**Substituir marcas**.</span><span class="sxs-lookup"><span data-stu-id="92541-174">**Replace tags**.</span></span> <span data-ttu-id="92541-175">Esta operação habilita Olá solução back-end toocompletely substituir todas as marcas existentes e substituir por um novo documento JSON para `tags`.</span><span class="sxs-lookup"><span data-stu-id="92541-175">This operation enables hello solution back end toocompletely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="92541-176">**Receba notificações gêmeas**.</span><span class="sxs-lookup"><span data-stu-id="92541-176">**Receive twin notifications**.</span></span> <span data-ttu-id="92541-177">Esta operação permite toobe de back-end de solução Olá notificado quando duas Olá é modificada.</span><span class="sxs-lookup"><span data-stu-id="92541-177">This operation allows hello solution back end toobe notified when hello twin is modified.</span></span> <span data-ttu-id="92541-178">toodo assim, sua solução de IoT precisa de uma rota de toocreate e tooset Olá fonte de dados igual muito*twinChangeEvents*.</span><span class="sxs-lookup"><span data-stu-id="92541-178">toodo so, your IoT solution needs toocreate a route and tooset hello Data Source equal too*twinChangeEvents*.</span></span> <span data-ttu-id="92541-179">Por padrão, nenhuma notificação gêmea é enviada, ou seja, nenhuma dessas rotas existe previamente.</span><span class="sxs-lookup"><span data-stu-id="92541-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="92541-180">Se a taxa de saudação de alteração é muito alta ou por outros motivos, como falhas internas, Olá IoT Hub pode enviar apenas uma notificação que contém todas as alterações.</span><span class="sxs-lookup"><span data-stu-id="92541-180">If hello rate of change is too high, or for other reasons, such as internal failures, hello IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="92541-181">Portanto, se seu aplicativo precisar de auditoria e registro em log confiáveis de todos os estados intermediários, ainda será recomendável que você use mensagens D2C.</span><span class="sxs-lookup"><span data-stu-id="92541-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="92541-182">mensagem de notificação de duas Olá inclui propriedades e corpo.</span><span class="sxs-lookup"><span data-stu-id="92541-182">hello twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="92541-183">Propriedades</span><span class="sxs-lookup"><span data-stu-id="92541-183">Properties</span></span>

    | <span data-ttu-id="92541-184">Nome</span><span class="sxs-lookup"><span data-stu-id="92541-184">Name</span></span> | <span data-ttu-id="92541-185">Valor</span><span class="sxs-lookup"><span data-stu-id="92541-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="92541-186">$content-type</span><span class="sxs-lookup"><span data-stu-id="92541-186">$content-type</span></span> | <span data-ttu-id="92541-187">aplicativo/json</span><span class="sxs-lookup"><span data-stu-id="92541-187">application/json</span></span> |
    <span data-ttu-id="92541-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="92541-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="92541-189">Hora de envio da notificação de saudação</span><span class="sxs-lookup"><span data-stu-id="92541-189">Time when hello notification was sent</span></span> |
    <span data-ttu-id="92541-190">$iothub-message-source</span><span class="sxs-lookup"><span data-stu-id="92541-190">$iothub-message-source</span></span> | <span data-ttu-id="92541-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="92541-191">twinChangeEvents</span></span> |
    <span data-ttu-id="92541-192">$content-encoding</span><span class="sxs-lookup"><span data-stu-id="92541-192">$content-encoding</span></span> | <span data-ttu-id="92541-193">utf-8</span><span class="sxs-lookup"><span data-stu-id="92541-193">utf-8</span></span> |
    <span data-ttu-id="92541-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="92541-194">deviceId</span></span> | <span data-ttu-id="92541-195">ID do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="92541-195">Id of hello device</span></span> |
    <span data-ttu-id="92541-196">hubName</span><span class="sxs-lookup"><span data-stu-id="92541-196">hubName</span></span> | <span data-ttu-id="92541-197">Nome do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="92541-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="92541-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="92541-198">operationTimestamp</span></span> | <span data-ttu-id="92541-199">Carimbo de data/hora [ISO8601] da operação</span><span class="sxs-lookup"><span data-stu-id="92541-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="92541-200">iothub-message-schema</span><span class="sxs-lookup"><span data-stu-id="92541-200">iothub-message-schema</span></span> | <span data-ttu-id="92541-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="92541-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="92541-202">opType</span><span class="sxs-lookup"><span data-stu-id="92541-202">opType</span></span> | <span data-ttu-id="92541-203">"replaceTwin" ou "updateTwin"</span><span class="sxs-lookup"><span data-stu-id="92541-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="92541-204">Propriedades do sistema de mensagens são prefixadas com hello `'$'` símbolo.</span><span class="sxs-lookup"><span data-stu-id="92541-204">Message system properties are prefixed with hello `'$'` symbol.</span></span>

    - <span data-ttu-id="92541-205">Corpo</span><span class="sxs-lookup"><span data-stu-id="92541-205">Body</span></span>
        
    <span data-ttu-id="92541-206">Esta seção inclui todas as alterações de duas Olá em um formato JSON.</span><span class="sxs-lookup"><span data-stu-id="92541-206">This section includes all hello twin changes in a JSON format.</span></span> <span data-ttu-id="92541-207">Ele usa o mesmo formato de saudação como um patch, com a diferença de saudação que ele pode conter todas as seções de duas: marcas, properties.reported, properties.desired e que contém elementos hello "$metadata".</span><span class="sxs-lookup"><span data-stu-id="92541-207">It uses hello same format as a patch, with hello difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains hello “$metadata” elements.</span></span> <span data-ttu-id="92541-208">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="92541-208">For example,</span></span>
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

<span data-ttu-id="92541-209">Todos os Olá anterior suporte a operações [simultaneidade otimista] [ lnk-concurrency] e exigem Olá **ServiceConnect** permissão, conforme definido no hello [segurança ] [ lnk-security] artigo.</span><span class="sxs-lookup"><span data-stu-id="92541-209">All hello preceding operations support [Optimistic concurrency][lnk-concurrency] and require hello **ServiceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="92541-210">Além disso, operações toothese, solução de saudação fazer final pode:</span><span class="sxs-lookup"><span data-stu-id="92541-210">In addition toothese operations, hello solution back end can:</span></span>

* <span data-ttu-id="92541-211">Consultar twins de dispositivo hello usando Olá tipo SQL [linguagem de consulta de IoT Hub][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="92541-211">Query hello device twins using hello SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="92541-212">Executar operações em conjuntos grandes de gêmeos de dispositivo usando [trabalhos][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="92541-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="92541-213">Operações de dispositivo</span><span class="sxs-lookup"><span data-stu-id="92541-213">Device operations</span></span>
<span data-ttu-id="92541-214">aplicativo de dispositivo Olá opera em duas de dispositivo hello usando Olá operações atômicas a seguir:</span><span class="sxs-lookup"><span data-stu-id="92541-214">hello device app operates on hello device twin using hello following atomic operations:</span></span>

1. <span data-ttu-id="92541-215">**Recuperar dispositivo gêmeo**.</span><span class="sxs-lookup"><span data-stu-id="92541-215">**Retrieve device twin**.</span></span> <span data-ttu-id="92541-216">Essa operação retorna um documento de duas dispositivo hello (incluindo marcas e desejado, relatado e propriedades do sistema) para Olá dispositivo conectado no momento.</span><span class="sxs-lookup"><span data-stu-id="92541-216">This operation returns hello device twin document (including tags and desired, reported and system properties) for hello currently connected device.</span></span>
2. <span data-ttu-id="92541-217">**Atualizar parcialmente as propriedades reportadas**.</span><span class="sxs-lookup"><span data-stu-id="92541-217">**Partially update reported properties**.</span></span> <span data-ttu-id="92541-218">Esta operação habilita Olá parcial atualização de saudação relatado propriedades de dispositivo de saudação conectado no momento.</span><span class="sxs-lookup"><span data-stu-id="92541-218">This operation enables hello partial update of hello reported properties of hello currently connected device.</span></span> <span data-ttu-id="92541-219">Saudação de usa essa operação Atualizar JSON mesmo formato que Olá solução back usos para uma atualização parcial de propriedades desejadas.</span><span class="sxs-lookup"><span data-stu-id="92541-219">This operation uses hello same JSON update format that hello solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="92541-220">**Observar as propriedades desejadas**.</span><span class="sxs-lookup"><span data-stu-id="92541-220">**Observe desired properties**.</span></span> <span data-ttu-id="92541-221">dispositivo conectado no momento da saudação pode escolher toobe notificado das propriedades de toohello desejado atualizações quando eles ocorrem.</span><span class="sxs-lookup"><span data-stu-id="92541-221">hello currently connected device can choose toobe notified of updates toohello desired properties when they happen.</span></span> <span data-ttu-id="92541-222">Olá receberá Olá mesmo formulário de atualização (substituição parcial ou completa) executado pelo back-end de solução hello.</span><span class="sxs-lookup"><span data-stu-id="92541-222">hello device receives hello same form of update (partial or full replacement) executed by hello solution back end.</span></span>

<span data-ttu-id="92541-223">Todas as operações anteriores de Olá exigem Olá **DeviceConnect** permissão, conforme definido no hello [segurança] [ lnk-security] artigo.</span><span class="sxs-lookup"><span data-stu-id="92541-223">All hello preceding operations require hello **DeviceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="92541-224">Olá [dispositivo IoT do Azure SDKs] [ lnk-sdks] tornar fácil toouse Olá anterior de operações de várias plataformas e idiomas.</span><span class="sxs-lookup"><span data-stu-id="92541-224">hello [Azure IoT device SDKs][lnk-sdks] make it easy toouse hello preceding operations from many languages and platforms.</span></span> <span data-ttu-id="92541-225">Mais informações sobre detalhes de saudação de primitivos de IoT Hub para sincronização de propriedades desejadas podem ser encontradas em [fluxo de reconexão do dispositivo][lnk-reconnection].</span><span class="sxs-lookup"><span data-stu-id="92541-225">More information on hello details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="92541-226">Atualmente, twins de dispositivo são acessíveis somente de dispositivos que se conectam tooIoT Hub usando o protocolo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="92541-226">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="92541-227">Tópicos de referência:</span><span class="sxs-lookup"><span data-stu-id="92541-227">Reference topics:</span></span>
<span data-ttu-id="92541-228">Hello seguinte referência tópicos fornecem mais informações sobre o controle hub de IoT tooyour de acesso.</span><span class="sxs-lookup"><span data-stu-id="92541-228">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="92541-229">Formato de marcas e propriedades</span><span class="sxs-lookup"><span data-stu-id="92541-229">Tags and properties format</span></span>
<span data-ttu-id="92541-230">Marcas, propriedades desejadas e relatadas são objetos JSON com hello restrições a seguir:</span><span class="sxs-lookup"><span data-stu-id="92541-230">Tags, desired, and reported properties are JSON objects with hello following restrictions:</span></span>

* <span data-ttu-id="92541-231">Todas as chaves em objetos JSON são cadeias de caracteres UNICODE UTF-8 de 64 bytes que diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="92541-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="92541-232">Os caracteres permitidos excluir caracteres de controle UNICODE (segmentos C0 e C1) e `'.'`, `' '` e `'$'`.</span><span class="sxs-lookup"><span data-stu-id="92541-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="92541-233">Todos os valores de objetos JSON podem ser dos seguintes tipos de JSON de saudação: booleano, número, cadeia de caracteres, objeto.</span><span class="sxs-lookup"><span data-stu-id="92541-233">All values in JSON objects can be of hello following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="92541-234">Não há permissão para matrizes.</span><span class="sxs-lookup"><span data-stu-id="92541-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="92541-235">Todos os objetos JSON em marcações, propriedades desejadas e reportadas podem ter uma profundidade máxima de 5.</span><span class="sxs-lookup"><span data-stu-id="92541-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="92541-236">Por exemplo, Olá após o objeto é válido:</span><span class="sxs-lookup"><span data-stu-id="92541-236">For instance, hello following object is valid:</span></span>

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* <span data-ttu-id="92541-237">Todos os valores de cadeia de caracteres podem ter no máximo 512 bytes de comprimento.</span><span class="sxs-lookup"><span data-stu-id="92541-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="92541-238">Tamanho do dispositivo gêmeo</span><span class="sxs-lookup"><span data-stu-id="92541-238">Device twin size</span></span>
<span data-ttu-id="92541-239">IoT Hub impõe um limite de tamanho de 8KB em valores de saudação do `tags`, `properties/desired`, e `properties/reported`, exceto elementos somente leitura.</span><span class="sxs-lookup"><span data-stu-id="92541-239">IoT Hub enforces an 8KB size limitation on hello values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="92541-240">Olá tamanho é calculado pela contagem de todos os caracteres UNICODE de excluindo controlam caracteres (segmentos C0 e C1) e o espaço `' '` quando ele for exibido fora de uma constante de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="92541-240">hello size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="92541-241">IoT Hub rejeitada com um erro de todas as operações que deve aumentar o tamanho de saudação desses documentos acima do limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="92541-241">IoT Hub rejects with an error all operations that would increase hello size of those documents above hello limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="92541-242">Metadados do dispositivo gêmeo</span><span class="sxs-lookup"><span data-stu-id="92541-242">Device twin metadata</span></span>
<span data-ttu-id="92541-243">IoT Hub mantém Olá carimbo de hora da última atualização Olá para cada objeto JSON em duas dispositivo desejado e relatado propriedades.</span><span class="sxs-lookup"><span data-stu-id="92541-243">IoT Hub maintains hello timestamp of hello last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="92541-244">Olá carimbos de hora estão em UTC e codificado em Olá [ISO8601] formato `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span><span class="sxs-lookup"><span data-stu-id="92541-244">hello timestamps are in UTC and encoded in hello [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="92541-245">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="92541-245">For example:</span></span>

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

<span data-ttu-id="92541-246">Essa informação é mantida em todas as atualizações de toopreserve (folhas de saudação não apenas da saudação estrutura JSON) níveis que remover chaves de objeto.</span><span class="sxs-lookup"><span data-stu-id="92541-246">This information is kept at every level (not just hello leaves of hello JSON structure) toopreserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="92541-247">Simultaneidade otimista</span><span class="sxs-lookup"><span data-stu-id="92541-247">Optimistic concurrency</span></span>
<span data-ttu-id="92541-248">Marcas, propriedades desejadas e reportadas oferecem suporte à simultaneidade otimista.</span><span class="sxs-lookup"><span data-stu-id="92541-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="92541-249">Marcas de tem uma ETag, como por [RFC7232], que representa a representação da marca hello.</span><span class="sxs-lookup"><span data-stu-id="92541-249">Tags have an ETag, as per [RFC7232], that represents hello tag's JSON representation.</span></span> <span data-ttu-id="92541-250">Você pode usar ETags em operações de atualização condicional de consistência de tooensure Olá solução back-end.</span><span class="sxs-lookup"><span data-stu-id="92541-250">You can use ETags in conditional update operations from hello solution back end tooensure consistency.</span></span>

<span data-ttu-id="92541-251">Duas dispositivo desejado e relatado propriedades não tem ETags, mas tem um `$version` valor garantia toobe incremental.</span><span class="sxs-lookup"><span data-stu-id="92541-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed toobe incremental.</span></span> <span data-ttu-id="92541-252">Da mesma forma tooan ETag, versão Olá pode ser usado por Olá atualizando consistência de tooenforce parte de atualizações.</span><span class="sxs-lookup"><span data-stu-id="92541-252">Similarly tooan ETag, hello version can be used by hello updating party tooenforce consistency of updates.</span></span> <span data-ttu-id="92541-253">Por exemplo, um aplicativo de dispositivo para um relatado propriedade ou hello solução back-end para a propriedade desejada.</span><span class="sxs-lookup"><span data-stu-id="92541-253">For example, a device app for a reported property or hello solution back end for a desired property.</span></span>

<span data-ttu-id="92541-254">Versões também são úteis quando um agente observando (como o aplicativo de dispositivo Olá observando propriedades Olá desejado) necessário reconciliar corridas entre o resultado de saudação de uma operação de recuperação e uma notificação de atualização.</span><span class="sxs-lookup"><span data-stu-id="92541-254">Versions are also useful when an observing agent (such as hello device app observing hello desired properties) must reconcile races between hello result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="92541-255">Olá seção [fluxo de reconexão do dispositivo] [ lnk-reconnection] fornece mais informações.</span><span class="sxs-lookup"><span data-stu-id="92541-255">hello section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="92541-256">Fluxo de reconexão do dispositivo</span><span class="sxs-lookup"><span data-stu-id="92541-256">Device reconnection flow</span></span>
<span data-ttu-id="92541-257">O Hub IoT não preserva notificações de atualização de propriedades desejadas para dispositivos desconectados.</span><span class="sxs-lookup"><span data-stu-id="92541-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="92541-258">Ele segue que um dispositivo que está se conectando deve recuperar o documento de propriedades desejada completo de Olá, no toosubscribing de adição para notificações de atualização.</span><span class="sxs-lookup"><span data-stu-id="92541-258">It follows that a device that is connecting must retrieve hello full desired properties document, in addition toosubscribing for update notifications.</span></span> <span data-ttu-id="92541-259">Considerando a possibilidade de saudação de corridas entre notificações de atualização e de recuperação completa, deve ser garantida Olá fluxo a seguir:</span><span class="sxs-lookup"><span data-stu-id="92541-259">Given hello possibility of races between update notifications and full retrieval, hello following flow must be ensured:</span></span>

1. <span data-ttu-id="92541-260">Aplicativo de dispositivo se conecta tooan IoT hub.</span><span class="sxs-lookup"><span data-stu-id="92541-260">Device app connects tooan IoT hub.</span></span>
2. <span data-ttu-id="92541-261">O aplicativo de dispositivo se inscreve para as notificações de atualização de propriedades desejadas .</span><span class="sxs-lookup"><span data-stu-id="92541-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="92541-262">Aplicativo de dispositivo recupera o documento completo de saudação para propriedades desejadas.</span><span class="sxs-lookup"><span data-stu-id="92541-262">Device app retrieves hello full document for desired properties.</span></span>

<span data-ttu-id="92541-263">aplicativo de dispositivo Olá pode ignorar todas as notificações com `$version` menor ou igual a versão Olá Olá documento de recuperados completo.</span><span class="sxs-lookup"><span data-stu-id="92541-263">hello device app can ignore all notifications with `$version` less or equal than hello version of hello full retrieved document.</span></span> <span data-ttu-id="92541-264">Essa abordagem é possível porque o Hub IoT garante que as versões sempre aumentam.</span><span class="sxs-lookup"><span data-stu-id="92541-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="92541-265">Essa lógica já foi implementada no hello [dispositivo IoT do Azure SDKs][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="92541-265">This logic is already implemented in hello [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="92541-266">Essa descrição é útil apenas se Olá aplicativo de dispositivo não é possível usar qualquer um dos SDKs de dispositivo de IoT do Azure e deve programar diretamente a interface MQTT Olá.</span><span class="sxs-lookup"><span data-stu-id="92541-266">This description is useful only if hello device app cannot use any of Azure IoT device SDKs and must program hello MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="92541-267">Material de referência adicional</span><span class="sxs-lookup"><span data-stu-id="92541-267">Additional reference material</span></span>
<span data-ttu-id="92541-268">Outros tópicos de referência Olá guia do desenvolvedor de IoT Hub incluem:</span><span class="sxs-lookup"><span data-stu-id="92541-268">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="92541-269">Olá [pontos de extremidade de IoT Hub] [ lnk-endpoints] descreve Olá vários pontos de extremidade que expõe a cada hub IoT para operações de tempo de execução e gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="92541-269">hello [IoT Hub endpoints][lnk-endpoints] article describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="92541-270">Olá [limitação e cotas] [ lnk-quotas] descreve cotas Olá que se aplicam a toohello serviço de IoT Hub e Olá limitação tooexpect de comportamento quando você usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="92541-270">hello [Throttling and quotas][lnk-quotas] article describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="92541-271">Olá [SDKs de dispositivo e serviço de Azure IoT] [ lnk-sdks] listas de artigo Olá vários SDKs de idioma, você pode usar ao desenvolver aplicativos do dispositivo e o serviço que interagem com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="92541-271">hello [Azure IoT device and service SDKs][lnk-sdks] article lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="92541-272">Olá [linguagem de consulta de IoT Hub para twins do dispositivo, trabalhos e roteamento de mensagens] [ lnk-query] descreve Olá linguagem de consulta de IoT Hub, você pode usar informações de tooretrieve de IoT Hub sobre seus trabalhos e twins do dispositivo .</span><span class="sxs-lookup"><span data-stu-id="92541-272">hello [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="92541-273">Olá [suporte de IoT Hub MQTT] [ lnk-devguide-mqtt] artigo fornece mais informações sobre o suporte de IoT Hub de protocolo de MQTT saudação.</span><span class="sxs-lookup"><span data-stu-id="92541-273">hello [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92541-274">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="92541-274">Next steps</span></span>
<span data-ttu-id="92541-275">Agora que você aprendeu sobre twins do dispositivo, você pode estar interessado em Olá tópicos do guia de desenvolvedor de IoT Hub a seguir:</span><span class="sxs-lookup"><span data-stu-id="92541-275">Now you have learned about device twins, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="92541-276">[Invocar um método direto em um dispositivo][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="92541-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="92541-277">[Agendar trabalhos em vários dispositivos][lnk-jobs]</span><span class="sxs-lookup"><span data-stu-id="92541-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="92541-278">Se você quiser tootry alguns dos conceitos de saudação descritos neste artigo, você pode estar interessado em Olá tutoriais de IoT Hub a seguir:</span><span class="sxs-lookup"><span data-stu-id="92541-278">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="92541-279">[Como toouse Olá duas do dispositivo][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="92541-279">[How toouse hello device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="92541-280">[Como o dispositivo toouse macros propriedades][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="92541-280">[How toouse device twin properties][lnk-twin-properties]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
