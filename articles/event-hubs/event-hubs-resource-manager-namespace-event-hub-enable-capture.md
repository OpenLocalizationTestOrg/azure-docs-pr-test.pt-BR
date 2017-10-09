---
title: um namespace de Hubs de eventos do Azure e habilitar capturam usando um modelo de aaaCreate | Microsoft Docs
description: Criar um namespace de Hubs de Eventos do Azure com um hub de eventos e habilitar a Captura usando um modelo do Azure Resource Manager
services: event-hubs
documentationcenter: .net
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 8bdda6a2-5ff1-45e3-b696-c553768f1090
ms.service: event-hubs
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: a43b4e8d690ae825047e8a9d609bfda89cf2a06f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a>Criar um namespace de Hubs de Eventos com o hub de eventos e habilitar a Captura usando um modelo do Azure Resource Manager

Este artigo mostra como toouse um modelo do Gerenciador de recursos do Azure que cria um namespace de Hubs de eventos, com instância de hub de um evento e também permite Olá [o recurso de captura](event-hubs-capture-overview.md) no hub de eventos de saudação. Olá artigo descreve como toodefine quais recursos são implantados e como toodefine parâmetros que são especificados quando a implantação de saudação for executada. Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos.

Este artigo também mostra como toospecify que os eventos são capturados em Blobs de armazenamento do Azure ou um repositório Azure Data Lake, com base em Olá destino que você escolher.

Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].

Para saber mais sobre as práticas e os padrões de convenções de nomenclatura de Recursos do Azure, confira [Convenções de nomenclatura de funcionalidade do Azure][Azure Resources naming conventions].

Para modelos de saudação concluída, clique em Olá GitHub links a seguir:

- [Modelo de tooStorage de captura de hub e habilitação de eventos][Event Hub and enable Capture tooStorage template] 
- [Hub e habilitar captura tooAzure repositório Data Lake modelo de evento][Event Hub and enable Capture tooAzure Data Lake Store template]

> [!NOTE]
> toocheck para modelos de hello mais recentes, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] galeria e pesquisa para Hubs de eventos.
> 
> 

## <a name="what-will-you-deploy"></a>O que você implantará?

Com esse modelo, você implanta um namespace de Hub de Eventos com um hub de eventos e também habilita a [Captura dos Hubs de Eventos](event-hubs-capture-overview.md).

[Hubs de eventos](event-hubs-what-is-event-hubs.md) é um evento de processamento de serviço usado tooprovide eventos e telemetria entrada tooAzure em grande escala, com baixa latência e alta confiabilidade. Evento Hubs de captura permite que você tooautomatically entregar Olá streaming de dados no armazenamento de Blob tooAzure Hubs de eventos ou repositório Azure Data Lake, dentro de um tempo especificado ou o intervalo de tamanho de sua escolha.

Clique em Olá tooenable botão capturar de Hubs de eventos a seguir no armazenamento do Azure:

[![Implantar tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)

Clique em Olá tooenable botão capturar de Hubs de eventos a seguir no repositório Azure Data Lake:

[![Implantar tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)

## <a name="parameters"></a>parâmetros

No Gerenciador de recursos do Azure, você define parâmetros para os valores desejados toospecify quando Olá modelo é implantado. modelo de saudação inclui uma seção chamada `Parameters` que contém todos os valores de parâmetro hello. Você deve definir um parâmetro para os valores que variam com base no projeto Olá que estiver implantando ou com base no ambiente de saudação que você está implantando. Não defina parâmetros para valores que permanecem sempre Olá mesmo. Cada valor de parâmetro é usado em Olá modelo toodefine Olá recursos implantados.

modelo de saudação define Olá parâmetros a seguir.

### <a name="eventhubnamespacename"></a>eventHubNamespaceName

nome de saudação do hello [Hubs de eventos namespace](event-hubs-create.md) toocreate.

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a>eventHubName

nome de saudação do hub de eventos de saudação criado no hello [namespace de Hubs de eventos](event-hubs-create.md).

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a>messageRetentionInDays

número de saudação de mensagens de saudação tooretain dias no hub de eventos de saudação. 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long tooretain hello data in event hub"
     }
 }
```

### <a name="partitioncount"></a>partitionCount

número de saudação de toocreate de partições no hub de eventos de saudação.

```json
"partitionCount":{
    "type":"int",
    "defaultValue":2,
    "minValue":2,
    "maxValue":32,
    "metadata":{
        "description":"Number of partitions chosen"
    }
 }
```

### <a name="captureenabled"></a>captureEnabled

Habilite a captura no hub de eventos de saudação.

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable hello Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a>captureEncodingFormat

formato de codificação Olá especificar dados de evento de saudação tooserialize.

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"hello encoding format in which Capture serializes hello EventData"
    }
}
```

### <a name="capturetime"></a>captureTime

