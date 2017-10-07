---
title: "trabalhos de aaaSchedule com o Azure IoT Hub (.NET/nó) | Microsoft Docs"
description: "Como tooschedule um Azure IoT Hub trabalho tooinvoke um método direto em vários dispositivos. Você pode usar dispositivo IoT do Azure de saudação SDK para aplicativos de dispositivos do Node. js tooimplement Olá simulado e hello serviço IoT do Azure SDK para .NET tooimplement um trabalho de saudação de toorun de aplicativo de serviço."
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
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a><span data-ttu-id="51bcd-104">Agendar e difundir trabalhos (.NET/Node.js)</span><span class="sxs-lookup"><span data-stu-id="51bcd-104">Schedule and broadcast jobs (.NET/Node.js)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="51bcd-105">Use trabalhos Azure IoT Hub tooschedule e rastrear que atualizam milhões de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="51bcd-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="51bcd-106">Use trabalhos para:</span><span class="sxs-lookup"><span data-stu-id="51bcd-106">Use jobs to:</span></span>

* <span data-ttu-id="51bcd-107">Atualizar as propriedades desejadas</span><span class="sxs-lookup"><span data-stu-id="51bcd-107">Update desired properties</span></span>
* <span data-ttu-id="51bcd-108">Marcas de atualização</span><span class="sxs-lookup"><span data-stu-id="51bcd-108">Update tags</span></span>
* <span data-ttu-id="51bcd-109">Chamar métodos diretos</span><span class="sxs-lookup"><span data-stu-id="51bcd-109">Invoke direct methods</span></span>

