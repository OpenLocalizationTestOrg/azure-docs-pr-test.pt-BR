---
title: "Introdução aos dispositivos gêmeos do Hub IoT do Azure (.NET/Node) | Microsoft Docs"
description: "Como usar dispositivos gêmeos do Hub IoT do Azure para adicionar marcas e usar uma consulta do Hub IoT. Use o SDK do dispositivo IoT do Azure para Node.js para implementar o aplicativo de dispositivo simulado e o SDK do serviço IoT do Azure para .NET para implementar um aplicativo de serviço que adiciona as marcas e executa a consulta do Hub IoT."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: elioda
ms.openlocfilehash: 07797b9159c9b926e9eb47d8864c63048951931a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="dd7d0-104">Introdução aos dispositivos gêmeos (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="dd7d0-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="dd7d0-105">No fim deste tutorial, você terá dois aplicativos de console, um .NET e um Node.js:</span><span class="sxs-lookup"><span data-stu-id="dd7d0-105">At the end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="dd7d0-106">**AddTagsAndQuery.sln**, um aplicativo de back-end .NET que adiciona marcas e consultas aos dispositivos gêmeos.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="dd7d0-107">**TwinSimulatedDevice.js**, um aplicativo Node.js que simula um dispositivo que se conecta ao seu Hub IoT com a identidade do dispositivo criada anteriormente e reporta sua condição de conectividade.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="dd7d0-108">O artigo [SDKs do IoT do Azure][lnk-hub-sdks] fornece informações sobre os SDKs do IoT do Azure que você pode usar para compilar dispositivos e aplicativos back-end.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="dd7d0-109">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="dd7d0-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="dd7d0-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="dd7d0-111">Node.js versão 0.10.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="dd7d0-112">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-112">An active Azure account.</span></span> <span data-ttu-id="dd7d0-113">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="dd7d0-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="dd7d0-114">Criar o aplicativo do serviço</span><span class="sxs-lookup"><span data-stu-id="dd7d0-114">Create the service app</span></span>
<span data-ttu-id="dd7d0-115">Nesta seção, você cria um aplicativo de console do .NET (usando C#) que adiciona metadados de local ao dispositivo gêmeo associado a **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-115">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="dd7d0-116">Ele então consulta os dispositivos gêmeos armazenados no Hub IoT selecionando os dispositivos localizados nos EUA e depois aqueles que relataram a existência de uma conexão celular.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-116">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="dd7d0-117">No Visual Studio, adicione um projeto da Área de Trabalho Clássica do Windows no Visual C# à solução atual usando o modelo de projeto **Aplicativo do Console** .</span><span class="sxs-lookup"><span data-stu-id="dd7d0-117">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="dd7d0-118">Nomeie o projeto **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-118">Name the project **AddTagsAndQuery**.</span></span>
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]
1. <span data-ttu-id="dd7d0-120">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **AddTagsAndQuery** e, em seguida, clique em **Gerenciar Pacotes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-120">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="dd7d0-121">Na janela **Gerenciador de Pacotes NuGet**, selecione **Procurar** e pesquise por **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-121">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="dd7d0-122">Selecione **Instalar** para instalar o pacote **Microsoft.Azure.Devices** e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-122">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="dd7d0-123">O procedimento baixa, instala e adiciona uma referência ao [pacote Nuget do SDK do Dispositivo IoT do Azure][lnk-nuget-service-sdk] e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-123">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
1. <span data-ttu-id="dd7d0-125">Adicione as instruções `using` abaixo na parte superior do arquivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="dd7d0-125">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="dd7d0-126">Adicione os seguintes campos à classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="dd7d0-126">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="dd7d0-127">Substitua o valor do espaço reservado pela cadeia de conexão do Hub IoT criado na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-127">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="dd7d0-128">Adicione o seguinte método à classe **Programa** :</span><span class="sxs-lookup"><span data-stu-id="dd7d0-128">Add the following method to the **Program** class:</span></span>
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    <span data-ttu-id="dd7d0-129">A classe **RegistryManager** expõe todos os métodos necessários para interagir com gêmeos de dispositivo do serviço.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-129">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="dd7d0-130">O código anterior inicializa primeiro o objeto **registryManager**, depois recupera o dispositivo gêmeo para **myDeviceId** e, finalmente, atualiza as marcações com as informações do local desejado.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-130">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="dd7d0-131">Após a atualização, ele executa duas consultas: a primeira seleciona somente os dispositivos gêmeos de dispositivos localizados na fábrica de **Redmond43**, enquanto o segundo aperfeiçoa a consulta para selecionar somente os dispositivos que também estão conectados por meio de rede celular.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-131">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="dd7d0-132">Observe que o código anterior, quando ele cria o objeto **query**, especifica um número máximo de documentos retornados.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-132">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="dd7d0-133">O objeto **query** contém uma propriedade booliana **HasMoreResults** que você pode usar para invocar os métodos **GetNextAsTwinAsync** várias vezes para recuperar todos os resultados.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-133">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="dd7d0-134">Um método chamado **GetNextAsJson** está disponível para os resultados que não são de dispositivos gêmeos, por exemplo, resultados de consultas de agregação.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="dd7d0-135">Por fim, adicione as seguintes linhas ao método **Main** :</span><span class="sxs-lookup"><span data-stu-id="dd7d0-135">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="dd7d0-136">No Gerenciador de Soluções, abra **Definir projetos de StartUp...** e certifique-se de que a **Ação** para o projeto **AddTagsAndQuery** é **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-136">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="dd7d0-137">Compilar a solução.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-137">Build the solution.</span></span>
1. <span data-ttu-id="dd7d0-138">Execute esse aplicativo clicando com o botão direito do mouse no projeto **AddTagsAndQuery** e selecionando **Depurar**, seguido de **Iniciar nova instância**.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-138">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="dd7d0-139">Você deve ver um dispositivo nos resultados da consulta que pergunta sobre todos os dispositivos localizados em **Redmond43**, e nenhum para a consulta que restringe os resultados para dispositivos que usam uma rede de celular.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-139">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![Resultados da consulta na janela][img-addtagapp]

<span data-ttu-id="dd7d0-141">Na seção seguinte, você cria um aplicativo de dispositivo que reporta as informações de conectividade e altera o resultado da consulta na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-141">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="dd7d0-142">Criar o aplicativo do dispositivo</span><span class="sxs-lookup"><span data-stu-id="dd7d0-142">Create the device app</span></span>
<span data-ttu-id="dd7d0-143">Nesta seção, você cria um aplicativo de console do Node.js que se conecta ao seu hub como **myDeviceId** e depois atualiza suas propriedades reportadas para conter as informações indicando que ele está conectado usando uma rede celular.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-143">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="dd7d0-144">Crie uma nova pasta vazia denominada **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="dd7d0-145">Na pasta **reportconnectivity**, crie um novo arquivo package.json usando o comando a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-145">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="dd7d0-146">Aceite todos os padrões.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-146">Accept all the defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="dd7d0-147">No prompt de comando, na pasta **reportconnectivity**, execute o seguinte comando para instalar os pacotes **azure-iot-device** e **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="dd7d0-147">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="dd7d0-148">Usando um editor de texto, crie um novo arquivo **ReportConnectivity.js** na pasta **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-148">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="dd7d0-149">Adicione o código a seguir ao arquivo **ReportConnectivity.js** e substitua o espaço reservado da cadeia de conexão do dispositivo por aquela copiada quando você criou a identidade do dispositivo **myDeviceId**:</span><span class="sxs-lookup"><span data-stu-id="dd7d0-149">Add the following code to the **ReportConnectivity.js** file, and substitute the placeholder for device connection string with the one you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="dd7d0-150">O objeto **Client** expõe todos os métodos necessários para você interagir com dispositivos gêmeos a partir do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-150">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="dd7d0-151">O código anterior, depois de inicializar o objeto **Client**, recupera o dispositivo gêmeo para **myDeviceId** e atualiza suas propriedades reportadas com as informações de conectividade.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-151">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
1. <span data-ttu-id="dd7d0-152">Executar o aplicativo do dispositivo</span><span class="sxs-lookup"><span data-stu-id="dd7d0-152">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="dd7d0-153">Você deve ver a mensagem `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-153">You should see the message `twin state reported`.</span></span>
1. <span data-ttu-id="dd7d0-154">Agora que o dispositivo divulgou suas informações de conectividade, ele deve aparecer em ambas as consultas.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-154">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="dd7d0-155">Execute o aplicativo .NET **AddTagsAndQuery** para executar as consultas novamente.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-155">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="dd7d0-156">Desta vez, **myDeviceId** deve aparecer em ambos os resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="dd7d0-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dd7d0-157">Next steps</span></span>
<span data-ttu-id="dd7d0-158">Neste tutorial, você configurou um novo hub IoT no portal do Azure e depois criou uma identidade do dispositivo no Registro de identidade do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-158">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="dd7d0-159">Você adicionou os metadados do dispositivo como marcações de um aplicativo de back-end e criou um aplicativo de dispositivo simulado para relatar informações de conectividade no dispositivo gêmeo.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-159">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="dd7d0-160">Você também aprendeu a consultar essas informações usando a linguagem de consulta do Hub IoT semelhante ao SQL.</span><span class="sxs-lookup"><span data-stu-id="dd7d0-160">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="dd7d0-161">Veja os recursos a seguir para saber como:</span><span class="sxs-lookup"><span data-stu-id="dd7d0-161">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="dd7d0-162">Enviar telemetria de dispositivos com o tutorial [Introdução ao Hub IoT][lnk-iothub-getstarted],</span><span class="sxs-lookup"><span data-stu-id="dd7d0-162">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="dd7d0-163">Configurar dispositivos usando as propriedades desejadas do dispositivo gêmeo com o tutorial [Usar propriedades desejadas para configurar dispositivos][lnk-twin-how-to-configure].</span><span class="sxs-lookup"><span data-stu-id="dd7d0-163">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="dd7d0-164">Controlar dispositivos interativamente (como ativar uma ventoinha de um aplicativo controlado pelo usuário), com o tutorial [Uso de métodos diretos][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="dd7d0-164">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-node-twin-getstarted/addtagapp.png
[img-addtagapp2]: media/iot-hub-csharp-node-twin-getstarted/addtagapp2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

