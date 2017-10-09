---
title: "Propriedades de duas aaaUse Azure IoT Hub dispositivo (nó) | Microsoft Docs"
description: "Como twins dispositivo do Azure IoT Hub toouse tooconfigure dispositivos. Você pode usar hello Azure IoT SDKs para Node. js tooimplement um aplicativo de dispositivo simulado e um aplicativo de serviço que modifica uma configuração de dispositivo usando duas um dispositivo."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a><span data-ttu-id="a1f8a-104">Use desejado propriedades tooconfigure dispositivos (nó)</span><span class="sxs-lookup"><span data-stu-id="a1f8a-104">Use desired properties tooconfigure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="a1f8a-105">No final de saudação deste tutorial, você terá dois aplicativos de console Node. js:</span><span class="sxs-lookup"><span data-stu-id="a1f8a-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="a1f8a-106">**SimulateDeviceConfiguration.js**, um aplicativo de dispositivo simulado que aguarda uma atualização de configurações desejadas e relata o status de saudação de um processo de atualização de configuração simulada.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="a1f8a-107">**SetDesiredConfigurationAndQuery.js**, um aplicativo de back-end node. js, que define a saudação da configuração em um dispositivo desejado e consultas Olá o processo de atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="a1f8a-108">artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild aplicativos de dispositivo e de back-end.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="a1f8a-109">toocomplete este tutorial, você precisa seguir hello:</span><span class="sxs-lookup"><span data-stu-id="a1f8a-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="a1f8a-110">Node.js versão 0.10.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="a1f8a-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-111">An active Azure account.</span></span> <span data-ttu-id="a1f8a-112">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="a1f8a-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="a1f8a-113">Se você seguiu Olá [Introdução ao twins dispositivo] [ lnk-twin-tutorial] tutorial, você já tem um hub IoT e uma identidade de dispositivo chamado **myDeviceId**; e você poderá ignorar toohello [ Criar aplicativo de dispositivo simulado Olá] [ lnk-how-to-configure-createapp] seção.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="a1f8a-114">Criar aplicativo de dispositivo simulado Olá</span><span class="sxs-lookup"><span data-stu-id="a1f8a-114">Create hello simulated device app</span></span>
<span data-ttu-id="a1f8a-115">Nesta seção, você cria um aplicativo de console Node. js que conecta o hub tooyour como **myDeviceId**, aguarda até que uma atualização de configurações desejadas e, em seguida, relatórios atualizações no processo de atualização de configuração Olá simulada.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-115">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="a1f8a-116">Crie uma nova pasta vazia denominada **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="a1f8a-117">Em Olá **simulatedeviceconfiguration** pasta, crie um novo arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-117">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="a1f8a-118">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="a1f8a-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="a1f8a-119">O prompt de comando no hello **simulatedeviceconfiguration** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure**, e **azure iot dispositivo-mqtt**pacote:</span><span class="sxs-lookup"><span data-stu-id="a1f8a-119">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="a1f8a-120">Usando um editor de texto, crie um novo **SimulateDeviceConfiguration.js** arquivo hello **simulatedeviceconfiguration** pasta.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="a1f8a-121">Adicionar Olá toohello de código a seguir **SimulateDeviceConfiguration.js** de arquivo e substituir Olá **{string de conexão do dispositivo}** espaço reservado com a cadeia de conexão do dispositivo Olá copiadas quando você criado Olá **myDeviceId** identidade do dispositivo:</span><span class="sxs-lookup"><span data-stu-id="a1f8a-121">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="a1f8a-122">Olá **cliente** objeto expõe toointeract necessária do todos os métodos de saudação com twins de dispositivo do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-122">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="a1f8a-123">Olá código anterior, depois que ele inicializa Olá **cliente** objeto recupera Olá duas de dispositivo para **myDeviceId**e anexa um manipulador de atualização de saudação em propriedades desejadas.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-123">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and attaches a handler for hello update on desired properties.</span></span> <span data-ttu-id="a1f8a-124">manipulador de saudação verifica que há é uma solicitação de alteração de configuração real comparando Olá configIds, em seguida, invoca um método que inicia a alteração de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-124">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="a1f8a-125">Observe que, para bem Olá de simplicidade, código anterior Olá usa um padrão embutido para a configuração inicial de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-125">Note that for hello sake of simplicity, hello previous code uses a hard-coded default for hello inital configuration.</span></span> <span data-ttu-id="a1f8a-126">Um aplicativo real provavelmente carregaria essa configuração de um armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="a1f8a-127">Eventos de alteração de propriedade desejados sempre são emitidos uma vez na conexão do dispositivo, certifique-se de toocheck que há uma alteração real no hello propriedades desejadas antes de executar qualquer ação.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-127">Desired property change events are always emitted once at device connection, make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="a1f8a-128">Adicionar Olá seguintes métodos antes de saudação `client.open()` invocação:</span><span class="sxs-lookup"><span data-stu-id="a1f8a-128">Add hello following methods before hello `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="a1f8a-129">Olá **initConfigChange** método atualizações relatado propriedades no objeto de duas Olá dispositivo local com a solicitação de atualização de configuração hello e conjuntos de Olá status muito**pendente**, e em seguida, as atualizações Olá dispositivo duas no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-129">hello **initConfigChange** method updates reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="a1f8a-130">Depois de atualizar com êxito duas de dispositivo hello, ele simula um processo de execução demorada que termina em execução de saudação do **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-130">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="a1f8a-131">Duas de dispositivo local este método atualizações saudação do relatado propriedades definindo o status de saudação muito**êxito** e removendo Olá **pendingConfig** objeto.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-131">This method updates hello local device twin's reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="a1f8a-132">Em seguida, atualiza as duas de dispositivo Olá no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-132">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="a1f8a-133">Observe que, a largura de banda toosave relatadas propriedades serão atualizadas, especificando somente o hello propriedades toobe modificado (denominado **patch** em Olá acima código), em vez de substituir todo o documento hello.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-133">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a1f8a-134">Este tutorial não simula nenhum comportamento para atualizações de configuração simultâneas.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="a1f8a-135">Alguns processos de atualização de configuração podem ser capaz de tooaccommodate alterações de configuração de destino durante a execução de atualização hello, outros podem ter tooqueue e outros podem rejeitá-las com uma condição de erro.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-135">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, others might have tooqueue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="a1f8a-136">Verifique tooconsider se Olá o comportamento desejado para o processo de configuração específica e adicionar lógica apropriada Olá antes de iniciar a alteração de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-136">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="a1f8a-137">Execute o aplicativo de dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="a1f8a-137">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="a1f8a-138">Você verá uma mensagem de saudação `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-138">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="a1f8a-139">Lembre-Olá aplicativo em execução.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-139">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="a1f8a-140">Criar aplicativo de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="a1f8a-140">Create hello service app</span></span>
<span data-ttu-id="a1f8a-141">Nesta seção, você criará um aplicativo de console Node. js que Olá atualizações *propriedades desejadas* em Olá dispositivo duas associada **myDeviceId** com um novo objeto de configuração de telemetria.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-141">In this section, you will create a Node.js console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="a1f8a-142">Ele, em seguida, consulta twins de dispositivo Olá armazenadas no hub IoT de saudação e mostra diferença Olá entre hello desejado e relatado configurações de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-142">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="a1f8a-143">Crie uma nova pasta vazia denominada **setdesiredandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="a1f8a-144">Em Olá **setdesiredandqueryapp** pasta, crie um novo arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-144">In hello **setdesiredandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="a1f8a-145">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="a1f8a-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="a1f8a-146">O prompt de comando no hello **setdesiredandqueryapp** pasta, execute Olá Olá de tooinstall de comando a seguir **hub IOT do azure** pacote:</span><span class="sxs-lookup"><span data-stu-id="a1f8a-146">At your command prompt in hello **setdesiredandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="a1f8a-147">Usando um editor de texto, crie um novo **SetDesiredAndQuery.js** arquivo hello **addtagsandqueryapp** pasta.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="a1f8a-148">Adicionar Olá toohello de código a seguir **SetDesiredAndQuery.js** de arquivo e substituir Olá **{string de conexão de hub iot}** espaço reservado com hello cadeia de caracteres de conexão de IoT Hub copiadas quando você criar o hub :</span><span class="sxs-lookup"><span data-stu-id="a1f8a-148">Add hello following code toohello **SetDesiredAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    <span data-ttu-id="a1f8a-149">Olá **registro** objeto expõe toointeract necessária do todos os métodos de saudação com twins de dispositivo do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-149">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="a1f8a-150">Olá código anterior, depois que ele inicializa Olá **registro** objeto recupera Olá duas de dispositivo para **myDeviceId**e atualiza as propriedades desejadas com um novo objeto de configuração de telemetria.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-150">hello previous code, after it initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="a1f8a-151">Depois disso, ele chama Olá **queryTwins** função evento 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-151">After that, it calls hello **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a1f8a-152">Esse aplicativo consulta o Hub IoT a cada 10 segundos para fins ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="a1f8a-153">Use consultas toogenerate voltadas para o usuário relatórios em vários dispositivos e não toodetect alterações.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-153">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="a1f8a-154">Se sua solução exigir notificações em tempo real de eventos de dispositivo, use [notificações gêmeas][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="a1f8a-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="a1f8a-155">.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-155">.</span></span>