<span data-ttu-id="51bcd-110">Um trabalho envolve uma dessas ações e rastreia Olá execução em um conjunto de dispositivos que é definido por uma consulta de duas do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="51bcd-110">A job wraps one of these actions and tracks hello execution against a set of devices that is defined by a device twin query.</span></span> <span data-ttu-id="51bcd-111">Por exemplo, um aplicativo de back-end pode usar um trabalho tooinvoke um método direto em 10.000 dispositivos que reinicia dispositivos hello.</span><span class="sxs-lookup"><span data-stu-id="51bcd-111">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="51bcd-112">Você especifica o conjunto de saudação de dispositivos com uma consulta de duas do dispositivo e agenda Olá trabalho toorun no futuro.</span><span class="sxs-lookup"><span data-stu-id="51bcd-112">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="51bcd-113">Olá trabalho rastreia progresso como cada um dos dispositivos de saudação receber e executar o método direto de reinicialização hello.</span><span class="sxs-lookup"><span data-stu-id="51bcd-113">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="51bcd-114">toolearn mais sobre cada um desses recursos, consulte:</span><span class="sxs-lookup"><span data-stu-id="51bcd-114">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="51bcd-115">Duas do dispositivo e propriedades: [Introdução ao twins dispositivo] [ lnk-get-started-twin] e [Tutorial: como dispositivo toouse macros propriedades][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="51bcd-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="51bcd-116">Métodos diretos: [Guia do desenvolvedor do Hub IoT – métodos diretos][lnk-dev-methods] e [Tutorial: Usar métodos diretos][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="51bcd-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="51bcd-117">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="51bcd-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="51bcd-118">Criar um aplicativo de dispositivo que implementa um método chamado **lockDoor** que pode ser chamado pelo aplicativo de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="51bcd-118">Create a device app that implements a direct method called **lockDoor** that can be called by hello back-end app.</span></span> <span data-ttu-id="51bcd-119">aplicativo de dispositivo Olá também recebe alterações de propriedade desejados do aplicativo de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="51bcd-119">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="51bcd-120">Criar um aplicativo de back-end que cria uma saudação do trabalho toocall **lockDoor** método direto em vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="51bcd-120">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="51bcd-121">Outro trabalho envia toomultiple dispositivos de atualizações de propriedade desejados.</span><span class="sxs-lookup"><span data-stu-id="51bcd-121">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="51bcd-122">No final da saudação deste tutorial, você tem um aplicativo de dispositivo do console Node. js e um aplicativo de back-end do console .NET (c#):</span><span class="sxs-lookup"><span data-stu-id="51bcd-122">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="51bcd-123">**simDevice.js** que se conecta tooyour IoT hub, implementa Olá **lockDoor** direcionar o método e manipula desejado alterações de propriedade.</span><span class="sxs-lookup"><span data-stu-id="51bcd-123">**simDevice.js** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="51bcd-124">**ScheduleJob** que usa a saudação de toocall trabalhos **lockDoor** direta duas de dispositivo de saudação do método e atualização desejado propriedades em vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="51bcd-124">**ScheduleJob** that uses jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

<span data-ttu-id="51bcd-125">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="51bcd-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="51bcd-126">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="51bcd-126">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="51bcd-127">Node.js versão 0.12.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="51bcd-127">Node.js version 0.12.x or later.</span></span> <span data-ttu-id="51bcd-128">artigo Olá [preparar seu ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Node. js para este tutorial no Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="51bcd-128">hello article [Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="51bcd-129">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="51bcd-129">An active Azure account.</span></span> <span data-ttu-id="51bcd-130">Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="51bcd-130">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a><span data-ttu-id="51bcd-131">Agendar trabalhos para chamar um método direto e enviar atualizações ao dispositivo gêmeo</span><span class="sxs-lookup"><span data-stu-id="51bcd-131">Schedule jobs for calling a direct method and sending device twin updates</span></span>

<span data-ttu-id="51bcd-132">Nesta seção, você cria um console aplicativo .NET (usando o c#) que usa a saudação de toocall trabalhos **lockDoor** método direto e enviar toomultiple dispositivos de atualizações de propriedade desejados.</span><span class="sxs-lookup"><span data-stu-id="51bcd-132">In this section, you create a .NET console app (using C#) that uses jobs toocall hello **lockDoor** direct method and send desired property updates toomultiple devices.</span></span>

1. <span data-ttu-id="51bcd-133">No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto toohello atual usando Olá **aplicativo de Console** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="51bcd-133">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="51bcd-134">Projeto de saudação do nome **ScheduleJob**.</span><span class="sxs-lookup"><span data-stu-id="51bcd-134">Name hello project **ScheduleJob**.</span></span>

    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]

1. <span data-ttu-id="51bcd-136">No Gerenciador de soluções, clique com botão direito Olá **ScheduleJob** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="51bcd-136">In Solution Explorer, right-click hello **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="51bcd-137">Em Olá **NuGet Package Manager** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="51bcd-137">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="51bcd-138">Esta etapa baixa, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="51bcd-138">This step downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
1. <span data-ttu-id="51bcd-140">Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="51bcd-140">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. <span data-ttu-id="51bcd-141">Adicione o seguinte Olá `using` instrução se não estiver presente em instruções de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="51bcd-141">Add hello following `using` statement if not already present in hello default statements.</span></span>

    ```csharp
    using System.Threading.Tasks;
    ```

1. <span data-ttu-id="51bcd-142">Adicionar Olá toohello campos a seguir **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="51bcd-142">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="51bcd-143">Substitua o espaço reservado de saudação com hello cadeia de caracteres de conexão de IoT Hub hub Olá que você criou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="51bcd-143">Replace hello placeholder with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. <span data-ttu-id="51bcd-144">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="51bcd-144">Add hello following method toohello **Program** class:</span></span>

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

1. <span data-ttu-id="51bcd-145">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="51bcd-145">Add hello following method toohello **Program** class:</span></span>

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

1. <span data-ttu-id="51bcd-146">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="51bcd-146">Add hello following method toohello **Program** class:</span></span>

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

1. <span data-ttu-id="51bcd-147">Finalmente, adicione Olá toohello linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="51bcd-147">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. <span data-ttu-id="51bcd-148">Olá Gerenciador de soluções, abra o hello **projetos de inicialização definido...**  e certifique-se de saudação **ação** para **ScheduleJob** projeto é **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="51bcd-148">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ScheduleJob** project is **Start**.</span></span> <span data-ttu-id="51bcd-149">Compile a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="51bcd-149">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="51bcd-150">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="51bcd-150">Create a simulated device app</span></span>

<span data-ttu-id="51bcd-151">Nesta seção, você cria um aplicativo de console Node. js que responde tooa método direto chamado pela nuvem hello, o que dispara uma reinicialização do dispositivo simulado e usa Olá relatado propriedades tooenable dispositivos duas consultas tooidentify dispositivos e quando eles reiniciado pela última vez.</span><span class="sxs-lookup"><span data-stu-id="51bcd-151">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="51bcd-152">Crie uma nova pasta vazia denominada **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="51bcd-152">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="51bcd-153">Em Olá **simDevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="51bcd-153">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="51bcd-154">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="51bcd-154">Accept all hello defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="51bcd-155">O prompt de comando no hello **simDevice** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure** e **azure iot-dispositivo mqtt** pacotes:</span><span class="sxs-lookup"><span data-stu-id="51bcd-155">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="51bcd-156">Usando um editor de texto, crie um novo **simDevice.js** arquivo hello **simDevice** pasta.</span><span class="sxs-lookup"><span data-stu-id="51bcd-156">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>

1. <span data-ttu-id="51bcd-157">Adicionar instruções no início de saudação do hello seguinte Olá 'requer' **simDevice.js** arquivo:</span><span class="sxs-lookup"><span data-stu-id="51bcd-157">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. <span data-ttu-id="51bcd-158">Adicionar um **connectionString** variável e use-toocreate uma **cliente** instância.</span><span class="sxs-lookup"><span data-stu-id="51bcd-158">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="51bcd-159">Verifique os espaços reservados de saudação tooreplace-se de que a instalação de tooyour apropriado de valores.</span><span class="sxs-lookup"><span data-stu-id="51bcd-159">Make sure tooreplace hello placeholders with values appropriate tooyour setup.</span></span>

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="51bcd-160">Adicionar Olá Olá de toohandle de função a seguir **lockDoor** método.</span><span class="sxs-lookup"><span data-stu-id="51bcd-160">Add hello following function toohandle hello **lockDoor** method.</span></span>

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. <span data-ttu-id="51bcd-161">Adicionar Olá após código tooregister Olá manipulador Olá **lockDoor** método.</span><span class="sxs-lookup"><span data-stu-id="51bcd-161">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. <span data-ttu-id="51bcd-162">Salve e feche o hello **simDevice.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="51bcd-162">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="51bcd-163">coisas tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="51bcd-163">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="51bcd-164">No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="51bcd-164">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="51bcd-165">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="51bcd-165">Run hello apps</span></span>

<span data-ttu-id="51bcd-166">Agora você está pronto toorun Olá aplicativos.</span><span class="sxs-lookup"><span data-stu-id="51bcd-166">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="51bcd-167">No prompt de comando de saudação de saudação **simDevice** pasta, execute Olá toobegin comando escuta para o método direto de reinicialização Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="51bcd-167">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>

    ```cmd/sh
    node simDevice.js
    ```

1. <span data-ttu-id="51bcd-168">Aplicativo de console Olá execução c# **ScheduleJob** clicando em Olá **ScheduleJob** projeto, selecionando **depurar** e **iniciar nova instância**.</span><span class="sxs-lookup"><span data-stu-id="51bcd-168">Run hello C# console app **ScheduleJob** by right-clicking on hello **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span></span>

1. <span data-ttu-id="51bcd-169">Você verá a saída de saudação do dispositivo e aplicativos de back-end.</span><span class="sxs-lookup"><span data-stu-id="51bcd-169">You see hello output from both device and back-end apps.</span></span>

    ![Executar aplicativos de saudação tooschedule trabalhos][img-schedulejobs]

## <a name="next-steps"></a><span data-ttu-id="51bcd-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="51bcd-171">Next steps</span></span>

<span data-ttu-id="51bcd-172">Neste tutorial, você usou um trabalho tooschedule um dispositivo de tooa método direto e atualização de saudação das propriedades do duas do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="51bcd-172">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="51bcd-173">toocontinue guia de Introdução com padrões de gerenciamento de IoT Hub e o dispositivo como remoto pela atualização de firmware ar hello, leia [Tutorial: como toodo um atualização do firmware][lnk-fwupdate].</span><span class="sxs-lookup"><span data-stu-id="51bcd-173">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, read [Tutorial: How toodo a firmware update][lnk-fwupdate].</span></span>

<span data-ttu-id="51bcd-174">toocontinue guia de Introdução ao IoT Hub, consulte [guia de Introdução com borda IoT][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="51bcd-174">toocontinue getting started with IoT Hub, see [Getting started with IoT Edge][lnk-iot-edge].</span></span>

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
