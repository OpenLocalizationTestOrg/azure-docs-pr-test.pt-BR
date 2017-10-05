---
title: Agendar trabalhos com o Hub IoT do Azure (.NET/Node) | Microsoft Docs
description: "Como agendar um trabalho do Hub IoT do Azure para invocar um método direto em vários dispositivos. Use o SDK do dispositivo IoT do Azure para Node.js para implementar os aplicativos de dispositivo e o SDK do serviço do IoT do Azure para .NET para implementar um aplicativo de serviço que executa o trabalho."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: a8f4f34aa99c4a9966957cac213ec9170de80a46
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a><span data-ttu-id="a7446-104">Agendar e difundir trabalhos (.NET/Node.js)</span><span class="sxs-lookup"><span data-stu-id="a7446-104">Schedule and broadcast jobs (.NET/Node.js)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="a7446-105">Use o Hub IoT do Azure para agendar e controlar os trabalhos que atualizam milhões de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a7446-105">Use Azure IoT Hub to schedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="a7446-106">Use trabalhos para:</span><span class="sxs-lookup"><span data-stu-id="a7446-106">Use jobs to:</span></span>

* <span data-ttu-id="a7446-107">Atualizar as propriedades desejadas</span><span class="sxs-lookup"><span data-stu-id="a7446-107">Update desired properties</span></span>
* <span data-ttu-id="a7446-108">Marcas de atualização</span><span class="sxs-lookup"><span data-stu-id="a7446-108">Update tags</span></span>
* <span data-ttu-id="a7446-109">Chamar métodos diretos</span><span class="sxs-lookup"><span data-stu-id="a7446-109">Invoke direct methods</span></span>

<span data-ttu-id="a7446-110">Um trabalho encapsula uma dessas ações e controla a execução em um conjunto de dispositivos definido por uma consulta de dispositivo gêmeo.</span><span class="sxs-lookup"><span data-stu-id="a7446-110">A job wraps one of these actions and tracks the execution against a set of devices that is defined by a device twin query.</span></span> <span data-ttu-id="a7446-111">Por exemplo, um aplicativo de back-end pode usar um trabalho para invocar um método direto em 10.000 dispositivos que reinicie os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a7446-111">For example, a back-end app can use a job to invoke a direct method on 10,000 devices that reboots the devices.</span></span> <span data-ttu-id="a7446-112">Você especifica o conjunto de dispositivos com uma consulta de dispositivo gêmeo e agenda o trabalho para execução futura.</span><span class="sxs-lookup"><span data-stu-id="a7446-112">You specify the set of devices with a device twin query and schedule the job to run at a future time.</span></span> <span data-ttu-id="a7446-113">O trabalho controla o andamento conforme cada um dos dispositivos recebe e executa o método direto de reinicialização.</span><span class="sxs-lookup"><span data-stu-id="a7446-113">The job tracks progress as each of the devices receive and execute the reboot direct method.</span></span>

