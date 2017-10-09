---
title: "Olá aaaCreate um hub IoT do Azure usando a API REST do provedor de recursos | Microsoft Docs"
description: "Como toouse Olá toocreate de API REST do provedor de recursos um IoT Hub."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 52814ee5-bc10-4abe-9eb2-f8973096c2d8
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 98d240ccce47dec13a255bce28943b40f5354ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a>Criar um hub IoT usando o provedor de recursos de saudação REST API (.NET)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Você pode usar o hello [provedor de recursos de IoT Hub API REST] [ lnk-rest-api] toocreate e gerenciar programaticamente os hubs de IoT do Azure. Este tutorial mostra como toouse Olá toocreate de API REST de provedor de recursos de IoT Hub um hub IoT de um programa c#.

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artigo aborda usando o modelo de implantação do Azure Resource Manager hello.

toocomplete neste tutorial, você precisa Olá a seguir:

* Visual Studio 2015 ou Visual Studio 2017.
* Uma conta ativa do Azure. <br/>Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.
* [Azure PowerShell 1.0][lnk-powershell-install] ou posterior.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Preparar seu projeto do Visual Studio

1. No Visual Studio, crie um projeto de Visual C# Windows clássico Desktop usando Olá **aplicativo de Console (.NET Framework)** modelo de projeto. Projeto de saudação do nome **CreateIoTHubREST**.

2. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e clique em **Gerenciar Pacotes NuGet**.

3. Verifique no Gerenciador de pacotes do NuGet, **incluir pré-lançamento**e em Olá **procurar** pesquisa de página para **Microsoft.Azure.Management.ResourceManager**. Selecionar pacote de saudação, clique em **instalar**, na **Revise as alterações** clique em **Okey**, em seguida, clique em **aceito** tooaccept licenças de saudação.

4. No Gerenciador de Pacotes do NuGet, procure **Microsoft.IdentityModel.Clients.ActiveDirectory**.  Clique em **instalar**, na **Revise as alterações** clique **Okey**, em seguida, clique em **aceito** tooaccept licença de saudação.

5. Em Program.cs, substituir Olá **usando** instruções com hello código a seguir:

    ```csharp
    using System;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Text;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    using Microsoft.Rest;
    using System.Linq;
    using System.Threading;
    ```

6. Em Program.cs, adicione Olá variáveis estáticas, substituindo os valores de espaço reservado Olá a seguir. Você fez uma anotação de **ApplicationId**, **SubscriptionId**, **TenantId** e **Password** anteriormente neste tutorial. **Nome do grupo de recursos** é Olá nome do grupo de recursos de saudação usar ao criar hello IoT hub. Use um grupo de recursos existente ou novo. **Nome do IoT Hub** é nome de saudação do hello IoT Hub cria, tais como **MyIoTHub**. nome de saudação do seu hub IoT deve ser globalmente exclusivo. **Nome da implantação** é um nome para a implantação de saudação, como **Deployment_01**.

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";

    static string rgName = "{Resource group name}";
    static string iotHubName = "{IoT Hub name including your initials}";
    ```
[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a>Use Olá recurso provedor API REST toocreate um hub IoT

Saudação de uso [provedor de recursos de IoT Hub API REST] [ lnk-rest-api] toocreate um hub IoT em seu grupo de recursos. Você também pode usar o hello recurso provedor API REST toomake alterações tooan IoT hub existente.

1. Adicione Olá tooProgram.cs do método a seguir:

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. Adicionar Olá toohello de código a seguir **CreateIoTHub** método. Esse código cria um **HttpClient** objeto com o token de autenticação Olá nos cabeçalhos de saudação:

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. Adicionar Olá toohello de código a seguir **CreateIoTHub** método. Esse código descreve Olá IoT hub toocreate e gera uma representação JSON. Para obter a lista atual Olá locais que dão suporte ao IoT Hub consulte [Status do Azure][lnk-status]:

    ```csharp
    var description = new
    {
      name = iotHubName,
      location = "East US",
      sku = new
      {
        name = "S1",
        tier = "Standard",
        capacity = 1
      }
    };

    var json = JsonConvert.SerializeObject(description, Formatting.Indented);
    ```

4. Adicionar Olá toohello de código a seguir **CreateIoTHub** método. Esse código envia Olá REST solicitação tooAzure. Olá código verifica a resposta hello e recupera a URL de hello, você pode usar toomonitor Olá estado da tarefa de implantação de saudação:

    ```csharp
    var content = new StringContent(JsonConvert.SerializeObject(description), Encoding.UTF8, "application/json");
    var requestUri = string.Format("https://management.azure.com/subscriptions/{0}/resourcegroups/{1}/providers/Microsoft.devices/IotHubs/{2}?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var result = client.PutAsync(requestUri, content).Result;

    if (!result.IsSuccessStatusCode)
    {
      Console.WriteLine("Failed {0}", result.Content.ReadAsStringAsync().Result);
      return;
    }

    var asyncStatusUri = result.Headers.GetValues("Azure-AsyncOperation").First();
    ```

5. Adicionar Olá após o final do código toohello de saudação **CreateIoTHub** método. Esse código usa Olá **asyncStatusUri** endereço recuperado em Olá toowait de etapa anterior para Olá toocomplete de implantação:

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. Adicionar Olá após o final do código toohello de saudação **CreateIoTHub** método. Este código recupera as chaves de saudação do hello hub IoT, você criou e imprime toohello console:

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a>Aplicativo hello completa e execução

Agora você pode concluir aplicativo hello Olá chamada **CreateIoTHub** método antes de compilar e executá-lo.

1. Adicionar Olá após o final do código toohello de saudação **principal** método:

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. Clique em **Criar** e **Compilar Solução**. Corrija todos os erros.

3. Clique em **depurar** e **iniciar depuração** aplicativo hello de toorun. Ele pode levar vários minutos para Olá toorun de implantação.

4. tooverify que seu aplicativo adicionado Olá novo hub IoT, visite Olá [portal do Azure] [ lnk-azure-portal] e exibir a lista de recursos. Como alternativa, use Olá **Get-AzureRmResource** cmdlet do PowerShell.

> [!NOTE]
> Este aplicativo de exemplo adiciona um Hub IoT Standard S1 pelo qual você será cobrado. Quando tiver terminado, você pode excluir o hub IoT de saudação por meio de saudação [portal do Azure] [ lnk-azure-portal] ou usando Olá **Remove-AzureRmResource** cmdlet do PowerShell quando tiver terminado.

## <a name="next-steps"></a>Próximas etapas
Agora que você implantou um hub IoT usando o provedor de recursos de saudação API REST, você poderá desejar tooexplore adicional:

* Leia sobre os recursos de saudação do hello [provedor de recursos de IoT Hub API REST][lnk-rest-api].
* Leitura [visão geral do Gerenciador de recursos do Azure] [ lnk-azure-rm-overview] toolearn mais sobre os recursos de saudação do Gerenciador de recursos do Azure.

toolearn mais sobre como desenvolver para o IoT Hub, consulte Olá artigos a seguir:

* [Introdução tooC SDK][lnk-c-sdk]
* [SDKs do Azure IoT][lnk-sdks]

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
