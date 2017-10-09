---
title: Propriedades de duas aaaUse Azure IoT Hub dispositivo (.NET/.NET) | Microsoft Docs
description: "Como twins dispositivo do Azure IoT Hub toouse tooconfigure dispositivos. Você usa dispositivos de Azure IoT Olá SDK para .NET tooimplement um aplicativo de dispositivo simulado e Olá serviço IoT do Azure SDK para .NET tooimplement um serviço de aplicativo que modifica uma configuração de dispositivo usando duas um dispositivo."
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
ms.openlocfilehash: 486436d29abfd5158c253adc5abf5935e0e1fdba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="f5d37-104">Usar propriedades desejadas tooconfigure dispositivos</span><span class="sxs-lookup"><span data-stu-id="f5d37-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="f5d37-105">No final da saudação deste tutorial, você tem dois aplicativos de console do .NET:</span><span class="sxs-lookup"><span data-stu-id="f5d37-105">At hello end of this tutorial, you will have two .NET console apps:</span></span>

* <span data-ttu-id="f5d37-106">**SimulateDeviceConfiguration**, um aplicativo de dispositivo simulado que aguarda uma atualização de configurações desejadas e relata o status de saudação de um processo de atualização de configuração simulada.</span><span class="sxs-lookup"><span data-stu-id="f5d37-106">**SimulateDeviceConfiguration**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="f5d37-107">**SetDesiredConfigurationAndQuery**, um aplicativo de back-end, que define a saudação da configuração em um dispositivo desejado e consultas Olá o processo de atualização de configuração.</span><span class="sxs-lookup"><span data-stu-id="f5d37-107">**SetDesiredConfigurationAndQuery**, a back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="f5d37-108">artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild aplicativos de dispositivo e de back-end.</span><span class="sxs-lookup"><span data-stu-id="f5d37-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="f5d37-109">toocomplete este tutorial, você precisa seguir hello:</span><span class="sxs-lookup"><span data-stu-id="f5d37-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="f5d37-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="f5d37-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="f5d37-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5d37-111">An active Azure account.</span></span> <span data-ttu-id="f5d37-112">Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f5d37-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="f5d37-113">Se você seguiu Olá [Introdução ao twins dispositivo] [ lnk-twin-tutorial] tutorial, você já tem um hub IoT e uma identidade de dispositivo chamado **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="f5d37-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="f5d37-114">Nesse caso, você pode ignorar toohello [criar aplicativo de dispositivo simulado Olá] [ lnk-how-to-configure-createapp] seção.</span><span class="sxs-lookup"><span data-stu-id="f5d37-114">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="f5d37-115">Criar aplicativo de dispositivo simulado Olá</span><span class="sxs-lookup"><span data-stu-id="f5d37-115">Create hello simulated device app</span></span>
<span data-ttu-id="f5d37-116">Nesta seção, você cria um aplicativo de console .NET que conecta o hub tooyour como **myDeviceId**, aguarda até que uma atualização de configurações desejadas e, em seguida, relatórios atualizações no processo de atualização de configuração Olá simulada.</span><span class="sxs-lookup"><span data-stu-id="f5d37-116">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="f5d37-117">No Visual Studio, criar um novo projeto do Visual c# Windows clássico Desktop usando Olá **aplicativo de Console** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="f5d37-117">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using hello **Console Application** project template.</span></span> <span data-ttu-id="f5d37-118">Projeto de saudação do nome **SimulateDeviceConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="f5d37-118">Name hello project **SimulateDeviceConfiguration**.</span></span>
   
    ![Novo aplicativo de dispositivo Visual C# Windows clássico][img-createdeviceapp]

1. <span data-ttu-id="f5d37-120">No Gerenciador de soluções, clique com botão direito Olá **SimulateDeviceConfiguration** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="f5d37-120">In Solution Explorer, right-click hello **SimulateDeviceConfiguration** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="f5d37-121">Em Olá **NuGet Package Manager** janela, selecione **procurar** e procure **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="f5d37-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="f5d37-122">Selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices.Client** empacotar e aceitar os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="f5d37-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="f5d37-123">Este procedimento faz o download, instala e adiciona uma referência toohello [dispositivo IoT do Azure SDK] [ lnk-nuget-client-sdk] NuGet pacote e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="f5d37-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Aplicativo de cliente de janela do Gerenciador de Pacotes NuGet][img-clientnuget]
1. <span data-ttu-id="f5d37-125">Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="f5d37-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="f5d37-126">Adicionar Olá toohello campos a seguir **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="f5d37-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="f5d37-127">Substitua o valor de espaço reservado de saudação com cadeia de conexão do dispositivo Olá observado na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="f5d37-127">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. <span data-ttu-id="f5d37-128">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="f5d37-128">Add hello following method toohello **Program** class:</span></span>
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    <span data-ttu-id="f5d37-129">Olá **cliente** objeto expõe todos os métodos de saudação exigem toointeract com twins de dispositivo do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="f5d37-129">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="f5d37-130">Olá código mostrado acima, inicializa Olá **cliente** objeto e, em seguida, recupera Olá dispositivo duas para **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="f5d37-130">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="f5d37-131">Adicionar Olá após o método toohello **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="f5d37-131">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="f5d37-132">Esse método define os valores iniciais de saudação de telemetria no dispositivo local hello e, em seguida, as atualizações Olá duas do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f5d37-132">This method sets hello initial values of telemetry on hello local device and then updates hello device twin.</span></span>

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

1. <span data-ttu-id="f5d37-133">Adicionar Olá após o método toohello **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="f5d37-133">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="f5d37-134">Este é um retorno de chamada que detecta uma alteração na *propriedades desejadas* em duas de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5d37-134">This is a callback which will detect a change in *desired properties* in hello device twin.</span></span>

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

    <span data-ttu-id="f5d37-135">Saudação de atualizações esse método relatado propriedades no objeto de duas Olá dispositivo local com a configuração de saudação atualizar status de saudação de solicitação e conjuntos muito**pendente**, e em seguida, as atualizações Olá duas de dispositivo no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5d37-135">This method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="f5d37-136">Depois de atualizar com êxito duas de dispositivo hello, concluir Olá alteração de configuração chamando o método hello `CompleteConfigChange` descrito no próximo ponto de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5d37-136">After successfully updating hello device twin, it completes hello config change by calling hello method `CompleteConfigChange` described in hello next point.</span></span>

1. <span data-ttu-id="f5d37-137">Adicionar Olá após o método toohello **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="f5d37-137">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="f5d37-138">Esse método simula uma redefinição do dispositivo, em seguida, atualizações Olá propriedades relatadas local definindo o status de saudação muito**êxito** e remove hello **pendingConfig** elemento.</span><span class="sxs-lookup"><span data-stu-id="f5d37-138">This method simulates a device reset, then updates hello local reported properties setting hello status too**Success** and removes hello **pendingConfig** element.</span></span> <span data-ttu-id="f5d37-139">Em seguida, atualiza as duas de dispositivo Olá no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5d37-139">It then updates hello device twin on hello service.</span></span> 

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
                Console.WriteLine("Config change complete \nPress any key tooexit.");
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

1. <span data-ttu-id="f5d37-140">Finalmente, adicione Olá toohello linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="f5d37-140">Finally add hello following lines toohello **Main** method:</span></span>

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
   > <span data-ttu-id="f5d37-141">Este tutorial não simula nenhum comportamento para atualizações de configuração simultâneas.</span><span class="sxs-lookup"><span data-stu-id="f5d37-141">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="f5d37-142">Alguns processos de atualização de configuração podem ser capaz de tooaccommodate alterações de configuração de destino durante a execução de atualização hello, alguns dados podem ter tooqueue e alguns podem rejeitá-las com uma condição de erro.</span><span class="sxs-lookup"><span data-stu-id="f5d37-142">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="f5d37-143">Verifique tooconsider se Olá o comportamento desejado para o processo de configuração específica e adicionar lógica apropriada Olá antes de iniciar a alteração de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5d37-143">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="f5d37-144">Criar solução hello e, em seguida, execute o aplicativo de dispositivo de saudação do Visual Studio clicando **F5**.</span><span class="sxs-lookup"><span data-stu-id="f5d37-144">Build hello solution and then run hello device app from Visual Studio by clicking **F5**.</span></span> <span data-ttu-id="f5d37-145">No console de saída de hello, você deve ver mensagens de saudação indicando que seu dispositivo simulado é recuperando duas de dispositivo Olá, configuração de telemetria hello e aguardando a alteração da propriedade desejada.</span><span class="sxs-lookup"><span data-stu-id="f5d37-145">On hello output console, you should see hello messages indicating that your simulated device is retrieving hello device twin, setting up hello telemetry, and waiting for desired property change.</span></span> <span data-ttu-id="f5d37-146">Lembre-Olá aplicativo em execução.</span><span class="sxs-lookup"><span data-stu-id="f5d37-146">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="f5d37-147">Criar aplicativo de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="f5d37-147">Create hello service app</span></span>
<span data-ttu-id="f5d37-148">Nesta seção, você criará um aplicativo de console .NET que Olá atualizações *propriedades desejadas* em Olá dispositivo duas associada **myDeviceId** com um novo objeto de configuração de telemetria.</span><span class="sxs-lookup"><span data-stu-id="f5d37-148">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="f5d37-149">Ele, em seguida, consulta twins de dispositivo Olá armazenadas no hub IoT de saudação e mostra diferença Olá entre hello desejado e relatado configurações de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5d37-149">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="f5d37-150">No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto toohello atual usando Olá **aplicativo de Console** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="f5d37-150">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="f5d37-151">Projeto de saudação do nome **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="f5d37-151">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]
1. <span data-ttu-id="f5d37-153">No Gerenciador de soluções, clique com botão direito Olá **SetDesiredConfigurationAndQuery** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="f5d37-153">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="f5d37-154">Em Olá **NuGet Package Manager** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="f5d37-154">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="f5d37-155">Este procedimento faz o download, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="f5d37-155">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
1. <span data-ttu-id="f5d37-157">Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="f5d37-157">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="f5d37-158">Adicionar Olá toohello campos a seguir **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="f5d37-158">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="f5d37-159">Substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub hub Olá que você criou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="f5d37-159">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="f5d37-160">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="f5d37-160">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="f5d37-161">Olá **registro** objeto expõe toointeract necessária do todos os métodos de saudação com twins de dispositivo do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5d37-161">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="f5d37-162">Esse código inicializa Olá **registro** objeto recupera Olá duas de dispositivo para **myDeviceId**e, em seguida, atualiza as propriedades desejadas com um novo objeto de configuração de telemetria.</span><span class="sxs-lookup"><span data-stu-id="f5d37-162">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="f5d37-163">Depois disso, ele consulta twins de dispositivo Olá armazenadas no hub IoT de saudação a cada 10 segundos, e imprime Olá desejado e relatado configurações de telemetria.</span><span class="sxs-lookup"><span data-stu-id="f5d37-163">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="f5d37-164">Consulte toohello [linguagem de consulta de IoT Hub] [ lnk-query] toolearn como toogenerate rich relatórios em todos os seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f5d37-164">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="f5d37-165">Esse aplicativo consulta o Hub IoT a cada 10 segundos para fins ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="f5d37-165">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="f5d37-166">Use consultas toogenerate voltadas para o usuário relatórios em vários dispositivos e não toodetect alterações.</span><span class="sxs-lookup"><span data-stu-id="f5d37-166">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="f5d37-167">Se sua solução exigir notificações em tempo real de eventos de dispositivo, use [notificações gêmeas][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="f5d37-167">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="f5d37-168">Finalmente, adicione Olá toohello linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="f5d37-168">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="f5d37-169">Olá Gerenciador de soluções, abra o hello **projetos de inicialização definido...**  e certifique-se de saudação **ação** para **SetDesiredConfigurationAndQuery** projeto é **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="f5d37-169">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="f5d37-170">Compile a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5d37-170">Build hello solution.</span></span>
1. <span data-ttu-id="f5d37-171">Com **SimulateDeviceConfiguration** dispositivo que executa o aplicativo, a saudação de execução do serviço de aplicativo do Visual Studio usando **F5**.</span><span class="sxs-lookup"><span data-stu-id="f5d37-171">With **SimulateDeviceConfiguration** device app running, run hello service app from Visual Studio using **F5**.</span></span> <span data-ttu-id="f5d37-172">Você deve ver a configuração relatado Olá alterar de **pendente** muito**êxito** com novo ativo de saudação enviar frequência de cinco minutos, em vez de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="f5d37-172">You should see hello reported configuration change from **Pending** too**Success** with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Dispositivo configurado com êxito][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="f5d37-174">Há um atraso de backup tooa minutos entre a operação de relatório de dispositivo hello e resultado da consulta hello.</span><span class="sxs-lookup"><span data-stu-id="f5d37-174">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="f5d37-175">Isso é tooenable Olá consulta infraestrutura toowork em escala muito alta.</span><span class="sxs-lookup"><span data-stu-id="f5d37-175">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="f5d37-176">modos de exibição consistente de duas um único dispositivo tooretrieve usam Olá **getDeviceTwin** método hello **registro** classe.</span><span class="sxs-lookup"><span data-stu-id="f5d37-176">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="f5d37-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f5d37-177">Next steps</span></span>
<span data-ttu-id="f5d37-178">Neste tutorial, você definir uma configuração desejada como *propriedades desejadas* da solução Olá back-end e gravou um toodetect de aplicativo de dispositivo que são alterados e simular um processo de atualização de várias etapas relatar seu status por meio de saudação relatada Propriedades.</span><span class="sxs-lookup"><span data-stu-id="f5d37-178">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="f5d37-179">Saudação de uso toolearn de recursos a seguir como a:</span><span class="sxs-lookup"><span data-stu-id="f5d37-179">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="f5d37-180">Enviar telemetria de dispositivos com hello [começar com o IoT Hub] [ lnk-iothub-getstarted] tutorial,</span><span class="sxs-lookup"><span data-stu-id="f5d37-180">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="f5d37-181">agendar ou executar operações em grandes conjuntos de dispositivos Consulte Olá [agenda e trabalhos de difusão] [ lnk-schedule-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="f5d37-181">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="f5d37-182">controlar dispositivos interativamente (como ativar um ventilador de um aplicativo controlado pelo usuário), com hello [usar métodos diretos] [ lnk-methods-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="f5d37-182">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
