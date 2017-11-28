---
title: "Introdução aos dispositivos gêmeos do Hub IoT do Azure (Node) | Microsoft Docs"
description: "Como usar dispositivos gêmeos do Hub IoT do Azure para adicionar marcas e usar uma consulta do Hub IoT. Use os SDKs do IoT do Azure para Node.js para implementar um aplicativo de dispositivo simulado e um aplicativo de serviço que adiciona as marcas e executa a consulta do Hub IoT."
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
ms.openlocfilehash: 633c9fd4f8a1d017d93148f8c2e860ccba14238c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="8e4b6-104">Introdução aos dispositivos gêmeos (Node)</span><span class="sxs-lookup"><span data-stu-id="8e4b6-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="8e4b6-105">No fim deste tutorial, você terá dois aplicativos de console do Node.js:</span><span class="sxs-lookup"><span data-stu-id="8e4b6-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="8e4b6-106">**AddTagsAndQuery.js**, um aplicativo de back-end Node.js que adiciona marcas e consultas aos dispositivos gêmeos.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="8e4b6-107">**TwinSimulatedDevice.js**, um aplicativo Node.js que simula um dispositivo que se conecta ao seu Hub IoT com a identidade do dispositivo criada anteriormente e reporta sua condição de conectividade.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="8e4b6-108">O artigo [SDKs do IoT do Azure][lnk-hub-sdks] fornece informações sobre os SDKs do IoT do Azure que você pode usar para compilar dispositivos e aplicativos back-end.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="8e4b6-109">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="8e4b6-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="8e4b6-110">Node.js versão 0.10.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="8e4b6-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-111">An active Azure account.</span></span> <span data-ttu-id="8e4b6-112">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="8e4b6-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="8e4b6-113">Criar o aplicativo do serviço</span><span class="sxs-lookup"><span data-stu-id="8e4b6-113">Create the service app</span></span>
<span data-ttu-id="8e4b6-114">Nesta seção, você cria um aplicativo de console do Node.js que adiciona metadados de local ao dispositivo gêmeo associado a **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-114">In this section, you create a Node.js console app that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="8e4b6-115">Em seguida, ele consulta os dispositivos gêmeos armazenados no hub IoT selecionando os dispositivos localizados nos EUA e, depois, aqueles que relatam uma conexão celular.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-115">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that are reporting a cellular connection.</span></span>

1. <span data-ttu-id="8e4b6-116">Crie uma nova pasta vazia denominada **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="8e4b6-117">Na pasta **addtagsandqueryapp**, crie um novo arquivo package.json usando o comando a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-117">In the **addtagsandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="8e4b6-118">Aceite todos os padrões:</span><span class="sxs-lookup"><span data-stu-id="8e4b6-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="8e4b6-119">No prompt de comando, na pasta **addtagsandqueryapp**, execute o seguinte comando para instalar o pacote **azure-iothub**:</span><span class="sxs-lookup"><span data-stu-id="8e4b6-119">At your command prompt in the **addtagsandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="8e4b6-120">Usando um editor de texto, crie um novo arquivo **AddTagsAndQuery.js** na pasta **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-120">Using a text editor, create a new **AddTagsAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="8e4b6-121">Adicione o seguinte código ao arquivo **AddTagsAndQuery.js** e substitua o espaço reservado **{iot hub connection string}** pela cadeia de conexão do Hub IoT que você copiou quando criou seu hub:</span><span class="sxs-lookup"><span data-stu-id="8e4b6-121">Add the following code to the **AddTagsAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
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
   
    <span data-ttu-id="8e4b6-122">O objeto **Registry** expõe todos os métodos necessários para interagir com gêmeos de dispositivo do serviço.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-122">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="8e4b6-123">O código anterior inicializa primeiro o objeto **Registry**, depois, recupera o dispositivo gêmeo para **myDeviceId** e finalmente atualiza as marcas com as informações do local desejado.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-123">The previous code first initializes the **Registry** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="8e4b6-124">Depois de atualizar as marcas, ele chama a função **queryTwins**.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-124">After the updating the tags it calls the **queryTwins** function.</span></span>
