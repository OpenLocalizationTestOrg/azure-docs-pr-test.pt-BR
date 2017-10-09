---
title: aaaGet iniciado com twins de dispositivo do Azure IoT Hub (.NET/.NET) | Microsoft Docs
description: "Como toouse Azure IoT Hub dispositivo twins tooadd marcas e, em seguida, use uma consulta de IoT Hub. Você usa dispositivo do hello IoT do Azure SDK para .NET tooimplement Olá dispositivo simulado aplicativo e Olá serviço IoT do Azure SDK para .NET tooimplement um aplicativo de serviço que adiciona marcas hello e executa Olá consulta de IoT Hub."
services: iot-hub
documentationcenter: node
author: dsk-2015
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: dkshir
ms.openlocfilehash: 7fa73ac896c44e79c6522d252cd1515bd6e7bb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="9dd52-104">Introdução aos dispositivos gêmeos (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="9dd52-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="9dd52-105">No final da saudação deste tutorial, você terá esses aplicativos de console .NET:</span><span class="sxs-lookup"><span data-stu-id="9dd52-105">At hello end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="9dd52-106">**CreateDeviceIdentity**, um aplicativo .NET que cria uma identidade de dispositivo e de segurança da chave tooconnect seu aplicativo de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="9dd52-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="9dd52-107">**AddTagsAndQuery**, um aplicativo de back-end .NET que adiciona marcas e consultas aos dispositivos gêmeos.</span><span class="sxs-lookup"><span data-stu-id="9dd52-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="9dd52-108">**ReportConnectivity**, um aplicativo de dispositivo de .NET que simula um dispositivo que conecta o hub IoT de tooyour com a identidade do dispositivo Olá criada anteriormente e sua condição de conectividade de relatórios.</span><span class="sxs-lookup"><span data-stu-id="9dd52-108">**ReportConnectivity**, a .NET device app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="9dd52-109">artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild aplicativos de dispositivo e de back-end.</span><span class="sxs-lookup"><span data-stu-id="9dd52-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="9dd52-110">toocomplete este tutorial, você precisa seguir hello:</span><span class="sxs-lookup"><span data-stu-id="9dd52-110">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="9dd52-111">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9dd52-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="9dd52-112">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dd52-112">An active Azure account.</span></span> <span data-ttu-id="9dd52-113">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="9dd52-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="9dd52-114">Identidade do dispositivo Olá toocreate programaticamente em vez disso, leia seção correspondente Olá Olá [conecte seu dispositivo simulado tooyour IoT hub que usando o .NET] [ lnk-device-identity-csharp] artigo.</span><span class="sxs-lookup"><span data-stu-id="9dd52-114">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="9dd52-115">Criar aplicativo de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="9dd52-115">Create hello service app</span></span>
<span data-ttu-id="9dd52-116">Nesta seção, você cria um aplicativo de console do .NET (usando o c#) adiciona duas de dispositivo do local metadados toohello associada **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="9dd52-116">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="9dd52-117">Em seguida, consultas twins de dispositivo Olá armazenadas no hub IoT de saudação selecionando Olá dispositivos localizados em Olá nos e hello, em seguida, aqueles que relatou uma conexão de celular.</span><span class="sxs-lookup"><span data-stu-id="9dd52-117">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="9dd52-118">No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto toohello atual usando Olá **aplicativo de Console** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="9dd52-118">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="9dd52-119">Projeto de saudação do nome **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="9dd52-119">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]
1. <span data-ttu-id="9dd52-121">No Gerenciador de soluções, clique com botão direito Olá **AddTagsAndQuery** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="9dd52-121">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="9dd52-122">Em Olá **NuGet Package Manager** janela, selecione **procurar** e procure **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="9dd52-122">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="9dd52-123">Selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="9dd52-123">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="9dd52-124">Este procedimento faz o download, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="9dd52-124">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
1. <span data-ttu-id="9dd52-126">Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="9dd52-126">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="9dd52-127">Adicionar Olá toohello campos a seguir **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="9dd52-127">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="9dd52-128">Substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub hub Olá que você criou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="9dd52-128">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="9dd52-129">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="9dd52-129">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="9dd52-130">Olá **RegistryManager** classe expõe toointeract necessária do todos os métodos de saudação com twins de dispositivo do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="9dd52-130">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="9dd52-131">código anterior Olá primeiro inicializa Olá **registryManager** do objeto, em seguida, recupera Olá duas de dispositivo para **myDeviceId**e finalmente atualiza as marcas com informações de localização de saudação desejada.</span><span class="sxs-lookup"><span data-stu-id="9dd52-131">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="9dd52-132">Depois de atualizar, ele executa duas consultas: Olá primeiro seleciona apenas twins de dispositivo de saudação de dispositivos localizados em Olá **Redmond43** fábrica Olá segundo refina Olá consulta tooselect somente Olá dispositivos e também são conectados por meio rede de celular.</span><span class="sxs-lookup"><span data-stu-id="9dd52-132">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="9dd52-133">Observe que Olá o código anterior, quando ele cria Olá **consulta** de objeto, especifica um número máximo de documentos retornados.</span><span class="sxs-lookup"><span data-stu-id="9dd52-133">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="9dd52-134">Olá **consulta** objeto contém um **HasMoreResults** propriedade booleana que você pode usar o hello tooinvoke **GetNextAsTwinAsync** métodos várias vezes tooretrieve todos os resultados.</span><span class="sxs-lookup"><span data-stu-id="9dd52-134">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="9dd52-135">Um método chamado **GetNextAsJson** está disponível para os resultados que não são de dispositivos gêmeos, por exemplo, resultados de consultas de agregação.</span><span class="sxs-lookup"><span data-stu-id="9dd52-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="9dd52-136">Finalmente, adicione Olá toohello linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="9dd52-136">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="9dd52-137">Olá Gerenciador de soluções, abra o hello **projetos de inicialização definido...**  e certifique-se de saudação **ação** para **AddTagsAndQuery** projeto é **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="9dd52-137">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="9dd52-138">Compile a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="9dd52-138">Build hello solution.</span></span>
1. <span data-ttu-id="9dd52-139">Executar este aplicativo clicando em Olá **AddTagsAndQuery** projeto e selecionando **depurar**, seguido por **iniciar nova instância**.</span><span class="sxs-lookup"><span data-stu-id="9dd52-139">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="9dd52-140">Você deve ver um dispositivo nos resultados de Olá Olá consulta pedindo para todos os dispositivos localizados no **Redmond43** e nenhuma consulta Olá que restringe Olá resultados toodevices que usam uma rede de celular.</span><span class="sxs-lookup"><span data-stu-id="9dd52-140">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![Resultados da consulta na janela][img-addtagapp]

<span data-ttu-id="9dd52-142">Na próxima seção, Olá, você cria um aplicativo de dispositivo com informações de conectividade de saudação e alterações Olá resultado de consulta Olá na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="9dd52-142">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="9dd52-143">Criar aplicativo de dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="9dd52-143">Create hello device app</span></span>
<span data-ttu-id="9dd52-144">Nesta seção, você cria um aplicativo de console .NET que conecta o hub tooyour como **myDeviceId**e, em seguida, atualiza as suas informações de saudação de toocontain propriedades relatado que ele está conectado usando uma rede de celular.</span><span class="sxs-lookup"><span data-stu-id="9dd52-144">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="9dd52-145">No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto toohello atual usando Olá **aplicativo de Console** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="9dd52-145">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="9dd52-146">Projeto de saudação do nome **ReportConnectivity**.</span><span class="sxs-lookup"><span data-stu-id="9dd52-146">Name hello project **ReportConnectivity**.</span></span>
   
    ![Novo aplicativo de dispositivo Visual C# Windows clássico][img-createdeviceapp]
    
1. <span data-ttu-id="9dd52-148">No Gerenciador de soluções, clique com botão direito Olá **ReportConnectivity** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="9dd52-148">In Solution Explorer, right-click hello **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="9dd52-149">Em Olá **NuGet Package Manager** janela, selecione **procurar** e procure **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="9dd52-149">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="9dd52-150">Selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices.Client** empacotar e aceitar os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="9dd52-150">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="9dd52-151">Este procedimento faz o download, instala e adiciona uma referência toohello [dispositivo IoT do Azure SDK] [ lnk-nuget-client-sdk] NuGet pacote e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="9dd52-151">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Aplicativo de cliente de janela do Gerenciador de Pacotes NuGet][img-clientnuget]
1. <span data-ttu-id="9dd52-153">Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="9dd52-153">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="9dd52-154">Adicionar Olá toohello campos a seguir **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="9dd52-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="9dd52-155">Substitua o valor de espaço reservado de saudação com cadeia de conexão do dispositivo Olá observado na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="9dd52-155">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="9dd52-156">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="9dd52-156">Add hello following method toohello **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
                Console.WriteLine("Retrieving twin");
                await Client.GetTwinAsync();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="9dd52-157">Olá **cliente** objeto expõe todos os métodos de saudação exigem toointeract com twins de dispositivo do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="9dd52-157">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="9dd52-158">Olá código mostrado acima, inicializa Olá **cliente** objeto e, em seguida, recupera Olá dispositivo duas para **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="9dd52-158">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="9dd52-159">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="9dd52-159">Add hello following method toohello **Program** class:</span></span>
   
        public static async void ReportConnectivity()
        {
            try
            {
                Console.WriteLine("Sending connectivity data as reported property");
                
                TwinCollection reportedProperties, connectivity;
                reportedProperties = new TwinCollection();
                connectivity = new TwinCollection();
                connectivity["type"] = "cellular";
                reportedProperties["connectivity"] = connectivity;
                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

   <span data-ttu-id="9dd52-160">Olá código acima atualizações **myDeviceId**do relatado propriedade com informações de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="9dd52-160">hello code above updates **myDeviceId**'s reported property with hello connectivity information.</span></span>

1. <span data-ttu-id="9dd52-161">Finalmente, adicione Olá toohello linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="9dd52-161">Finally, add hello following lines toohello **Main** method:</span></span>
   
       try
       {
            InitClient();
            ReportConnectivity();
       }
       catch (Exception ex)
       {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
       }
       Console.WriteLine("Press Enter tooexit.");
       Console.ReadLine();

1. <span data-ttu-id="9dd52-162">Olá Gerenciador de soluções, abra o hello **projetos de inicialização definido...**  e certifique-se de saudação **ação** para **ReportConnectivity** projeto é **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="9dd52-162">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="9dd52-163">Compile a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="9dd52-163">Build hello solution.</span></span>
1. <span data-ttu-id="9dd52-164">Executar este aplicativo clicando em Olá **ReportConnectivity** projeto e selecionando **depurar**, seguido por **iniciar nova instância**.</span><span class="sxs-lookup"><span data-stu-id="9dd52-164">Run this application by right-clicking on hello **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="9dd52-165">Você deve ver obtendo Olá duas informações e, em seguida, enviar conectividade como uma *relatado propriedade*.</span><span class="sxs-lookup"><span data-stu-id="9dd52-165">You should see it getting hello twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![Execute conectividade de tooreport do aplicativo de dispositivo][img-rundeviceapp]
    
    
1. <span data-ttu-id="9dd52-167">Agora que hello dispositivo relatado suas informações de conectividade, ele aparecerá em ambas as consultas.</span><span class="sxs-lookup"><span data-stu-id="9dd52-167">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="9dd52-168">Executar Olá .NET **AddTagsAndQuery** saudação do aplicativo toorun consultas novamente.</span><span class="sxs-lookup"><span data-stu-id="9dd52-168">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="9dd52-169">Desta vez, **myDeviceId** deve aparecer em ambos os resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="9dd52-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![Conectividade do dispositivo relatada com êxito][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="9dd52-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9dd52-171">Next steps</span></span>
<span data-ttu-id="9dd52-172">Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello.</span><span class="sxs-lookup"><span data-stu-id="9dd52-172">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="9dd52-173">Você adicionou o metadados do dispositivo como marcas de um aplicativo de back-end e gravou informações de conectividade do dispositivo do dispositivo simulado aplicativo tooreport em duas de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9dd52-173">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="9dd52-174">Você também aprendeu como tooquery essas informações usando a linguagem de consulta do tipo SQL IoT Hub hello.</span><span class="sxs-lookup"><span data-stu-id="9dd52-174">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="9dd52-175">Saudação de uso toolearn de recursos a seguir como a:</span><span class="sxs-lookup"><span data-stu-id="9dd52-175">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="9dd52-176">Enviar telemetria de dispositivos com hello [começar com o IoT Hub] [ lnk-iothub-getstarted] tutorial,</span><span class="sxs-lookup"><span data-stu-id="9dd52-176">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="9dd52-177">Configurar dispositivos com propriedades desejadas de duas dispositivo Olá [uso desejado dispositivos de tooconfigure propriedades] [ lnk-twin-how-to-configure] tutorial,</span><span class="sxs-lookup"><span data-stu-id="9dd52-177">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="9dd52-178">controlar dispositivos interativamente (como ativar um ventilador de um aplicativo controlado pelo usuário) com hello [usar métodos diretos] [ lnk-methods-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="9dd52-178">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png
[img-rundeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png
[img-tagappsuccess]: media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

