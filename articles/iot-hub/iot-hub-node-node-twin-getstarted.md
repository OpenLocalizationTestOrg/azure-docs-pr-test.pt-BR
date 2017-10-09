---
title: "aaaGet iniciado com twins de dispositivo do Azure IoT Hub (nó) | Microsoft Docs"
description: "Como toouse Azure IoT Hub dispositivo twins tooadd marcas e, em seguida, use uma consulta de IoT Hub. Use hello Azure IoT SDKs para aplicativo de dispositivo simulado Node. js tooimplement hello e um aplicativo de serviço que adiciona marcas hello e executa Olá consulta de IoT Hub."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="01545-104">Introdução aos dispositivos gêmeos (Node)</span><span class="sxs-lookup"><span data-stu-id="01545-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="01545-105">No final de saudação deste tutorial, você terá dois aplicativos de console Node. js:</span><span class="sxs-lookup"><span data-stu-id="01545-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="01545-106">**AddTagsAndQuery.js**, um aplicativo de back-end Node.js que adiciona marcas e consultas aos dispositivos gêmeos.</span><span class="sxs-lookup"><span data-stu-id="01545-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="01545-107">**TwinSimulatedDevice.js**, um aplicativo Node. js que simula um dispositivo que conecta o hub IoT de tooyour com a identidade do dispositivo Olá criada anteriormente e sua condição de conectividade de relatórios.</span><span class="sxs-lookup"><span data-stu-id="01545-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="01545-108">artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild aplicativos de dispositivo e de back-end.</span><span class="sxs-lookup"><span data-stu-id="01545-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="01545-109">toocomplete este tutorial, você precisa seguir hello:</span><span class="sxs-lookup"><span data-stu-id="01545-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="01545-110">Node.js versão 0.10.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="01545-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="01545-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="01545-111">An active Azure account.</span></span> <span data-ttu-id="01545-112">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="01545-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="01545-113">Criar aplicativo de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="01545-113">Create hello service app</span></span>
<span data-ttu-id="01545-114">Nesta seção, você cria um aplicativo de console Node. js que adiciona associada duas de dispositivo local metadados toohello **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="01545-114">In this section, you create a Node.js console app that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="01545-115">Em seguida, consultas twins de dispositivo Olá armazenadas no hub IoT de saudação selecionando Olá dispositivos localizados em Olá nos e hello, em seguida, aqueles que estão se comunicando uma conexão de celular.</span><span class="sxs-lookup"><span data-stu-id="01545-115">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that are reporting a cellular connection.</span></span>

1. <span data-ttu-id="01545-116">Crie uma nova pasta vazia denominada **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="01545-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="01545-117">Em Olá **addtagsandqueryapp** pasta, crie um novo arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="01545-117">In hello **addtagsandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="01545-118">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="01545-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="01545-119">O prompt de comando no hello **addtagsandqueryapp** pasta, execute Olá Olá de tooinstall de comando a seguir **hub IOT do azure** pacote:</span><span class="sxs-lookup"><span data-stu-id="01545-119">At your command prompt in hello **addtagsandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="01545-120">Usando um editor de texto, crie um novo **AddTagsAndQuery.js** arquivo hello **addtagsandqueryapp** pasta.</span><span class="sxs-lookup"><span data-stu-id="01545-120">Using a text editor, create a new **AddTagsAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="01545-121">Adicionar Olá toohello de código a seguir **AddTagsAndQuery.js** de arquivo e substituir Olá **{string de conexão de hub iot}** espaço reservado com hello cadeia de caracteres de conexão de IoT Hub copiadas quando você criar o hub:</span><span class="sxs-lookup"><span data-stu-id="01545-121">Add hello following code toohello **AddTagsAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    <span data-ttu-id="01545-122">Olá **registro** objeto expõe toointeract necessária do todos os métodos de saudação com twins de dispositivo do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="01545-122">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="01545-123">código anterior Olá primeiro inicializa Olá **registro** do objeto, em seguida, recupera Olá duas de dispositivo para **myDeviceId**e finalmente atualiza as marcas com informações de localização de saudação desejada.</span><span class="sxs-lookup"><span data-stu-id="01545-123">hello previous code first initializes hello **Registry** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="01545-124">Após Olá atualizar Olá marcas-Olá chamadas **queryTwins** função.</span><span class="sxs-lookup"><span data-stu-id="01545-124">After hello updating hello tags it calls hello **queryTwins** function.</span></span>
5. <span data-ttu-id="01545-125">Adicionar Olá após código final Olá **AddTagsAndQuery.js** tooimplement Olá **queryTwins** função:</span><span class="sxs-lookup"><span data-stu-id="01545-125">Add hello following code at hello end of  **AddTagsAndQuery.js** tooimplement hello **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    <span data-ttu-id="01545-126">código anterior Olá executa duas consultas: Olá primeiro seleciona apenas twins de dispositivo de saudação de dispositivos localizados em Olá **Redmond43** fábrica Olá segundo refina Olá consulta tooselect somente Olá dispositivos e também são conectados por meio rede de celular.</span><span class="sxs-lookup"><span data-stu-id="01545-126">hello previous code executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="01545-127">Observe que Olá o código anterior, quando ele cria Olá **consulta** de objeto, especifica um número máximo de documentos retornados.</span><span class="sxs-lookup"><span data-stu-id="01545-127">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="01545-128">Olá **consulta** objeto contém um **hasMoreResults** propriedade booleana que você pode usar o hello tooinvoke **nextAsTwin** métodos tooretrieve todos os resultados de várias vezes.</span><span class="sxs-lookup"><span data-stu-id="01545-128">hello **query** object contains a **hasMoreResults** boolean property that you can use tooinvoke hello **nextAsTwin** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="01545-129">Um método chamado **next** está disponível para os resultados que não são de dispositivos gêmeos, por exemplo, resultados de consultas de agregação.</span><span class="sxs-lookup"><span data-stu-id="01545-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="01545-130">Execute o aplicativo hello com:</span><span class="sxs-lookup"><span data-stu-id="01545-130">Run hello application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="01545-131">Você deve ver um dispositivo nos resultados de Olá Olá consulta pedindo para todos os dispositivos localizados no **Redmond43** e nenhuma consulta Olá que restringe Olá resultados toodevices que usam uma rede de celular.</span><span class="sxs-lookup"><span data-stu-id="01545-131">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="01545-132">Na próxima seção, Olá você criar um aplicativo de dispositivo com informações de conectividade de saudação e resultado da consulta de saudação na seção anterior Olá Olá a alterações.</span><span class="sxs-lookup"><span data-stu-id="01545-132">In hello next section you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="01545-133">Criar aplicativo de dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="01545-133">Create hello device app</span></span>
<span data-ttu-id="01545-134">Nesta seção, você cria um aplicativo de console Node. js que conecta o hub tooyour como **myDeviceId**e, em seguida, as atualizações duas seu dispositivo do relatado informações Olá toocontain das propriedades que ele está conectado usando uma rede de celular.</span><span class="sxs-lookup"><span data-stu-id="01545-134">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its device twin's reported properties toocontain hello information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="01545-135">Neste momento, twins de dispositivo são acessíveis somente de dispositivos que se conectam tooIoT Hub usando o protocolo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="01545-135">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="01545-136">Consulte toohello [suporte MQTT] [ lnk-devguide-mqtt] artigo para obter instruções sobre como tooconvert existente dispositivo aplicativo toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="01545-136">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

