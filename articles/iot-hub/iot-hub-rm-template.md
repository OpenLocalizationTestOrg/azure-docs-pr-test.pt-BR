---
title: aaaCreate um IoT Hub do Azure usando um modelo (.NET) | Microsoft Docs
description: Como toouse uma toocreate de modelo do Azure Resource Manager um IoT Hub com um programa c#.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a447b40c-c728-487e-875d-db554db5adc3
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 6140deff3553701f994502fd4a60178f874e27cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a>Criar um Hub IoT usando um modelo do Azure Resource Manager (.NET)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Você pode usar o Gerenciador de recursos do Azure toocreate e gerenciar programaticamente os hubs de IoT do Azure. Este tutorial mostra como toouse uma toocreate de modelo do Azure Resource Manager um hub IoT de um programa c#.

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artigo aborda usando o modelo de implantação do Azure Resource Manager hello.

toocomplete neste tutorial, você precisa Olá a seguir:

* Visual Studio 2015 ou Visual Studio 2017.
* Uma conta ativa do Azure. <br/>Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.
* Uma [conta de armazenamento do Azure][lnk-storage-account] em que é possível armazenar seus arquivos de modelo do Azure Resource Manager.
* [Azure PowerShell 1.0][lnk-powershell-install] ou posterior.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Preparar seu projeto do Visual Studio

1. No Visual Studio, crie um projeto de Visual C# Windows clássico Desktop usando Olá **aplicativo de Console (.NET Framework)** modelo de projeto. Projeto de saudação do nome **CreateIoTHub**.

2. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e clique em **Gerenciar Pacotes NuGet**.

3. Verifique no Gerenciador de pacotes do NuGet, **incluir pré-lançamento**e em Olá **procurar** pesquisa de página para **Microsoft.Azure.Management.ResourceManager**. Selecionar pacote de saudação, clique em **instalar**, na **Revise as alterações** clique em **Okey**, em seguida, clique em **aceito** tooaccept licenças de saudação.

4. No Gerenciador de Pacotes do NuGet, procure **Microsoft.IdentityModel.Clients.ActiveDirectory**.  Clique em **instalar**, na **Revise as alterações** clique **Okey**, em seguida, clique em **aceito** tooaccept licença de saudação.

5. Em Program.cs, substituir Olá **usando** instruções com hello código a seguir:

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. Em Program.cs, adicione Olá variáveis estáticas, substituindo os valores de espaço reservado Olá a seguir. Você fez uma anotação de **ApplicationId**, **SubscriptionId**, **TenantId** e **Password** anteriormente neste tutorial. **O nome da sua conta de armazenamento do Azure** é o nome de saudação do hello conta de armazenamento do Azure onde você armazena seus arquivos de modelo do Azure Resource Manager. **Nome do grupo de recursos** é Olá nome do grupo de recursos de saudação usar ao criar hello IoT hub. nome de saudação pode ser um grupo de recursos já existente ou novo. **Nome da implantação** é um nome para a implantação de saudação, como **Deployment_01**.

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";
    static string storageAddress = "https://{Your storage account name}.blob.core.windows.net";
    static string rgName = "{Resource group name}";
    static string deploymentName = "{Deployment name}";
    ```

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Enviar um toocreate modelo um hub IoT

Use um JSON modelo e o parâmetro de arquivo toocreate um hub IoT no grupo de recursos. Você também pode usar um hub de IoT do Azure Resource Manager modelo toomake alterações tooan existente.

1. No Gerenciador de Soluções, clique com o botão direito do mouse no seu projeto, clique em **Adicionar** e depois em **Novo Item**. Adicione um arquivo JSON chamado **template.json** tooyour projeto.

2. tooadd um toohello de hub IoT padrão **Leste dos EUA** região, substituir conteúdo de saudação do **template.json** com hello após a definição de recurso. Para obter a lista atual Olá de regiões que dão suporte ao IoT Hub consulte [Status do Azure][lnk-status]:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

3. No Gerenciador de Soluções, clique com o botão direito do mouse no seu projeto, clique em **Adicionar** e depois em **Novo Item**. Adicione um arquivo JSON chamado **parameters.json** tooyour projeto.

4. Substitua o conteúdo de saudação do **parameters.json** com hello segue as informações de parâmetro que define um nome para o hub IoT da nova hello como **{suas iniciais} mynewiothub**. o nome do hub IoT Olá deve ser globalmente exclusivo para que ele deve incluir seu nome ou iniciais:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": { "value": "mynewiothub" }
      }
    }
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

5. Em **Server Explorer**, conectar tooyour assinatura do Azure e no seu armazenamento do Azure conta criar um contêiner chamado **modelos**. Em Olá **propriedades** painel, Olá conjunto **acesso de leitura público** permissões para Olá **modelos** contêiner muito**Blob**.

6. Em **Server Explorer**, com o botão direito em Olá **modelos** contêiner e clique **exibir contêiner de Blob**. Clique em Olá **carregar Blob** botão, selecione dois arquivos de hello, **parameters.json** e **templates.json**e, em seguida, clique em **abrir** Olá tooupload JSON arquivos toohello **modelos** contêiner. Olá URLs de blobs Olá contendo Olá dados JSON são:

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. Adicione Olá tooProgram.cs do método a seguir:

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. Adicionar Olá toohello de código a seguir **CreateIoTHub** método toosubmit Olá modelo e o parâmetro arquivos toohello Azure Resource Manager:

    ```csharp
    var createResponse = client.Deployments.CreateOrUpdate(
        rgName,
        deploymentName,
        new Deployment()
        {
          Properties = new DeploymentProperties
          {
            Mode = DeploymentMode.Incremental,
            TemplateLink = new TemplateLink
            {
              Uri = storageAddress + "/templates/template.json"
            },
            ParametersLink = new ParametersLink
            {
              Uri = storageAddress + "/templates/parameters.json"
            }
          }
        });
    ```

9. Adicionar Olá toohello de código a seguir **CreateIoTHub** método que exibe o status de saudação e chaves Olá para o hub IoT da nova hello:

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a>Aplicativo hello completa e execução

Agora você pode concluir aplicativo hello Olá chamada **CreateIoTHub** método antes de compilar e executá-lo.

1. Adicionar Olá após o final do código toohello de saudação **principal** método:

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. Clique em **Criar** e **Compilar Solução**. Corrija todos os erros.

3. Clique em **depurar** e **iniciar depuração** aplicativo hello de toorun. Ele pode levar vários minutos para Olá toorun de implantação.

4. tooverify seu aplicativo adicionado Olá novo hub IoT, visite Olá [portal do Azure] [ lnk-azure-portal] e exibir a lista de recursos. Como alternativa, use Olá **Get-AzureRmResource** cmdlet do PowerShell.

> [!NOTE]
> Este aplicativo de exemplo adiciona um Hub IoT Standard S1 pelo qual você será cobrado. Você pode excluir o hub IoT de saudação por meio de saudação [portal do Azure] [ lnk-azure-portal] ou usando Olá **Remove-AzureRmResource** cmdlet do PowerShell quando tiver terminado.

## <a name="next-steps"></a>Próximas etapas
Agora que você implantou um hub IoT usando um modelo do Gerenciador de recursos do Azure com um programa c#, você poderá desejar tooexplore adicional:

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
[lnk-storage-account]:../storage/common/storage-create-storage-account.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
