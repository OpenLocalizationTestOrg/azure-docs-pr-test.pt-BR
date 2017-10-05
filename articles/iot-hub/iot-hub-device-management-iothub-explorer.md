---
title: Gerenciamento de dispositivos IoT do Azure com o iothub-explorer | Microsoft Docs
description: "Use a ferramenta da CLI iothub-explorer para o gerenciamento de dispositivos Hub IoT do Azure, que contam com métodos Diretos e as opções de gerenciamento de propriedades desejadas do Gêmeo."
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
ms.openlocfilehash: 5b7a5057bdfb5920fbb5759bed1f5561cfa1d7e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="30635-104">Usar o iothub-explorer para o gerenciamento de dispositivos Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="30635-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="30635-106">O [iothub-explorer](https://github.com/azure/iothub-explorer) é uma ferramenta da CLI executada em um computador host para gerenciar identidades de dispositivo no Registro do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="30635-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer to manage device identities in your IoT hub registry.</span></span> <span data-ttu-id="30635-107">Ela é fornecida com opções de gerenciamento que podem ser usadas para executar várias tarefas.</span><span class="sxs-lookup"><span data-stu-id="30635-107">It comes with management options that you can use to perform various tasks.</span></span>

| <span data-ttu-id="30635-108">Opção de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="30635-108">Management option</span></span>          | <span data-ttu-id="30635-109">Tarefa</span><span class="sxs-lookup"><span data-stu-id="30635-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="30635-110">Métodos diretos</span><span class="sxs-lookup"><span data-stu-id="30635-110">Direct methods</span></span>             | <span data-ttu-id="30635-111">Faça com que um dispositivo comece ou pare de enviar mensagens ou seja reinicializado.</span><span class="sxs-lookup"><span data-stu-id="30635-111">Make a device act such as starting or stopping sending messages or rebooting the device.</span></span>                                        |
| <span data-ttu-id="30635-112">Propriedades desejadas do gêmeo</span><span class="sxs-lookup"><span data-stu-id="30635-112">Twin desired properties</span></span>    | <span data-ttu-id="30635-113">Coloque um dispositivo em alguns estados, como definir um LED como verde ou definir o intervalo de envio de telemetria como 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="30635-113">Put a device into certain states, such as setting an LED to green or setting the telemetry send interval to 30 minutes.</span></span>         |
| <span data-ttu-id="30635-114">Propriedades relatadas do gêmeo</span><span class="sxs-lookup"><span data-stu-id="30635-114">Twin reported properties</span></span>   | <span data-ttu-id="30635-115">Obtenha o estado relatado de um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="30635-115">Get the reported state of a device.</span></span> <span data-ttu-id="30635-116">Por exemplo, o dispositivo relata que o LED está piscando no momento.</span><span class="sxs-lookup"><span data-stu-id="30635-116">For example, the device reports the LED is blinking now.</span></span>                                    |
| <span data-ttu-id="30635-117">Marcações do gêmeo</span><span class="sxs-lookup"><span data-stu-id="30635-117">Twin tags</span></span>                  | <span data-ttu-id="30635-118">Armazene os metadados específicos do dispositivo na nuvem.</span><span class="sxs-lookup"><span data-stu-id="30635-118">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="30635-119">Por exemplo, o local de implantação de uma máquina de vendas.</span><span class="sxs-lookup"><span data-stu-id="30635-119">For example, the deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="30635-120">Mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="30635-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="30635-121">Envie notificações para um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="30635-121">Send notifications to a device.</span></span> <span data-ttu-id="30635-122">Por exemplo, “É muito provável que chova hoje.</span><span class="sxs-lookup"><span data-stu-id="30635-122">For example, "It is very likely to rain today.</span></span> <span data-ttu-id="30635-123">Não se esqueça de levar um guarda-chuva”.</span><span class="sxs-lookup"><span data-stu-id="30635-123">Don't forget to bring an umbrella."</span></span>              |
| <span data-ttu-id="30635-124">Consultas de dispositivo gêmeo</span><span class="sxs-lookup"><span data-stu-id="30635-124">Device twin queries</span></span>        | <span data-ttu-id="30635-125">Consulte todos os dispositivos gêmeos para recuperar aqueles com condições arbitrárias, como identificar os dispositivos que estão disponíveis para uso.</span><span class="sxs-lookup"><span data-stu-id="30635-125">Query all device twins to retrieve those with arbitrary conditions, such as identifying the devices that are available for use.</span></span> |

