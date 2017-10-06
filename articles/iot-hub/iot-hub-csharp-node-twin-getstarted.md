---
title: "aaaGet iniciado com twins de dispositivo do Azure IoT Hub (.NET/nó) | Microsoft Docs"
description: "Como toouse Azure IoT Hub dispositivo twins tooadd marcas e, em seguida, use uma consulta de IoT Hub. Usa dispositivo do hello IoT do Azure SDK para Node.js tooimplement Olá dispositivo simulado aplicativo e Olá serviço IoT do Azure SDK para .NET tooimplement um aplicativo de serviço que adiciona marcas hello e executa Olá consulta de IoT Hub."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: elioda
ms.openlocfilehash: 1cec082ebddc19c9b87998a5fd0159d32b07acd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnode"></a>Introdução aos dispositivos gêmeos (.NET/Node)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

No final da saudação deste tutorial, você terá .NET e um aplicativo de console Node. js:

* **AddTagsAndQuery.sln**, um aplicativo de back-end .NET que adiciona marcas e consultas aos dispositivos gêmeos.
* **TwinSimulatedDevice.js**, um aplicativo Node. js que simula um dispositivo que conecta o hub IoT de tooyour com a identidade do dispositivo Olá criada anteriormente e sua condição de conectividade de relatórios.

> [!NOTE]
> artigo Olá [SDKs do Azure IoT] [ lnk-hub-sdks] fornece informações sobre Olá SDKs IoT do Azure que você pode usar toobuild aplicativos de dispositivo e de back-end.
> 
> 

toocomplete este tutorial, você precisa seguir hello:

