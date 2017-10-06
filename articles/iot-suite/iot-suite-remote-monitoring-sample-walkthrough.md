---
title: "passo a passo de solução de monitoramento pré-configurado aaaRemote | Microsoft Docs"
description: "Uma descrição do hello Azure IoT pré-configurado solução de monitoramento remoto e sua arquitetura."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a><span data-ttu-id="5448d-103">Passo a passo da solução pré-configurada de monitoramento remoto</span><span class="sxs-lookup"><span data-stu-id="5448d-103">Remote monitoring preconfigured solution walkthrough</span></span>

<span data-ttu-id="5448d-104">Olá monitoramento remoto do IoT Suite [pré-configurado solução] [ lnk-preconfigured-solutions] é uma implementação de uma ponta a ponta solução para várias máquinas em execução em locais remotos de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="5448d-104">hello IoT Suite remote monitoring [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end monitoring solution for multiple machines running in remote locations.</span></span> <span data-ttu-id="5448d-105">Olá combina serviços do Azure chave tooprovide uma implementação genérica do cenário de negócios hello.</span><span class="sxs-lookup"><span data-stu-id="5448d-105">hello solution combines key Azure services tooprovide a generic implementation of hello business scenario.</span></span> <span data-ttu-id="5448d-106">Você pode usar a solução hello como ponto de partida para sua própria implementação e [personalizar] [ lnk-customize] -toomeet seus próprios requisitos comerciais específicos.</span><span class="sxs-lookup"><span data-stu-id="5448d-106">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="5448d-107">Este artigo o orienta por meio de alguns dos elementos principais de saudação do hello tooenable de solução de monitoramento remoto toounderstand como ele funciona.</span><span class="sxs-lookup"><span data-stu-id="5448d-107">This article walks you through some of hello key elements of hello remote monitoring solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="5448d-108">Esse conhecimento ajuda a:</span><span class="sxs-lookup"><span data-stu-id="5448d-108">This knowledge helps you to:</span></span>

* <span data-ttu-id="5448d-109">Solucione problemas na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="5448d-109">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="5448d-110">Planejar como toocustomize toohello solução toomeet necessidades específicas.</span><span class="sxs-lookup"><span data-stu-id="5448d-110">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span> 
* <span data-ttu-id="5448d-111">Criar sua própria solução IoT que usa os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="5448d-111">Design your own IoT solution that uses Azure services.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="5448d-112">Arquitetura lógica</span><span class="sxs-lookup"><span data-stu-id="5448d-112">Logical architecture</span></span>

<span data-ttu-id="5448d-113">Olá diagrama a seguir descreve os componentes lógicos de saudação da solução Olá pré-configurados:</span><span class="sxs-lookup"><span data-stu-id="5448d-113">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Arquitetura lógica](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a><span data-ttu-id="5448d-115">Dispositivos simulados</span><span class="sxs-lookup"><span data-stu-id="5448d-115">Simulated devices</span></span>

<span data-ttu-id="5448d-116">Solução Olá pré-configurado, dispositivo simulado Olá representa um dispositivo de resfriamento (como uma construção ar condicionado ou unidade de manuseio de ar de recurso).</span><span class="sxs-lookup"><span data-stu-id="5448d-116">In hello preconfigured solution, hello simulated device represents a cooling device (such as a building air conditioner or facility air handling unit).</span></span> <span data-ttu-id="5448d-117">Quando você implanta a solução Olá pré-configurados, você provisionar automaticamente quatro dispositivos simulados que são executados em um [Azure WebJob][lnk-webjobs].</span><span class="sxs-lookup"><span data-stu-id="5448d-117">When you deploy hello preconfigured solution, you also automatically provision four simulated devices that run in an [Azure WebJob][lnk-webjobs].</span></span> <span data-ttu-id="5448d-118">dispositivos de saudação simulada tornam mais fácil para você tooexplore Olá comportamento de solução de saudação sem Olá necessidade toodeploy quaisquer dispositivos físicos.</span><span class="sxs-lookup"><span data-stu-id="5448d-118">hello simulated devices make it easy for you tooexplore hello behavior of hello solution without hello need toodeploy any physical devices.</span></span> <span data-ttu-id="5448d-119">toodeploy um dispositivo físico real, consulte Olá [conectar sua solução pré-configurada de monitoramento remoto de toohello dispositivo] [ lnk-connect-rm] tutorial.</span><span class="sxs-lookup"><span data-stu-id="5448d-119">toodeploy a real physical device, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

### <a name="device-to-cloud-messages"></a><span data-ttu-id="5448d-120">Mensagens do dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="5448d-120">Device-to-cloud messages</span></span>

<span data-ttu-id="5448d-121">Cada dispositivo simulado pode enviar Olá tooIoT tipos de mensagem Hub a seguir:</span><span class="sxs-lookup"><span data-stu-id="5448d-121">Each simulated device can send hello following message types tooIoT Hub:</span></span>

| <span data-ttu-id="5448d-122">Mensagem</span><span class="sxs-lookup"><span data-stu-id="5448d-122">Message</span></span> | <span data-ttu-id="5448d-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="5448d-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5448d-124">Inicialização</span><span class="sxs-lookup"><span data-stu-id="5448d-124">Startup</span></span> |<span data-ttu-id="5448d-125">Quando o dispositivo Olá é iniciado, ele envia um **informações do dispositivo** mensagem que contém informações sobre o próprio toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="5448d-125">When hello device starts, it sends a **device-info** message containing information about itself toohello back end.</span></span> <span data-ttu-id="5448d-126">Esses dados incluem a id do dispositivo hello e uma lista de comandos de saudação e métodos Olá dispositivo suporta.</span><span class="sxs-lookup"><span data-stu-id="5448d-126">This data includes hello device id and a list of hello commands and methods hello device supports.</span></span> |
| <span data-ttu-id="5448d-127">Presença</span><span class="sxs-lookup"><span data-stu-id="5448d-127">Presence</span></span> |<span data-ttu-id="5448d-128">Um dispositivo envia periodicamente uma **presença** tooreport da mensagem se o dispositivo Olá pode detectar a presença de saudação de um sensor.</span><span class="sxs-lookup"><span data-stu-id="5448d-128">A device periodically sends a **presence** message tooreport whether hello device can sense hello presence of a sensor.</span></span> |
| <span data-ttu-id="5448d-129">Telemetria</span><span class="sxs-lookup"><span data-stu-id="5448d-129">Telemetry</span></span> |<span data-ttu-id="5448d-130">Um dispositivo envia periodicamente uma **telemetria** mensagem que informa simulados valores de temperatura hello e umidade coletados de dispositivo de saudação do simulados sensores.</span><span class="sxs-lookup"><span data-stu-id="5448d-130">A device periodically sends a **telemetry** message that reports simulated values for hello temperature and humidity collected from hello device's simulated sensors.</span></span> |

> [!NOTE]
> <span data-ttu-id="5448d-131">solução de saudação armazena a lista de saudação de comandos com suporte pelo dispositivo de saudação em um banco de dados do banco de dados do Cosmos e não em duas de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5448d-131">hello solution stores hello list of commands supported by hello device in a Cosmos DB database and not in hello device twin.</span></span>

### <a name="properties-and-device-twins"></a><span data-ttu-id="5448d-132">Propriedades e dispositivos gêmeos</span><span class="sxs-lookup"><span data-stu-id="5448d-132">Properties and device twins</span></span>

<span data-ttu-id="5448d-133">dispositivos simulados Hello enviam Olá toohello de propriedades de dispositivo a seguir [duas] [ lnk-device-twins] no hub IoT de saudação como *relatado propriedades*.</span><span class="sxs-lookup"><span data-stu-id="5448d-133">hello simulated devices send hello following device properties toohello [twin][lnk-device-twins] in hello IoT hub as *reported properties*.</span></span> <span data-ttu-id="5448d-134">envios de dispositivo Hello relatado propriedades na inicialização e na resposta tooa **alterar estado do dispositivo** método ou comando.</span><span class="sxs-lookup"><span data-stu-id="5448d-134">hello device sends reported properties at startup and in response tooa **Change Device State** command or method.</span></span>

| <span data-ttu-id="5448d-135">Propriedade</span><span class="sxs-lookup"><span data-stu-id="5448d-135">Property</span></span> | <span data-ttu-id="5448d-136">Finalidade</span><span class="sxs-lookup"><span data-stu-id="5448d-136">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="5448d-137">Config.TelemetryInterval</span><span class="sxs-lookup"><span data-stu-id="5448d-137">Config.TelemetryInterval</span></span> | <span data-ttu-id="5448d-138">Dispositivo de saudação de frequência (segundos) envia a Telemetria</span><span class="sxs-lookup"><span data-stu-id="5448d-138">Frequency (seconds) hello device sends telemetry</span></span> |
| <span data-ttu-id="5448d-139">Config.TemperatureMeanValue</span><span class="sxs-lookup"><span data-stu-id="5448d-139">Config.TemperatureMeanValue</span></span> | <span data-ttu-id="5448d-140">Especifica o valor médio de saudação de telemetria de temperatura Olá simulado</span><span class="sxs-lookup"><span data-stu-id="5448d-140">Specifies hello mean value for hello simulated temperature telemetry</span></span> |
| <span data-ttu-id="5448d-141">Device.DeviceID</span><span class="sxs-lookup"><span data-stu-id="5448d-141">Device.DeviceID</span></span> |<span data-ttu-id="5448d-142">ID que é fornecido ou atribuído quando um dispositivo é criado na solução Olá</span><span class="sxs-lookup"><span data-stu-id="5448d-142">Id that is either provided or assigned when a device is created in hello solution</span></span> |
| <span data-ttu-id="5448d-143">Device.DeviceState</span><span class="sxs-lookup"><span data-stu-id="5448d-143">Device.DeviceState</span></span> | <span data-ttu-id="5448d-144">Estado relatado pelo dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="5448d-144">State reported by hello device</span></span> |
| <span data-ttu-id="5448d-145">Device.CreatedTime</span><span class="sxs-lookup"><span data-stu-id="5448d-145">Device.CreatedTime</span></span> |<span data-ttu-id="5448d-146">Dispositivo de saudação do tempo foi criado na solução de saudação</span><span class="sxs-lookup"><span data-stu-id="5448d-146">Time hello device was created in hello solution</span></span> |
| <span data-ttu-id="5448d-147">Device.StartupTime</span><span class="sxs-lookup"><span data-stu-id="5448d-147">Device.StartupTime</span></span> |<span data-ttu-id="5448d-148">Dispositivo de saudação do tempo foi iniciado</span><span class="sxs-lookup"><span data-stu-id="5448d-148">Time hello device was started</span></span> |
| <span data-ttu-id="5448d-149">Device.LastDesiredPropertyChange</span><span class="sxs-lookup"><span data-stu-id="5448d-149">Device.LastDesiredPropertyChange</span></span> |<span data-ttu-id="5448d-150">número de versão de saudação da propriedade desejada do último Olá alterar</span><span class="sxs-lookup"><span data-stu-id="5448d-150">hello version number of hello last desired property change</span></span> |
| <span data-ttu-id="5448d-151">Device.Location.Latitude</span><span class="sxs-lookup"><span data-stu-id="5448d-151">Device.Location.Latitude</span></span> |<span data-ttu-id="5448d-152">Local da Latitude do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="5448d-152">Latitude location of hello device</span></span> |
| <span data-ttu-id="5448d-153">Device.Location.Longitude</span><span class="sxs-lookup"><span data-stu-id="5448d-153">Device.Location.Longitude</span></span> |<span data-ttu-id="5448d-154">Local de longitude do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="5448d-154">Longitude location of hello device</span></span> |
| <span data-ttu-id="5448d-155">System.Manufacturer</span><span class="sxs-lookup"><span data-stu-id="5448d-155">System.Manufacturer</span></span> |<span data-ttu-id="5448d-156">Fabricante do dispositivo</span><span class="sxs-lookup"><span data-stu-id="5448d-156">Device manufacturer</span></span> |
| <span data-ttu-id="5448d-157">System.ModelNumber</span><span class="sxs-lookup"><span data-stu-id="5448d-157">System.ModelNumber</span></span> |<span data-ttu-id="5448d-158">Número do modelo de dispositivo de saudação</span><span class="sxs-lookup"><span data-stu-id="5448d-158">Model number of hello device</span></span> |
| <span data-ttu-id="5448d-159">System.SerialNumber</span><span class="sxs-lookup"><span data-stu-id="5448d-159">System.SerialNumber</span></span> |<span data-ttu-id="5448d-160">Número de série do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="5448d-160">Serial number of hello device</span></span> |
| <span data-ttu-id="5448d-161">System.FirmwareVersion</span><span class="sxs-lookup"><span data-stu-id="5448d-161">System.FirmwareVersion</span></span> |<span data-ttu-id="5448d-162">Versão atual do firmware no dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="5448d-162">Current version of firmware on hello device</span></span> |
| <span data-ttu-id="5448d-163">System.Platform</span><span class="sxs-lookup"><span data-stu-id="5448d-163">System.Platform</span></span> |<span data-ttu-id="5448d-164">Arquitetura da plataforma de dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="5448d-164">Platform architecture of hello device</span></span> |
| <span data-ttu-id="5448d-165">System.Processor</span><span class="sxs-lookup"><span data-stu-id="5448d-165">System.Processor</span></span> |<span data-ttu-id="5448d-166">Dispositivo de saudação em execução do processador</span><span class="sxs-lookup"><span data-stu-id="5448d-166">Processor running hello device</span></span> |
| <span data-ttu-id="5448d-167">System.InstalledRAM</span><span class="sxs-lookup"><span data-stu-id="5448d-167">System.InstalledRAM</span></span> |<span data-ttu-id="5448d-168">Quantidade de RAM instalada no dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="5448d-168">Amount of RAM installed on hello device</span></span> |

<span data-ttu-id="5448d-169">simulador Olá propaga essas propriedades em dispositivos simuladas com valores de exemplo.</span><span class="sxs-lookup"><span data-stu-id="5448d-169">hello simulator seeds these properties in simulated devices with sample values.</span></span> <span data-ttu-id="5448d-170">Cada vez simulador Olá inicializa um dispositivo simulado, dispositivo Olá reporta Olá metadados predefinidos tooIoT Hub como propriedades relatadas.</span><span class="sxs-lookup"><span data-stu-id="5448d-170">Each time hello simulator initializes a simulated device, hello device reports hello pre-defined metadata tooIoT Hub as reported properties.</span></span> <span data-ttu-id="5448d-171">Propriedades relatadas só podem ser atualizadas por dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="5448d-171">Reported properties can only be updated by hello device.</span></span> <span data-ttu-id="5448d-172">toochange uma propriedade relatada, definir uma propriedade desejada no portal de solução.</span><span class="sxs-lookup"><span data-stu-id="5448d-172">toochange a reported property, you set a desired property in solution portal.</span></span> <span data-ttu-id="5448d-173">É responsabilidade de saudação do dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="5448d-173">It is hello responsibility of hello device to:</span></span>

1. <span data-ttu-id="5448d-174">Recupere periodicamente as propriedades desejadas de hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="5448d-174">Periodically retrieve desired properties from hello IoT hub.</span></span>
2. <span data-ttu-id="5448d-175">Atualize sua configuração com o valor da propriedade Olá desejado.</span><span class="sxs-lookup"><span data-stu-id="5448d-175">Update its configuration with hello desired property value.</span></span>
3. <span data-ttu-id="5448d-176">Envie novo hub de toohello back valor hello como uma propriedade relatada.</span><span class="sxs-lookup"><span data-stu-id="5448d-176">Send hello new value back toohello hub as a reported property.</span></span>

<span data-ttu-id="5448d-177">No painel de solução hello, você pode usar *propriedades desejadas* tooset propriedades em um dispositivo usando Olá [duas dispositivo][lnk-device-twins].</span><span class="sxs-lookup"><span data-stu-id="5448d-177">From hello solution dashboard, you can use *desired properties* tooset properties on a device by using hello [device twin][lnk-device-twins].</span></span> <span data-ttu-id="5448d-178">Normalmente, um dispositivo lê um valor de propriedade desejados do hello hub tooupdate que seu estado interno e Olá relatório alterar novamente como uma propriedade relatada.</span><span class="sxs-lookup"><span data-stu-id="5448d-178">Typically, a device reads a desired property value from hello hub tooupdate its internal state and report hello change back as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="5448d-179">Olá dispositivo simulado código só usa Olá **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** Olá de tooupdate propriedades desejadas relatado propriedades enviadas de volta tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5448d-179">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="5448d-180">Todas as outras solicitações de alteração de propriedade desejados são ignoradas no dispositivo simulado hello.</span><span class="sxs-lookup"><span data-stu-id="5448d-180">All other desired property change requests are ignored in hello simulated device.</span></span>

### <a name="methods"></a><span data-ttu-id="5448d-181">Métodos</span><span class="sxs-lookup"><span data-stu-id="5448d-181">Methods</span></span>

<span data-ttu-id="5448d-182">Olá simulados dispositivos podem manipular Olá métodos a seguir ([direto métodos][lnk-direct-methods]) chamado a partir do portal de solução de saudação por meio de hub IoT de saudação:</span><span class="sxs-lookup"><span data-stu-id="5448d-182">hello simulated devices can handle hello following methods ([direct methods][lnk-direct-methods]) invoked from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="5448d-183">Método</span><span class="sxs-lookup"><span data-stu-id="5448d-183">Method</span></span> | <span data-ttu-id="5448d-184">Descrição</span><span class="sxs-lookup"><span data-stu-id="5448d-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5448d-185">InitiateFirmwareUpdate</span><span class="sxs-lookup"><span data-stu-id="5448d-185">InitiateFirmwareUpdate</span></span> |<span data-ttu-id="5448d-186">Instrui o hello dispositivo tooperform uma atualização de firmware</span><span class="sxs-lookup"><span data-stu-id="5448d-186">Instructs hello device tooperform a firmware update</span></span> |
| <span data-ttu-id="5448d-187">Reboot</span><span class="sxs-lookup"><span data-stu-id="5448d-187">Reboot</span></span> |<span data-ttu-id="5448d-188">Instrui o hello dispositivo tooreboot</span><span class="sxs-lookup"><span data-stu-id="5448d-188">Instructs hello device tooreboot</span></span> |
| <span data-ttu-id="5448d-189">FactoryReset</span><span class="sxs-lookup"><span data-stu-id="5448d-189">FactoryReset</span></span> |<span data-ttu-id="5448d-190">Instrui o hello dispositivo tooperform redefinição de fábrica</span><span class="sxs-lookup"><span data-stu-id="5448d-190">Instructs hello device tooperform a factory reset</span></span> |

<span data-ttu-id="5448d-191">Alguns métodos usam tooreport propriedades relatado em andamento.</span><span class="sxs-lookup"><span data-stu-id="5448d-191">Some methods use reported properties tooreport on progress.</span></span> <span data-ttu-id="5448d-192">Por exemplo, Olá **InitiateFirmwareUpdate** método simula a atualização de saudação em execução assíncrona no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5448d-192">For example, hello **InitiateFirmwareUpdate** method simulates running hello update asynchronously on hello device.</span></span> <span data-ttu-id="5448d-193">método Hello retorna imediatamente no dispositivo Olá, interromper a tarefa assíncrona Olá fazer atualizações de status toosend toohello solução dashboard usando relatado propriedades.</span><span class="sxs-lookup"><span data-stu-id="5448d-193">hello method returns immediately on hello device, while hello asynchronous task continues toosend status updates back toohello solution dashboard using reported properties.</span></span>

### <a name="commands"></a><span data-ttu-id="5448d-194">Comandos</span><span class="sxs-lookup"><span data-stu-id="5448d-194">Commands</span></span>

<span data-ttu-id="5448d-195">dispositivos Olá simulado podem manipular Olá comandos (mensagens de nuvem para dispositivo) enviados do portal de solução de saudação por meio de hub IoT de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="5448d-195">hello simulated devices can handle hello following commands (cloud-to-device messages) sent from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="5448d-196">Command</span><span class="sxs-lookup"><span data-stu-id="5448d-196">Command</span></span> | <span data-ttu-id="5448d-197">Descrição</span><span class="sxs-lookup"><span data-stu-id="5448d-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5448d-198">PingDevice</span><span class="sxs-lookup"><span data-stu-id="5448d-198">PingDevice</span></span> |<span data-ttu-id="5448d-199">Envia um *ping* toohello dispositivo toocheck está ativo</span><span class="sxs-lookup"><span data-stu-id="5448d-199">Sends a *ping* toohello device toocheck it is alive</span></span> |
| <span data-ttu-id="5448d-200">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="5448d-200">StartTelemetry</span></span> |<span data-ttu-id="5448d-201">Inicia Olá dispositivo enviar Telemetria</span><span class="sxs-lookup"><span data-stu-id="5448d-201">Starts hello device sending telemetry</span></span> |
| <span data-ttu-id="5448d-202">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="5448d-202">StopTelemetry</span></span> |<span data-ttu-id="5448d-203">Dispositivo de saudação para de enviar Telemetria</span><span class="sxs-lookup"><span data-stu-id="5448d-203">Stops hello device from sending telemetry</span></span> |
| <span data-ttu-id="5448d-204">ChangeSetPointTemp</span><span class="sxs-lookup"><span data-stu-id="5448d-204">ChangeSetPointTemp</span></span> |<span data-ttu-id="5448d-205">Altera o valor de ponto de conjunto de saudação em torno da qual Olá dados aleatórios são gerados</span><span class="sxs-lookup"><span data-stu-id="5448d-205">Changes hello set point value around which hello random data is generated</span></span> |
| <span data-ttu-id="5448d-206">DiagnosticTelemetry</span><span class="sxs-lookup"><span data-stu-id="5448d-206">DiagnosticTelemetry</span></span> |<span data-ttu-id="5448d-207">Gatilhos Olá simulador de dispositivo toosend um valor de telemetria adicionais (externalTemp)</span><span class="sxs-lookup"><span data-stu-id="5448d-207">Triggers hello device simulator toosend an additional telemetry value (externalTemp)</span></span> |
| <span data-ttu-id="5448d-208">ChangeDeviceState</span><span class="sxs-lookup"><span data-stu-id="5448d-208">ChangeDeviceState</span></span> |<span data-ttu-id="5448d-209">Altera uma propriedade estendida estado dispositivo hello e envia mensagens de informações de dispositivo Olá Olá dispositivo</span><span class="sxs-lookup"><span data-stu-id="5448d-209">Changes an extended state property for hello device and sends hello device info message from hello device</span></span> |

> [!NOTE]
> <span data-ttu-id="5448d-210">Para obter uma comparação desses comandos (mensagens da nuvem para o dispositivo) e métodos (métodos diretos), consulte [Orientação para comunicações entre o dispositivo e a nuvem][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="5448d-210">For a comparison of these commands (cloud-to-device messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

## <a name="iot-hub"></a><span data-ttu-id="5448d-211">Hub IoT</span><span class="sxs-lookup"><span data-stu-id="5448d-211">IoT Hub</span></span>

<span data-ttu-id="5448d-212">Olá [hub IoT] [ lnk-iothub] consome dados enviados de dispositivos de saudação em nuvem hello e torna disponível toohello trabalhos de análise de fluxo do Azure (ASA).</span><span class="sxs-lookup"><span data-stu-id="5448d-212">hello [IoT hub][lnk-iothub] ingests data sent from hello devices into hello cloud and makes it available toohello Azure Stream Analytics (ASA) jobs.</span></span> <span data-ttu-id="5448d-213">Cada trabalho ASA fluxo usa um IoT Hub consumidor grupo tooread Olá fluxo separado de mensagens de seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="5448d-213">Each stream ASA job uses a separate IoT Hub consumer group tooread hello stream of messages from your devices.</span></span>

<span data-ttu-id="5448d-214">Olá hub IoT na solução Olá também:</span><span class="sxs-lookup"><span data-stu-id="5448d-214">hello IoT hub in hello solution also:</span></span>

- <span data-ttu-id="5448d-215">Mantém um registro de identidade que armazena ids de saudação e chaves de autenticação de todos os dispositivos de saudação permitidos tooconnect toohello portal.</span><span class="sxs-lookup"><span data-stu-id="5448d-215">Maintains an identity registry that stores hello ids and authentication keys of all hello devices permitted tooconnect toohello portal.</span></span> <span data-ttu-id="5448d-216">Você pode habilitar e desabilitar dispositivos por meio do registro de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="5448d-216">You can enable and disable devices through hello identity registry.</span></span>
- <span data-ttu-id="5448d-217">Envia comandos tooyour dispositivos em nome do portal de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="5448d-217">Sends commands tooyour devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="5448d-218">Chama os métodos em seus dispositivos em nome do portal de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="5448d-218">Invokes methods on your devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="5448d-219">Mantém dispositivos gêmeos para todos os dispositivos registrados.</span><span class="sxs-lookup"><span data-stu-id="5448d-219">Maintains device twins for all registered devices.</span></span> <span data-ttu-id="5448d-220">Duas um dispositivo armazena valores de propriedade Olá relatados por um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5448d-220">A device twin stores hello property values reported by a device.</span></span> <span data-ttu-id="5448d-221">Duas um dispositivo também armazena as propriedades desejadas, definidas no portal de solução de Olá para Olá dispositivo tooretrieve ao próximo se conectar.</span><span class="sxs-lookup"><span data-stu-id="5448d-221">A device twin also stores desired properties, set in hello solution portal, for hello device tooretrieve when it next connects.</span></span>
- <span data-ttu-id="5448d-222">Agendamentos de trabalhos tooset propriedades para vários dispositivos ou chamar métodos em vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="5448d-222">Schedules jobs tooset properties for multiple devices or invoke methods on multiple devices.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="5448d-223">Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="5448d-223">Azure Stream Analytics</span></span>

<span data-ttu-id="5448d-224">Na solução de monitoramento remoto de saudação [Azure Stream Analytics] [ lnk-asa] (ASA) envia mensagens de dispositivo recebidas pelos componentes de saudação IoT hub tooother back-end para processamento ou armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5448d-224">In hello remote monitoring solution, [Azure Stream Analytics][lnk-asa] (ASA) dispatches device messages received by hello IoT hub tooother back-end components for processing or storage.</span></span> <span data-ttu-id="5448d-225">Trabalhos ASA diferentes executam funções específicas com base no conteúdo de saudação das mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="5448d-225">Different ASA jobs perform specific functions based on hello content of hello messages.</span></span>

<span data-ttu-id="5448d-226">**Tarefa 1: Informações sobre o dispositivo** filtra as mensagens de informações de dispositivo de fluxo de mensagem de entrada hello e envia o ponto de extremidade do tooan Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="5448d-226">**Job 1: Device Info** filters device information messages from hello incoming message stream and sends them tooan Event Hub endpoint.</span></span> <span data-ttu-id="5448d-227">Um dispositivo envia mensagens de informações de dispositivo durante a inicialização e na resposta tooa **SendDeviceInfo** comando.</span><span class="sxs-lookup"><span data-stu-id="5448d-227">A device sends device information messages at startup and in response tooa **SendDeviceInfo** command.</span></span> <span data-ttu-id="5448d-228">Esta tarefa usa Olá tooidentify de definição de consulta a seguir **informações do dispositivo** mensagens:</span><span class="sxs-lookup"><span data-stu-id="5448d-228">This job uses hello following query definition tooidentify **device-info** messages:</span></span>

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

<span data-ttu-id="5448d-229">Esse trabalho envia seu Hub de eventos de tooan de saída para processamento adicional.</span><span class="sxs-lookup"><span data-stu-id="5448d-229">This job sends its output tooan Event Hub for further processing.</span></span>

<span data-ttu-id="5448d-230">**Trabalho 2: as Regras** avaliam os valores de telemetria da temperatura e da umidade de entrada em relação aos limites de cada dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5448d-230">**Job 2: Rules** evaluates incoming temperature and humidity telemetry values against per-device thresholds.</span></span> <span data-ttu-id="5448d-231">Valores de limite são definidos no editor de regras de saudação disponível no portal de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="5448d-231">Threshold values are set in hello rules editor available in hello solution portal.</span></span> <span data-ttu-id="5448d-232">Cada par de dispositivo/valor é armazenado por carimbo de data/hora em um blob que o Stream Analytics lê como **Dados de Referência**.</span><span class="sxs-lookup"><span data-stu-id="5448d-232">Each device/value pair is stored by timestamp in a blob which Stream Analytics reads in as **Reference Data**.</span></span> <span data-ttu-id="5448d-233">trabalho de saudação compara qualquer valor não vazio com limite de conjunto de saudação para dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="5448d-233">hello job compares any non-empty value against hello set threshold for hello device.</span></span> <span data-ttu-id="5448d-234">Se ele exceder Olá ' >' condição, a saída do trabalho de saudação um **alarme** evento que indica que esse limite Olá for excedido e fornece dispositivo hello, valor e valores de carimbo de hora.</span><span class="sxs-lookup"><span data-stu-id="5448d-234">If it exceeds hello '>' condition, hello job outputs an **alarm** event that indicates that hello threshold is exceeded and provides hello device, value, and timestamp values.</span></span> <span data-ttu-id="5448d-235">Esta tarefa usa Olá mensagens telemetria de tooidentify de definição de consulta que devem disparar um alarme a seguir:</span><span class="sxs-lookup"><span data-stu-id="5448d-235">This job uses hello following query definition tooidentify telemetry messages that should trigger an alarm:</span></span>

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

<span data-ttu-id="5448d-236">Olá trabalho envia seu Hub de eventos de tooan de saída para processamento adicional e evita que os detalhes de cada armazenamento de alerta tooblob onde portal de solução Olá pode ler as informações de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="5448d-236">hello job sends its output tooan Event Hub for further processing and saves details of each alert tooblob storage from where hello solution portal can read hello alert information.</span></span>

<span data-ttu-id="5448d-237">**Tarefa 3: Telemetria** opera em fluxo telemetria dispositivo de saudação entrada de duas maneiras.</span><span class="sxs-lookup"><span data-stu-id="5448d-237">**Job 3: Telemetry** operates on hello incoming device telemetry stream in two ways.</span></span> <span data-ttu-id="5448d-238">Olá primeiro envia todas as mensagens de telemetria Olá dispositivos toopersistent do armazenamento de blob para armazenamento de longo prazo.</span><span class="sxs-lookup"><span data-stu-id="5448d-238">hello first sends all telemetry messages from hello devices toopersistent blob storage for long-term storage.</span></span> <span data-ttu-id="5448d-239">Olá segundo calcula umidade média, mínima e máxima de valores em uma janela deslizante de cinco minutos e envia esse armazenamento tooblob de dados.</span><span class="sxs-lookup"><span data-stu-id="5448d-239">hello second computes average, minimum, and maximum humidity values over a five-minute sliding window and sends this data tooblob storage.</span></span> <span data-ttu-id="5448d-240">portal de solução Olá lê dados de telemetria de saudação de gráficos de saudação de toopopulate de armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="5448d-240">hello solution portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="5448d-241">Esta tarefa usa Olá definição de consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="5448d-241">This job uses hello following query definition:</span></span>

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a><span data-ttu-id="5448d-242">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="5448d-242">Event Hubs</span></span>

<span data-ttu-id="5448d-243">Olá **informações do dispositivo** e **regras** trabalhos ASA saída seu dados tooEvent Hubs tooreliably forward em toohello **processador de eventos** em execução no hello WebJob.</span><span class="sxs-lookup"><span data-stu-id="5448d-243">hello **device info** and **rules** ASA jobs output their data tooEvent Hubs tooreliably forward on toohello **Event Processor** running in hello WebJob.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="5448d-244">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="5448d-244">Azure storage</span></span>

<span data-ttu-id="5448d-245">solução de saudação usa toopersist de armazenamento de BLOBs do Azure todos os dados de telemetria bruto e resumidos Olá dos dispositivos de saudação na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="5448d-245">hello solution uses Azure blob storage toopersist all hello raw and summarized telemetry data from hello devices in hello solution.</span></span> <span data-ttu-id="5448d-246">portal de saudação lê dados de telemetria de saudação de gráficos de saudação de toopopulate de armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="5448d-246">hello portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="5448d-247">toodisplay alertas, portal de solução de saudação lê dados saudação do armazenamento de blob que registra quando Olá de valores excedidos telemetria configurado valores de limite.</span><span class="sxs-lookup"><span data-stu-id="5448d-247">toodisplay alerts, hello solution portal reads hello data from blob storage that records when telemetry values exceeded hello configured threshold values.</span></span> <span data-ttu-id="5448d-248">solução de saudação também usa valores de limite de saudação do blob storage toorecord definido no portal de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="5448d-248">hello solution also uses blob storage toorecord hello threshold values you set in hello solution portal.</span></span>

## <a name="webjobs"></a><span data-ttu-id="5448d-249">Trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="5448d-249">WebJobs</span></span>

<span data-ttu-id="5448d-250">Além disso toohosting simuladores de dispositivo hello, Olá WebJobs na solução Olá também Olá host **processador de eventos** em execução em um trabalho Web do Azure que manipula as respostas de comando.</span><span class="sxs-lookup"><span data-stu-id="5448d-250">In addition toohosting hello device simulators, hello WebJobs in hello solution also host hello **Event Processor** running in an Azure WebJob that handles command responses.</span></span> <span data-ttu-id="5448d-251">Ele usa o comando resposta mensagens tooupdate Olá comando histórico de dispositivo (armazenado no banco de dados de banco de dados do Cosmos Olá).</span><span class="sxs-lookup"><span data-stu-id="5448d-251">It uses command response messages tooupdate hello device command history (stored in hello Cosmos DB database).</span></span>

## <a name="cosmos-db"></a><span data-ttu-id="5448d-252">Banco de Dados Cosmos</span><span class="sxs-lookup"><span data-stu-id="5448d-252">Cosmos DB</span></span>

<span data-ttu-id="5448d-253">solução de saudação usa um banco de dados do Cosmos banco de dados toostore saber Olá dispositivos conectados toohello solução.</span><span class="sxs-lookup"><span data-stu-id="5448d-253">hello solution uses a Cosmos DB database toostore information about hello devices connected toohello solution.</span></span> <span data-ttu-id="5448d-254">Essas informações incluem o histórico de saudação de comandos enviados toodevices do portal de solução hello e métodos invocados a partir do portal de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="5448d-254">This information includes hello history of commands sent toodevices from hello solution portal and of methods invoked from hello solution portal.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="5448d-255">Portal de solução</span><span class="sxs-lookup"><span data-stu-id="5448d-255">Solution portal</span></span>

<span data-ttu-id="5448d-256">portal de solução de saudação é um aplicativo web implantado como parte da solução Olá pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="5448d-256">hello solution portal is a web app deployed as part of hello preconfigured solution.</span></span> <span data-ttu-id="5448d-257">páginas de chave Olá no portal de solução de saudação são painel hello e lista de dispositivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="5448d-257">hello key pages in hello solution portal are hello dashboard and hello device list.</span></span>

### <a name="dashboard"></a><span data-ttu-id="5448d-258">Painel</span><span class="sxs-lookup"><span data-stu-id="5448d-258">Dashboard</span></span>

<span data-ttu-id="5448d-259">Esta página no aplicativo web de saudação usa os controles de javascript do PowerBI (consulte [repositório PowerBI-visuals](https://www.github.com/Microsoft/PowerBI-visuals)) dados de telemetria Olá toovisualize de dispositivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="5448d-259">This page in hello web app uses PowerBI javascript controls (See [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) toovisualize hello telemetry data from hello devices.</span></span> <span data-ttu-id="5448d-260">solução de saudação usa Olá ASA telemetria trabalho toowrite Olá telemetria tooblob armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="5448d-260">hello solution uses hello ASA telemetry job toowrite hello telemetry data tooblob storage.</span></span>

### <a name="device-list"></a><span data-ttu-id="5448d-261">Lista de dispositivos</span><span class="sxs-lookup"><span data-stu-id="5448d-261">Device list</span></span>

<span data-ttu-id="5448d-262">Nessa página no portal de solução hello, você pode:</span><span class="sxs-lookup"><span data-stu-id="5448d-262">From this page in hello solution portal you can:</span></span>

* <span data-ttu-id="5448d-263">Provisione um novo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5448d-263">Provision a new device.</span></span> <span data-ttu-id="5448d-264">Essa ação define a id de dispositivo exclusivo hello e gera a chave de autenticação hello.</span><span class="sxs-lookup"><span data-stu-id="5448d-264">This action sets hello unique device id and generates hello authentication key.</span></span> <span data-ttu-id="5448d-265">Ele grava informações sobre Olá tooboth de dispositivo Olá registro de identidade de IoT Hub e o banco de dados de banco de dados do Cosmos de solução específica Olá.</span><span class="sxs-lookup"><span data-stu-id="5448d-265">It writes information about hello device tooboth hello IoT Hub identity registry and hello solution-specific Cosmos DB database.</span></span>
* <span data-ttu-id="5448d-266">Gerencie propriedades de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5448d-266">Manage device properties.</span></span> <span data-ttu-id="5448d-267">Esta ação inclui a exibição de propriedades existentes e a atualização com novas propriedades.</span><span class="sxs-lookup"><span data-stu-id="5448d-267">This action includes viewing existing properties and updating with new properties.</span></span>
* <span data-ttu-id="5448d-268">Envie o dispositivo de tooa de comandos.</span><span class="sxs-lookup"><span data-stu-id="5448d-268">Send commands tooa device.</span></span>
* <span data-ttu-id="5448d-269">Exibir o histórico do comando Olá para um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5448d-269">View hello command history for a device.</span></span>
* <span data-ttu-id="5448d-270">Habilite e desabilite dispositivos.</span><span class="sxs-lookup"><span data-stu-id="5448d-270">Enable and disable devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5448d-271">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5448d-271">Next steps</span></span>

<span data-ttu-id="5448d-272">Olá, seguir postagens de blog do TechNet fornecem mais detalhes sobre Olá solução pré-configurada de monitoramento remoto:</span><span class="sxs-lookup"><span data-stu-id="5448d-272">hello following TechNet blog posts provide more detail about hello remote monitoring preconfigured solution:</span></span>

* [<span data-ttu-id="5448d-273">Monitoramento remoto do IoT Suite - em Olá bastidores-</span><span class="sxs-lookup"><span data-stu-id="5448d-273">IoT Suite - Under hello Hood - Remote Monitoring</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [<span data-ttu-id="5448d-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices (Adicionando dispositivos ativos e simulados)</span><span class="sxs-lookup"><span data-stu-id="5448d-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

<span data-ttu-id="5448d-275">Você pode continuar a guia de Introdução com IoT Suite lendo Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5448d-275">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="5448d-276">[Conecte-se a sua solução pré-configurada de monitoramento remoto de toohello de dispositivo][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="5448d-276">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="5448d-277">[Permissões no site de azureiotsuite.com Olá][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="5448d-277">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
