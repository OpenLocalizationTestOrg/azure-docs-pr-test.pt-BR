---
title: "Introdução ao gerenciamento de dispositivo de Hub IoT do Azure (.NET/Node) | Microsoft Docs"
description: "Como usar o gerenciamento de dispositivos do Hub IoT do Azure para iniciar uma reinicialização do dispositivo remoto. Use o SDK do dispositivo IoT do Azure para Node.js para implementar um aplicativo de dispositivo simulado que inclui um método direto e o SDK do serviço do Azure IoT para .NET para implementar um aplicativo de serviço que invoca o método direto."
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
ms.openlocfilehash: d97fc5493570985f94c23032c870628d6a089dcd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-management-netnode"></a><span data-ttu-id="73de7-104">Introdução ao gerenciamento de dispositivos (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="73de7-104">Get started with device management (.NET/Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="73de7-105">Este tutorial mostra como:</span><span class="sxs-lookup"><span data-stu-id="73de7-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="73de7-106">Usar o portal do Azure para criar um Hub IoT e criar uma identidade de dispositivo em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="73de7-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="73de7-107">Crie um aplicativo de dispositivo simulado contendo um método direto que reinicia o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="73de7-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="73de7-108">Métodos diretos são invocados da nuvem.</span><span class="sxs-lookup"><span data-stu-id="73de7-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="73de7-109">Criar um aplicativo de console .NET que chama um método direto de reinicialização no aplicativo de dispositivo simulado por meio do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="73de7-109">Create a .NET console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="73de7-110">Ao final deste tutorial, você terá um aplicativo de dispositivo de console Node.js e um aplicativo de back-end do console .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="73de7-110">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="73de7-111">**dmpatterns_getstarted_device.js**, que conecta seu hub IoT com a identidade do dispositivo criada anteriormente, recebe um método direto de reinicialização, simula uma reinicialização física e informa a hora da última reinicialização.</span><span class="sxs-lookup"><span data-stu-id="73de7-111">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="73de7-112">**TriggerReboot**, que chama um método direto no aplicativo de dispositivo simulado, exibe a resposta e exibe as propriedades relatadas atualizadas.</span><span class="sxs-lookup"><span data-stu-id="73de7-112">**TriggerReboot**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="73de7-113">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="73de7-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="73de7-114">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="73de7-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="73de7-115">Node.js versão 0.12.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="73de7-115">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="73de7-116">[Preparar o ambiente de desenvolvimento][lnk-dev-setup] descreve como instalar o Node.js para este tutorial no Windows ou no Linux.</span><span class="sxs-lookup"><span data-stu-id="73de7-116">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="73de7-117">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="73de7-117">An active Azure account.</span></span> <span data-ttu-id="73de7-118">(Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)</span><span class="sxs-lookup"><span data-stu-id="73de7-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="73de7-119">Disparar uma reinicialização remota no dispositivo usando um método direto</span><span class="sxs-lookup"><span data-stu-id="73de7-119">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="73de7-120">Nesta seção, você criará um aplicativo do console .NET (usando C#) que inicia uma reinicialização remota em um dispositivo usando um método direto.</span><span class="sxs-lookup"><span data-stu-id="73de7-120">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="73de7-121">O aplicativo usa consultas de dispositivo gêmeo para descobrir o último horário de reinicialização para esse dispositivo.</span><span class="sxs-lookup"><span data-stu-id="73de7-121">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="73de7-122">No Visual Studio, adicione um projeto da Área de Trabalho Clássica do Windows no Visual C# a uma nova solução usando o modelo de projeto **Aplicativo do Console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="73de7-122">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="73de7-123">Verifique se a versão do .NET Framework é 4.5.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="73de7-123">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="73de7-124">Nomeie o projeto como **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="73de7-124">Name the project **TriggerReboot**.</span></span>

    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]

2. <span data-ttu-id="73de7-126">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **TriggerReboot** e, em seguida, clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="73de7-126">In Solution Explorer, right-click the **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="73de7-127">Na janela **Gerenciador de Pacotes Nuget**, selecione **Procurar**, procure **microsoft.azure.devices**, selecione **Instalar** para instalar o pacote **Microsoft.Azure.Devices** e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="73de7-127">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="73de7-128">O procedimento baixa, instala e adiciona uma referência ao [pacote Nuget do SDK do Dispositivo IoT do Azure][lnk-nuget-service-sdk] e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="73de7-128">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
4. <span data-ttu-id="73de7-130">Adicione as instruções `using` abaixo na parte superior do arquivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="73de7-130">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. <span data-ttu-id="73de7-131">Adicione os seguintes campos à classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="73de7-131">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="73de7-132">Substitua o valor do espaço reservado pela cadeia de conexão do Hub IoT criado na seção anterior e no dispositivo de destino.</span><span class="sxs-lookup"><span data-stu-id="73de7-132">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section and the target device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. <span data-ttu-id="73de7-133">Adicione o seguinte método à classe **Programa**.</span><span class="sxs-lookup"><span data-stu-id="73de7-133">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="73de7-134">Esse código obtém o dispositivo gêmeo para o dispositivo de reinicialização e gera as propriedades relatadas.</span><span class="sxs-lookup"><span data-stu-id="73de7-134">This code gets the device twin for the rebooting device and outputs the reported properties.</span></span>
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. <span data-ttu-id="73de7-135">Adicione o seguinte método à classe **Programa**.</span><span class="sxs-lookup"><span data-stu-id="73de7-135">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="73de7-136">Esse código inicia uma reinicialização no dispositivo usando um método direto.</span><span class="sxs-lookup"><span data-stu-id="73de7-136">This code initiates the reboot on the device using a direct method.</span></span>

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. <span data-ttu-id="73de7-137">Por fim, adicione as seguintes linhas ao método **Main** :</span><span class="sxs-lookup"><span data-stu-id="73de7-137">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
8. <span data-ttu-id="73de7-138">Compilar a solução.</span><span class="sxs-lookup"><span data-stu-id="73de7-138">Build the solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="73de7-139">Criar um aplicativo de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="73de7-139">Create a simulated device app</span></span>
<span data-ttu-id="73de7-140">Nesta seção, você irá</span><span class="sxs-lookup"><span data-stu-id="73de7-140">In this section, you will</span></span>

