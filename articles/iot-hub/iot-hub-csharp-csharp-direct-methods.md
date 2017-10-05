---
title: "Usar métodos diretos do Hub IoT do Azure (.NET/.NET) | Microsoft Docs"
description: "Como usar os métodos diretos do Hub IoT do Azure. Use o SDK do dispositivo IoT do Azure para .NET para implementar um aplicativo de dispositivo simulado que inclua um método direto e o SDK do serviço do Azure IoT para .NET para implementar um aplicativo de serviço que invoque o método direto."
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
ms.openlocfilehash: 9ce1fbebb6417c10618aa182e3c1d9ddf8132fb6
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="44211-104">Usar métodos diretos (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="44211-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="44211-105">Neste tutorial, vamos desenvolver dois aplicativos de console .NET:</span><span class="sxs-lookup"><span data-stu-id="44211-105">In this tutorial, we are going to develop two .NET console apps:</span></span>

* <span data-ttu-id="44211-106">**CallMethodOnDevice**, um aplicativo de back-end que chama um método no aplicativo do dispositivo simulado e exibe a resposta.</span><span class="sxs-lookup"><span data-stu-id="44211-106">**CallMethodOnDevice**, a back-end app, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="44211-107">**SimulateDeviceMethods**, um aplicativo de console que simula um dispositivo que se conecta ao seu hub IoT com a identidade do dispositivo criada anteriormente e responde ao método chamado pela nuvem.</span><span class="sxs-lookup"><span data-stu-id="44211-107">**SimulateDeviceMethods**, a console app which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="44211-108">O artigo [SDKs de IoT do Azure][lnk-hub-sdks] fornece informações sobre os SDKs de IoT do Azure que você pode usar para criar aplicativos executados em dispositivos e no back-end da solução.</span><span class="sxs-lookup"><span data-stu-id="44211-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="44211-109">Para concluir este tutorial, você precisará:</span><span class="sxs-lookup"><span data-stu-id="44211-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="44211-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="44211-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="44211-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="44211-111">An active Azure account.</span></span> <span data-ttu-id="44211-112">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="44211-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="44211-113">Se você deseja criar a identidade do dispositivo de forma programática, leia a seção correspondente no artigo [Conecte seu dispositivo simulado ao Hub IoT usando o .NET][lnk-device-identity-csharp].</span><span class="sxs-lookup"><span data-stu-id="44211-113">If you want to create the device identity programmatically instead, read the corresponding section in the [Connect your simulated device to your IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="44211-114">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="44211-114">Create a simulated device app</span></span>
<span data-ttu-id="44211-115">Nesta seção, você cria um aplicativo de console .NET que responde a um método chamado pelo back-end da solução.</span><span class="sxs-lookup"><span data-stu-id="44211-115">In this section, you create a .NET console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="44211-116">No Visual Studio, adicione um projeto da Área de Trabalho Clássica do Windows no Visual C# à solução atual usando o modelo de projeto **Aplicativo do Console** .</span><span class="sxs-lookup"><span data-stu-id="44211-116">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="44211-117">Dê ao projeto o nome de **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="44211-117">Name the project **SimulateDeviceMethods**.</span></span>
   
    ![Novo aplicativo de dispositivo Visual C# Windows clássico][img-createdeviceapp]
    
1. <span data-ttu-id="44211-119">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **SimulateDeviceMethods**, então em **Gerenciar Pacotes do NuGet…**.</span><span class="sxs-lookup"><span data-stu-id="44211-119">In Solution Explorer, right-click the **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="44211-120">Na janela **Gerenciador de Pacotes NuGet**, selecione **Procurar** e pesquise por **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="44211-120">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="44211-121">Selecione **Instalar** para instalar o pacote **Microsoft.Azure.Devices.Client** e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="44211-121">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="44211-122">O procedimento baixa, instala e adiciona uma referência ao [pacote NuGet do SDK do Dispositivo IoT do Azure][lnk-nuget-client-sdk] e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="44211-122">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Aplicativo de cliente de janela do Gerenciador de Pacotes NuGet][img-clientnuget]
1. <span data-ttu-id="44211-124">Adicione as instruções `using` abaixo na parte superior do arquivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="44211-124">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="44211-125">Adicione os seguintes campos à classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="44211-125">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="44211-126">Substitua o valor de espaço reservado pela cadeia de conexão do dispositivo que você anotou na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="44211-126">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="44211-127">Adicione o seguinte para implementar o método direto no dispositivo:</span><span class="sxs-lookup"><span data-stu-id="44211-127">Add the following to implement the direct method on the device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written to log.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="44211-128">Por fim, adicione o seguinte código ao método **Principal** para abrir a conexão para o hub IoT e inicializar o ouvinte do método:</span><span class="sxs-lookup"><span data-stu-id="44211-128">Finally, add the following code to the **Main** method to open the connection to your IoT hub and initialize the method listener:</span></span>
   
        try
        {
            Console.WriteLine("Connecting to hub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter to exit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove the "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. <span data-ttu-id="44211-129">No Visual Studio, no Gerenciador de Soluções, clique com o botão direito na solução e clique em **Definir Projetos de Inicialização...**.</span><span class="sxs-lookup"><span data-stu-id="44211-129">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="44211-130">Selecione **Projeto único de inicialização** e, em seguida, selecione o projeto **SimulateDeviceMethods** no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="44211-130">Select **Single startup project**, and then select the **SimulateDeviceMethods** project in the dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="44211-131">Para simplificar, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="44211-131">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="44211-132">No código de produção, você deve implementar políticas de repetição (tais como tentar conexão novamente), conforme sugerido no artigo do MSDN [Tratamento de Falhas Transitórias][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="44211-132">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="44211-133">Chama um método direto em um dispositivo</span><span class="sxs-lookup"><span data-stu-id="44211-133">Call a direct method on a device</span></span>
<span data-ttu-id="44211-134">Nesta seção, você cria um aplicativo de console do .NET que chama um método no dispositivo simulado e, em seguida, exibe a resposta.</span><span class="sxs-lookup"><span data-stu-id="44211-134">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="44211-135">No Visual Studio, adicione um projeto da Área de Trabalho Clássica do Windows no Visual C# à solução atual usando o modelo de projeto **Aplicativo do Console** .</span><span class="sxs-lookup"><span data-stu-id="44211-135">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="44211-136">Verifique se a versão do .NET Framework é 4.5.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="44211-136">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="44211-137">Nomeie o projeto como **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="44211-137">Name the project **CallMethodOnDevice**.</span></span>
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createserviceapp]
2. <span data-ttu-id="44211-139">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **CallMethodOnDevice** e clique em **Gerenciar Pacotes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="44211-139">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="44211-140">Na janela **Gerenciador de Pacotes Nuget**, selecione **Procurar**, procure **microsoft.azure.devices**, selecione **Instalar** para instalar o pacote **Microsoft.Azure.Devices** e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="44211-140">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="44211-141">O procedimento baixa, instala e adiciona uma referência ao [pacote Nuget do SDK do Dispositivo IoT do Azure][lnk-nuget-service-sdk] e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="44211-141">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]

4. <span data-ttu-id="44211-143">Adicione as instruções `using` abaixo na parte superior do arquivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="44211-143">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="44211-144">Adicione os seguintes campos à classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="44211-144">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="44211-145">Substitua o valor do espaço reservado pela cadeia de conexão do Hub IoT criado na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="44211-145">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="44211-146">Adicione o seguinte método à classe **Programa** :</span><span class="sxs-lookup"><span data-stu-id="44211-146">Add the following method to the **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line to be written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="44211-147">Este método invoca um método direto com o nome `writeLine` no dispositivo `myDeviceId`.</span><span class="sxs-lookup"><span data-stu-id="44211-147">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span></span> <span data-ttu-id="44211-148">Em seguida, ele grava a resposta fornecida pelo dispositivo no console.</span><span class="sxs-lookup"><span data-stu-id="44211-148">Then, it writes the response provided by the device on the console.</span></span> <span data-ttu-id="44211-149">Observe como é possível especificar um valor de tempo limite para a resposta do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="44211-149">Note how it is possible to specify a timeout value for the device to respond.</span></span>
7. <span data-ttu-id="44211-150">Por fim, adicione as seguintes linhas ao método **Main** :</span><span class="sxs-lookup"><span data-stu-id="44211-150">Finally, add the following lines to the **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="44211-151">No Visual Studio, no Gerenciador de Soluções, clique com o botão direito na solução e clique em **Definir Projetos de Inicialização...**.</span><span class="sxs-lookup"><span data-stu-id="44211-151">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="44211-152">Selecione **Único projeto de inicialização**e, em seguida, selecione o projeto **CallMethodOnDevice** no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="44211-152">Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="44211-153">Executar os aplicativos</span><span class="sxs-lookup"><span data-stu-id="44211-153">Run the applications</span></span>
<span data-ttu-id="44211-154">Agora você está pronto para executar os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="44211-154">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="44211-155">Execute o aplicativo de dispositivo .NET **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="44211-155">Run the .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="44211-156">Ele deve iniciar a escuta para chamadas de método do seu Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="44211-156">It should start listening for method calls from your IoT Hub:</span></span> 

    ![Execução de aplicativo de dispositivo][img-deviceapprun]
1. <span data-ttu-id="44211-158">Agora que o dispositivo está conectado e aguardando chamadas de método, execute o aplicativo **CallMethodOnDevice** .NET para chamar o método no aplicativo do dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="44211-158">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span></span> <span data-ttu-id="44211-159">Você deve ver a resposta do dispositivo escrita no console.</span><span class="sxs-lookup"><span data-stu-id="44211-159">You should see the device response written in the console.</span></span>
   
    ![Execução de aplicativo de serviço][img-serviceapprun]
1. <span data-ttu-id="44211-161">O dispositivo reage ao método imprimindo esta mensagem:</span><span class="sxs-lookup"><span data-stu-id="44211-161">The device then reacts to the method by printing this message:</span></span>
   
    ![Método direto invocado no dispositivo][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="44211-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="44211-163">Next steps</span></span>
<span data-ttu-id="44211-164">Neste tutorial, você configurou um novo hub IoT no portal do Azure e depois criou uma identidade do dispositivo no Registro de identidade do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="44211-164">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="44211-165">Você usou essa identidade do dispositivo para habilitar o aplicativo do dispositivo simulado para reagir aos métodos invocados pela nuvem.</span><span class="sxs-lookup"><span data-stu-id="44211-165">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="44211-166">Você também criou um aplicativo que invoca métodos no dispositivo e exibe a resposta do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="44211-166">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="44211-167">Para continuar a introdução ao Hub IoT e explorar outros cenários de IoT, confira:</span><span class="sxs-lookup"><span data-stu-id="44211-167">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="44211-168">[Introdução ao Hub IoT]</span><span class="sxs-lookup"><span data-stu-id="44211-168">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="44211-169">[Agendar trabalhos em vários dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="44211-169">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="44211-170">Para saber como estender sua solução de IoT e agendar chamadas de método em vários dispositivos, confira o tutorial [Agendar e difundir trabalhos][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="44211-170">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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

<span data-ttu-id="44211-171">[Introdução ao Hub IoT]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="44211-171">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
