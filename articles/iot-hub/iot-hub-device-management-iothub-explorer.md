---
title: aaaAzure gerenciamento de dispositivo IoT com o Gerenciador de Hub IOT | Microsoft Docs
description: "Use a ferramenta CLI de Gerenciador de Hub IOT de saudação para gerenciamento de dispositivos do Azure IoT Hub, apresentando métodos diretos hello e opções de gerenciamento do hello duas propriedades desejadas."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: gerenciamento de dispositivos iot do azure, gerenciamento de dispositivos hub iot do azure, iot de gerenciamento de dispositivos, gerenciamento de dispositivos hub iot
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="7dedf-104">Usar o iothub-explorer para o gerenciamento de dispositivos Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="7dedf-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="7dedf-106">[Gerenciador de Hub IOT](https://github.com/azure/iothub-explorer) é uma ferramenta CLI que são executados em um identidades de dispositivo de toomanage do computador host no registro do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7dedf-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer toomanage device identities in your IoT hub registry.</span></span> <span data-ttu-id="7dedf-107">Ela vem com opções de gerenciamento que você pode usar tooperform várias tarefas.</span><span class="sxs-lookup"><span data-stu-id="7dedf-107">It comes with management options that you can use tooperform various tasks.</span></span>

| <span data-ttu-id="7dedf-108">Opção de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="7dedf-108">Management option</span></span>          | <span data-ttu-id="7dedf-109">Tarefa</span><span class="sxs-lookup"><span data-stu-id="7dedf-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7dedf-110">Métodos diretos</span><span class="sxs-lookup"><span data-stu-id="7dedf-110">Direct methods</span></span>             | <span data-ttu-id="7dedf-111">Tornar um dispositivo para atuar como iniciar ou parar o envio de mensagens ou a reinicialização do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="7dedf-111">Make a device act such as starting or stopping sending messages or rebooting hello device.</span></span>                                        |
| <span data-ttu-id="7dedf-112">Propriedades desejadas do gêmeo</span><span class="sxs-lookup"><span data-stu-id="7dedf-112">Twin desired properties</span></span>    | <span data-ttu-id="7dedf-113">Colocar um dispositivo em alguns estados, como definir um LED toogreen ou configuração de telemetria Olá enviar intervalo (minutos) too30.</span><span class="sxs-lookup"><span data-stu-id="7dedf-113">Put a device into certain states, such as setting an LED toogreen or setting hello telemetry send interval too30 minutes.</span></span>         |
| <span data-ttu-id="7dedf-114">Propriedades relatadas do gêmeo</span><span class="sxs-lookup"><span data-stu-id="7dedf-114">Twin reported properties</span></span>   | <span data-ttu-id="7dedf-115">Obter Olá relatou o estado de um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7dedf-115">Get hello reported state of a device.</span></span> <span data-ttu-id="7dedf-116">Por exemplo, o dispositivo Olá relata Olá que LED estiver piscando agora.</span><span class="sxs-lookup"><span data-stu-id="7dedf-116">For example, hello device reports hello LED is blinking now.</span></span>                                    |
| <span data-ttu-id="7dedf-117">Marcações do gêmeo</span><span class="sxs-lookup"><span data-stu-id="7dedf-117">Twin tags</span></span>                  | <span data-ttu-id="7dedf-118">Armazenar os metadados específicos do dispositivo na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="7dedf-118">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="7dedf-119">Por exemplo, Olá local de implantação de uma máquina de vendas.</span><span class="sxs-lookup"><span data-stu-id="7dedf-119">For example, hello deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="7dedf-120">Mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="7dedf-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="7dedf-121">Dispositivo de tooa de notificações de envio.</span><span class="sxs-lookup"><span data-stu-id="7dedf-121">Send notifications tooa device.</span></span> <span data-ttu-id="7dedf-122">Por exemplo, "é muito provável que toorain hoje.</span><span class="sxs-lookup"><span data-stu-id="7dedf-122">For example, "It is very likely toorain today.</span></span> <span data-ttu-id="7dedf-123">Não se esqueça de um conjunto de toobring."</span><span class="sxs-lookup"><span data-stu-id="7dedf-123">Don't forget toobring an umbrella."</span></span>              |
| <span data-ttu-id="7dedf-124">Consultas de dispositivo gêmeo</span><span class="sxs-lookup"><span data-stu-id="7dedf-124">Device twin queries</span></span>        | <span data-ttu-id="7dedf-125">Consulta tooretrieve de twins todos os dispositivos com condições arbitrárias, como identificar os dispositivos de saudação que estão disponíveis para uso.</span><span class="sxs-lookup"><span data-stu-id="7dedf-125">Query all device twins tooretrieve those with arbitrary conditions, such as identifying hello devices that are available for use.</span></span> |

