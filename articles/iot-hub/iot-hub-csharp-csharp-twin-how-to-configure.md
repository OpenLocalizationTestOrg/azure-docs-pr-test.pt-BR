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
# <a name="use-desired-properties-tooconfigure-devices"></a>Usar propriedades desejadas tooconfigure dispositivos
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

No final da saudação deste tutorial, você tem dois aplicativos de console do .NET:

* **SimulateDeviceConfiguration**, um aplicativo de dispositivo simulado que aguarda uma atualização de configurações desejadas e relata o status de saudação de um processo de atualização de configuração simulada.
* **SetDesiredConfigurationAndQuery**, um aplicativo de back-end, que define a saudação da configuração em um dispositivo desejado e consultas Olá o processo de atualização de configuração.

> [!NOTE]
> artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild aplicativos de dispositivo e de back-end.
> 
> 

toocomplete este tutorial, você precisa seguir hello:

* Visual Studio 2015 ou Visual Studio 2017.
* Uma conta ativa do Azure. Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.

Se você seguiu Olá [Introdução ao twins dispositivo] [ lnk-twin-tutorial] tutorial, você já tem um hub IoT e uma identidade de dispositivo chamado **myDeviceId**. Nesse caso, você pode ignorar toohello [criar aplicativo de dispositivo simulado Olá] [ lnk-how-to-configure-createapp] seção.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a>Criar aplicativo de dispositivo simulado Olá
Nesta seção, você cria um aplicativo de console .NET que conecta o hub tooyour como **myDeviceId**, aguarda até que uma atualização de configurações desejadas e, em seguida, relatórios atualizações no processo de atualização de configuração Olá simulada.

1. No Visual Studio, criar um novo projeto do Visual c# Windows clássico Desktop usando Olá **aplicativo de Console** modelo de projeto. Projeto de saudação do nome **SimulateDeviceConfiguration**.
   
    ![Novo aplicativo de dispositivo Visual C# Windows clássico][img-createdeviceapp]

1. No Gerenciador de soluções, clique com botão direito Olá **SimulateDeviceConfiguration** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .
1. Em Olá **NuGet Package Manager** janela, selecione **procurar** e procure **microsoft.azure.devices.client**. Selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices.Client** empacotar e aceitar os termos de uso do hello. Este procedimento faz o download, instala e adiciona uma referência toohello [dispositivo IoT do Azure SDK] [ lnk-nuget-client-sdk] NuGet pacote e suas dependências.
   
    ![Aplicativo de cliente de janela do Gerenciador de Pacotes NuGet][img-clientnuget]
1. Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. Adicionar Olá toohello campos a seguir **programa** classe. Substitua o valor de espaço reservado de saudação com cadeia de conexão do dispositivo Olá observado na seção anterior hello.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. Adicionar Olá após o método toohello **programa** classe:
 
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
    Olá **cliente** objeto expõe todos os métodos de saudação exigem toointeract com twins de dispositivo do dispositivo hello. Olá código mostrado acima, inicializa Olá **cliente** objeto e, em seguida, recupera Olá dispositivo duas para **myDeviceId**.

1. Adicionar Olá após o método toohello **programa** classe. Esse método define os valores iniciais de saudação de telemetria no dispositivo local hello e, em seguida, as atualizações Olá duas do dispositivo.

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

1. Adicionar Olá após o método toohello **programa** classe. Este é um retorno de chamada que detecta uma alteração na *propriedades desejadas* em duas de dispositivo de saudação.

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

    Saudação de atualizações esse método relatado propriedades no objeto de duas Olá dispositivo local com a configuração de saudação atualizar status de saudação de solicitação e conjuntos muito**pendente**, e em seguida, as atualizações Olá duas de dispositivo no serviço de saudação. Depois de atualizar com êxito duas de dispositivo hello, concluir Olá alteração de configuração chamando o método hello `CompleteConfigChange` descrito no próximo ponto de saudação.

1. Adicionar Olá após o método toohello **programa** classe. Esse método simula uma redefinição do dispositivo, em seguida, atualizações Olá propriedades relatadas local definindo o status de saudação muito**êxito** e remove hello **pendingConfig** elemento. Em seguida, atualiza as duas de dispositivo Olá no serviço de saudação. 

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

1. Finalmente, adicione Olá toohello linhas a seguir **principal** método:

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
   > Este tutorial não simula nenhum comportamento para atualizações de configuração simultâneas. Alguns processos de atualização de configuração podem ser capaz de tooaccommodate alterações de configuração de destino durante a execução de atualização hello, alguns dados podem ter tooqueue e alguns podem rejeitá-las com uma condição de erro. Verifique tooconsider se Olá o comportamento desejado para o processo de configuração específica e adicionar lógica apropriada Olá antes de iniciar a alteração de configuração de saudação.
   > 
   > 
1. Criar solução hello e, em seguida, execute o aplicativo de dispositivo de saudação do Visual Studio clicando **F5**. No console de saída de hello, você deve ver mensagens de saudação indicando que seu dispositivo simulado é recuperando duas de dispositivo Olá, configuração de telemetria hello e aguardando a alteração da propriedade desejada. Lembre-Olá aplicativo em execução.

## <a name="create-hello-service-app"></a>Criar aplicativo de serviço Olá
Nesta seção, você criará um aplicativo de console .NET que Olá atualizações *propriedades desejadas* em Olá dispositivo duas associada **myDeviceId** com um novo objeto de configuração de telemetria. Ele, em seguida, consulta twins de dispositivo Olá armazenadas no hub IoT de saudação e mostra diferença Olá entre hello desejado e relatado configurações de dispositivo de saudação.

1. No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto toohello atual usando Olá **aplicativo de Console** modelo de projeto. Projeto de saudação do nome **SetDesiredConfigurationAndQuery**.
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]
1. No Gerenciador de soluções, clique com botão direito Olá **SetDesiredConfigurationAndQuery** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .
1. Em Olá **NuGet Package Manager** janela, selecione **procurar**, procure **microsoft.azure.devices**, selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello. Este procedimento faz o download, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.
   
    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
1. Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. Adicionar Olá toohello campos a seguir **programa** classe. Substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub hub Olá que você criou na seção anterior hello.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Adicionar Olá após o método toohello **programa** classe:
   
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
   
    Olá **registro** objeto expõe toointeract necessária do todos os métodos de saudação com twins de dispositivo do serviço de saudação. Esse código inicializa Olá **registro** objeto recupera Olá duas de dispositivo para **myDeviceId**e, em seguida, atualiza as propriedades desejadas com um novo objeto de configuração de telemetria.
    Depois disso, ele consulta twins de dispositivo Olá armazenadas no hub IoT de saudação a cada 10 segundos, e imprime Olá desejado e relatado configurações de telemetria. Consulte toohello [linguagem de consulta de IoT Hub] [ lnk-query] toolearn como toogenerate rich relatórios em todos os seus dispositivos.
   
   > [!IMPORTANT]
   > Esse aplicativo consulta o Hub IoT a cada 10 segundos para fins ilustrativos. Use consultas toogenerate voltadas para o usuário relatórios em vários dispositivos e não toodetect alterações. Se sua solução exigir notificações em tempo real de eventos de dispositivo, use [notificações gêmeas][lnk-twin-notifications].
   > 
   > 
1. Finalmente, adicione Olá toohello linhas a seguir **principal** método:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. Olá Gerenciador de soluções, abra o hello **projetos de inicialização definido...**  e certifique-se de saudação **ação** para **SetDesiredConfigurationAndQuery** projeto é **iniciar**. Compile a solução de saudação.
1. Com **SimulateDeviceConfiguration** dispositivo que executa o aplicativo, a saudação de execução do serviço de aplicativo do Visual Studio usando **F5**. Você deve ver a configuração relatado Olá alterar de **pendente** muito**êxito** com novo ativo de saudação enviar frequência de cinco minutos, em vez de 24 horas.

 ![Dispositivo configurado com êxito][img-deviceconfigured]
   
   > [!IMPORTANT]
   > Há um atraso de backup tooa minutos entre a operação de relatório de dispositivo hello e resultado da consulta hello. Isso é tooenable Olá consulta infraestrutura toowork em escala muito alta. modos de exibição consistente de duas um único dispositivo tooretrieve usam Olá **getDeviceTwin** método hello **registro** classe.
   > 
   > 

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você definir uma configuração desejada como *propriedades desejadas* da solução Olá back-end e gravou um toodetect de aplicativo de dispositivo que são alterados e simular um processo de atualização de várias etapas relatar seu status por meio de saudação relatada Propriedades.

Saudação de uso toolearn de recursos a seguir como a:

* Enviar telemetria de dispositivos com hello [começar com o IoT Hub] [ lnk-iothub-getstarted] tutorial,
* agendar ou executar operações em grandes conjuntos de dispositivos Consulte Olá [agenda e trabalhos de difusão] [ lnk-schedule-jobs] tutorial.
* controlar dispositivos interativamente (como ativar um ventilador de um aplicativo controlado pelo usuário), com hello [usar métodos diretos] [ lnk-methods-tutorial] tutorial.

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
