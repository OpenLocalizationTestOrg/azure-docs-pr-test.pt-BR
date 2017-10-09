---
title: "aaaGet de Introdução ao gerenciamento de dispositivos do Azure IoT Hub (.NET/nó) | Microsoft Docs"
description: "Como tooinitiate de gerenciamento de dispositivo de Azure IoT Hub toouse um dispositivo remoto reinicializar. Você usar o dispositivo de IoT do Azure de saudação SDK para Node.js tooimplement um aplicativo de dispositivo simulado que inclui um método direto e hello serviço IoT do Azure SDK para .NET tooimplement um aplicativo de serviço que invoca o método direto hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: ea6d50dfac1c222d7836e3bf5503c6c9b8c89dfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-netnode"></a><span data-ttu-id="64a65-104">Introdução ao gerenciamento de dispositivos (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="64a65-104">Get started with device management (.NET/Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="64a65-105">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="64a65-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="64a65-106">Use Olá toocreate portal do Azure um IoT Hub e criar uma identidade de dispositivo em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="64a65-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="64a65-107">Crie um aplicativo de dispositivo simulado contendo um método direto que reinicia o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="64a65-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="64a65-108">Métodos diretos são chamados de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="64a65-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="64a65-109">Crie um aplicativo de console .NET que chama o método direto de reinicialização Olá no aplicativo do dispositivo simulado Olá por meio de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="64a65-109">Create a .NET console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="64a65-110">No final da saudação deste tutorial, você tem um aplicativo de dispositivo do console Node. js e um aplicativo de back-end do console .NET (c#):</span><span class="sxs-lookup"><span data-stu-id="64a65-110">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="64a65-111">**dmpatterns_getstarted_device.js**, que conecta o hub IoT de tooyour com a identidade do dispositivo Olá criada anteriormente, recebe um método direto de reinicialização, simula uma reinicialização física e relata o tempo para a última reinicialização do Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="64a65-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="64a65-112">**TriggerReboot**, que chama um método direto no aplicativo do dispositivo simulado hello, exibe a resposta de saudação e exibe Olá atualizado relatado propriedades.</span><span class="sxs-lookup"><span data-stu-id="64a65-112">**TriggerReboot**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="64a65-113">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="64a65-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="64a65-114">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="64a65-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="64a65-115">Node.js versão 0.12.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="64a65-115">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="64a65-116">[Preparar o ambiente de desenvolvimento] [ lnk-dev-setup] descreve como tooinstall Node. js para este tutorial no Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="64a65-116">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="64a65-117">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="64a65-117">An active Azure account.</span></span> <span data-ttu-id="64a65-118">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="64a65-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="64a65-119">Disparar uma reinicialização remota no dispositivo hello usando um método direto</span><span class="sxs-lookup"><span data-stu-id="64a65-119">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="64a65-120">Nesta seção, você criará um aplicativo do console .NET (usando C#) que inicia uma reinicialização remota em um dispositivo usando um método direto.</span><span class="sxs-lookup"><span data-stu-id="64a65-120">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="64a65-121">aplicativo Hello usa Olá de toodiscover hora da última reinicialização do dispositivo duas consultas para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="64a65-121">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="64a65-122">No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto tooa novo usando Olá **aplicativo de Console (.NET Framework)** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="64a65-122">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="64a65-123">Certifique-se de versão do .NET Framework Olá é 4.5.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="64a65-123">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="64a65-124">Projeto de saudação do nome **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="64a65-124">Name hello project **TriggerReboot**.</span></span>

    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]

2. <span data-ttu-id="64a65-126">No Gerenciador de soluções, clique com botão direito Olá **TriggerReboot** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="64a65-126">In Solution Explorer, right-click hello **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="64a65-127">Em Olá **NuGet Package Manager** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="64a65-127">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="64a65-128">Este procedimento faz o download, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="64a65-128">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
4. <span data-ttu-id="64a65-130">Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="64a65-130">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. <span data-ttu-id="64a65-131">Adicionar Olá toohello campos a seguir **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="64a65-131">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="64a65-132">Substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub hub Olá que você criou na seção anterior hello e o dispositivo de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="64a65-132">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section and hello target device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. <span data-ttu-id="64a65-133">Adicionar Olá após o método toohello **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="64a65-133">Add hello following method toohello **Program** class.</span></span>  <span data-ttu-id="64a65-134">Este dispositivo duas do código obtém Olá para Olá Olá dispositivo e saídas de reinicialização relatado propriedades.</span><span class="sxs-lookup"><span data-stu-id="64a65-134">This code gets hello device twin for hello rebooting device and outputs hello reported properties.</span></span>
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. <span data-ttu-id="64a65-135">Adicionar Olá após o método toohello **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="64a65-135">Add hello following method toohello **Program** class.</span></span>  <span data-ttu-id="64a65-136">Esse código inicia Olá reinicialização no dispositivo hello usando um método direto.</span><span class="sxs-lookup"><span data-stu-id="64a65-136">This code initiates hello reboot on hello device using a direct method.</span></span>

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. <span data-ttu-id="64a65-137">Finalmente, adicione Olá toohello linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="64a65-137">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. <span data-ttu-id="64a65-138">Compile a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="64a65-138">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="64a65-139">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="64a65-139">Create a simulated device app</span></span>
<span data-ttu-id="64a65-140">Nesta seção, você irá</span><span class="sxs-lookup"><span data-stu-id="64a65-140">In this section, you will</span></span>

* <span data-ttu-id="64a65-141">Criar um aplicativo de console do Node. js que responde tooa método direto chamado pela nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="64a65-141">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="64a65-142">Disparar uma reinicialização do dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="64a65-142">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="64a65-143">Olá Use relatado propriedades tooenable dispositivos duas consultas tooidentify dispositivos e quando eles reiniciado pela última vez</span><span class="sxs-lookup"><span data-stu-id="64a65-143">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="64a65-144">Criar uma nova pasta vazia denominada **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="64a65-144">Create a new empty folder called **manageddevice**.</span></span>  <span data-ttu-id="64a65-145">Em Olá **manageddevice** pasta, crie um arquivo Package. JSON usando Olá comando no prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="64a65-145">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="64a65-146">Aceite todos os padrões de saudação:</span><span class="sxs-lookup"><span data-stu-id="64a65-146">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="64a65-147">O prompt de comando no hello **manageddevice** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure** pacote do SDK do dispositivo e **azure iot dispositivo-mqtt**pacote:</span><span class="sxs-lookup"><span data-stu-id="64a65-147">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="64a65-148">Usando um editor de texto, crie um novo **dmpatterns_getstarted_device.js** arquivo hello **manageddevice** pasta.</span><span class="sxs-lookup"><span data-stu-id="64a65-148">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="64a65-149">Adicionar instruções no início de saudação do hello seguinte Olá 'requer' **dmpatterns_getstarted_device.js** arquivo:</span><span class="sxs-lookup"><span data-stu-id="64a65-149">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="64a65-150">Adicionar um **connectionString** variável e use-toocreate uma **cliente** instância.</span><span class="sxs-lookup"><span data-stu-id="64a65-150">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="64a65-151">Substitua a cadeia de caracteres de conexão de saudação com a cadeia de caracteres de conexão do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="64a65-151">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="64a65-152">Adicionar Olá seguinte função tooimplement Olá ao método direto no dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="64a65-152">Add hello following function tooimplement hello direct method on hello device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. <span data-ttu-id="64a65-153">Adicione o seguinte Olá hub IoT do tooopen Olá conexão tooyour de código e iniciar o ouvinte de método direto de saudação:</span><span class="sxs-lookup"><span data-stu-id="64a65-153">Add hello following code tooopen hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. <span data-ttu-id="64a65-154">Salve e feche o hello **dmpatterns_getstarted_device.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="64a65-154">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>
   
> [!NOTE]
> <span data-ttu-id="64a65-155">coisas tookeep simples, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="64a65-155">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="64a65-156">No código de produção, você deve implementar políticas de repetição (por exemplo, uma retirada exponencial), conforme sugerido no artigo do MSDN Olá [tratamento de falhas transitórias][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="64a65-156">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="run-hello-apps"></a><span data-ttu-id="64a65-157">Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="64a65-157">Run hello apps</span></span>
<span data-ttu-id="64a65-158">Agora você está pronto toorun Olá aplicativos.</span><span class="sxs-lookup"><span data-stu-id="64a65-158">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="64a65-159">No prompt de comando de saudação de saudação **manageddevice** pasta, execute Olá toobegin comando escuta para o método direto de reinicialização Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="64a65-159">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="64a65-160">Aplicativo de console Olá execução c# **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="64a65-160">Run hello C# console app **TriggerReboot**.</span></span> <span data-ttu-id="64a65-161">Saudação de atalho **TriggerReboot** projeto, selecione **depurar**e, em seguida, selecione **iniciar nova instância**.</span><span class="sxs-lookup"><span data-stu-id="64a65-161">Right-click hello **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span>

3. <span data-ttu-id="64a65-162">Consulte o hello dispositivo resposta toohello método direto no console de saudação.</span><span class="sxs-lookup"><span data-stu-id="64a65-162">You see hello device response toohello direct method in hello console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/