1. <span data-ttu-id="01545-137">Crie uma nova pasta vazia denominada **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="01545-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="01545-138">Em Olá **reportconnectivity** pasta, crie um novo arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="01545-138">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="01545-139">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="01545-139">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="01545-140">O prompt de comando no hello **reportconnectivity** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure**, e **azure iot-dispositivo mqtt** pacote :</span><span class="sxs-lookup"><span data-stu-id="01545-140">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="01545-141">Usando um editor de texto, crie um novo **ReportConnectivity.js** arquivo hello **reportconnectivity** pasta.</span><span class="sxs-lookup"><span data-stu-id="01545-141">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="01545-142">Adicionar Olá toohello de código a seguir **ReportConnectivity.js** de arquivo e substituir Olá **{string de conexão do dispositivo}** espaço reservado com cadeia de conexão do dispositivo Olá copiadas quando você criou Olá **myDeviceId** identidade do dispositivo:</span><span class="sxs-lookup"><span data-stu-id="01545-142">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    <span data-ttu-id="01545-143">Olá **cliente** objeto expõe todos os métodos de saudação exigem toointeract com twins de dispositivo do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="01545-143">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="01545-144">Olá código anterior, depois que ele inicializa Olá **cliente** objeto recupera Olá duas de dispositivo para **myDeviceId** e atualiza sua propriedade relatada com informações de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="01545-144">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
5. <span data-ttu-id="01545-145">Executar o aplicativo de dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="01545-145">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="01545-146">Você verá uma mensagem de saudação `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="01545-146">You should see hello message `twin state reported`.</span></span>
6. <span data-ttu-id="01545-147">Agora que hello dispositivo relatado suas informações de conectividade, ele aparecerá em ambas as consultas.</span><span class="sxs-lookup"><span data-stu-id="01545-147">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="01545-148">Vá em Olá **addtagsandqueryapp** Olá pasta e executar consultas novamente:</span><span class="sxs-lookup"><span data-stu-id="01545-148">Go back in hello **addtagsandqueryapp** folder and run hello queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="01545-149">Desta vez, **myDeviceId** deve aparecer em ambos os resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="01545-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="01545-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="01545-150">Next steps</span></span>
<span data-ttu-id="01545-151">Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello.</span><span class="sxs-lookup"><span data-stu-id="01545-151">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="01545-152">Você adicionou o metadados do dispositivo como marcas de um aplicativo de back-end e gravou informações de conectividade do dispositivo do dispositivo simulado aplicativo tooreport em duas de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="01545-152">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="01545-153">Você também aprendeu como tooquery essas informações usando a linguagem de consulta do tipo SQL IoT Hub hello.</span><span class="sxs-lookup"><span data-stu-id="01545-153">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="01545-154">Saudação de uso toolearn de recursos a seguir como a:</span><span class="sxs-lookup"><span data-stu-id="01545-154">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="01545-155">Enviar telemetria de dispositivos com hello [começar com o IoT Hub] [ lnk-iothub-getstarted] tutorial,</span><span class="sxs-lookup"><span data-stu-id="01545-155">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="01545-156">Configurar dispositivos com propriedades desejadas de duas dispositivo Olá [uso desejado dispositivos de tooconfigure propriedades] [ lnk-twin-how-to-configure] tutorial,</span><span class="sxs-lookup"><span data-stu-id="01545-156">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="01545-157">controlar dispositivos interativamente (como ativar um ventilador de um aplicativo controlado pelo usuário), com hello [usar métodos diretos] [ lnk-methods-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="01545-157">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
