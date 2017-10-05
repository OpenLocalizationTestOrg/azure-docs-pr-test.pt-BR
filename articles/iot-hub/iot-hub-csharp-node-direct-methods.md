---
title: "Usar métodos diretos do Hub IoT do Azure (.NET/Node) | Microsoft Docs"
description: "Como usar os métodos diretos do Hub IoT do Azure. Use o SDK do dispositivo IoT do Azure para Node.js para implementar um aplicativo de dispositivo simulado que inclui um método direto e o SDK do serviço do Azure IoT para .NET para implementar um aplicativo de serviço que invoca o método direto."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: ad705789a153381e21b2ccb05d4e0c17f78671fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="fc8fa-104">Usar métodos diretos para (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="fc8fa-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="fc8fa-105">Neste tutorial, vamos desenvolver um .NET e um aplicativo de console do Node.js:</span><span class="sxs-lookup"><span data-stu-id="fc8fa-105">In this tutorial, we are going to develop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="fc8fa-106">**CallMethodOnDevice.sln**, um aplicativo de back-end .NET que chama um método no aplicativo do dispositivo simulado e exibe a resposta.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="fc8fa-107">**SimulatedDevice.js**, um aplicativo Node.js que simula um dispositivo que se conecta ao seu Hub IoT com a identidade do dispositivo criada anteriormente e responde ao método chamado pela nuvem.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="fc8fa-108">O artigo [SDKs de IoT do Azure][lnk-hub-sdks] fornece informações sobre os SDKs de IoT do Azure que você pode usar para criar aplicativos executados em dispositivos e no back-end da solução.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="fc8fa-109">Para concluir este tutorial, você precisará:</span><span class="sxs-lookup"><span data-stu-id="fc8fa-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="fc8fa-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="fc8fa-111">Node.js versão 0.10.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="fc8fa-112">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-112">An active Azure account.</span></span> <span data-ttu-id="fc8fa-113">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="fc8fa-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="fc8fa-114">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="fc8fa-114">Create a simulated device app</span></span>
<span data-ttu-id="fc8fa-115">Nesta seção, você cria um aplicativo de console do Node.js que responde a um método chamado pelo back-end da solução.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-115">In this section, you create a Node.js console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="fc8fa-116">Crie uma nova pasta vazia denominada **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="fc8fa-117">Na pasta **simulateddevice** , crie um arquivo package.json usando o comando a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-117">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="fc8fa-118">Aceite todos os padrões:</span><span class="sxs-lookup"><span data-stu-id="fc8fa-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="fc8fa-119">No prompt de comando, na pasta **simulateddevice**, execute o seguinte comando para instalar o pacote **azure-iot-device** e pacotes **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="fc8fa-119">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="fc8fa-120">Usando um editor de texto, crie um arquivo na pasta **simulateddevice** e coloque o nome **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-120">Using a text editor, create a file in the **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="fc8fa-121">Adicione as seguintes instruções `require` no início do arquivo **SimulatedDevice.js** :</span><span class="sxs-lookup"><span data-stu-id="fc8fa-121">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="fc8fa-122">Adicione uma variável **connectionString** e use-a para criar uma instância **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-122">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="fc8fa-123">Substitua **{cadeia de conexão do dispositivo}** pela cadeia de conexão de dispositivo gerada na seção *Criar uma identidade de dispositivo*:</span><span class="sxs-lookup"><span data-stu-id="fc8fa-123">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="fc8fa-124">Adicione a seguinte função para implementar o método direto no dispositivo:</span><span class="sxs-lookup"><span data-stu-id="fc8fa-124">Add the following function to implement the direct method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="fc8fa-125">Abra a conexão com o Hub IoT e inicialize o ouvinte do método:</span><span class="sxs-lookup"><span data-stu-id="fc8fa-125">Open the connection to your IoT hub and initialize the method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. <span data-ttu-id="fc8fa-126">Salve e feche o arquivo **SimulatedDevice.js** .</span><span class="sxs-lookup"><span data-stu-id="fc8fa-126">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="fc8fa-127">Para simplificar, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-127">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="fc8fa-128">No código de produção, você deve implementar políticas de repetição (tais como tentar conexão novamente), conforme sugerido no artigo do MSDN [Tratamento de Falhas Transitórias][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="fc8fa-128">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="fc8fa-129">Chama um método direto em um dispositivo</span><span class="sxs-lookup"><span data-stu-id="fc8fa-129">Call a direct method on a device</span></span>
<span data-ttu-id="fc8fa-130">Nesta seção, você cria um aplicativo de console do .NET que chama um método no dispositivo simulado e, em seguida, exibe a resposta.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-130">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="fc8fa-131">No Visual Studio, adicione um projeto da Área de Trabalho Clássica do Windows no Visual C# à solução atual usando o modelo de projeto **Aplicativo do Console** .</span><span class="sxs-lookup"><span data-stu-id="fc8fa-131">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="fc8fa-132">Verifique se a versão do .NET Framework é 4.5.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-132">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="fc8fa-133">Nomeie o projeto como **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-133">Name the project **CallMethodOnDevice**.</span></span>
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][10]
2. <span data-ttu-id="fc8fa-135">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **CallMethodOnDevice** e clique em **Gerenciar Pacotes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-135">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="fc8fa-136">Na janela **Gerenciador de Pacotes Nuget**, selecione **Procurar**, procure **microsoft.azure.devices**, selecione **Instalar** para instalar o pacote **Microsoft.Azure.Devices** e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-136">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="fc8fa-137">O procedimento baixa, instala e adiciona uma referência ao [pacote Nuget do SDK do Dispositivo IoT do Azure][lnk-nuget-service-sdk] e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-137">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Janela do Gerenciador de Pacotes NuGet][11]

4. <span data-ttu-id="fc8fa-139">Adicione as instruções `using` abaixo na parte superior do arquivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="fc8fa-139">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="fc8fa-140">Adicione os seguintes campos à classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="fc8fa-140">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="fc8fa-141">Substitua o valor do espaço reservado pela cadeia de conexão do Hub IoT criado na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-141">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="fc8fa-142">Adicione o seguinte método à classe **Programa** :</span><span class="sxs-lookup"><span data-stu-id="fc8fa-142">Add the following method to the **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line to be written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="fc8fa-143">Este método invoca um método direto com o nome `writeLine` no dispositivo `myDeviceId`.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-143">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span></span> <span data-ttu-id="fc8fa-144">Em seguida, ele grava a resposta fornecida pelo dispositivo no console.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-144">Then, it writes the response provided by the device on the console.</span></span> <span data-ttu-id="fc8fa-145">Observe como é possível especificar um valor de tempo limite para a resposta do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-145">Note how it is possible to specify a timeout value for the device to respond.</span></span>
7. <span data-ttu-id="fc8fa-146">Por fim, adicione as seguintes linhas ao método **Main** :</span><span class="sxs-lookup"><span data-stu-id="fc8fa-146">Finally, add the following lines to the **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

## <a name="run-the-applications"></a><span data-ttu-id="fc8fa-147">Executar os aplicativos</span><span class="sxs-lookup"><span data-stu-id="fc8fa-147">Run the applications</span></span>
<span data-ttu-id="fc8fa-148">Agora você está pronto para executar os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-148">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="fc8fa-149">No Visual Studio, no Gerenciador de Soluções, clique com o botão direito na solução e clique em **Definir Projetos de Inicialização...**.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-149">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="fc8fa-150">Selecione **Único projeto de inicialização**e, em seguida, selecione o projeto **CallMethodOnDevice** no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-150">Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span></span>

2. <span data-ttu-id="fc8fa-151">Em um prompt de comando, na pasta **simulateddevice**, execute o seguinte comando para iniciar a escuta de chamadas de método de seu Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="fc8fa-151">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="fc8fa-152">Aguarde a abertura do dispositivo simulado: ![][7]</span><span class="sxs-lookup"><span data-stu-id="fc8fa-152">Wait for the simulated device to open:  ![][7]</span></span>
3. <span data-ttu-id="fc8fa-153">Agora que o dispositivo está conectado e aguardando chamadas de método, execute o aplicativo **CallMethodOnDevice** .NET para chamar o método no aplicativo do dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-153">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span></span> <span data-ttu-id="fc8fa-154">Você deve ver a resposta do dispositivo escrita no console.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-154">You should see the device response written in the console.</span></span>
   
    ![][8]
4. <span data-ttu-id="fc8fa-155">O dispositivo reage ao método imprimindo esta mensagem:</span><span class="sxs-lookup"><span data-stu-id="fc8fa-155">The device then reacts to the method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="fc8fa-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fc8fa-156">Next steps</span></span>
<span data-ttu-id="fc8fa-157">Neste tutorial, você configurou um novo hub IoT no portal do Azure e depois criou uma identidade do dispositivo no Registro de identidade do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-157">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="fc8fa-158">Você usou essa identidade do dispositivo para habilitar o aplicativo do dispositivo simulado para reagir aos métodos invocados pela nuvem.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-158">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="fc8fa-159">Você também criou um aplicativo que invoca métodos no dispositivo e exibe a resposta do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-159">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="fc8fa-160">Para continuar a introdução ao Hub IoT e explorar outros cenários de IoT, confira:</span><span class="sxs-lookup"><span data-stu-id="fc8fa-160">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="fc8fa-161">[Introdução ao Hub IoT]</span><span class="sxs-lookup"><span data-stu-id="fc8fa-161">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="fc8fa-162">[Agendar trabalhos em vários dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="fc8fa-162">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="fc8fa-163">Para saber como estender sua solução de IoT e agendar chamadas de método em vários dispositivos, confira o tutorial [Agendar e difundir trabalhos][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="fc8fa-163">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
<span data-ttu-id="fc8fa-164">[Introdução ao Hub IoT]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="fc8fa-164">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