<span data-ttu-id="30635-126">Para obter explicações mais detalhadas sobre as diferenças e diretrizes sobre como usar essas opções, consulte [Diretrizes de comunicação do dispositivo para a nuvem](iot-hub-devguide-d2c-guidance.md) e [Diretrizes de comunicação da nuvem para o dispositivo](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="30635-126">For more detailed explanation on the differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="30635-127">Dispositivos gêmeos são documentos JSON que armazenam informações do estado do dispositivo (metadados, configurações e condições).</span><span class="sxs-lookup"><span data-stu-id="30635-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="30635-128">O Hub IoT persiste um dispositivo gêmeo para cada dispositivo que você conecta a ele.</span><span class="sxs-lookup"><span data-stu-id="30635-128">IoT Hub persists a device twin for each device that connects to it.</span></span> <span data-ttu-id="30635-129">Para obter mais informações sobre dispositivos gêmeos, consulte [Introdução aos dispositivos gêmeos](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="30635-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="30635-130">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="30635-130">What you learn</span></span>

<span data-ttu-id="30635-131">Você aprenderá a usar o iothub-explorer com várias opções de gerenciamento em seu computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="30635-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="30635-132">O que fazer</span><span class="sxs-lookup"><span data-stu-id="30635-132">What you do</span></span>

<span data-ttu-id="30635-133">Execute o iothub-explorer com várias opções de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="30635-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="30635-134">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="30635-134">What you need</span></span>

- <span data-ttu-id="30635-135">Tutorial [Configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) concluído que aborda os seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="30635-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="30635-136">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="30635-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="30635-137">Um hub IoT do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="30635-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="30635-138">O aplicativo cliente que envia mensagens para o hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="30635-138">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="30635-139">Verifique se o dispositivo está sendo executado com o aplicativo cliente durante este tutorial.</span><span class="sxs-lookup"><span data-stu-id="30635-139">Make sure your device is running with the client application during this tutorial.</span></span>
- <span data-ttu-id="30635-140">iothub-explorer, [Instalar iothub-explorer](https://github.com/azure/iothub-explorer) no computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="30635-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-to-your-iot-hub"></a><span data-ttu-id="30635-141">Conectar ao seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="30635-141">Connect to your IoT hub</span></span>

<span data-ttu-id="30635-142">Conecte-se ao seu Hub IoT executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="30635-142">Connect to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="30635-143">Usar o iothub-explorer com métodos diretos</span><span class="sxs-lookup"><span data-stu-id="30635-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="30635-144">Invoque o método `start` no aplicativo do dispositivo para enviar mensagens para o Hub IoT executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="30635-144">Invoke the `start` method in the device app to send messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="30635-145">Invoque o método `stop` no aplicativo do dispositivo para parar de enviar mensagens para o Hub IoT executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="30635-145">Invoke the `stop` method in the device app to stop sending messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="30635-146">Usar o iothub-explorer com as propriedades desejadas do gêmeo</span><span class="sxs-lookup"><span data-stu-id="30635-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="30635-147">Defina um intervalo de propriedade desejado = 3000 executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="30635-147">Set a desired property interval = 3000 by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="30635-148">Essa propriedade pode ser lida pelo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="30635-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="30635-149">Usar o iothub-explorer com as propriedades relatadas do gêmeo</span><span class="sxs-lookup"><span data-stu-id="30635-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="30635-150">Obtenha as propriedades relatadas do dispositivo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="30635-150">Get the reported properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="30635-151">Uma das propriedades é $metadata.$lastUpdated, que mostra a última vez que esse dispositivo enviou ou recebeu uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="30635-151">One of the properties is $metadata.$lastUpdated which shows the last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="30635-152">Usar o iothub-explorer com marcações do gêmeo</span><span class="sxs-lookup"><span data-stu-id="30635-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="30635-153">Exiba as marcações e as propriedades do dispositivo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="30635-153">Display the tags and properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="30635-154">Adicione uma função de campo = temperature&humidity ao dispositivo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="30635-154">Add a field role = temperature&humidity to the device by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="30635-155">Usar o iothub-explorer para enviar mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="30635-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="30635-156">Envie uma mensagem “Olá, mundo” para o dispositivo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="30635-156">Send a "Hello World" message to the device by running the following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="30635-157">Consulte [Usar o iothub-explorer para enviar e receber mensagens entre o dispositivo e o Hub IoT](iot-hub-explorer-cloud-device-messaging.md) para obter um cenário real do uso desse comando.</span><span class="sxs-lookup"><span data-stu-id="30635-157">See [Use iothub-explorer to send and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="30635-158">Usar o iothub-explorer com consultas de dispositivos gêmeos</span><span class="sxs-lookup"><span data-stu-id="30635-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="30635-159">Consulte dispositivos com uma marcação de função = 'temperature&humidity' executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="30635-159">Query devices with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="30635-160">Consulte todos os dispositivos, exceto aqueles com uma marcação de função = 'temperature&humidity', executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="30635-160">Query all devices except those with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="30635-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="30635-161">Next steps</span></span>

<span data-ttu-id="30635-162">Você aprendeu a usar o iothub-explorer com várias opções de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="30635-162">You've learned how to use iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
