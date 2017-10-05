---
title: "Introdução aos dispositivos gêmeos do Hub IoT do Azure (.NET/.NET) | Microsoft Docs"
description: "Como usar dispositivos gêmeos do Hub IoT do Azure para adicionar marcas e usar uma consulta do Hub IoT. Use o SDK do dispositivo IoT do Azure para .NET para implementar o aplicativo de dispositivo simulado e o SDK do serviço IoT do Azure para .NET para implementar um aplicativo de serviço que adiciona as marcas e executa a consulta do Hub IoT."
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
ms.openlocfilehash: 6073d594117e69676b753a1e3af25fffa3583a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="f7c98-104">Introdução aos dispositivos gêmeos (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="f7c98-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="f7c98-105">Ao fim deste tutorial, você terá estes aplicativos de console .NET:</span><span class="sxs-lookup"><span data-stu-id="f7c98-105">At the end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="f7c98-106">**CreateDeviceIdentity**, um aplicativo do .NET que cria uma identidade do dispositivo e uma chave de segurança associada para conectar o aplicativo de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="f7c98-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="f7c98-107">**AddTagsAndQuery**, um aplicativo de back-end .NET que adiciona marcas e consultas aos dispositivos gêmeos.</span><span class="sxs-lookup"><span data-stu-id="f7c98-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="f7c98-108">**ReportConnectivity**, um aplicativo de dispositivo do .NET que simula um dispositivo que se conecta ao seu Hub IoT com a identidade do dispositivo criada anteriormente e reporta sua condição de conectividade.</span><span class="sxs-lookup"><span data-stu-id="f7c98-108">**ReportConnectivity**, a .NET device app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="f7c98-109">O artigo [SDKs do IoT do Azure][lnk-hub-sdks] fornece informações sobre os SDKs do IoT do Azure que você pode usar para compilar dispositivos e aplicativos back-end.</span><span class="sxs-lookup"><span data-stu-id="f7c98-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="f7c98-110">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="f7c98-110">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="f7c98-111">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="f7c98-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="f7c98-112">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7c98-112">An active Azure account.</span></span> <span data-ttu-id="f7c98-113">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="f7c98-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="f7c98-114">Se você deseja criar a identidade do dispositivo de forma programática, leia a seção correspondente no artigo [Conecte seu dispositivo simulado ao Hub IoT usando o .NET][lnk-device-identity-csharp].</span><span class="sxs-lookup"><span data-stu-id="f7c98-114">If you want to create the device identity programmatically instead, read the corresponding section in the [Connect your simulated device to your IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="f7c98-115">Criar o aplicativo do serviço</span><span class="sxs-lookup"><span data-stu-id="f7c98-115">Create the service app</span></span>
<span data-ttu-id="f7c98-116">Nesta seção, você cria um aplicativo de console do .NET (usando C#) que adiciona metadados de local ao dispositivo gêmeo associado a **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="f7c98-116">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="f7c98-117">Ele então consulta os dispositivos gêmeos armazenados no Hub IoT selecionando os dispositivos localizados nos EUA e depois aqueles que relataram a existência de uma conexão celular.</span><span class="sxs-lookup"><span data-stu-id="f7c98-117">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="f7c98-118">No Visual Studio, adicione um projeto da Área de Trabalho Clássica do Windows no Visual C# à solução atual usando o modelo de projeto **Aplicativo do Console** .</span><span class="sxs-lookup"><span data-stu-id="f7c98-118">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="f7c98-119">Nomeie o projeto **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="f7c98-119">Name the project **AddTagsAndQuery**.</span></span>
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]
1. <span data-ttu-id="f7c98-121">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **AddTagsAndQuery** e, em seguida, clique em **Gerenciar Pacotes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="f7c98-121">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="f7c98-122">Na janela **Gerenciador de Pacotes NuGet**, selecione **Procurar** e pesquise por **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="f7c98-122">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="f7c98-123">Selecione **Instalar** para instalar o pacote **Microsoft.Azure.Devices** e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="f7c98-123">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="f7c98-124">O procedimento baixa, instala e adiciona uma referência ao [pacote Nuget do SDK do Dispositivo IoT do Azure][lnk-nuget-service-sdk] e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="f7c98-124">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
1. <span data-ttu-id="f7c98-126">Adicione as instruções `using` abaixo na parte superior do arquivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="f7c98-126">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="f7c98-127">Adicione os seguintes campos à classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="f7c98-127">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="f7c98-128">Substitua o valor do espaço reservado pela cadeia de conexão do Hub IoT criado na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="f7c98-128">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="f7c98-129">Adicione o seguinte método à classe **Programa** :</span><span class="sxs-lookup"><span data-stu-id="f7c98-129">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="f7c98-130">A classe **RegistryManager** expõe todos os métodos necessários para interagir com gêmeos de dispositivo do serviço.</span><span class="sxs-lookup"><span data-stu-id="f7c98-130">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="f7c98-131">O código anterior inicializa primeiro o objeto **registryManager**, depois recupera o dispositivo gêmeo para **myDeviceId** e, finalmente, atualiza as marcações com as informações do local desejado.</span><span class="sxs-lookup"><span data-stu-id="f7c98-131">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="f7c98-132">Após a atualização, ele executa duas consultas: a primeira seleciona somente os dispositivos gêmeos de dispositivos localizados na fábrica de **Redmond43**, enquanto o segundo aperfeiçoa a consulta para selecionar somente os dispositivos que também estão conectados por meio de rede celular.</span><span class="sxs-lookup"><span data-stu-id="f7c98-132">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="f7c98-133">Observe que o código anterior, quando ele cria o objeto **query**, especifica um número máximo de documentos retornados.</span><span class="sxs-lookup"><span data-stu-id="f7c98-133">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="f7c98-134">O objeto **query** contém uma propriedade booliana **HasMoreResults** que você pode usar para invocar os métodos **GetNextAsTwinAsync** várias vezes para recuperar todos os resultados.</span><span class="sxs-lookup"><span data-stu-id="f7c98-134">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="f7c98-135">Um método chamado **GetNextAsJson** está disponível para os resultados que não são de dispositivos gêmeos, por exemplo, resultados de consultas de agregação.</span><span class="sxs-lookup"><span data-stu-id="f7c98-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="f7c98-136">Por fim, adicione as seguintes linhas ao método **Main** :</span><span class="sxs-lookup"><span data-stu-id="f7c98-136">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="f7c98-137">No Gerenciador de Soluções, abra **Definir projetos de StartUp...** e certifique-se de que a **Ação** para o projeto **AddTagsAndQuery** é **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="f7c98-137">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="f7c98-138">Compilar a solução.</span><span class="sxs-lookup"><span data-stu-id="f7c98-138">Build the solution.</span></span>
1. <span data-ttu-id="f7c98-139">Execute esse aplicativo clicando com o botão direito do mouse no projeto **AddTagsAndQuery** e selecionando **Depurar**, seguido de **Iniciar nova instância**.</span><span class="sxs-lookup"><span data-stu-id="f7c98-139">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="f7c98-140">Você deve ver um dispositivo nos resultados da consulta que pergunta sobre todos os dispositivos localizados em **Redmond43**, e nenhum para a consulta que restringe os resultados para dispositivos que usam uma rede de celular.</span><span class="sxs-lookup"><span data-stu-id="f7c98-140">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![Resultados da consulta na janela][img-addtagapp]

<span data-ttu-id="f7c98-142">Na seção seguinte, você cria um aplicativo de dispositivo que reporta as informações de conectividade e altera o resultado da consulta na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="f7c98-142">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="f7c98-143">Criar o aplicativo do dispositivo</span><span class="sxs-lookup"><span data-stu-id="f7c98-143">Create the device app</span></span>
<span data-ttu-id="f7c98-144">Nesta seção, você cria um aplicativo de console do .NET que se conecta ao seu hub como **myDeviceId** e depois atualiza suas propriedades reportadas para conter as informações indicando que ele está conectado usando uma rede celular.</span><span class="sxs-lookup"><span data-stu-id="f7c98-144">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="f7c98-145">No Visual Studio, adicione um projeto da Área de Trabalho Clássica do Windows no Visual C# à solução atual usando o modelo de projeto **Aplicativo do Console** .</span><span class="sxs-lookup"><span data-stu-id="f7c98-145">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="f7c98-146">Nomeie o projeto como **ReportConnectivity**.</span><span class="sxs-lookup"><span data-stu-id="f7c98-146">Name the project **ReportConnectivity**.</span></span>
   
    ![Novo aplicativo de dispositivo Visual C# Windows clássico][img-createdeviceapp]
    
1. <span data-ttu-id="f7c98-148">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **ReportConnectivity** e clique em **Gerenciar Pacotes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="f7c98-148">In Solution Explorer, right-click the **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="f7c98-149">Na janela **Gerenciador de Pacotes NuGet**, selecione **Procurar** e pesquise por **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="f7c98-149">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="f7c98-150">Selecione **Instalar** para instalar o pacote **Microsoft.Azure.Devices.Client** e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="f7c98-150">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="f7c98-151">O procedimento baixa, instala e adiciona uma referência ao [pacote NuGet do SDK do Dispositivo IoT do Azure][lnk-nuget-client-sdk] e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="f7c98-151">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Aplicativo de cliente de janela do Gerenciador de Pacotes NuGet][img-clientnuget]
1. <span data-ttu-id="f7c98-153">Adicione as instruções `using` abaixo na parte superior do arquivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="f7c98-153">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="f7c98-154">Adicione os seguintes campos à classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="f7c98-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="f7c98-155">Substitua o valor de espaço reservado pela cadeia de conexão do dispositivo que você anotou na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="f7c98-155">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="f7c98-156">Adicione o seguinte método à classe **Programa** :</span><span class="sxs-lookup"><span data-stu-id="f7c98-156">Add the following method to the **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting to hub");
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

    <span data-ttu-id="f7c98-157">O objeto **Client** expõe todos os métodos necessários para você interagir com dispositivos gêmeos a partir do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f7c98-157">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="f7c98-158">O código mostrado acima inicializa o objeto **Cliente** e recupera o dispositivo gêmeo para **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="f7c98-158">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="f7c98-159">Adicione o seguinte método à classe **Programa** :</span><span class="sxs-lookup"><span data-stu-id="f7c98-159">Add the following method to the **Program** class:</span></span>
   
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

   <span data-ttu-id="f7c98-160">O código acima atualiza a propriedade relatada de **myDeviceId** com as informações de conectividade.</span><span class="sxs-lookup"><span data-stu-id="f7c98-160">The code above updates **myDeviceId**'s reported property with the connectivity information.</span></span>

