---
title: "aaaGet iniciado com twins de dispositivo do Azure IoT Hub (.NET/nó) | Microsoft Docs"
description: "Como toouse Azure IoT Hub dispositivo twins tooadd marcas e, em seguida, use uma consulta de IoT Hub. Usa dispositivo do hello IoT do Azure SDK para Node.js tooimplement Olá dispositivo simulado aplicativo e Olá serviço IoT do Azure SDK para .NET tooimplement um aplicativo de serviço que adiciona marcas hello e executa Olá consulta de IoT Hub."
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
ms.openlocfilehash: 1cec082ebddc19c9b87998a5fd0159d32b07acd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="ef9b4-104">Introdução aos dispositivos gêmeos (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="ef9b4-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="ef9b4-105">No final da saudação deste tutorial, você terá .NET e um aplicativo de console Node. js:</span><span class="sxs-lookup"><span data-stu-id="ef9b4-105">At hello end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="ef9b4-106">**AddTagsAndQuery.sln**, um aplicativo de back-end .NET que adiciona marcas e consultas aos dispositivos gêmeos.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="ef9b4-107">**TwinSimulatedDevice.js**, um aplicativo Node. js que simula um dispositivo que conecta o hub IoT de tooyour com a identidade do dispositivo Olá criada anteriormente e sua condição de conectividade de relatórios.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="ef9b4-108">artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild aplicativos de dispositivo e de back-end.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="ef9b4-109">toocomplete este tutorial, você precisa seguir hello:</span><span class="sxs-lookup"><span data-stu-id="ef9b4-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="ef9b4-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="ef9b4-111">Node.js versão 0.10.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="ef9b4-112">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-112">An active Azure account.</span></span> <span data-ttu-id="ef9b4-113">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="ef9b4-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="ef9b4-114">Criar aplicativo de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="ef9b4-114">Create hello service app</span></span>
<span data-ttu-id="ef9b4-115">Nesta seção, você cria um aplicativo de console do .NET (usando o c#) adiciona duas de dispositivo do local metadados toohello associada **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-115">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="ef9b4-116">Em seguida, consultas twins de dispositivo Olá armazenadas no hub IoT de saudação selecionando Olá dispositivos localizados em Olá nos e hello, em seguida, aqueles que relatou uma conexão de celular.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-116">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="ef9b4-117">No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto toohello atual usando Olá **aplicativo de Console** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-117">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="ef9b4-118">Projeto de saudação do nome **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-118">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]
1. <span data-ttu-id="ef9b4-120">No Gerenciador de soluções, clique com botão direito Olá **AddTagsAndQuery** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="ef9b4-120">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="ef9b4-121">Em Olá **NuGet Package Manager** janela, selecione **procurar** e procure **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="ef9b4-122">Selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="ef9b4-123">Este procedimento faz o download, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
1. <span data-ttu-id="ef9b4-125">Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="ef9b4-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="ef9b4-126">Adicionar Olá toohello campos a seguir **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="ef9b4-127">Substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub hub Olá que você criou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-127">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="ef9b4-128">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="ef9b4-128">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="ef9b4-129">Olá **RegistryManager** classe expõe toointeract necessária do todos os métodos de saudação com twins de dispositivo do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-129">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="ef9b4-130">código anterior Olá primeiro inicializa Olá **registryManager** do objeto, em seguida, recupera Olá duas de dispositivo para **myDeviceId**e finalmente atualiza as marcas com informações de localização de saudação desejada.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-130">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="ef9b4-131">Depois de atualizar, ele executa duas consultas: Olá primeiro seleciona apenas twins de dispositivo de saudação de dispositivos localizados em Olá **Redmond43** fábrica Olá segundo refina Olá consulta tooselect somente Olá dispositivos e também são conectados por meio rede de celular.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-131">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="ef9b4-132">Observe que Olá o código anterior, quando ele cria Olá **consulta** de objeto, especifica um número máximo de documentos retornados.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-132">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="ef9b4-133">Olá **consulta** objeto contém um **HasMoreResults** propriedade booleana que você pode usar o hello tooinvoke **GetNextAsTwinAsync** métodos várias vezes tooretrieve todos os resultados.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-133">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="ef9b4-134">Um método chamado **GetNextAsJson** está disponível para os resultados que não são de dispositivos gêmeos, por exemplo, resultados de consultas de agregação.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="ef9b4-135">Finalmente, adicione Olá toohello linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="ef9b4-135">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="ef9b4-136">Olá Gerenciador de soluções, abra o hello **projetos de inicialização definido...**  e certifique-se de saudação **ação** para **AddTagsAndQuery** projeto é **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-136">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="ef9b4-137">Compile a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-137">Build hello solution.</span></span>
1. <span data-ttu-id="ef9b4-138">Executar este aplicativo clicando em Olá **AddTagsAndQuery** projeto e selecionando **depurar**, seguido por **iniciar nova instância**.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-138">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="ef9b4-139">Você deve ver um dispositivo nos resultados de Olá Olá consulta pedindo para todos os dispositivos localizados no **Redmond43** e nenhuma consulta Olá que restringe Olá resultados toodevices que usam uma rede de celular.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-139">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![Resultados da consulta na janela][img-addtagapp]

<span data-ttu-id="ef9b4-141">Na próxima seção, Olá, você cria um aplicativo de dispositivo com informações de conectividade de saudação e alterações Olá resultado de consulta Olá na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-141">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="ef9b4-142">Criar aplicativo de dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="ef9b4-142">Create hello device app</span></span>
<span data-ttu-id="ef9b4-143">Nesta seção, você cria um aplicativo de console Node. js que conecta o hub tooyour como **myDeviceId**e, em seguida, atualiza as suas informações de saudação de toocontain propriedades relatado que ele está conectado usando uma rede de celular.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-143">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="ef9b4-144">Crie uma nova pasta vazia denominada **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="ef9b4-145">Em Olá **reportconnectivity** pasta, crie um novo arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-145">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="ef9b4-146">Aceite todos os padrões de saudação.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-146">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="ef9b4-147">O prompt de comando no hello **reportconnectivity** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure**, e **azure iot-dispositivo mqtt** pacote :</span><span class="sxs-lookup"><span data-stu-id="ef9b4-147">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="ef9b4-148">Usando um editor de texto, crie um novo **ReportConnectivity.js** arquivo hello **reportconnectivity** pasta.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-148">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="ef9b4-149">Adicionar Olá toohello de código a seguir **ReportConnectivity.js** de arquivo e substitua o espaço reservado de saudação para cadeia de caracteres de conexão de dispositivo com hello um copiadas quando você criou Olá **myDeviceId** dispositivo identidade:</span><span class="sxs-lookup"><span data-stu-id="ef9b4-149">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello placeholder for device connection string with hello one you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="ef9b4-150">Olá **cliente** objeto expõe todos os métodos de saudação exigem toointeract com twins de dispositivo do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-150">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="ef9b4-151">Olá código anterior, depois que ele inicializa Olá **cliente** objeto recupera Olá duas de dispositivo para **myDeviceId** e atualiza sua propriedade relatada com informações de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-151">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
1. <span data-ttu-id="ef9b4-152">Executar o aplicativo de dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="ef9b4-152">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="ef9b4-153">Você verá uma mensagem de saudação `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-153">You should see hello message `twin state reported`.</span></span>
1. <span data-ttu-id="ef9b4-154">Agora que hello dispositivo relatado suas informações de conectividade, ele aparecerá em ambas as consultas.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-154">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="ef9b4-155">Executar Olá .NET **AddTagsAndQuery** saudação do aplicativo toorun consultas novamente.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-155">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="ef9b4-156">Desta vez, **myDeviceId** deve aparecer em ambos os resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="ef9b4-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ef9b4-157">Next steps</span></span>
<span data-ttu-id="ef9b4-158">Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-158">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="ef9b4-159">Você adicionou o metadados do dispositivo como marcas de um aplicativo de back-end e gravou informações de conectividade do dispositivo do dispositivo simulado aplicativo tooreport em duas de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-159">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="ef9b4-160">Você também aprendeu como tooquery essas informações usando a linguagem de consulta do tipo SQL IoT Hub hello.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-160">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="ef9b4-161">Saudação de uso toolearn de recursos a seguir como a:</span><span class="sxs-lookup"><span data-stu-id="ef9b4-161">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="ef9b4-162">Enviar telemetria de dispositivos com hello [começar com o IoT Hub] [ lnk-iothub-getstarted] tutorial,</span><span class="sxs-lookup"><span data-stu-id="ef9b4-162">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="ef9b4-163">Configurar dispositivos com propriedades desejadas de duas dispositivo Olá [uso desejado dispositivos de tooconfigure propriedades] [ lnk-twin-how-to-configure] tutorial,</span><span class="sxs-lookup"><span data-stu-id="ef9b4-163">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="ef9b4-164">controlar dispositivos interativamente (como ativar um ventilador de um aplicativo controlado pelo usuário) com hello [usar métodos diretos] [ lnk-methods-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="ef9b4-164">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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