1. <span data-ttu-id="a1f8a-156">Adicionar Olá seguindo o direito de código antes de saudação `registry.getDeviceTwin()` saudação do invocação tooimplement **queryTwins** função:</span><span class="sxs-lookup"><span data-stu-id="a1f8a-156">Add hello following code right before hello `registry.getDeviceTwin()` invocation tooimplement hello **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    <span data-ttu-id="a1f8a-157">consultas de código anteriores Olá Olá twins dispositivo armazenadas no hub IoT de saudação e imprime Olá desejado e relatado configurações de telemetria.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-157">hello previous code queries hello device twins stored in hello IoT hub and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="a1f8a-158">Consulte toohello [linguagem de consulta de IoT Hub] [ lnk-query] toolearn como toogenerate rich relatórios em todos os seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-158">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
2. <span data-ttu-id="a1f8a-159">Com **SimulateDeviceConfiguration.js** em execução, execute o aplicativo hello com:</span><span class="sxs-lookup"><span data-stu-id="a1f8a-159">With **SimulateDeviceConfiguration.js** running, run hello application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="a1f8a-160">Você deve ver a configuração relatado Olá alterar de **êxito** muito**pendente** muito**êxito** novamente com um novo ativo de saudação enviar frequência de cinco minutos, em vez de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-160">You should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="a1f8a-161">Há um atraso de backup tooa minutos entre a operação de relatório de dispositivo hello e resultado da consulta hello.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-161">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="a1f8a-162">Isso é tooenable Olá consulta infraestrutura toowork em escala muito alta.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-162">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="a1f8a-163">modos de exibição consistente de duas um único dispositivo tooretrieve usam Olá **getDeviceTwin** método hello **registro** classe.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-163">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="a1f8a-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a1f8a-164">Next steps</span></span>
<span data-ttu-id="a1f8a-165">Neste tutorial, você definir uma configuração desejada como *propriedades desejadas* de um aplicativo de back-end e escreveu um toodetect de aplicativo do dispositivo simulado que são alterados e simular um processo de atualização de várias etapas relatar seu status como  *relatado propriedades* toohello duas de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app toodetect that change and simulate a multi-step update process reporting its status as *reported properties* toohello device twin.</span></span>

<span data-ttu-id="a1f8a-166">Saudação de uso toolearn de recursos a seguir como a:</span><span class="sxs-lookup"><span data-stu-id="a1f8a-166">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="a1f8a-167">Enviar telemetria de dispositivos com hello [começar com o IoT Hub] [ lnk-iothub-getstarted] tutorial,</span><span class="sxs-lookup"><span data-stu-id="a1f8a-167">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="a1f8a-168">agendar ou executar operações em grandes conjuntos de dispositivos Consulte Olá [agenda e trabalhos de difusão] [ lnk-schedule-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-168">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="a1f8a-169">controlar dispositivos interativamente (como ativar um ventilador de um aplicativo controlado pelo usuário), com hello [usar métodos diretos] [ lnk-methods-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="a1f8a-169">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

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
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
