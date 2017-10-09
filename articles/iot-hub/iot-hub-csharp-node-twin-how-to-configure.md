---
title: "Propriedades de duas aaaUse Azure IoT Hub dispositivo (.NET/nó) | Microsoft Docs"
description: "Como twins dispositivo do Azure IoT Hub toouse tooconfigure dispositivos. Você usar o dispositivo de Azure IoT Olá SDK para Node.js tooimplement um aplicativo de dispositivo simulado e hello serviço IoT do Azure SDK para .NET tooimplement um serviço de aplicativo que modifica uma configuração de dispositivo usando duas um dispositivo."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="35aaf-104">Usar propriedades desejadas tooconfigure dispositivos</span><span class="sxs-lookup"><span data-stu-id="35aaf-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="35aaf-105">No final de saudação deste tutorial, você terá dois aplicativos de console:</span><span class="sxs-lookup"><span data-stu-id="35aaf-105">At hello end of this tutorial, you will have two console apps:</span></span>

* <span data-ttu-id="35aaf-106">**SimulateDeviceConfiguration.js**, um aplicativo de dispositivo simulado que aguarda uma atualização de configurações desejadas e relata o status de saudação de um processo de atualização de configuração simulada.</span><span class="sxs-lookup"><span data-stu-id="35aaf-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="35aaf-107">**SetDesiredConfigurationAndQuery**, um aplicativo de back-end .NET, que define a saudação da configuração em um dispositivo desejado e consultas Olá o processo de atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="35aaf-107">**SetDesiredConfigurationAndQuery**, a .NET back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="35aaf-108">artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild aplicativos de dispositivo e de back-end.</span><span class="sxs-lookup"><span data-stu-id="35aaf-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="35aaf-109">toocomplete este tutorial, você precisa seguir hello:</span><span class="sxs-lookup"><span data-stu-id="35aaf-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="35aaf-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="35aaf-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="35aaf-111">Node.js versão 0.10.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="35aaf-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="35aaf-112">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="35aaf-112">An active Azure account.</span></span> <span data-ttu-id="35aaf-113">Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="35aaf-113">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="35aaf-114">Se você seguiu Olá [Introdução ao twins dispositivo] [ lnk-twin-tutorial] tutorial, você já tem um hub IoT e uma identidade de dispositivo chamado **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="35aaf-114">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="35aaf-115">Nesse caso, você pode ignorar toohello [criar aplicativo de dispositivo simulado Olá] [ lnk-how-to-configure-createapp] seção.</span><span class="sxs-lookup"><span data-stu-id="35aaf-115">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="35aaf-116">Criar aplicativo de dispositivo simulado Olá</span><span class="sxs-lookup"><span data-stu-id="35aaf-116">Create hello simulated device app</span></span>
<span data-ttu-id="35aaf-117">Nesta seção, você cria um aplicativo de console Node. js que conecta o hub tooyour como **myDeviceId**, aguarda até que uma atualização de configurações desejadas e, em seguida, relatórios atualizações no processo de atualização de configuração Olá simulada.</span><span class="sxs-lookup"><span data-stu-id="35aaf-117">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="35aaf-118">Crie uma nova pasta vazia denominada **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="35aaf-118">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="35aaf-119">Em Olá **simulatedeviceconfiguration** pasta, crie um novo arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="35aaf-119">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="35aaf-120">Aceite todos os padrões de saudação.</span><span class="sxs-lookup"><span data-stu-id="35aaf-120">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="35aaf-121">O prompt de comando no hello **simulatedeviceconfiguration** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure** e **azure iot dispositivo-mqtt**pacotes:</span><span class="sxs-lookup"><span data-stu-id="35aaf-121">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="35aaf-122">Usando um editor de texto, crie um novo **SimulateDeviceConfiguration.js** arquivo hello **simulatedeviceconfiguration** pasta.</span><span class="sxs-lookup"><span data-stu-id="35aaf-122">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
1. <span data-ttu-id="35aaf-123">Adicionar Olá toohello de código a seguir **SimulateDeviceConfiguration.js** de arquivo e substituir Olá **{string de conexão do dispositivo}** espaço reservado com a cadeia de conexão do dispositivo Olá copiadas quando você criado Olá **myDeviceId** identidade do dispositivo:</span><span class="sxs-lookup"><span data-stu-id="35aaf-123">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    <span data-ttu-id="35aaf-124">Olá **cliente** objeto expõe toointeract necessária do todos os métodos de saudação com twins de dispositivo do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="35aaf-124">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="35aaf-125">Esse código inicializa Olá **cliente** objeto recupera Olá duas de dispositivo para **myDeviceId**e, em seguida, anexa um manipulador de atualização de saudação em *propriedades desejadas*.</span><span class="sxs-lookup"><span data-stu-id="35aaf-125">This code initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and then attaches a handler for hello update on *desired properties*.</span></span> <span data-ttu-id="35aaf-126">manipulador de saudação verifica que há é uma solicitação de alteração de configuração real comparando Olá configIds, em seguida, invoca um método que inicia a alteração de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="35aaf-126">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="35aaf-127">Observe que, para bem Olá de simplicidade, esse código usa um padrão embutido para a configuração inicial de saudação.</span><span class="sxs-lookup"><span data-stu-id="35aaf-127">Note that for hello sake of simplicity, this code uses a hard-coded default for hello initial configuration.</span></span> <span data-ttu-id="35aaf-128">Um aplicativo real provavelmente carregaria essa configuração de um armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="35aaf-128">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="35aaf-129">Eventos de alteração da propriedade desejada sempre são emitidos uma vez na conexão do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="35aaf-129">Desired property change events are always emitted once at device connection.</span></span> <span data-ttu-id="35aaf-130">Certifique-se de toocheck que há uma alteração real no hello propriedades desejadas antes de executar qualquer ação.</span><span class="sxs-lookup"><span data-stu-id="35aaf-130">Make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
1. <span data-ttu-id="35aaf-131">Adicionar Olá seguintes métodos antes de saudação `client.open()` invocação:</span><span class="sxs-lookup"><span data-stu-id="35aaf-131">Add hello following methods before hello `client.open()` invocation:</span></span>
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    <span data-ttu-id="35aaf-132">Olá **initConfigChange** método atualizações Olá relatado propriedades no objeto de duas Olá dispositivo local com a configuração de saudação atualizar status de saudação de solicitação e conjuntos muito**pendente**, em seguida, Olá atualizações duas de dispositivo no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="35aaf-132">hello **initConfigChange** method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="35aaf-133">Depois de atualizar com êxito duas de dispositivo hello, ele simula um processo de execução demorada que termina em execução de saudação do **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="35aaf-133">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="35aaf-134">Este método atualiza propriedades relatado local Olá definindo o status de saudação muito**êxito** e removendo Olá **pendingConfig** objeto.</span><span class="sxs-lookup"><span data-stu-id="35aaf-134">This method updates hello local reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="35aaf-135">Em seguida, atualiza as duas de dispositivo Olá no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="35aaf-135">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="35aaf-136">Observe que, a largura de banda toosave relatadas propriedades serão atualizadas, especificando somente o hello propriedades toobe modificado (denominado **patch** em Olá acima código), em vez de substituir todo o documento hello.</span><span class="sxs-lookup"><span data-stu-id="35aaf-136">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="35aaf-137">Este tutorial não simula nenhum comportamento para atualizações de configuração simultâneas.</span><span class="sxs-lookup"><span data-stu-id="35aaf-137">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="35aaf-138">Alguns processos de atualização de configuração podem ser capaz de tooaccommodate alterações de configuração de destino durante a execução de atualização hello, alguns dados podem ter tooqueue e alguns podem rejeitá-las com uma condição de erro.</span><span class="sxs-lookup"><span data-stu-id="35aaf-138">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="35aaf-139">Verifique tooconsider se Olá o comportamento desejado para o processo de configuração específica e adicionar lógica apropriada Olá antes de iniciar a alteração de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="35aaf-139">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="35aaf-140">Execute o aplicativo de dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="35aaf-140">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="35aaf-141">Você verá uma mensagem de saudação `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="35aaf-141">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="35aaf-142">Lembre-Olá aplicativo em execução.</span><span class="sxs-lookup"><span data-stu-id="35aaf-142">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="35aaf-143">Criar aplicativo de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="35aaf-143">Create hello service app</span></span>
<span data-ttu-id="35aaf-144">Nesta seção, você criará um aplicativo de console .NET que Olá atualizações *propriedades desejadas* em Olá dispositivo duas associada **myDeviceId** com um novo objeto de configuração de telemetria.</span><span class="sxs-lookup"><span data-stu-id="35aaf-144">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="35aaf-145">Ele, em seguida, consulta twins de dispositivo Olá armazenadas no hub IoT de saudação e mostra diferença Olá entre hello desejado e relatado configurações de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="35aaf-145">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="35aaf-146">No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto toohello atual usando Olá **aplicativo de Console** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="35aaf-146">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="35aaf-147">Projeto de saudação do nome **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="35aaf-147">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]
1. <span data-ttu-id="35aaf-149">No Gerenciador de soluções, clique com botão direito Olá **SetDesiredConfigurationAndQuery** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="35aaf-149">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="35aaf-150">Em Olá **NuGet Package Manager** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="35aaf-150">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="35aaf-151">Este procedimento faz o download, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="35aaf-151">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
1. <span data-ttu-id="35aaf-153">Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="35aaf-153">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="35aaf-154">Adicionar Olá toohello campos a seguir **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="35aaf-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="35aaf-155">Substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub hub Olá que você criou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="35aaf-155">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="35aaf-156">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="35aaf-156">Add hello following method toohello **Program** class:</span></span>
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            try
            {
                while (true)
                {
                    var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                    var results = await query.GetNextAsTwinAsync();
                    foreach (var result in results)
                    {
                        Console.WriteLine("Config report for: {0}", result.DeviceId);
                        Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine();
                    }
                    Thread.Sleep(10000);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    <span data-ttu-id="35aaf-157">Olá **registro** objeto expõe toointeract necessária do todos os métodos de saudação com twins de dispositivo do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="35aaf-157">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="35aaf-158">Esse código inicializa Olá **registro** objeto recupera Olá duas de dispositivo para **myDeviceId**e, em seguida, atualiza as propriedades desejadas com um novo objeto de configuração de telemetria.</span><span class="sxs-lookup"><span data-stu-id="35aaf-158">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="35aaf-159">Depois disso, ele consulta twins de dispositivo Olá armazenadas no hub IoT de saudação a cada 10 segundos, e imprime Olá desejado e relatado configurações de telemetria.</span><span class="sxs-lookup"><span data-stu-id="35aaf-159">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="35aaf-160">Consulte toohello [linguagem de consulta de IoT Hub] [ lnk-query] toolearn como toogenerate rich relatórios em todos os seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="35aaf-160">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="35aaf-161">Esse aplicativo consulta o Hub IoT a cada 10 segundos para fins ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="35aaf-161">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="35aaf-162">Use consultas toogenerate voltadas para o usuário relatórios em vários dispositivos e não toodetect alterações.</span><span class="sxs-lookup"><span data-stu-id="35aaf-162">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="35aaf-163">Se sua solução exigir notificações em tempo real de eventos de dispositivo, use [notificações gêmeas][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="35aaf-163">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="35aaf-164">Finalmente, adicione Olá toohello linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="35aaf-164">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="35aaf-165">Olá Gerenciador de soluções, abra o hello **projetos de inicialização definido...**  e certifique-se de saudação **ação** para **SetDesiredConfigurationAndQuery** projeto é **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="35aaf-165">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="35aaf-166">Compile a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="35aaf-166">Build hello solution.</span></span>
1. <span data-ttu-id="35aaf-167">Com **SimulateDeviceConfiguration.js** em execução, execute o aplicativo de .NET de saudação do Visual Studio usando **F5** e você deverá ver a configuração relatado Olá alterar de **êxito** muito**pendente** muito**êxito** novamente com um novo ativo de saudação enviar frequência de cinco minutos, em vez de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="35aaf-167">With **SimulateDeviceConfiguration.js** running, run hello .NET application from Visual Studio using **F5** and you should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Dispositivo configurado com êxito][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="35aaf-169">Há um atraso de backup tooa minutos entre a operação de relatório de dispositivo hello e resultado da consulta hello.</span><span class="sxs-lookup"><span data-stu-id="35aaf-169">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="35aaf-170">Isso é tooenable Olá consulta infraestrutura toowork em escala muito alta.</span><span class="sxs-lookup"><span data-stu-id="35aaf-170">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="35aaf-171">modos de exibição consistente de duas um único dispositivo tooretrieve usam Olá **getDeviceTwin** método hello **registro** classe.</span><span class="sxs-lookup"><span data-stu-id="35aaf-171">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="35aaf-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="35aaf-172">Next steps</span></span>
<span data-ttu-id="35aaf-173">Neste tutorial, você definir uma configuração desejada como *propriedades desejadas* da solução Olá back-end e gravou um toodetect de aplicativo de dispositivo que são alterados e simular um processo de atualização de várias etapas relatar seu status por meio de saudação relatada Propriedades.</span><span class="sxs-lookup"><span data-stu-id="35aaf-173">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="35aaf-174">Saudação de uso toolearn de recursos a seguir como a:</span><span class="sxs-lookup"><span data-stu-id="35aaf-174">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="35aaf-175">Enviar telemetria de dispositivos com hello [começar com o IoT Hub] [ lnk-iothub-getstarted] tutorial,</span><span class="sxs-lookup"><span data-stu-id="35aaf-175">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="35aaf-176">agendar ou executar operações em grandes conjuntos de dispositivos Consulte Olá [agenda e trabalhos de difusão] [ lnk-schedule-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="35aaf-176">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="35aaf-177">controlar dispositivos interativamente (como ativar um ventilador de um aplicativo controlado pelo usuário), com hello [usar métodos diretos] [ lnk-methods-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="35aaf-177">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app