<span data-ttu-id="7dedf-126">Para obter mais explicações sobre as diferenças de saudação e orientação sobre como usar essas opções, consulte [orientação de comunicação do dispositivo para nuvem](iot-hub-devguide-d2c-guidance.md) e [orientação de comunicação de nuvem para dispositivo](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="7dedf-126">For more detailed explanation on hello differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7dedf-127">Dispositivos gêmeos são documentos JSON que armazenam informações do estado do dispositivo (metadados, configurações e condições).</span><span class="sxs-lookup"><span data-stu-id="7dedf-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="7dedf-128">IoT Hub mantém duas um dispositivo de cada dispositivo que se conecta tooit.</span><span class="sxs-lookup"><span data-stu-id="7dedf-128">IoT Hub persists a device twin for each device that connects tooit.</span></span> <span data-ttu-id="7dedf-129">Para obter mais informações sobre dispositivos gêmeos, consulte [Introdução aos dispositivos gêmeos](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="7dedf-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="7dedf-130">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="7dedf-130">What you learn</span></span>

<span data-ttu-id="7dedf-131">Você aprenderá a usar o iothub-explorer com várias opções de gerenciamento em seu computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="7dedf-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="7dedf-132">O que fazer</span><span class="sxs-lookup"><span data-stu-id="7dedf-132">What you do</span></span>

<span data-ttu-id="7dedf-133">Execute o iothub-explorer com várias opções de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="7dedf-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7dedf-134">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="7dedf-134">What you need</span></span>

- <span data-ttu-id="7dedf-135">Tutorial [configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) concluída que abrange Olá requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7dedf-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="7dedf-136">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="7dedf-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="7dedf-137">Um hub IoT do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="7dedf-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="7dedf-138">Um aplicativo cliente que envia o hub do mensagens tooyour IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="7dedf-138">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="7dedf-139">Verifique se que o dispositivo está em execução com o aplicativo de cliente hello durante este tutorial.</span><span class="sxs-lookup"><span data-stu-id="7dedf-139">Make sure your device is running with hello client application during this tutorial.</span></span>
- <span data-ttu-id="7dedf-140">iothub-explorer, [Instalar iothub-explorer](https://github.com/azure/iothub-explorer) no computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="7dedf-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-tooyour-iot-hub"></a><span data-ttu-id="7dedf-141">Conecte tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="7dedf-141">Connect tooyour IoT hub</span></span>

<span data-ttu-id="7dedf-142">Conecte-se tooyour IoT hub executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7dedf-142">Connect tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="7dedf-143">Usar o iothub-explorer com métodos diretos</span><span class="sxs-lookup"><span data-stu-id="7dedf-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="7dedf-144">Invocar Olá `start` método hello dispositivo toosend mensagens tooyour IoT hub de aplicativos executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7dedf-144">Invoke hello `start` method in hello device app toosend messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="7dedf-145">Invocar Olá `stop` método hello dispositivo aplicativo toostop enviar mensagens tooyour IoT hub executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7dedf-145">Invoke hello `stop` method in hello device app toostop sending messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="7dedf-146">Usar o iothub-explorer com as propriedades desejadas do gêmeo</span><span class="sxs-lookup"><span data-stu-id="7dedf-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="7dedf-147">Definir um intervalo de propriedade desejados = 3000 executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7dedf-147">Set a desired property interval = 3000 by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="7dedf-148">Essa propriedade pode ser lida pelo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7dedf-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="7dedf-149">Usar o iothub-explorer com as propriedades relatadas do gêmeo</span><span class="sxs-lookup"><span data-stu-id="7dedf-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="7dedf-150">Obtenham hello relatadas propriedades de dispositivo de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7dedf-150">Get hello reported properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="7dedf-151">Uma das propriedades de saudação é $metadata. $lastUpdated que mostra Olá última vez em que o dispositivo envia ou recebe uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="7dedf-151">One of hello properties is $metadata.$lastUpdated which shows hello last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="7dedf-152">Usar o iothub-explorer com marcações do gêmeo</span><span class="sxs-lookup"><span data-stu-id="7dedf-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="7dedf-153">Exibir marcas hello e propriedades de dispositivo de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7dedf-153">Display hello tags and properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="7dedf-154">Adicionar uma função de campo = dispositivo toohello de temperatura e umidade executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7dedf-154">Add a field role = temperature&humidity toohello device by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="7dedf-155">Usar o iothub-explorer para enviar mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="7dedf-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="7dedf-156">Envie um dispositivo de toohello de mensagem "Hello World" executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7dedf-156">Send a "Hello World" message toohello device by running hello following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="7dedf-157">Consulte [usar o Gerenciador de Hub IOT toosend e receber mensagens entre o dispositivo e o IoT Hub](iot-hub-explorer-cloud-device-messaging.md) para um cenário real de usar esse comando.</span><span class="sxs-lookup"><span data-stu-id="7dedf-157">See [Use iothub-explorer toosend and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="7dedf-158">Usar o iothub-explorer com consultas de dispositivos gêmeos</span><span class="sxs-lookup"><span data-stu-id="7dedf-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="7dedf-159">Dispositivos com uma marca de função de consulta = 'temperatura e umidade' executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7dedf-159">Query devices with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="7dedf-160">Consultar todos os dispositivos, exceto aqueles com uma marca de função = 'temperatura e umidade' executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7dedf-160">Query all devices except those with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="7dedf-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7dedf-161">Next steps</span></span>

<span data-ttu-id="7dedf-162">Você aprendeu como toouse hub IOT-explorer com várias opções de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="7dedf-162">You've learned how toouse iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
