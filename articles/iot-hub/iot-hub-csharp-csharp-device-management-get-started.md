---
title: "Introdução ao gerenciamento de dispositivo de Hub IoT do Azure (.NET/.NET) | Microsoft Docs"
description: "Como usar o gerenciamento de dispositivos do Hub IoT do Azure para iniciar uma reinicialização do dispositivo remoto. Use o SDK do dispositivo IoT do Azure para .NET para implementar um aplicativo de dispositivo simulado que inclua um método direto e o SDK do serviço do Azure IoT para .NET para implementar um aplicativo de serviço que invoque o método direto."
services: iot-hub
documentationcenter: .net
author: JimacoMS2
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/15/2017
ms.author: v-jamebr
ms.openlocfilehash: 3af7fbfb9740e00d9ff9c2b077cb444a8057b8c3
ms.sourcegitcommit: 0930aabc3ede63240f60c2c61baa88ac6576c508
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2017
---
# <a name="get-started-with-device-management-netnet"></a>Introdução ao gerenciamento de dispositivos (.NET/.NET)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Este tutorial mostra como:

* Usar o portal do Azure para criar um Hub IoT e criar uma identidade de dispositivo em seu Hub IoT.
* Crie um aplicativo de dispositivo simulado contendo um método direto que reinicia o dispositivo. Métodos diretos são invocados da nuvem.
* Criar um aplicativo de console .NET que chama um método direto de reinicialização no aplicativo de dispositivo simulado por meio do Hub IoT.

No fim deste tutorial, você terá dois aplicativos de console .NET:

* **SimulateManagedDevice**, que conecta seu hub IoT com a identidade do dispositivo criada anteriormente, recebe um método direto de reinicialização, simula uma reinicialização física e informa a hora da última reinicialização.
* **TriggerReboot**, que chama um método direto no aplicativo de dispositivo simulado, exibe a resposta e exibe as propriedades relatadas atualizadas.

Para concluir este tutorial, você precisará do seguinte:

* Visual Studio 2015 ou Visual Studio 2017.
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a>Disparar uma reinicialização remota no dispositivo usando um método direto
Nesta seção, você criará um aplicativo do console .NET (usando C#) que inicia uma reinicialização remota em um dispositivo usando um método direto. O aplicativo usa consultas de dispositivo gêmeo para descobrir o último horário de reinicialização para esse dispositivo.

1. No Visual Studio, adicione um projeto da Área de Trabalho Clássica do Windows no Visual C# a uma nova solução usando o modelo de projeto **Aplicativo do Console (.NET Framework)**. Verifique se a versão do .NET Framework é 4.5.1 ou posterior. Nomeie o projeto como **TriggerReboot**.

    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createserviceapp]

2. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **TriggerReboot** e, em seguida, clique em **Gerenciar Pacotes NuGet**.
3. Na janela **Gerenciador de Pacotes Nuget**, selecione **Procurar**, procure **microsoft.azure.devices**, selecione **Instalar** para instalar o pacote **Microsoft.Azure.Devices** e aceite os termos de uso. O procedimento baixa, instala e adiciona uma referência ao [pacote Nuget do SDK do Dispositivo IoT do Azure][lnk-nuget-service-sdk] e suas dependências.

    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
4. Adicione as instruções `using` abaixo na parte superior do arquivo **Program.cs** :
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. Adicione os seguintes campos à classe **Program** . Substitua o valor do espaço reservado pela cadeia de conexão do Hub IoT para o hub criado na seção "Criar um hub IoT". 
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static string targetDevice = "myDeviceId";
        
6. Adicione o seguinte método à classe **Programa**.  Esse código obtém o dispositivo gêmeo para o dispositivo de reinicialização e gera as propriedades relatadas.
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. Adicione o seguinte método à classe **Programa**.  Esse código inicia uma reinicialização no dispositivo usando um método direto.

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. Por fim, adicione as seguintes linhas ao método **Main** :
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
8. Compilar a solução.

> [!NOTE]
> Este tutorial executa somente uma única consulta para propriedades relatadas do dispositivo. No código de produção, recomendamos a sondagem para detectar alterações nas propriedades relatadas.

## <a name="create-a-simulated-device-app"></a>Criar um aplicativo de dispositivo simulado
Nesta seção, você irá

* Criar um aplicativo de console do .NET que responde a um método direto chamado pela nuvem
* Disparar uma reinicialização do dispositivo simulado
* Usar as propriedades relatadas para habilitar consultas de dispositivo gêmeo para identificar dispositivos e a última reinicialização

