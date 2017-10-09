---
title: "aaaUse Azure IoT Hub direcionar métodos (.NET/.NET) | Microsoft Docs"
description: "Como toouse Azure IoT Hub direta métodos. Use dispositivo IoT do Azure de saudação SDK para .NET tooimplement um aplicativo de dispositivo simulado que inclui um método direto e hello serviço IoT do Azure SDK para .NET tooimplement um aplicativo de serviço que invoca o método direto hello."
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="60cd3-104">Usar métodos diretos (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="60cd3-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="60cd3-105">Neste tutorial, estamos indo toodevelop dois .NET os aplicativos de console:</span><span class="sxs-lookup"><span data-stu-id="60cd3-105">In this tutorial, we are going toodevelop two .NET console apps:</span></span>

* <span data-ttu-id="60cd3-106">**CallMethodOnDevice**, um aplicativo de back-end, que chama um método no aplicativo do dispositivo simulado hello e exibe a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="60cd3-106">**CallMethodOnDevice**, a back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="60cd3-107">**SimulateDeviceMethods**, um aplicativo de console que simula um dispositivo conectado tooyour IoT hub com a identidade do dispositivo Olá criada anteriormente e responde toohello método chamado pela nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="60cd3-107">**SimulateDeviceMethods**, a console app which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="60cd3-108">artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild toorun ambos os aplicativos em dispositivos e o back-end da solução.</span><span class="sxs-lookup"><span data-stu-id="60cd3-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="60cd3-109">toocomplete neste tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="60cd3-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="60cd3-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="60cd3-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="60cd3-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="60cd3-111">An active Azure account.</span></span> <span data-ttu-id="60cd3-112">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="60cd3-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="60cd3-113">Identidade do dispositivo Olá toocreate programaticamente em vez disso, leia seção correspondente Olá Olá [conecte seu dispositivo simulado tooyour IoT hub que usando o .NET] [ lnk-device-identity-csharp] artigo.</span><span class="sxs-lookup"><span data-stu-id="60cd3-113">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="60cd3-114">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="60cd3-114">Create a simulated device app</span></span>
<span data-ttu-id="60cd3-115">Nesta seção, você deve criar um aplicativo de console .NET que responde tooa método chamado pela solução de saudação volta final.</span><span class="sxs-lookup"><span data-stu-id="60cd3-115">In this section, you create a .NET console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="60cd3-116">No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto toohello atual usando Olá **aplicativo de Console** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="60cd3-116">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="60cd3-117">Projeto de saudação do nome **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="60cd3-117">Name hello project **SimulateDeviceMethods**.</span></span>
   
    ![Novo aplicativo de dispositivo Visual C# Windows clássico][img-createdeviceapp]
    
1. <span data-ttu-id="60cd3-119">No Gerenciador de soluções, clique com botão direito Olá **SimulateDeviceMethods** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="60cd3-119">In Solution Explorer, right-click hello **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="60cd3-120">Em Olá **NuGet Package Manager** janela, selecione **procurar** e procure **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="60cd3-120">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="60cd3-121">Selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices.Client** empacotar e aceitar os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="60cd3-121">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="60cd3-122">Este procedimento faz o download, instala e adiciona uma referência toohello [dispositivo IoT do Azure SDK] [ lnk-nuget-client-sdk] NuGet pacote e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="60cd3-122">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Aplicativo de cliente de janela do Gerenciador de Pacotes NuGet][img-clientnuget]
1. <span data-ttu-id="60cd3-124">Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="60cd3-124">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="60cd3-125">Adicionar Olá toohello campos a seguir **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="60cd3-125">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="60cd3-126">Substitua o valor de espaço reservado de saudação com cadeia de conexão do dispositivo Olá observado na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="60cd3-126">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="60cd3-127">Adicione Olá seguinte tooimplement Olá ao método direto no dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="60cd3-127">Add hello following tooimplement hello direct method on hello device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="60cd3-128">Finalmente, adicione Olá toohello de código a seguir **principal** método tooopen Olá conexão tooyour IoT hub e inicializar Olá método ouvinte:</span><span class="sxs-lookup"><span data-stu-id="60cd3-128">Finally, add hello following code toohello **Main** method tooopen hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. <span data-ttu-id="60cd3-129">Olá Gerenciador de soluções do Visual Studio, com o botão direito sua solução e clique em **definir projetos de inicialização...** . Selecione **único projeto de inicialização**e, em seguida, selecione Olá **SimulateDeviceMethods** projeto no menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="60cd3-129">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **SimulateDeviceMethods** project in hello dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="60cd3-130">coisas tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="60cd3-130">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="60cd3-131">No código de produção, você deve implementar políticas de repetição (como tentativas de conexão), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="60cd3-131">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="60cd3-132">Chama um método direto em um dispositivo</span><span class="sxs-lookup"><span data-stu-id="60cd3-132">Call a direct method on a device</span></span>
<span data-ttu-id="60cd3-133">Nesta seção, você deve criar um aplicativo de console .NET que chama um método no aplicativo do dispositivo simulado hello e, em seguida, exibe a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="60cd3-133">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="60cd3-134">No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto toohello atual usando Olá **aplicativo de Console** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="60cd3-134">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="60cd3-135">Certifique-se de versão do .NET Framework Olá é 4.5.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="60cd3-135">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="60cd3-136">Projeto de saudação do nome **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="60cd3-136">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createserviceapp]
2. <span data-ttu-id="60cd3-138">No Gerenciador de soluções, clique com botão direito Olá **CallMethodOnDevice** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="60cd3-138">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="60cd3-139">Em Olá **NuGet Package Manager** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="60cd3-139">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="60cd3-140">Este procedimento faz o download, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="60cd3-140">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]