5. <span data-ttu-id="8e4b6-125">Adicione o seguinte código ao final do **AddTagsAndQuery.js** para implementar a função **queryTwins**:</span><span class="sxs-lookup"><span data-stu-id="8e4b6-125">Add the following code at the end of  **AddTagsAndQuery.js** to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    <span data-ttu-id="8e4b6-126">O código anterior executa duas consultas: a primeira seleciona somente os dispositivos gêmeos de dispositivos localizados na fábrica de **Redmond43**, e o segundo aperfeiçoa a consulta para selecionar somente os dispositivos que também estão conectados por meio de rede celular.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-126">The previous code executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="8e4b6-127">Observe que o código anterior, quando ele cria o objeto **query**, especifica um número máximo de documentos retornados.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-127">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="8e4b6-128">O objeto **query** contém uma propriedade booliana **hasMoreResults** que você pode usar para invocar os métodos **nextAsTwin** várias vezes para recuperar todos os resultados.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-128">The **query** object contains a **hasMoreResults** boolean property that you can use to invoke the **nextAsTwin** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="8e4b6-129">Um método chamado **next** está disponível para os resultados que não são de dispositivos gêmeos, por exemplo, resultados de consultas de agregação.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="8e4b6-130">Execute o aplicativo com:</span><span class="sxs-lookup"><span data-stu-id="8e4b6-130">Run the application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="8e4b6-131">Você deve ver um dispositivo nos resultados da consulta que pergunta sobre todos os dispositivos localizados em **Redmond43**, e nenhum para a consulta que restringe os resultados para dispositivos que usam uma rede de celular.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-131">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="8e4b6-132">Na próxima seção, você criará um aplicativo de dispositivo que reporta as informações de conectividade e altera o resultado da consulta na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-132">In the next section you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="8e4b6-133">Criar o aplicativo do dispositivo</span><span class="sxs-lookup"><span data-stu-id="8e4b6-133">Create the device app</span></span>
<span data-ttu-id="8e4b6-134">Nesta seção, você cria um aplicativo de console do Node.js que se conecta ao seu hub como **myDeviceId**, e depois atualiza seu as propriedades reportadas de seu dispositivo gêmeo a fim de conter as informações indicando que ele está conectado usando uma rede de celular.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-134">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its device twin's reported properties to contain the information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="8e4b6-135">Neste momento, os dispositivos gêmeos podem ser acessados somente de dispositivos que se conectam ao Hub IoT usando o protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-135">At this time, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="8e4b6-136">Confira o artigo do [suporte a MQTT][lnk-devguide-mqtt] para obter instruções sobre como converter o aplicativo de dispositivo existente para usar MQTT.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-136">Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

1. <span data-ttu-id="8e4b6-137">Crie uma nova pasta vazia denominada **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="8e4b6-138">Na pasta **reportconnectivity**, crie um novo arquivo package.json usando o comando a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-138">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="8e4b6-139">Aceite todos os padrões:</span><span class="sxs-lookup"><span data-stu-id="8e4b6-139">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="8e4b6-140">No prompt de comando, na pasta **reportconnectivity**, execute o seguinte comando para instalar os pacotes **azure-iot-device** e **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="8e4b6-140">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="8e4b6-141">Usando um editor de texto, crie um novo arquivo **ReportConnectivity.js** na pasta **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-141">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="8e4b6-142">Adicione o seguinte código ao arquivo **ReportConnectivity.js** e substitua o espaço reservado **{cadeia de conexão do dispositivo}** pela cadeia de conexão do dispositivo copiada quando você criou a identidade do dispositivo **myDeviceId**:</span><span class="sxs-lookup"><span data-stu-id="8e4b6-142">Add the following code to the **ReportConnectivity.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="8e4b6-143">O objeto **Client** expõe todos os métodos necessários para você interagir com dispositivos gêmeos a partir do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-143">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="8e4b6-144">O código anterior, depois de inicializar o objeto **Client**, recupera o dispositivo gêmeo para **myDeviceId** e atualiza suas propriedades reportadas com as informações de conectividade.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-144">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
5. <span data-ttu-id="8e4b6-145">Executar o aplicativo do dispositivo</span><span class="sxs-lookup"><span data-stu-id="8e4b6-145">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="8e4b6-146">Você deve ver a mensagem `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-146">You should see the message `twin state reported`.</span></span>
6. <span data-ttu-id="8e4b6-147">Agora que o dispositivo divulgou suas informações de conectividade, ele deve aparecer em ambas as consultas.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-147">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="8e4b6-148">Acesse novamente a pasta **addtagsandqueryapp** e execute as consultas novamente:</span><span class="sxs-lookup"><span data-stu-id="8e4b6-148">Go back in the **addtagsandqueryapp** folder and run the queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="8e4b6-149">Desta vez, **myDeviceId** deve aparecer em ambos os resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="8e4b6-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8e4b6-150">Next steps</span></span>
<span data-ttu-id="8e4b6-151">Neste tutorial, você configurou um novo hub IoT no portal do Azure e depois criou uma identidade do dispositivo no Registro de identidade do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-151">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="8e4b6-152">Você adicionou os metadados do dispositivo como marcações de um aplicativo de back-end e criou um aplicativo de dispositivo simulado para relatar informações de conectividade no dispositivo gêmeo.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-152">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="8e4b6-153">Você também aprendeu a consultar essas informações usando a linguagem de consulta do Hub IoT semelhante ao SQL.</span><span class="sxs-lookup"><span data-stu-id="8e4b6-153">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="8e4b6-154">Veja os recursos a seguir para saber como:</span><span class="sxs-lookup"><span data-stu-id="8e4b6-154">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="8e4b6-155">Enviar telemetria de dispositivos com o tutorial [Introdução ao Hub IoT][lnk-iothub-getstarted],</span><span class="sxs-lookup"><span data-stu-id="8e4b6-155">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="8e4b6-156">configurar dispositivos usando as propriedades desejadas do dispositivo gêmeo com o tutorial [Usar propriedades desejadas para configurar dispositivos][lnk-twin-how-to-configure],</span><span class="sxs-lookup"><span data-stu-id="8e4b6-156">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="8e4b6-157">Controlar dispositivos interativamente (como ativar um ventilador de um aplicativo controlado pelo usuário), com o tutorial [Usar métodos diretos][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="8e4b6-157">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