1. No Visual Studio, adicione um projeto da Área de Trabalho Clássica do Windows no Visual C# à solução atual usando o modelo de projeto **Aplicativo do Console** . Chame o projeto de **SimulateManagedDevice**.
   
    ![Novo aplicativo de dispositivo Visual C# Windows clássico][img-createdeviceapp]
    
2. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **SimulateManagedDevice** e clique em **Gerenciar Pacotes NuGet...**.
3. Na janela **Gerenciador de Pacotes NuGet**, selecione **Procurar** e pesquise por **microsoft.azure.devices.client**. Selecione **Instalar** para instalar o pacote **Microsoft.Azure.Devices.Client** e aceite os termos de uso. O procedimento baixa, instala e adiciona uma referência ao [pacote NuGet do SDK do Dispositivo IoT do Azure][lnk-nuget-client-sdk] e suas dependências.
   
    ![Aplicativo de cliente de janela do Gerenciador de Pacotes NuGet][img-clientnuget]
4. Adicione as instruções `using` abaixo na parte superior do arquivo **Program.cs** :
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

5. Adicione os seguintes campos à classe **Program** . Substitua o valor de espaço reservado pela cadeia de conexão do dispositivo que você anotou na seção anterior.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

6. Adicione o seguinte para implementar o método direto no dispositivo:

        static Task<MethodResponse> onReboot(MethodRequest methodRequest, object userContext)
        {
            // In a production device, you would trigger a reboot scheduled to start after this method returns
            // For this sample, we simulate the reboot by writing to the console and updating the reported properties 
            try
            {
                Console.WriteLine("Rebooting!");

                // Update device twin with reboot time. 
                TwinCollection reportedProperties, reboot, lastReboot;
                lastReboot = new TwinCollection();
                reboot = new TwinCollection();
                reportedProperties = new TwinCollection();
                lastReboot["lastReboot"] = DateTime.Now;
                reboot["reboot"] = lastReboot;
                reportedProperties["iothubDM"] = reboot;
                Client.UpdateReportedPropertiesAsync(reportedProperties).Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }

            string result = "'Reboot started.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

7. Por fim, adicione o seguinte código ao método **Principal** para abrir a conexão para o hub IoT e inicializar o ouvinte do método:
   
        try
        {
            Console.WriteLine("Connecting to hub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "reboot" method
            Client.SetMethodHandlerAsync("reboot", onReboot, null).Wait();
            Console.WriteLine("Waiting for reboot method\n Press enter to exit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove the "reboot" handler
            Client.SetMethodHandlerAsync("reboot", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
8. No Visual Studio, no Gerenciador de Soluções, clique com o botão direito na solução e clique em **Definir Projetos de Inicialização...**. Selecione **Projeto único de inicialização** e, em seguida, selecione o projeto **SimulateManagedDevice** no menu suspenso. Compilar a solução.       

> [!NOTE]
> Para simplificar, este tutorial não implementa nenhuma política de repetição. No código de produção, implemente políticas de repetição (como uma retirada exponencial), como sugerido no artigo [Tratamento de falhas transitórias][lnk-transient-faults] do MSDN.


## <a name="run-the-apps"></a>Executar os aplicativos
Agora você está pronto para executar os aplicativos.
1. Execute o aplicativo de dispositivo .NET **SimulateManagedDevice**.  Clique com o botão direito do mouse no projeto **SimulateManagedDevice**, selecione **Depurar** e, em seguida, **Iniciar nova instância**. Ele deve iniciar a escuta para chamadas de método do seu Hub IoT: 

2. Agora que o dispositivo está conectado e aguardando chamadas de método, execute o aplicativo **TriggerReboot** .NET para invocar o método de reinicialização no aplicativo do dispositivo simulado. Clique com o botão direito do mouse no projeto **TriggerReboot**, selecione **Depurar** e, em seguida, **Iniciar nova instância**. Você deverá ver “Reiniciando!” escrito no console **SimulatedManagedDevice** e as propriedades relatadas do dispositivo, que incluem a hora da última reinicialização, escritas no console **TriggerReboot**.
   
    ![Execução de aplicativo de serviço e dispositivo][img-combinedrun]

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-csharp-device-management-get-started/servicesdknuget.png
[img-createserviceapp]: media/iot-hub-csharp-csharp-device-management-get-started/createserviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-device-management-get-started/clientsdknuget.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-device-management-get-started/createdeviceapp.png
[img-combinedrun]: media/iot-hub-csharp-csharp-device-management-get-started/combinedrun.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