intervalo de tempo de saudação na qual Hubs de evento captura inicia a captura de dados de saudação.

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"hello time window in seconds for hello capture"
    }
}
```

### <a name="capturesize"></a>captureSize
intervalo de tamanho de saudação em que a captura inicia a captura de dados de saudação.

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"hello size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a>captureNameFormat

formato de nome de saudação usado por Hubs de evento captura o toowrite Olá Avro arquivos. Observe que um formato de nome de Captura deve conter os campos `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` e `{Second}`. Eles podem ficar organizados em qualquer ordem, com ou sem delimitadores.
 
```json
"captureNameFormat": {
      "type": "string",
      "defaultValue": "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}",
      "metadata": {
        "description": "A Capture Name Format must contain {Namespace}, {EventHub}, {PartitionId}, {Year}, {Month}, {Day}, {Hour}, {Minute} and {Second} fields. These can be arranged in any order with or without delimeters. E.g.  Prod_{EventHub}/{Namespace}\\{PartitionId}_{Year}_{Month}/{Day}/{Hour}/{Minute}/{Second}"
      }
    }
  }
```

### <a name="apiversion"></a>apiVersion

versão de API de saudação do modelo de hello.

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

Use Olá parâmetros a seguir se você escolher o armazenamento do Azure como seu destino.

### <a name="destinationstorageaccountresourceid"></a>destinationStorageAccountResourceId

Captura requer um tooenable de ID de recurso do armazenamento do Azure conta capturar tooyour desejado a conta de armazenamento.

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a>blobContainerName

Olá contêiner de blob no qual toocapture seus dados de evento.

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

Use Olá parâmetros a seguir se você escolher o repositório Azure Data Lake como seu destino. Você deve definir permissões em seu caminho de repositório Data Lake, no qual você deseja que o evento de saudação tooCapture. tooset permissões, consulte [neste artigo](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).

###<a name="subscriptionid"></a>subscriptionId

ID de assinatura do namespace de Hubs de eventos hello e repositório Azure Data Lake. Ambos os recursos devem estar sob Olá mesmo ID de assinatura.

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a>dataLakeAccountName

nome do repositório Azure Data Lake Olá Olá dos eventos capturados.

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a>dataLakeFolderPath

caminho de pasta de destino Olá para Olá dos eventos capturados.

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a>Toodeploy de recursos de armazenamento do Azure como eventos de toocaptured de destino

Cria um namespace do tipo **EventHubs**, com um evento e também permite capturar tooAzure armazenamento de Blob.

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('eventHubNamespaceName')]",
         "type":"Microsoft.EventHub/Namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]",
                  "MessageRetentionInDays":"[parameters('messageRetentionInDays')]",
                  "PartitionCount":"[parameters('partitionCount')]",
                  "CaptureDescription":{
                        "enabled":"[parameters('captureEnabled')]",
                        "encoding":"[parameters('captureEncodingFormat')]",
                        "intervalInSeconds":"[parameters('captureTime')]",
                        "sizeLimitInBytes":"[parameters('captureSize')]",
                        "destination":{
                            "name":"EventHubCapture.AzureBlockBlob",
                            "properties":{
                                "StorageAccountResourceId":"[parameters('destinationStorageAccountResourceId')]",
                                "BlobContainer":"[parameters('blobContainerName')]"
                            }
                        } 
                  }

               }

            }
         ]
      }
   ]
```

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a>Toodeploy de recursos para o repositório Azure Data Lake como destino

Cria um namespace do tipo **EventHubs**, hub de eventos de um e também permite que o repositório do captura tooAzure Data Lake.

```json
 "resources": [
        {
            "apiVersion": "2015-08-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "2015-08-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('eventHubName')]",
                        "ArchiveDescription": {
                            "enabled": "true",
                            "encoding": "[parameters('archiveEncodingFormat')]",
                            "intervalInSeconds": "[parameters('archiveTime')]",
                            "sizeLimitInBytes": "[parameters('archiveSize')]",
                            "destination": {
                                "name": "EventHubArchive.AzureDataLake",
                                "properties": {
                                    "DataLakeSubscriptionId": "[parameters('subscriptionId')]",
                                    "DataLakeAccountName": "[parameters('dataLakeAccountName')]",
                                    "DataLakeFolderPath": "[parameters('dataLakeFolderPath')]",
                                    "ArchiveNameFormat": "[parameters('archiveNameFormat')]"
                                }
                            }
                        }
                    }
                }
            ]
        }
    ]
```

## <a name="commands-toorun-deployment"></a>Implantação de toorun de comandos

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell

Implante seu tooenable modelo capturar de Hubs de evento no armazenamento do Azure:
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

Implante seu tooenable modelo capturar de Hubs de evento no repositório Azure Data Lake:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a>CLI do Azure

Escolhendo o Armazenamento de Blobs do Azure como destino:

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

Escolhendo o Azure Data Lake Store como destino:

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a>Próximas etapas

Você também pode configurar a captura de Hubs de eventos por meio de saudação [portal do Azure](https://portal.azure.com). Para obter mais informações, consulte [habilitar a captura de Hubs de evento usando Olá portal do Azure](event-hubs-capture-enable-through-portal.md).

Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

* [Visão Geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Criar um hub de eventos](event-hubs-create.md)
* [Perguntas frequentes sobre os Hubs de Eventos](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