4. <span data-ttu-id="60cd3-142">Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="60cd3-142">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="60cd3-143">Adicionar Olá toohello campos a seguir **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="60cd3-143">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="60cd3-144">Substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub hub Olá que você criou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="60cd3-144">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="60cd3-145">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="60cd3-145">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="60cd3-146">Este método invoca um método direto com o nome `writeLine` em Olá `myDeviceId` dispositivo.</span><span class="sxs-lookup"><span data-stu-id="60cd3-146">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="60cd3-147">Em seguida, ele grava resposta Olá fornecida pelo dispositivo Olá no console de saudação.</span><span class="sxs-lookup"><span data-stu-id="60cd3-147">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="60cd3-148">Observe como é possível toospecify um valor de tempo limite para Olá dispositivo toorespond.</span><span class="sxs-lookup"><span data-stu-id="60cd3-148">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="60cd3-149">Finalmente, adicione Olá toohello linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="60cd3-149">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="60cd3-150">Olá Gerenciador de soluções do Visual Studio, com o botão direito sua solução e clique em **definir projetos de inicialização...** . Selecione **único projeto de inicialização**e, em seguida, selecione Olá **CallMethodOnDevice** projeto no menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="60cd3-150">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="60cd3-151">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="60cd3-151">Run hello applications</span></span>
<span data-ttu-id="60cd3-152">Agora você está pronto toorun aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="60cd3-152">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="60cd3-153">Execute o aplicativo de dispositivo de .NET Olá **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="60cd3-153">Run hello .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="60cd3-154">Ele deve iniciar a escuta para chamadas de método do seu Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="60cd3-154">It should start listening for method calls from your IoT Hub:</span></span> 

    ![Execução de aplicativo de dispositivo][img-deviceapprun]
1. <span data-ttu-id="60cd3-156">Agora esse dispositivo hello está conectado e esperando para invocações de método, execute Olá .NET **CallMethodOnDevice** método do aplicativo tooinvoke hello no aplicativo do dispositivo simulado hello.</span><span class="sxs-lookup"><span data-stu-id="60cd3-156">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="60cd3-157">Você deve ver a resposta do dispositivo Olá gravada no console de saudação.</span><span class="sxs-lookup"><span data-stu-id="60cd3-157">You should see hello device response written in hello console.</span></span>
   
    ![Execução de aplicativo de serviço][img-serviceapprun]
1. <span data-ttu-id="60cd3-159">dispositivo Hello, em seguida, reage toohello método imprimindo esta mensagem:</span><span class="sxs-lookup"><span data-stu-id="60cd3-159">hello device then reacts toohello method by printing this message:</span></span>
   
    ![Método direto invocado no dispositivo Olá][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="60cd3-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="60cd3-161">Next steps</span></span>
<span data-ttu-id="60cd3-162">Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello.</span><span class="sxs-lookup"><span data-stu-id="60cd3-162">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="60cd3-163">Você usou esse dispositivo identidade tooenable Olá simulado dispositivo aplicativo tooreact toomethods invocado pela nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="60cd3-163">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="60cd3-164">Você também criou um aplicativo que chama métodos no dispositivo hello e exibe a resposta de saudação do dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="60cd3-164">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="60cd3-165">toocontinue guia de Introdução com o IoT Hub e tooexplore outros cenários de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="60cd3-165">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="60cd3-166">[Introdução ao Hub IoT]</span><span class="sxs-lookup"><span data-stu-id="60cd3-166">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="60cd3-167">[Agendar trabalhos em vários dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="60cd3-167">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="60cd3-168">toolearn como tooextend seu método de solução e agenda IoT chama em vários dispositivos, consulte Olá [agenda e trabalhos de difusão] [ lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="60cd3-168">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[Introdução ao Hub IoT]: iot-hub-node-node-getstarted.md
