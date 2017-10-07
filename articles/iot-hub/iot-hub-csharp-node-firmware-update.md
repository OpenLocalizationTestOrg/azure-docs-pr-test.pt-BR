---
title: "atualização de firmware aaaDevice com o Azure IoT Hub (.NET/nó) | Microsoft Docs"
description: "Como atualizar o gerenciamento de dispositivos de toouse no Azure IoT Hub tooinitiate um firmware do dispositivo. Use o dispositivo de IoT do Azure de saudação SDK para Node.js tooimplement um aplicativo de dispositivo simulado e Olá serviço IoT do Azure SDK para .NET tooimplement um aplicativo de serviço que dispara a atualização de firmware de saudação."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: d48899651bcd5d67e577c971be0f9453c8f21592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a><span data-ttu-id="fe13d-104">Use o gerenciamento de dispositivo tooinitiate uma atualização de firmware do dispositivo (.NET/nó)</span><span class="sxs-lookup"><span data-stu-id="fe13d-104">Use device management tooinitiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="fe13d-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="fe13d-105">Introduction</span></span>
<span data-ttu-id="fe13d-106">Em Olá [Introdução ao gerenciamento de dispositivo] [ lnk-dm-getstarted] tutorial, você viu como Olá toouse [duas dispositivo] [ lnk-devtwin] e [direto métodos] [ lnk-c2dmethod] tooremotely primitivos reinicializar um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fe13d-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="fe13d-107">Este tutorial usa Olá mesmas primitivas de Hub IoT e mostra como toodo uma ponta a ponta simulados atualização de firmware.</span><span class="sxs-lookup"><span data-stu-id="fe13d-107">This tutorial uses hello same IoT Hub primitives and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="fe13d-108">Esse padrão é usado na implementação de atualização de firmware Olá Olá [exemplo de implementação de dispositivo de Pi framboesa][lnk-rpi-implementation].</span><span class="sxs-lookup"><span data-stu-id="fe13d-108">This pattern is used in hello firmware update implementation for hello [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="fe13d-109">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="fe13d-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="fe13d-110">Crie um aplicativo de console .NET que chama o método direto do hello firmwareUpdate no aplicativo do dispositivo simulado Olá por meio de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fe13d-110">Create a .NET console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="fe13d-111">Criar um aplicativo de dispositivo simulado que implementa um método direto **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="fe13d-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="fe13d-112">Esse método inicia um processo de vários estágio que aguarda a imagem do firmware toodownload hello, baixa a imagem do firmware hello e finalmente se aplica a imagem do firmware hello.</span><span class="sxs-lookup"><span data-stu-id="fe13d-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="fe13d-113">Durante cada fase da atualização hello, Olá dispositivo usa Olá relatado propriedades tooreport em andamento.</span><span class="sxs-lookup"><span data-stu-id="fe13d-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="fe13d-114">No final da saudação deste tutorial, você tem um aplicativo de dispositivo do console Node. js e um aplicativo de back-end do console .NET (c#):</span><span class="sxs-lookup"><span data-stu-id="fe13d-114">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="fe13d-115">**dmpatterns_fwupdate_service.js**, que chama um método direto no aplicativo do dispositivo simulado hello, exibe a resposta hello e periodicamente (cada 500 ms) exibe Olá atualizado relatado propriedades.</span><span class="sxs-lookup"><span data-stu-id="fe13d-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="fe13d-116">**TriggerFWUpdate**, que conecta o hub IoT de tooyour com a identidade do dispositivo Olá criada anteriormente, recebe um método firmwareUpdate, é executado por meio de um processo de vários estados toosimulate uma atualização de firmware, incluindo: aguardando o download da imagem Olá, Baixando Olá nova imagem e finalmente aplicar imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe13d-116">**TriggerFWUpdate**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="fe13d-117">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="fe13d-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="fe13d-118">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="fe13d-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="fe13d-119">Node.js versão 0.12.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="fe13d-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="fe13d-120">[Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Node. js para este tutorial no Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="fe13d-120">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="fe13d-121">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe13d-121">An active Azure account.</span></span> <span data-ttu-id="fe13d-122">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="fe13d-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="fe13d-123">Siga Olá [Introdução ao gerenciamento de dispositivo](iot-hub-csharp-node-device-management-get-started.md) artigo toocreate seu hub IoT e obter sua cadeia de caracteres de conexão de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="fe13d-123">Follow hello [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="fe13d-124">Disparar uma atualização de firmware remota no dispositivo hello usando um método direto</span><span class="sxs-lookup"><span data-stu-id="fe13d-124">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="fe13d-125">Nesta seção, você criará um aplicativo do console .NET (usando C#) que inicia uma atualização remota de firmware em um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fe13d-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="fe13d-126">aplicativo Hello usa uma atualização de saudação do método direto tooinitiate e usa dispositivo duas consultas tooperiodically obter status de saudação de atualização de firmware active hello.</span><span class="sxs-lookup"><span data-stu-id="fe13d-126">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="fe13d-127">No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto toohello atual usando Olá **aplicativo de Console** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="fe13d-127">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="fe13d-128">Projeto de saudação do nome **TriggerFWUpdate**.</span><span class="sxs-lookup"><span data-stu-id="fe13d-128">Name hello project **TriggerFWUpdate**.</span></span>

    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]

1. <span data-ttu-id="fe13d-130">No Gerenciador de soluções, clique com botão direito Olá **TriggerFWUpdate** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="fe13d-130">In Solution Explorer, right-click hello **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="fe13d-131">Em Olá **NuGet Package Manager** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="fe13d-131">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="fe13d-132">Este procedimento faz o download, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="fe13d-132">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
1. <span data-ttu-id="fe13d-134">Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="fe13d-134">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="fe13d-135">Adicionar Olá toohello campos a seguir **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="fe13d-135">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="fe13d-136">Substitua Olá Olá de vários valores de espaço reservado com cadeia de caracteres de conexão de IoT Hub hub Olá que você criou na seção anterior hello e hello Id do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fe13d-136">Replace hello multiple placeholder values with hello IoT Hub connection string for hello hub that you created in hello previous section and hello Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="fe13d-137">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="fe13d-137">Add hello following method toohello **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="fe13d-138">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="fe13d-138">Add hello following method toohello **Program** class:</span></span>

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. <span data-ttu-id="fe13d-139">Finalmente, adicione Olá toohello linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="fe13d-139">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. <span data-ttu-id="fe13d-140">Olá Gerenciador de soluções, abra o hello **projetos de inicialização definido...**  e certifique-se de saudação **ação** para **TriggerFWUpdate** projeto é **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="fe13d-140">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="fe13d-141">Compile a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe13d-141">Build hello solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="fe13d-142">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="fe13d-142">Run hello apps</span></span>
<span data-ttu-id="fe13d-143">Agora você está pronto toorun Olá aplicativos.</span><span class="sxs-lookup"><span data-stu-id="fe13d-143">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="fe13d-144">No prompt de comando de saudação de saudação **manageddevice** pasta, execute Olá toobegin comando escuta para o método direto de reinicialização Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="fe13d-144">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="fe13d-145">No Visual Studio, clique em Olá **TriggerFWUpdate** aplicativo de console toohello c# projectRun, selecione **depurar** e **iniciar nova instância**.</span><span class="sxs-lookup"><span data-stu-id="fe13d-145">In Visual Studio, right-click on hello **TriggerFWUpdate** projectRun toohello C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="fe13d-146">Consulte o hello dispositivo resposta toohello método direto no console de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe13d-146">You see hello device response toohello direct method in hello console.</span></span>

    ![Firmware atualizado com êxito][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="fe13d-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fe13d-148">Next steps</span></span>
<span data-ttu-id="fe13d-149">Neste tutorial, você usou um método direto de tootrigger remoto atualização de firmware em um dispositivo e Olá usado o progresso de saudação de toofollow propriedades de atualização de firmware de saudação relatado.</span><span class="sxs-lookup"><span data-stu-id="fe13d-149">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="fe13d-150">toolearn como tooextend seu método de solução e agenda IoT chama em vários dispositivos, consulte Olá [agenda e trabalhos de difusão] [ lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="fe13d-150">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/