* Visual Studio 2015 ou Visual Studio 2017.
* Node.js versão 0.10.x ou posterior.
* Uma conta ativa do Azure. (Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a>Criar aplicativo de serviço Olá
Nesta seção, você cria um aplicativo de console do .NET (usando o c#) adiciona duas de dispositivo do local metadados toohello associada **myDeviceId**. Em seguida, consultas twins de dispositivo Olá armazenadas no hub IoT de saudação selecionando Olá dispositivos localizados em Olá nos e hello, em seguida, aqueles que relatou uma conexão de celular.

1. No Visual Studio, adicione uma solução do Visual C# Windows clássico Desktop projeto toohello atual usando Olá **aplicativo de Console** modelo de projeto. Projeto de saudação do nome **AddTagsAndQuery**.
   
    ![Novo projeto da Área de Trabalho Clássica do Windows no Visual C#][img-createapp]
1. No Gerenciador de soluções, clique com botão direito Olá **AddTagsAndQuery** do projeto e, em seguida, clique em **gerenciar pacotes NuGet...** .
1. Em Olá **NuGet Package Manager** janela, selecione **procurar** e procure **microsoft.azure.devices**. Selecione **instalar** tooinstall Olá **Microsoft.Azure.Devices** empacotar e aceitar os termos de uso do hello. Este procedimento faz o download, instala e adiciona uma referência toohello [SDK do serviço de Azure IoT] [ lnk-nuget-service-sdk] NuGet pacote e suas dependências.
   
    ![Janela do Gerenciador de Pacotes NuGet][img-servicenuget]
1. Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:
   
        using Microsoft.Azure.Devices;
1. Adicionar Olá toohello campos a seguir **programa** classe. Substitua o valor de espaço reservado Olá Olá cadeia de caracteres de conexão de IoT Hub hub Olá que você criou na seção anterior hello.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Adicionar Olá após o método toohello **programa** classe:
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    Olá **RegistryManager** classe expõe toointeract necessária do todos os métodos de saudação com twins de dispositivo do serviço de saudação. código anterior Olá primeiro inicializa Olá **registryManager** do objeto, em seguida, recupera Olá duas de dispositivo para **myDeviceId**e finalmente atualiza as marcas com informações de localização de saudação desejada.
   
    Depois de atualizar, ele executa duas consultas: Olá primeiro seleciona apenas twins de dispositivo de saudação de dispositivos localizados em Olá **Redmond43** fábrica Olá segundo refina Olá consulta tooselect somente Olá dispositivos e também são conectados por meio rede de celular.
   
    Observe que Olá o código anterior, quando ele cria Olá **consulta** de objeto, especifica um número máximo de documentos retornados. Olá **consulta** objeto contém um **HasMoreResults** propriedade booleana que você pode usar o hello tooinvoke **GetNextAsTwinAsync** métodos várias vezes tooretrieve todos os resultados. Um método chamado **GetNextAsJson** está disponível para os resultados que não são de dispositivos gêmeos, por exemplo, resultados de consultas de agregação.
1. Finalmente, adicione Olá toohello linhas a seguir **principal** método:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. Olá Gerenciador de soluções, abra o hello **projetos de inicialização definido...**  e certifique-se de saudação **ação** para **AddTagsAndQuery** projeto é **iniciar**. Compile a solução de saudação.
1. Executar este aplicativo clicando em Olá **AddTagsAndQuery** projeto e selecionando **depurar**, seguido por **iniciar nova instância**. Você deve ver um dispositivo nos resultados de Olá Olá consulta pedindo para todos os dispositivos localizados no **Redmond43** e nenhuma consulta Olá que restringe Olá resultados toodevices que usam uma rede de celular.
   
    ![Resultados da consulta na janela][img-addtagapp]

Na próxima seção, Olá, você cria um aplicativo de dispositivo com informações de conectividade de saudação e alterações Olá resultado de consulta Olá na seção anterior hello.

## <a name="create-hello-device-app"></a>Criar aplicativo de dispositivo Olá
Nesta seção, você cria um aplicativo de console Node. js que conecta o hub tooyour como **myDeviceId**e, em seguida, atualiza as suas informações de saudação de toocontain propriedades relatado que ele está conectado usando uma rede de celular.

1. Crie uma nova pasta vazia denominada **reportconnectivity**. Em Olá **reportconnectivity** pasta, crie um novo arquivo Package. JSON usando Olá comando no prompt de comando a seguir. Aceite todos os padrões de saudação.
   
    ```
    npm init
    ```
1. O prompt de comando no hello **reportconnectivity** pasta, execute Olá Olá de tooinstall de comando a seguir **dispositivo de iot do azure**, e **azure iot-dispositivo mqtt** pacote :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. Usando um editor de texto, crie um novo **ReportConnectivity.js** arquivo hello **reportconnectivity** pasta.
1. Adicionar Olá toohello de código a seguir **ReportConnectivity.js** de arquivo e substitua o espaço reservado de saudação para cadeia de caracteres de conexão de dispositivo com hello um copiadas quando você criou Olá **myDeviceId** dispositivo identidade:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    Olá **cliente** objeto expõe todos os métodos de saudação exigem toointeract com twins de dispositivo do dispositivo hello. Olá código anterior, depois que ele inicializa Olá **cliente** objeto recupera Olá duas de dispositivo para **myDeviceId** e atualiza sua propriedade relatada com informações de conectividade de saudação.
1. Executar o aplicativo de dispositivo Olá
   
        node ReportConnectivity.js
   
    Você verá uma mensagem de saudação `twin state reported`.
1. Agora que hello dispositivo relatado suas informações de conectividade, ele aparecerá em ambas as consultas. Executar Olá .NET **AddTagsAndQuery** saudação do aplicativo toorun consultas novamente. Desta vez, **myDeviceId** deve aparecer em ambos os resultados da consulta.
   
    ![][img-addtagapp2]

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, configurado um novo hub IoT no hello portal do Azure e, em seguida, criou uma identidade de dispositivo no registro de identidade do hub de IoT hello. Você adicionou o metadados do dispositivo como marcas de um aplicativo de back-end e gravou informações de conectividade do dispositivo do dispositivo simulado aplicativo tooreport em duas de dispositivo de saudação. Você também aprendeu como tooquery essas informações usando a linguagem de consulta do tipo SQL IoT Hub hello.

Saudação de uso toolearn de recursos a seguir como a:

* Enviar telemetria de dispositivos com hello [começar com o IoT Hub] [ lnk-iothub-getstarted] tutorial,
* Configurar dispositivos com propriedades desejadas de duas dispositivo Olá [uso desejado dispositivos de tooconfigure propriedades] [ lnk-twin-how-to-configure] tutorial,
* controlar dispositivos interativamente (como ativar um ventilador de um aplicativo controlado pelo usuário) com hello [usar métodos diretos] [ lnk-methods-tutorial] tutorial.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-node-twin-getstarted/addtagapp.png
[img-addtagapp2]: media/iot-hub-csharp-node-twin-getstarted/addtagapp2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