* <span data-ttu-id="73de7-141">Criar um aplicativo de console do Node.js que responde a um método direto chamado pela nuvem</span><span class="sxs-lookup"><span data-stu-id="73de7-141">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="73de7-142">Disparar uma reinicialização do dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="73de7-142">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="73de7-143">Usar as propriedades relatadas para habilitar consultas de dispositivo gêmeo para identificar dispositivos e a última reinicialização</span><span class="sxs-lookup"><span data-stu-id="73de7-143">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="73de7-144">Criar uma nova pasta vazia denominada **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="73de7-144">Create a new empty folder called **manageddevice**.</span></span>  <span data-ttu-id="73de7-145">Na pasta **manageddevice**, crie um arquivo package.json usando o comando a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="73de7-145">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="73de7-146">Aceite todos os padrões:</span><span class="sxs-lookup"><span data-stu-id="73de7-146">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="73de7-147">No prompt de comando na pasta **manageddevice**, execute o seguinte comando para instalar o pacote **azure-iot-device** do SDK do Dispositivo e o pacote **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="73de7-147">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="73de7-148">Usando um editor de texto, crie um novo arquivo **dmpatterns_getstarted_device.js** na pasta **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="73de7-148">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="73de7-149">Adicione as seguintes instruções ‘require’ no início do arquivo **dmpatterns_getstarted_device.js**:</span><span class="sxs-lookup"><span data-stu-id="73de7-149">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="73de7-150">Adicione uma variável **connectionString** e use-a para criar um **Cliente** do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="73de7-150">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="73de7-151">Substitua a cadeia de conexão de dispositivo pela cadeia de conexão do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="73de7-151">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="73de7-152">Adicione a seguinte função para implementar o método direto no dispositivo</span><span class="sxs-lookup"><span data-stu-id="73de7-152">Add the following function to implement the direct method on the device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report the reboot before the physical restart
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
7. <span data-ttu-id="73de7-153">Adicione o seguinte código para abrir a conexão com o Hub IoT e inicie o ouvinte do método direto:</span><span class="sxs-lookup"><span data-stu-id="73de7-153">Add the following code to open the connection to your IoT hub and start the direct method listener:</span></span>
   
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
8. <span data-ttu-id="73de7-154">Salve e feche o arquivo **dmpatterns_getstarted_device.js**.</span><span class="sxs-lookup"><span data-stu-id="73de7-154">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>
   
> [!NOTE]
> <span data-ttu-id="73de7-155">Para simplificar, este tutorial não implementa nenhuma política de repetição.</span><span class="sxs-lookup"><span data-stu-id="73de7-155">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="73de7-156">No código de produção, implemente políticas de repetição (como uma retirada exponencial), como sugerido no artigo [Tratamento de falhas transitórias][lnk-transient-faults] do MSDN.</span><span class="sxs-lookup"><span data-stu-id="73de7-156">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="run-the-apps"></a><span data-ttu-id="73de7-157">Executar os aplicativos</span><span class="sxs-lookup"><span data-stu-id="73de7-157">Run the apps</span></span>
<span data-ttu-id="73de7-158">Agora você está pronto para executar os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="73de7-158">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="73de7-159">No prompt de comando da pasta **manageddevice**, execute o seguinte comando para iniciar a escutar o método direto de reinicialização.</span><span class="sxs-lookup"><span data-stu-id="73de7-159">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="73de7-160">Execute o aplicativo de console do C# **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="73de7-160">Run the C# console app **TriggerReboot**.</span></span> <span data-ttu-id="73de7-161">Clique com o botão direito do mouse no projeto **TriggerReboot**, selecione **Depurar** e, em seguida, **Iniciar nova instância**.</span><span class="sxs-lookup"><span data-stu-id="73de7-161">Right-click the **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span>

3. <span data-ttu-id="73de7-162">Você verá a resposta do dispositivo para o método direto no console.</span><span class="sxs-lookup"><span data-stu-id="73de7-162">You see the device response to the direct method in the console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/