1. <span data-ttu-id="f7c98-161">Por fim, adicione as seguintes linhas ao método **Main** :</span><span class="sxs-lookup"><span data-stu-id="f7c98-161">Finally, add the following lines to the **Main** method:</span></span>
   
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
       Console.WriteLine("Press Enter to exit.");
       Console.ReadLine();

1. <span data-ttu-id="f7c98-162">No Gerenciador de Soluções, abra **Definir projetos de StartUp...** e certifique-se de que a **Ação** para o projeto **ReportConnectivity** é **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="f7c98-162">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="f7c98-163">Compilar a solução.</span><span class="sxs-lookup"><span data-stu-id="f7c98-163">Build the solution.</span></span>
1. <span data-ttu-id="f7c98-164">Execute esse aplicativo clicando com o botão direito do mouse no projeto **ReportConnectivity** e selecionando **Depurar**, seguido de **Iniciar nova instância**.</span><span class="sxs-lookup"><span data-stu-id="f7c98-164">Run this application by right-clicking on the **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="f7c98-165">Você deve vê-lo obter as informações de gêmeo e enviar a conectividade como uma *propriedade relatada*.</span><span class="sxs-lookup"><span data-stu-id="f7c98-165">You should see it getting the twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![Execute o aplicativo de dispositivo para conectividade de relatório][img-rundeviceapp]
    
    
1. <span data-ttu-id="f7c98-167">Agora que o dispositivo divulgou suas informações de conectividade, ele deve aparecer em ambas as consultas.</span><span class="sxs-lookup"><span data-stu-id="f7c98-167">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="f7c98-168">Execute o aplicativo .NET **AddTagsAndQuery** para executar as consultas novamente.</span><span class="sxs-lookup"><span data-stu-id="f7c98-168">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="f7c98-169">Desta vez, **myDeviceId** deve aparecer em ambos os resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="f7c98-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![Conectividade do dispositivo relatada com êxito][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="f7c98-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f7c98-171">Next steps</span></span>
<span data-ttu-id="f7c98-172">Neste tutorial, você configurou um novo hub IoT no portal do Azure e depois criou uma identidade do dispositivo no Registro de identidade do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f7c98-172">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="f7c98-173">Você adicionou os metadados do dispositivo como marcações de um aplicativo de back-end e criou um aplicativo de dispositivo simulado para relatar informações de conectividade no dispositivo gêmeo.</span><span class="sxs-lookup"><span data-stu-id="f7c98-173">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="f7c98-174">Você também aprendeu a consultar essas informações usando a linguagem de consulta do Hub IoT semelhante ao SQL.</span><span class="sxs-lookup"><span data-stu-id="f7c98-174">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="f7c98-175">Veja os recursos a seguir para saber como:</span><span class="sxs-lookup"><span data-stu-id="f7c98-175">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="f7c98-176">Enviar telemetria de dispositivos com o tutorial [Introdução ao Hub IoT][lnk-iothub-getstarted],</span><span class="sxs-lookup"><span data-stu-id="f7c98-176">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="f7c98-177">Configurar dispositivos usando as propriedades desejadas do dispositivo gêmeo com o tutorial [Usar propriedades desejadas para configurar dispositivos][lnk-twin-how-to-configure].</span><span class="sxs-lookup"><span data-stu-id="f7c98-177">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="f7c98-178">Controlar dispositivos interativamente (como ativar uma ventoinha de um aplicativo controlado pelo usuário), com o tutorial [Uso de métodos diretos][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="f7c98-178">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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