<span data-ttu-id="a7446-114">Para saber mais sobre cada uma dessas capacidades, consulte:</span><span class="sxs-lookup"><span data-stu-id="a7446-114">To learn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="a7446-115">Dispositivo gêmeo e propriedades: [Introdução os dispositivos gêmeos][lnk-get-started-twin] e [Tutorial: Como usar as propriedades do dispositivo gêmeo][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="a7446-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="a7446-116">Métodos diretos: [Guia do desenvolvedor do Hub IoT – métodos diretos][lnk-dev-methods] e [Tutorial: Usar métodos diretos][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="a7446-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="a7446-117">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="a7446-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="a7446-118">Criar um aplicativo de dispositivo que implemente um método chamado **lockDoor** que possa ser chamado pelo aplicativo de back-end.</span><span class="sxs-lookup"><span data-stu-id="a7446-118">Create a device app that implements a direct method called **lockDoor** that can be called by the back-end app.</span></span> <span data-ttu-id="a7446-119">O aplicativo de dispositivo também recebe as alterações de propriedade desejadas do aplicativo de back-end.</span><span class="sxs-lookup"><span data-stu-id="a7446-119">The device app also receives desired property changes from the back-end app.</span></span>
* <span data-ttu-id="a7446-120">Criar um aplicativo de back-end que gere um trabalho para chamar o método direto **lockDoor** em vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a7446-120">Create a back-end app that creates a job to call the **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="a7446-121">Outro trabalho envia as atualizações de propriedade desejadas para vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a7446-121">Another job sends desired property updates to multiple devices.</span></span>

<span data-ttu-id="a7446-122">Ao final deste tutorial, você terá um aplicativo de dispositivo de console Node.js e um aplicativo de back-end do console .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="a7446-122">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="a7446-123">**simDevice.js** que se conecta ao seu hub IoT, implementa o método direto **lockDoor** e manipula as alterações de propriedade desejadas.</span><span class="sxs-lookup"><span data-stu-id="a7446-123">**simDevice.js** that connects to your IoT hub, implements the **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="a7446-124">**ScheduleJob** que usa trabalhos para chamar o método direto **lockDoor** e atualizar as propriedades desejada do dispositivo gêmeo em vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a7446-124">**ScheduleJob** that uses jobs to call the **lockDoor** direct method and update the device twin desired properties on multiple devices.</span></span>

<span data-ttu-id="a7446-125">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="a7446-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="a7446-126">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a7446-126">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="a7446-127">Node.js versão 0.12.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a7446-127">Node.js version 0.12.x or later.</span></span> <span data-ttu-id="a7446-128">O artigo [Preparar o ambiente de desenvolvimento][lnk-dev-setup] descreve como instalar o Node.js para este tutorial no Windows ou no Linux.</span><span class="sxs-lookup"><span data-stu-id="a7446-128">The article [Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="a7446-129">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7446-129">An active Azure account.</span></span> <span data-ttu-id="a7446-130">Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="a7446-130">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a><span data-ttu-id="a7446-131">Agendar trabalhos para chamar um método direto e enviar atualizações ao dispositivo gêmeo</span><span class="sxs-lookup"><span data-stu-id="a7446-131">Schedule jobs for calling a direct method and sending device twin updates</span></span>

<span data-ttu-id="a7446-132">Nesta seção, você cria um aplicativo de console .NET (usando C#) que usa trabalhos para chamar o método direto **lockDoor** e enviar as atualizações de propriedade desejadas para vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a7446-132">In this section, you create a .NET console app (using C#) that uses jobs to call the **lockDoor** direct method and send desired property updates to multiple devices.</span></span>

1. <span data-ttu-id="a7446-133">No Visual Studio, adicione um projeto da Área de Trabalho Clássica do Windows no Visual C# à solução atual usando o modelo de projeto **Aplicativo do Console** .</span><span class="sxs-lookup"><span data-stu-id="a7446-133">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="a7446-134">Nomeie o projeto como **ScheduleJob**.</span><span class="sxs-lookup"><span data-stu-id="a7446-134">Name the project **ScheduleJob**.</span></span>

    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]

1. <span data-ttu-id="a7446-136">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **ScheduleJob** e, em seguida, clique em **Gerenciar Pacotes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="a7446-136">In Solution Explorer, right-click the **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="a7446-137">Na janela **Gerenciador de Pacotes Nuget**, selecione **Procurar**, procure **microsoft.azure.devices**, selecione **Instalar** para instalar o pacote **Microsoft.Azure.Devices** e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="a7446-137">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="a7446-138">Esta etapa baixa, instala e adiciona uma referência ao pacote NuGet do [SDK do serviço IoT do Azure][lnk-nuget-service-sdk] e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="a7446-138">This step downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
1. <span data-ttu-id="a7446-140">Adicione as instruções `using` abaixo na parte superior do arquivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="a7446-140">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. <span data-ttu-id="a7446-141">Adicione a instrução `using` a seguir caso ela não esteja presente nas instruções padrão.</span><span class="sxs-lookup"><span data-stu-id="a7446-141">Add the following `using` statement if not already present in the default statements.</span></span>

    ```csharp
    using System.Threading.Tasks;
    ```

1. <span data-ttu-id="a7446-142">Adicione os seguintes campos à classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="a7446-142">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="a7446-143">Substitua o espaço reservado pela cadeia de conexão do Hub IoT criado na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="a7446-143">Replace the placeholder with the IoT Hub connection string for the hub that you created in the previous section.</span></span>

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. <span data-ttu-id="a7446-144">Adicione o seguinte método à classe **Programa** :</span><span class="sxs-lookup"><span data-stu-id="a7446-144">Add the following method to the **Program** class:</span></span>

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. <span data-ttu-id="a7446-145">Adicione o seguinte método à classe **Programa** :</span><span class="sxs-lookup"><span data-stu-id="a7446-145">Add the following method to the **Program** class:</span></span>

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. <span data-ttu-id="a7446-146">Adicione o seguinte método à classe **Programa** :</span><span class="sxs-lookup"><span data-stu-id="a7446-146">Add the following method to the **Program** class:</span></span>

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. <span data-ttu-id="a7446-147">Por fim, adicione as seguintes linhas ao método **Main** :</span><span class="sxs-lookup"><span data-stu-id="a7446-147">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER to run the next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER to exit.");
    Console.ReadLine();
    ```

1. <span data-ttu-id="a7446-148">No Gerenciador de Soluções, abra **Definir projetos de StartUp...** e verifique se a **Ação** para o projeto **ScheduleJob** é **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="a7446-148">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ScheduleJob** project is **Start**.</span></span> <span data-ttu-id="a7446-149">Compilar a solução.</span><span class="sxs-lookup"><span data-stu-id="a7446-149">Build the solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="a7446-150">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="a7446-150">Create a simulated device app</span></span>

<span data-ttu-id="a7446-151">Nesta seção, você cria um aplicativo de console do Node.js que responde a um método direto chamado pela nuvem, que dispara uma reinicialização de dispositivo simulado e usa propriedades relatadas para habilitar consultas em dispositivos gêmeos e identificar os dispositivos e quando eles foram reiniciados pela última vez.</span><span class="sxs-lookup"><span data-stu-id="a7446-151">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated device reboot and uses the reported properties to enable device twin queries to identify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="a7446-152">Crie uma nova pasta vazia denominada **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="a7446-152">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="a7446-153">Na pasta **simDevice**, crie um arquivo package.json usando o comando a seguir no seu prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="a7446-153">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="a7446-154">Aceite todos os padrões:</span><span class="sxs-lookup"><span data-stu-id="a7446-154">Accept all the defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="a7446-155">No prompt de comando, na pasta **simDevice**, execute o seguinte comando para instalar o pacote **azure-iot-device** e os pacotes **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="a7446-155">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="a7446-156">Usando um editor de texto, crie um novo arquivo **SimDevice.js** na pasta **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="a7446-156">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span></span>

1. <span data-ttu-id="a7446-157">Adicione as seguintes instruções "require" no início do arquivo **simDevice.js**:</span><span class="sxs-lookup"><span data-stu-id="a7446-157">Add the following 'require' statements at the start of the **simDevice.js** file:</span></span>

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. <span data-ttu-id="a7446-158">Adicione uma variável **connectionString** e use-a para criar um **Cliente** do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a7446-158">Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="a7446-159">Lembre-se de substituir os espaços reservados pelos valores apropriados para sua instalação.</span><span class="sxs-lookup"><span data-stu-id="a7446-159">Make sure to replace the placeholders with values appropriate to your setup.</span></span>

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="a7446-160">Adicione a seguinte função para manipular o método **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="a7446-160">Add the following function to handle the **lockDoor** method.</span></span>

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. <span data-ttu-id="a7446-161">Adicione o seguinte código para registrar o manipulador do método **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="a7446-161">Add the following code to register the handler for the **lockDoor** method.</span></span>

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect to IotHub client.');
        }  else {
            console.log('Client connected to IoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. <span data-ttu-id="a7446-162">Salve e feche o arquivo **simDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="a7446-162">Save and close the **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="a7446-163">Para simplificar, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="a7446-163">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="a7446-164">No código de produção, implemente políticas de repetição (como uma retirada exponencial), como sugerido no artigo [Tratamento de falhas transitórias][lnk-transient-faults] do MSDN.</span><span class="sxs-lookup"><span data-stu-id="a7446-164">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="a7446-165">Executar os aplicativos</span><span class="sxs-lookup"><span data-stu-id="a7446-165">Run the apps</span></span>

<span data-ttu-id="a7446-166">Agora você está pronto para executar os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a7446-166">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="a7446-167">No prompt de comando, na pasta **simDevice**, execute o seguinte comando para começar a escutar o método direto de reinicialização.</span><span class="sxs-lookup"><span data-stu-id="a7446-167">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span></span>

    ```cmd/sh
    node simDevice.js
    ```

1. <span data-ttu-id="a7446-168">Execute o aplicativo de console do C# **ScheduleJob** clicando com o botão direito do mouse no projeto **ScheduleJob** e selecionando **Depurar** e **Iniciar nova instância**.</span><span class="sxs-lookup"><span data-stu-id="a7446-168">Run the C# console app **ScheduleJob** by right-clicking on the **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span></span>

1. <span data-ttu-id="a7446-169">Você verá a saída do dispositivo e dos aplicativos back-end.</span><span class="sxs-lookup"><span data-stu-id="a7446-169">You see the output from both device and back-end apps.</span></span>

    ![Executar os aplicativos para agendar trabalhos][img-schedulejobs]

## <a name="next-steps"></a><span data-ttu-id="a7446-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a7446-171">Next steps</span></span>

<span data-ttu-id="a7446-172">Neste tutorial, você usou um trabalho para agendar um método direto para um dispositivo e a atualização das propriedades do twin do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a7446-172">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span></span>

<span data-ttu-id="a7446-173">Para continuar com a introdução ao Hub IoT e aos padrões de gerenciamento de dispositivos como atualização de firmware remota aérea, leia: [Tutorial: Como fazer uma atualização de firmware][lnk-fwupdate].</span><span class="sxs-lookup"><span data-stu-id="a7446-173">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, read [Tutorial: How to do a firmware update][lnk-fwupdate].</span></span>

<span data-ttu-id="a7446-174">Para continuar a introdução ao Hub IoT, consulte [Introdução ao IoT Edge][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="a7446-174">To continue getting started with IoT Hub, see [Getting started with IoT Edge][lnk-iot-edge].</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
