---
title: "Usar as propriedades do dispositivo gêmeo do Hub IoT do Azure (Node) | Microsoft Docs"
description: "Como usar dispositivos gêmeos do Hub IoT do Azure para configurar dispositivos. Use os SDKs do IoT do Azure para Node.js para implementar um aplicativo de dispositivo simulado e um aplicativo de serviço que modifica a configuração de um dispositivo usando um dispositivo gêmeo."
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
ms.openlocfilehash: 771106ce7b00a5231d9929e4b5ea34aefe693597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-desired-properties-to-configure-devices-node"></a><span data-ttu-id="4ba29-104">Usar as propriedades desejadas para configurar os dispositivos (Node)</span><span class="sxs-lookup"><span data-stu-id="4ba29-104">Use desired properties to configure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="4ba29-105">No fim deste tutorial, você terá dois aplicativos de console do Node.js:</span><span class="sxs-lookup"><span data-stu-id="4ba29-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="4ba29-106">**SimulateDeviceConfiguration.js**, um aplicativo de dispositivo simulado que aguarda uma atualização da configuração desejada e reporta o status de um processo simulado de atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="4ba29-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="4ba29-107">**SetDesiredConfigurationAndQuery.js**, um aplicativo de back-end Node.js que define a configuração desejada em um dispositivo e consulta o processo de atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="4ba29-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="4ba29-108">O artigo [SDKs do IoT do Azure][lnk-hub-sdks] fornece informações sobre os SDKs do IoT do Azure que você pode usar para compilar dispositivos e aplicativos back-end.</span><span class="sxs-lookup"><span data-stu-id="4ba29-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="4ba29-109">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="4ba29-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="4ba29-110">Node.js versão 0.10.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="4ba29-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="4ba29-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ba29-111">An active Azure account.</span></span> <span data-ttu-id="4ba29-112">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="4ba29-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="4ba29-113">Caso tenha seguido o tutorial [Introdução aos dispositivos gêmeos][lnk-twin-tutorial], você já terá um Hub IoT e uma identidade de dispositivo chamada **myDeviceId**; você poderá pular para a seção [Criar o aplicativo do dispositivo simulado][lnk-how-to-configure-createapp].</span><span class="sxs-lookup"><span data-stu-id="4ba29-113">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-simulated-device-app"></a><span data-ttu-id="4ba29-114">Criar o aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="4ba29-114">Create the simulated device app</span></span>
<span data-ttu-id="4ba29-115">Nesta seção, você cria um aplicativo de console do Node.js que se conecta ao seu hub como **myDeviceId**, aguarda uma atualização de configuração desejada e, em seguida, reporta atualizações sobre o processo simulado de atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="4ba29-115">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="4ba29-116">Crie uma nova pasta vazia denominada **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="4ba29-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="4ba29-117">Na pasta **simulatedeviceconfiguration**, crie um novo arquivo package.json usando o comando a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="4ba29-117">In the **simulatedeviceconfiguration** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="4ba29-118">Aceite todos os padrões:</span><span class="sxs-lookup"><span data-stu-id="4ba29-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="4ba29-119">No prompt de comando, na pasta **simulatedeviceconfiguration**, execute o seguinte comando para instalar os pacotes **azure-iot-device** e **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="4ba29-119">At your command prompt in the **simulatedeviceconfiguration** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="4ba29-120">Usando um editor de texto, crie um novo arquivo **SimulateDeviceConfiguration.js** na pasta **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="4ba29-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in the **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="4ba29-121">Adicione o seguinte código ao arquivo **SimulateDeviceConfiguration.js** e substitua o espaço reservado **{cadeia de conexão do dispositivo}** pela cadeia de conexão do dispositivo copiada quando você criou a identidade do dispositivo **myDeviceId**:</span><span class="sxs-lookup"><span data-stu-id="4ba29-121">Add the following code to the **SimulateDeviceConfiguration.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="4ba29-122">O objeto **Client** expõe todos os métodos necessários para você, do dispositivo, interagir com gêmeos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4ba29-122">The **Client** object exposes all the methods required to interact with device twins from the device.</span></span> <span data-ttu-id="4ba29-123">O código anterior, depois de inicializar o objeto **Client**, recupera o dispositivo gêmeo para **myDeviceId** e anexa um manipulador para a atualização em propriedades desejadas.</span><span class="sxs-lookup"><span data-stu-id="4ba29-123">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId**, and attaches a handler for the update on desired properties.</span></span> <span data-ttu-id="4ba29-124">O manipulador verifica que há uma solicitação de alteração de configuração real ao comparar as configIds, então invoca um método que inicia a alteração de configuração.</span><span class="sxs-lookup"><span data-stu-id="4ba29-124">The handler verifies that there is an actual configuration change request by comparing the configIds, then invokes a method that starts the configuration change.</span></span>
   
    <span data-ttu-id="4ba29-125">Observe que, para simplificar, o código anterior usa um padrão embutido em código para a configuração inicial.</span><span class="sxs-lookup"><span data-stu-id="4ba29-125">Note that for the sake of simplicity, the previous code uses a hard-coded default for the inital configuration.</span></span> <span data-ttu-id="4ba29-126">Um aplicativo real provavelmente carregaria essa configuração de um armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="4ba29-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="4ba29-127">Eventos de alteração de propriedade desejada são sempre emitidos uma vez no ato da conexão com o dispositivo, não deixe de verificar se há uma alteração real nas propriedades desejadas antes de executar qualquer ação.</span><span class="sxs-lookup"><span data-stu-id="4ba29-127">Desired property change events are always emitted once at device connection, make sure to check that there is an actual change in the desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="4ba29-128">Adicione os seguintes métodos antes da invocação de `client.open()`:</span><span class="sxs-lookup"><span data-stu-id="4ba29-128">Add the following methods before the `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="4ba29-129">O método **initConfigChange** atualiza as propriedades relatadas no objeto do dispositivo gêmeo local com a solicitação de atualização de configuração, define o status para **Pendente** e atualiza o dispositivo gêmeo no serviço.</span><span class="sxs-lookup"><span data-stu-id="4ba29-129">The **initConfigChange** method updates reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="4ba29-130">Depois de atualizar o dispositivo gêmeo com êxito, ele simula um processo de execução longa que termina com a execução de **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="4ba29-130">After successfully updating the device twin, it simulates a long running process that terminates in the execution of **completeConfigChange**.</span></span> <span data-ttu-id="4ba29-131">Esse método atualiza propriedades relatadas do dispositivo gêmeo local definindo o status como **Êxito** e removendo o objeto **pendingConfig**.</span><span class="sxs-lookup"><span data-stu-id="4ba29-131">This method updates the local device twin's reported properties setting the status to **Success** and removing the **pendingConfig** object.</span></span> <span data-ttu-id="4ba29-132">Em seguida, ele atualiza o dispositivo gêmeo no serviço.</span><span class="sxs-lookup"><span data-stu-id="4ba29-132">It then updates the device twin on the service.</span></span>
   
    <span data-ttu-id="4ba29-133">Observe que, para economizar largura de banda, as propriedades reportadas são atualizadas especificando-se apenas as propriedades a serem modificadas (chamadas de **patch** no código acima), em vez de substituir o documento inteiro.</span><span class="sxs-lookup"><span data-stu-id="4ba29-133">Note that, to save bandwidth, reported properties are updated by specifying only the properties to be modified (named **patch** in the above code), instead of replacing the whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4ba29-134">Este tutorial não simula nenhum comportamento para atualizações de configuração simultâneas.</span><span class="sxs-lookup"><span data-stu-id="4ba29-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="4ba29-135">Alguns processos de atualização de configuração podem ser capazes de acomodar as alterações de configuração de destino enquanto a atualização está em execução, outros podem colocá-las em fila e outros poderiam ainda rejeitá-las com uma condição de erro.</span><span class="sxs-lookup"><span data-stu-id="4ba29-135">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, others might have to queue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="4ba29-136">Certifique-se de considerar o comportamento desejado para o seu processo de configuração específico e adicione a lógica apropriada antes de iniciar a alteração de configuração.</span><span class="sxs-lookup"><span data-stu-id="4ba29-136">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="4ba29-137">Execute o aplicativo do dispositivo:</span><span class="sxs-lookup"><span data-stu-id="4ba29-137">Run the device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="4ba29-138">Você deve ver a mensagem `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="4ba29-138">You should see the message `retrieved device twin`.</span></span> <span data-ttu-id="4ba29-139">Mantenha o aplicativo em execução.</span><span class="sxs-lookup"><span data-stu-id="4ba29-139">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="4ba29-140">Criar o aplicativo do serviço</span><span class="sxs-lookup"><span data-stu-id="4ba29-140">Create the service app</span></span>
<span data-ttu-id="4ba29-141">Nesta seção, você criará um aplicativo de console do Node. js que atualiza as *propriedades desejadas* no dispositivo gêmeo associado à **myDeviceId** com um novo objeto de configuração de telemetria.</span><span class="sxs-lookup"><span data-stu-id="4ba29-141">In this section, you will create a Node.js console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="4ba29-142">Então, ele consulta os gêmeos de dispositivo armazenados no Hub IoT e mostra a diferença entre as configurações desejadas e as reportadas do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4ba29-142">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="4ba29-143">Crie uma nova pasta vazia denominada **setdesiredandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="4ba29-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="4ba29-144">Na pasta **setdesiredandqueryapp**, crie um novo arquivo package.json usando o comando a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="4ba29-144">In the **setdesiredandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="4ba29-145">Aceite todos os padrões:</span><span class="sxs-lookup"><span data-stu-id="4ba29-145">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="4ba29-146">No prompt de comando, na pasta **setdesiredandqueryapp**, execute o seguinte comando para instalar o pacote **azure-iothub**:</span><span class="sxs-lookup"><span data-stu-id="4ba29-146">At your command prompt in the **setdesiredandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="4ba29-147">Usando um editor de texto, crie um novo arquivo **SetDesiredAndQuery.js** na pasta **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="4ba29-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="4ba29-148">Adicione o seguinte código ao arquivo **SetDesiredAndQuery.js** e substitua o espaço reservado **{iot hub connection string}** pela cadeia de conexão do Hub IoT que você copiou quando criou seu hub:</span><span class="sxs-lookup"><span data-stu-id="4ba29-148">Add the following code to the **SetDesiredAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
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

    <span data-ttu-id="4ba29-149">O objeto **Registry** expõe todos os métodos necessários para interagir com gêmeos de dispositivo do serviço.</span><span class="sxs-lookup"><span data-stu-id="4ba29-149">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="4ba29-150">O código anterior, depois de inicializar o objeto **Registry**, recupera o dispositivo gêmeo para **myDeviceId** e atualiza as propriedades desejadas com um novo objeto de configuração de telemetria.</span><span class="sxs-lookup"><span data-stu-id="4ba29-150">The previous code, after it initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="4ba29-151">Depois disso, ele chama o evento da função **queryTwins** em 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="4ba29-151">After that, it calls the **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4ba29-152">Esse aplicativo consulta o Hub IoT a cada 10 segundos para fins ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="4ba29-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="4ba29-153">Use consultas para gerar relatórios voltados para o usuário em vários dispositivos, não para detectar alterações.</span><span class="sxs-lookup"><span data-stu-id="4ba29-153">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="4ba29-154">Se sua solução exigir notificações em tempo real de eventos de dispositivo, use [notificações gêmeas][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="4ba29-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="4ba29-155">.</span><span class="sxs-lookup"><span data-stu-id="4ba29-155">.</span></span>

1. <span data-ttu-id="4ba29-156">Adicione o código a seguir logo antes da invocação de `registry.getDeviceTwin()` para implementar a função **queryTwins**:</span><span class="sxs-lookup"><span data-stu-id="4ba29-156">Add the following code right before the `registry.getDeviceTwin()` invocation to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
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
   
    <span data-ttu-id="4ba29-157">O código anterior consulta os dispositivos gêmeos armazenados no Hub IoT e imprime as configurações de telemetria desejadas e reportadas.</span><span class="sxs-lookup"><span data-stu-id="4ba29-157">The previous code queries the device twins stored in the IoT hub and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="4ba29-158">Consulte a [Linguagem de consulta de Hub IoT][lnk-query] para saber como gerar relatórios em todos os seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4ba29-158">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
2. <span data-ttu-id="4ba29-159">Com **SimulateDeviceConfiguration.js** em execução, execute o aplicativo com:</span><span class="sxs-lookup"><span data-stu-id="4ba29-159">With **SimulateDeviceConfiguration.js** running, run the application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="4ba29-160">Você deve ver a configuração reportada mudar de **Êxito** para **Pendente** e para **Êxito** novamente com a nova frequência de envio ativo de cinco minutos em vez de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="4ba29-160">You should see the reported configuration change from **Success** to **Pending** to **Success** again with the new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="4ba29-161">Há um atraso de até um minuto entre a operação de relatório de dispositivo e o resultado da consulta.</span><span class="sxs-lookup"><span data-stu-id="4ba29-161">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="4ba29-162">Isso é para habilitar a infraestrutura de consulta a trabalhar em escala muito alta.</span><span class="sxs-lookup"><span data-stu-id="4ba29-162">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="4ba29-163">Para recuperar os modos de exibição consistentes de um único dispositivo gêmeo, use o método **getDeviceTwin** na classe **Registry**.</span><span class="sxs-lookup"><span data-stu-id="4ba29-163">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="4ba29-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4ba29-164">Next steps</span></span>
<span data-ttu-id="4ba29-165">Neste tutorial, você definiu uma configuração desejada como *propriedades desejadas* de um aplicativo de back-end e escreveu um aplicativo de dispositivo simulado para detectar essa alteração e simular um processo de atualização de várias etapas, relatando seu status como *propriedades relatadas* ao dispositivo gêmeo.</span><span class="sxs-lookup"><span data-stu-id="4ba29-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app to detect that change and simulate a multi-step update process reporting its status as *reported properties* to the device twin.</span></span>

<span data-ttu-id="4ba29-166">Veja os recursos a seguir para saber como:</span><span class="sxs-lookup"><span data-stu-id="4ba29-166">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="4ba29-167">Enviar telemetria de dispositivos com o tutorial [Introdução ao Hub IoT][lnk-iothub-getstarted].</span><span class="sxs-lookup"><span data-stu-id="4ba29-167">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="4ba29-168">Agendar ou executar operações em grandes conjuntos de dispositivos. Veja o tutorial [Schedule and broadcast jobs][lnk-schedule-jobs] (Agendar e transmitir trabalhos).</span><span class="sxs-lookup"><span data-stu-id="4ba29-168">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="4ba29-169">Controlar dispositivos interativamente (como ativar uma ventoinha de um aplicativo controlado pelo usuário), com o tutorial [Uso de métodos diretos][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="4ba29-169">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
