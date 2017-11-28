---
title: "Usar as propriedades do dispositivo gêmeo do Hub IoT do Azure (.NET/Node) | Microsoft Docs"
description: "Como usar dispositivos gêmeos do Hub IoT do Azure para configurar dispositivos. Use o SDK do dispositivo IoT do Azure para .NET para implementar um aplicativo de dispositivo simulado e o SDK do serviço IoT do Azure para .NET para implementar um aplicativo de serviço que modifique uma configuração de dispositivo usando um dispositivo gêmeo."
services: iot-hub
documentationcenter: .net
author: dsk-2015
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dkshir
ms.openlocfilehash: 679cda28bf3ce9fb207fe3693a3453b355f1de15
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="use-desired-properties-to-configure-devices"></a><span data-ttu-id="3b057-104">Usar as propriedades desejadas para configurar os dispositivos</span><span class="sxs-lookup"><span data-stu-id="3b057-104">Use desired properties to configure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="3b057-105">No fim deste tutorial, você terá dois aplicativos de console .NET:</span><span class="sxs-lookup"><span data-stu-id="3b057-105">At the end of this tutorial, you will have two .NET console apps:</span></span>

* <span data-ttu-id="3b057-106">**SimulateDeviceConfiguration.js**, um aplicativo de dispositivo simulado que aguarda uma atualização da configuração desejada e reporta o status de um processo simulado de atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="3b057-106">**SimulateDeviceConfiguration**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="3b057-107">**SetDesiredConfigurationAndQuery**, um aplicativo de back-end que define a configuração desejada em um dispositivo e consulta o processo de atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="3b057-107">**SetDesiredConfigurationAndQuery**, a back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="3b057-108">O artigo [SDKs do IoT do Azure][lnk-hub-sdks] fornece informações sobre os SDKs do IoT do Azure que você pode usar para compilar dispositivos e aplicativos back-end.</span><span class="sxs-lookup"><span data-stu-id="3b057-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="3b057-109">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="3b057-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="3b057-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3b057-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="3b057-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b057-111">An active Azure account.</span></span> <span data-ttu-id="3b057-112">Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="3b057-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="3b057-113">Caso tenha seguido o tutorial [Introdução aos dispositivos gêmeos][lnk-twin-tutorial], você já terá um Hub IoT e uma identidade de dispositivo chamada **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="3b057-113">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="3b057-114">Nesse caso, você pode pular para a seção [Criar o aplicativo do dispositivo simulado][lnk-how-to-configure-createapp].</span><span class="sxs-lookup"><span data-stu-id="3b057-114">In that case, you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-the-simulated-device-app"></a><span data-ttu-id="3b057-115">Criar o aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="3b057-115">Create the simulated device app</span></span>
<span data-ttu-id="3b057-116">Nesta seção, você cria um aplicativo de console .NET que se conecta ao seu hub como **myDeviceId**, aguarda uma atualização de configuração desejada e, em seguida, reporta atualizações sobre o processo simulado de atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="3b057-116">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="3b057-117">No Visual Studio, crie um projeto da Área de Trabalho Clássica do Windows no Visual C# usando o modelo de projeto **Aplicativo de Console**.</span><span class="sxs-lookup"><span data-stu-id="3b057-117">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using the **Console Application** project template.</span></span> <span data-ttu-id="3b057-118">Dê ao projeto o nome de **SimulateDeviceConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="3b057-118">Name the project **SimulateDeviceConfiguration**.</span></span>
   
    ![Novo aplicativo de dispositivo Visual C# Windows clássico][img-createdeviceapp]

1. <span data-ttu-id="3b057-120">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **SimulateDeviceConfiguration** e, em seguida, clique em **Gerenciar Pacotes NuGet…**.</span><span class="sxs-lookup"><span data-stu-id="3b057-120">In Solution Explorer, right-click the **SimulateDeviceConfiguration** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="3b057-121">Na janela **Gerenciador de Pacotes NuGet**, selecione **Procurar** e pesquise por **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="3b057-121">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="3b057-122">Selecione **Instalar** para instalar o pacote **Microsoft.Azure.Devices.Client** e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="3b057-122">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="3b057-123">O procedimento baixa, instala e adiciona uma referência ao [pacote NuGet do SDK do Dispositivo IoT do Azure][lnk-nuget-client-sdk] e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="3b057-123">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Aplicativo de cliente de janela do Gerenciador de Pacotes NuGet][img-clientnuget]
1. <span data-ttu-id="3b057-125">Adicione as instruções `using` abaixo na parte superior do arquivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="3b057-125">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="3b057-126">Adicione os seguintes campos à classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="3b057-126">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="3b057-127">Substitua o valor de espaço reservado pela cadeia de conexão do dispositivo que você anotou na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="3b057-127">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. <span data-ttu-id="3b057-128">Adicione o seguinte método à classe **Programa** :</span><span class="sxs-lookup"><span data-stu-id="3b057-128">Add the following method to the **Program** class:</span></span>
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting to hub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    <span data-ttu-id="3b057-129">O objeto **Client** expõe todos os métodos necessários para você interagir com dispositivos gêmeos a partir do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3b057-129">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="3b057-130">O código mostrado acima inicializa o objeto **Cliente** e recupera o dispositivo gêmeo para **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="3b057-130">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="3b057-131">Adicione o seguinte método à classe **Programa**.</span><span class="sxs-lookup"><span data-stu-id="3b057-131">Add the following method to the **Program** class.</span></span> <span data-ttu-id="3b057-132">Esse método define os valores iniciais de telemetria no dispositivo local e, em seguida, atualiza o dispositivo gêmeo.</span><span class="sxs-lookup"><span data-stu-id="3b057-132">This method sets the initial values of telemetry on the local device and then updates the device twin.</span></span>

        public static async void InitTelemetry()
        {
            try
            {
                Console.WriteLine("Report initial telemetry config:");
                TwinCollection telemetryConfig = new TwinCollection();
                
                telemetryConfig["configId"] = "0";
                telemetryConfig["sendFrequency"] = "24h";
                reportedProperties["telemetryConfig"] = telemetryConfig;
                Console.WriteLine(JsonConvert.SerializeObject(reportedProperties));

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="3b057-133">Adicione o seguinte método à classe **Programa**.</span><span class="sxs-lookup"><span data-stu-id="3b057-133">Add the following method to the **Program** class.</span></span> <span data-ttu-id="3b057-134">Isso é um retorno de chamada que detectará uma alteração nas *propriedades desejadas* no dispositivo gêmeo.</span><span class="sxs-lookup"><span data-stu-id="3b057-134">This is a callback which will detect a change in *desired properties* in the device twin.</span></span>

        private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, object userContext)
        {
            try
            {
                Console.WriteLine("Desired property change:");
                Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

                var currentTelemetryConfig = reportedProperties["telemetryConfig"];
                var desiredTelemetryConfig = desiredProperties["telemetryConfig"];

                if ((desiredTelemetryConfig != null) && (desiredTelemetryConfig["configId"] != currentTelemetryConfig["configId"]))
                {
                    Console.WriteLine("\nInitiating config change");
                    currentTelemetryConfig["status"] = "Pending";
                    currentTelemetryConfig["pendingConfig"] = desiredTelemetryConfig;

                    await Client.UpdateReportedPropertiesAsync(reportedProperties);

                    CompleteConfigChange();
                }
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="3b057-135">Esse método atualiza as propriedades relatadas no objeto do dispositivo gêmeo local com a solicitação de atualização de configuração e define o status como **Pendente**, então atualiza o dispositivo gêmeo no serviço.</span><span class="sxs-lookup"><span data-stu-id="3b057-135">This method updates the reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="3b057-136">Depois de atualizar com êxito o dispositivo gêmeo, ele conclui a mudança de configuração chamando o método `CompleteConfigChange` descrito no próximo ponto.</span><span class="sxs-lookup"><span data-stu-id="3b057-136">After successfully updating the device twin, it completes the config change by calling the method `CompleteConfigChange` described in the next point.</span></span>

1. <span data-ttu-id="3b057-137">Adicione o seguinte método à classe **Programa**.</span><span class="sxs-lookup"><span data-stu-id="3b057-137">Add the following method to the **Program** class.</span></span> <span data-ttu-id="3b057-138">Esse método simula uma redefinição do dispositivo, em seguida, atualiza as propriedades relatadas do local configurando o status como **Êxito** e remove o elemento **pendingConfig**.</span><span class="sxs-lookup"><span data-stu-id="3b057-138">This method simulates a device reset, then updates the local reported properties setting the status to **Success** and removes the **pendingConfig** element.</span></span> <span data-ttu-id="3b057-139">Em seguida, ele atualiza o dispositivo gêmeo no serviço.</span><span class="sxs-lookup"><span data-stu-id="3b057-139">It then updates the device twin on the service.</span></span> 

        public static async void CompleteConfigChange()
        {
            try
            {
                var currentTelemetryConfig = reportedProperties["telemetryConfig"];

                Console.WriteLine("\nSimulating device reset");
                await Task.Delay(30000); 

                Console.WriteLine("\nCompleting config change");
                currentTelemetryConfig["configId"] = currentTelemetryConfig["pendingConfig"]["configId"];
                currentTelemetryConfig["sendFrequency"] = currentTelemetryConfig["pendingConfig"]["sendFrequency"];
                currentTelemetryConfig["status"] = "Success";
                currentTelemetryConfig["pendingConfig"] = null;

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
                Console.WriteLine("Config change complete \nPress any key to exit.");
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="3b057-140">Por fim, adicione as seguintes linhas ao método **Principal**:</span><span class="sxs-lookup"><span data-stu-id="3b057-140">Finally add the following lines to the **Main** method:</span></span>

        try
        {
            InitClient();
            InitTelemetry();

            Console.WriteLine("Wait for desired telemetry...");
            Client.SetDesiredPropertyUpdateCallback(OnDesiredPropertyChanged, null).Wait();
            Console.ReadKey();
        }
        catch (AggregateException ex)
        {
            foreach (Exception exception in ex.InnerExceptions)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", exception);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }

   > [!NOTE]
   > <span data-ttu-id="3b057-141">Este tutorial não simula nenhum comportamento para atualizações de configuração simultâneas.</span><span class="sxs-lookup"><span data-stu-id="3b057-141">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="3b057-142">Alguns processos de atualização de configuração podem ser capazes de acomodar as alterações de configuração de destino enquanto a atualização está em execução, outros podem colocá-las em fila e outros poderiam ainda rejeitá-las com uma condição de erro.</span><span class="sxs-lookup"><span data-stu-id="3b057-142">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, some might have to queue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="3b057-143">Certifique-se de considerar o comportamento desejado para o seu processo de configuração específico e adicione a lógica apropriada antes de iniciar a alteração de configuração.</span><span class="sxs-lookup"><span data-stu-id="3b057-143">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="3b057-144">Compile a solução e, em seguida, execute o aplicativo de dispositivo do Visual Studio clicando em **F5**.</span><span class="sxs-lookup"><span data-stu-id="3b057-144">Build the solution and then run the device app from Visual Studio by clicking **F5**.</span></span> <span data-ttu-id="3b057-145">No console de saída, você deve ver as mensagens indicando que o seu dispositivo simulado está recuperando o dispositivo gêmeo, configurando a telemetria e aguardando a alteração da propriedade desejada.</span><span class="sxs-lookup"><span data-stu-id="3b057-145">On the output console, you should see the messages indicating that your simulated device is retrieving the device twin, setting up the telemetry, and waiting for desired property change.</span></span> <span data-ttu-id="3b057-146">Mantenha o aplicativo em execução.</span><span class="sxs-lookup"><span data-stu-id="3b057-146">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="3b057-147">Criar o aplicativo do serviço</span><span class="sxs-lookup"><span data-stu-id="3b057-147">Create the service app</span></span>
<span data-ttu-id="3b057-148">Nesta seção, você criará um aplicativo de console .NET que atualiza as *propriedades desejadas* no dispositivo gêmeo associado à **myDeviceId** com um novo objeto de configuração de telemetria.</span><span class="sxs-lookup"><span data-stu-id="3b057-148">In this section, you will create a .NET console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="3b057-149">Ele então consulta os dispositivos gêmeos armazenados no Hub IoT e mostra a diferença entre as configurações desejadas e reportadas do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3b057-149">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="3b057-150">No Visual Studio, adicione um projeto da Área de Trabalho Clássica do Windows no Visual C# à solução atual usando o modelo de projeto **Aplicativo do Console** .</span><span class="sxs-lookup"><span data-stu-id="3b057-150">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="3b057-151">Nomeie o projeto **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="3b057-151">Name the project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]
1. <span data-ttu-id="3b057-153">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **SetDesiredConfigurationAndQuery** e clique em **Gerenciar Pacotes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="3b057-153">In Solution Explorer, right-click the **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="3b057-154">Na janela **Gerenciador de Pacotes Nuget**, selecione **Procurar**, procure **microsoft.azure.devices**, selecione **Instalar** para instalar o pacote **Microsoft.Azure.Devices** e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="3b057-154">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="3b057-155">O procedimento baixa, instala e adiciona uma referência ao [pacote Nuget do SDK do Dispositivo IoT do Azure][lnk-nuget-service-sdk] e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="3b057-155">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
1. <span data-ttu-id="3b057-157">Adicione as instruções `using` abaixo na parte superior do arquivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="3b057-157">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="3b057-158">Adicione os seguintes campos à classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="3b057-158">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="3b057-159">Substitua o valor do espaço reservado pela cadeia de conexão do Hub IoT criado na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="3b057-159">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="3b057-160">Adicione o seguinte método à classe **Programa** :</span><span class="sxs-lookup"><span data-stu-id="3b057-160">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="3b057-161">O objeto **Registry** expõe todos os métodos necessários para interagir com gêmeos de dispositivo do serviço.</span><span class="sxs-lookup"><span data-stu-id="3b057-161">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="3b057-162">Esse código inicializa o objeto **Registry**, recupera o dispositivo gêmeo para **myDeviceId** e então atualiza as propriedades desejadas com um novo objeto de configuração de telemetria.</span><span class="sxs-lookup"><span data-stu-id="3b057-162">This code initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="3b057-163">Depois disso, a cada 10 segundos, ele consulta os dispositivos gêmeos armazenados no Hub IoT e imprime as configurações de telemetria desejadas e relatadas.</span><span class="sxs-lookup"><span data-stu-id="3b057-163">After that, it queries the device twins stored in the IoT hub every 10 seconds, and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="3b057-164">Consulte a [Linguagem de consulta de Hub IoT][lnk-query] para saber como gerar relatórios em todos os seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3b057-164">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="3b057-165">Esse aplicativo consulta o Hub IoT a cada 10 segundos para fins ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="3b057-165">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="3b057-166">Use consultas para gerar relatórios voltados para o usuário em vários dispositivos, não para detectar alterações.</span><span class="sxs-lookup"><span data-stu-id="3b057-166">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="3b057-167">Se sua solução exigir notificações em tempo real de eventos de dispositivo, use [notificações gêmeas][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="3b057-167">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="3b057-168">Por fim, adicione as seguintes linhas ao método **Main** :</span><span class="sxs-lookup"><span data-stu-id="3b057-168">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key to quit.");
        Console.ReadLine();
1. <span data-ttu-id="3b057-169">No Gerenciador de Soluções, abra **Definir projetos de StartUp...** e certifique-se de que a **Ação** para o projeto **SetDesiredConfigurationAndQuery** é **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="3b057-169">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="3b057-170">Compilar a solução.</span><span class="sxs-lookup"><span data-stu-id="3b057-170">Build the solution.</span></span>
1. <span data-ttu-id="3b057-171">Com o aplicativo de dispositivo **SimulateDeviceConfiguration** em execução, execute o aplicativo de serviço do Visual Studio usando **F5**.</span><span class="sxs-lookup"><span data-stu-id="3b057-171">With **SimulateDeviceConfiguration** device app running, run the service app from Visual Studio using **F5**.</span></span> <span data-ttu-id="3b057-172">Você deve ver a configuração reportada mudar de **Pendente** para **Êxito** com a nova frequência de envio ativo de cinco minutos, em vez de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="3b057-172">You should see the reported configuration change from **Pending** to **Success** with the new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Dispositivo configurado com êxito][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="3b057-174">Há um atraso de até um minuto entre a operação de relatório de dispositivo e o resultado da consulta.</span><span class="sxs-lookup"><span data-stu-id="3b057-174">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="3b057-175">Isso é para habilitar a infraestrutura de consulta a trabalhar em escala muito alta.</span><span class="sxs-lookup"><span data-stu-id="3b057-175">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="3b057-176">Para recuperar os modos de exibição consistentes de um único dispositivo gêmeo, use o método **getDeviceTwin** na classe **Registry**.</span><span class="sxs-lookup"><span data-stu-id="3b057-176">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="3b057-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3b057-177">Next steps</span></span>
<span data-ttu-id="3b057-178">Neste tutorial, você definiu uma configuração desejada como *propriedades desejadas* no back-end da solução e criou um aplicativo de dispositivo para detectar essa alteração e simular um processo de atualização de várias etapas, relatando seu status por meio das propriedades relatadas.</span><span class="sxs-lookup"><span data-stu-id="3b057-178">In this tutorial, you set a desired configuration as *desired properties* from the solution back end, and wrote a device app to detect that change and simulate a multi-step update process reporting its status through the reported properties.</span></span>

<span data-ttu-id="3b057-179">Veja os recursos a seguir para saber como:</span><span class="sxs-lookup"><span data-stu-id="3b057-179">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="3b057-180">Enviar telemetria de dispositivos com o tutorial [Introdução ao Hub IoT][lnk-iothub-getstarted].</span><span class="sxs-lookup"><span data-stu-id="3b057-180">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="3b057-181">Agendar ou executar operações em grandes conjuntos de dispositivos. Veja o tutorial [Schedule and broadcast jobs][lnk-schedule-jobs] (Agendar e transmitir trabalhos).</span><span class="sxs-lookup"><span data-stu-id="3b057-181">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="3b057-182">Controlar dispositivos interativamente (como ativar uma ventoinha de um aplicativo controlado pelo usuário), com o tutorial [Uso de métodos diretos][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="3b057-182">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/devicesdknuget.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png


<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-twin-tutorial]: iot-hub-csharp-csharp-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-how-to-configure-createapp]: iot-hub-csharp-csharp-twin-how-to-configure.md#create-the-simulated-device-app
