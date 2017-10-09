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
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a><span data-ttu-id="fd180-103">Criar um namespace de Hubs de Eventos com o hub de eventos e habilitar a Captura usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fd180-103">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>

<span data-ttu-id="fd180-104">Este artigo mostra como toouse um modelo do Gerenciador de recursos do Azure que cria um namespace de Hubs de eventos, com instância de hub de um evento e também permite Olá [o recurso de captura](event-hubs-capture-overview.md) no hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd180-104">This article shows how toouse an Azure Resource Manager template that creates an Event Hubs namespace, with one event hub instance, and also enables hello [Capture feature](event-hubs-capture-overview.md) on hello event hub.</span></span> <span data-ttu-id="fd180-105">Olá artigo descreve como toodefine quais recursos são implantados e como toodefine parâmetros que são especificados quando a implantação de saudação for executada.</span><span class="sxs-lookup"><span data-stu-id="fd180-105">hello article describes how toodefine which resources are deployed, and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="fd180-106">Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="fd180-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="fd180-107">Este artigo também mostra como toospecify que os eventos são capturados em Blobs de armazenamento do Azure ou um repositório Azure Data Lake, com base em Olá destino que você escolher.</span><span class="sxs-lookup"><span data-stu-id="fd180-107">This article also shows how toospecify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on hello destination you choose.</span></span>

<span data-ttu-id="fd180-108">Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="fd180-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="fd180-109">Para saber mais sobre as práticas e os padrões de convenções de nomenclatura de Recursos do Azure, confira [Convenções de nomenclatura de funcionalidade do Azure][Azure Resources naming conventions].</span><span class="sxs-lookup"><span data-stu-id="fd180-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span></span>

<span data-ttu-id="fd180-110">Para modelos de saudação concluída, clique em Olá GitHub links a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd180-110">For hello complete templates, click hello following GitHub links:</span></span>

- <span data-ttu-id="fd180-111">[Modelo de tooStorage de captura de hub e habilitação de eventos][Event Hub and enable Capture tooStorage template]</span><span class="sxs-lookup"><span data-stu-id="fd180-111">[Event hub and enable Capture tooStorage template][Event Hub and enable Capture tooStorage template]</span></span> 
- <span data-ttu-id="fd180-112">[Hub e habilitar captura tooAzure repositório Data Lake modelo de evento][Event Hub and enable Capture tooAzure Data Lake Store template]</span><span class="sxs-lookup"><span data-stu-id="fd180-112">[Event hub and enable Capture tooAzure Data Lake Store template][Event Hub and enable Capture tooAzure Data Lake Store template]</span></span>

> [!NOTE]
> <span data-ttu-id="fd180-113">toocheck para modelos de hello mais recentes, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] galeria e pesquisa para Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="fd180-113">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="fd180-114">O que você implantará?</span><span class="sxs-lookup"><span data-stu-id="fd180-114">What will you deploy?</span></span>

<span data-ttu-id="fd180-115">Com esse modelo, você implanta um namespace de Hub de Eventos com um hub de eventos e também habilita a [Captura dos Hubs de Eventos](event-hubs-capture-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fd180-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span></span>

<span data-ttu-id="fd180-116">[Hubs de eventos](event-hubs-what-is-event-hubs.md) é um evento de processamento de serviço usado tooprovide eventos e telemetria entrada tooAzure em grande escala, com baixa latência e alta confiabilidade.</span><span class="sxs-lookup"><span data-stu-id="fd180-116">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span> <span data-ttu-id="fd180-117">Evento Hubs de captura permite que você tooautomatically entregar Olá streaming de dados no armazenamento de Blob tooAzure Hubs de eventos ou repositório Azure Data Lake, dentro de um tempo especificado ou o intervalo de tamanho de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="fd180-117">Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooAzure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span></span>

<span data-ttu-id="fd180-118">Clique em Olá tooenable botão capturar de Hubs de eventos a seguir no armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="fd180-118">Click hello following button tooenable Event Hubs Capture into Azure Storage:</span></span>

<span data-ttu-id="fd180-119">[![Implantar tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="fd180-119">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span></span>

<span data-ttu-id="fd180-120">Clique em Olá tooenable botão capturar de Hubs de eventos a seguir no repositório Azure Data Lake:</span><span class="sxs-lookup"><span data-stu-id="fd180-120">Click hello following button tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

<span data-ttu-id="fd180-121">[![Implantar tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="fd180-121">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="fd180-122">parâmetros</span><span class="sxs-lookup"><span data-stu-id="fd180-122">Parameters</span></span>

<span data-ttu-id="fd180-123">No Gerenciador de recursos do Azure, você define parâmetros para os valores desejados toospecify quando Olá modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="fd180-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="fd180-124">modelo de saudação inclui uma seção chamada `Parameters` que contém todos os valores de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="fd180-124">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="fd180-125">Você deve definir um parâmetro para os valores que variam com base no projeto Olá que estiver implantando ou com base no ambiente de saudação que você está implantando.</span><span class="sxs-lookup"><span data-stu-id="fd180-125">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="fd180-126">Não defina parâmetros para valores que permanecem sempre Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="fd180-126">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="fd180-127">Cada valor de parâmetro é usado em Olá modelo toodefine Olá recursos implantados.</span><span class="sxs-lookup"><span data-stu-id="fd180-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="fd180-128">modelo de saudação define Olá parâmetros a seguir.</span><span class="sxs-lookup"><span data-stu-id="fd180-128">hello template defines hello following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="fd180-129">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="fd180-129">eventHubNamespaceName</span></span>

<span data-ttu-id="fd180-130">nome de saudação do hello [Hubs de eventos namespace](event-hubs-create.md) toocreate.</span><span class="sxs-lookup"><span data-stu-id="fd180-130">hello name of hello [Event Hubs namespace](event-hubs-create.md) toocreate.</span></span>

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a><span data-ttu-id="fd180-131">eventHubName</span><span class="sxs-lookup"><span data-stu-id="fd180-131">eventHubName</span></span>

<span data-ttu-id="fd180-132">nome de saudação do hub de eventos de saudação criado no hello [namespace de Hubs de eventos](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="fd180-132">hello name of hello event hub created in hello [Event Hubs namespace](event-hubs-create.md).</span></span>

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a><span data-ttu-id="fd180-133">messageRetentionInDays</span><span class="sxs-lookup"><span data-stu-id="fd180-133">messageRetentionInDays</span></span>

<span data-ttu-id="fd180-134">número de saudação de mensagens de saudação tooretain dias no hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd180-134">hello number of days tooretain hello messages in hello event hub.</span></span> 

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

### <a name="partitioncount"></a><span data-ttu-id="fd180-135">partitionCount</span><span class="sxs-lookup"><span data-stu-id="fd180-135">partitionCount</span></span>

<span data-ttu-id="fd180-136">número de saudação de toocreate de partições no hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd180-136">hello number of partitions toocreate in hello event hub.</span></span>

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

### <a name="captureenabled"></a><span data-ttu-id="fd180-137">captureEnabled</span><span class="sxs-lookup"><span data-stu-id="fd180-137">captureEnabled</span></span>

<span data-ttu-id="fd180-138">Habilite a captura no hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd180-138">Enable Capture on hello event hub.</span></span>

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
### <a name="captureencodingformat"></a><span data-ttu-id="fd180-139">captureEncodingFormat</span><span class="sxs-lookup"><span data-stu-id="fd180-139">captureEncodingFormat</span></span>

<span data-ttu-id="fd180-140">formato de codificação Olá especificar dados de evento de saudação tooserialize.</span><span class="sxs-lookup"><span data-stu-id="fd180-140">hello encoding format you specify tooserialize hello event data.</span></span>

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

### <a name="capturetime"></a><span data-ttu-id="fd180-141">captureTime</span><span class="sxs-lookup"><span data-stu-id="fd180-141">captureTime</span></span>

<span data-ttu-id="fd180-142">intervalo de tempo de saudação na qual Hubs de evento captura inicia a captura de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd180-142">hello time interval in which Event Hubs Capture starts capturing hello data.</span></span>

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

### <a name="capturesize"></a><span data-ttu-id="fd180-143">captureSize</span><span class="sxs-lookup"><span data-stu-id="fd180-143">captureSize</span></span>
<span data-ttu-id="fd180-144">intervalo de tamanho de saudação em que a captura inicia a captura de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd180-144">hello size interval at which Capture starts capturing hello data.</span></span>

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

###<a name="capturenameformat"></a><span data-ttu-id="fd180-145">captureNameFormat</span><span class="sxs-lookup"><span data-stu-id="fd180-145">captureNameFormat</span></span>

<span data-ttu-id="fd180-146">formato de nome de saudação usado por Hubs de evento captura o toowrite Olá Avro arquivos.</span><span class="sxs-lookup"><span data-stu-id="fd180-146">hello name format used by Event Hubs Capture toowrite hello Avro files.</span></span> <span data-ttu-id="fd180-147">Observe que um formato de nome de Captura deve conter os campos `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` e `{Second}`.</span><span class="sxs-lookup"><span data-stu-id="fd180-147">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span></span> <span data-ttu-id="fd180-148">Eles podem ficar organizados em qualquer ordem, com ou sem delimitadores.</span><span class="sxs-lookup"><span data-stu-id="fd180-148">These can be arranged in any order, with or without delimiters.</span></span>
 
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

### <a name="apiversion"></a><span data-ttu-id="fd180-149">apiVersion</span><span class="sxs-lookup"><span data-stu-id="fd180-149">apiVersion</span></span>

<span data-ttu-id="fd180-150">versão de API de saudação do modelo de hello.</span><span class="sxs-lookup"><span data-stu-id="fd180-150">hello API version of hello template.</span></span>

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

<span data-ttu-id="fd180-151">Use Olá parâmetros a seguir se você escolher o armazenamento do Azure como seu destino.</span><span class="sxs-lookup"><span data-stu-id="fd180-151">Use hello following parameters if you choose Azure Storage as your destination.</span></span>

### <a name="destinationstorageaccountresourceid"></a><span data-ttu-id="fd180-152">destinationStorageAccountResourceId</span><span class="sxs-lookup"><span data-stu-id="fd180-152">destinationStorageAccountResourceId</span></span>

<span data-ttu-id="fd180-153">Captura requer um tooenable de ID de recurso do armazenamento do Azure conta capturar tooyour desejado a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fd180-153">Capture requires an Azure Storage account resource ID tooenable capturing tooyour desired Storage account.</span></span>

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a><span data-ttu-id="fd180-154">blobContainerName</span><span class="sxs-lookup"><span data-stu-id="fd180-154">blobContainerName</span></span>

<span data-ttu-id="fd180-155">Olá contêiner de blob no qual toocapture seus dados de evento.</span><span class="sxs-lookup"><span data-stu-id="fd180-155">hello blob container in which toocapture your event data.</span></span>

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

<span data-ttu-id="fd180-156">Use Olá parâmetros a seguir se você escolher o repositório Azure Data Lake como seu destino.</span><span class="sxs-lookup"><span data-stu-id="fd180-156">Use hello following parameters if you choose Azure Data Lake Store as your destination.</span></span> <span data-ttu-id="fd180-157">Você deve definir permissões em seu caminho de repositório Data Lake, no qual você deseja que o evento de saudação tooCapture.</span><span class="sxs-lookup"><span data-stu-id="fd180-157">You must set permissions on your Data Lake Store path, in which you want tooCapture hello event.</span></span> <span data-ttu-id="fd180-158">tooset permissões, consulte [neste artigo](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="fd180-158">tooset permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span></span>

###<a name="subscriptionid"></a><span data-ttu-id="fd180-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="fd180-159">subscriptionId</span></span>

<span data-ttu-id="fd180-160">ID de assinatura do namespace de Hubs de eventos hello e repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd180-160">Subscription ID for hello Event Hubs namespace and Azure Data Lake Store.</span></span> <span data-ttu-id="fd180-161">Ambos os recursos devem estar sob Olá mesmo ID de assinatura.</span><span class="sxs-lookup"><span data-stu-id="fd180-161">Both these resources must be under hello same subscription ID.</span></span>

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a><span data-ttu-id="fd180-162">dataLakeAccountName</span><span class="sxs-lookup"><span data-stu-id="fd180-162">dataLakeAccountName</span></span>

<span data-ttu-id="fd180-163">nome do repositório Azure Data Lake Olá Olá dos eventos capturados.</span><span class="sxs-lookup"><span data-stu-id="fd180-163">hello Azure Data Lake Store name for hello captured events.</span></span>

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a><span data-ttu-id="fd180-164">dataLakeFolderPath</span><span class="sxs-lookup"><span data-stu-id="fd180-164">dataLakeFolderPath</span></span>

<span data-ttu-id="fd180-165">caminho de pasta de destino Olá para Olá dos eventos capturados.</span><span class="sxs-lookup"><span data-stu-id="fd180-165">hello destination folder path for hello captured events.</span></span>

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a><span data-ttu-id="fd180-166">Toodeploy de recursos de armazenamento do Azure como eventos de toocaptured de destino</span><span class="sxs-lookup"><span data-stu-id="fd180-166">Resources toodeploy for Azure Storage as destination toocaptured events</span></span>

<span data-ttu-id="fd180-167">Cria um namespace do tipo **EventHubs**, com um evento e também permite capturar tooAzure armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="fd180-167">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Blob Storage.</span></span>

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

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a><span data-ttu-id="fd180-168">Toodeploy de recursos para o repositório Azure Data Lake como destino</span><span class="sxs-lookup"><span data-stu-id="fd180-168">Resources toodeploy for Azure Data Lake Store as destination</span></span>

<span data-ttu-id="fd180-169">Cria um namespace do tipo **EventHubs**, hub de eventos de um e também permite que o repositório do captura tooAzure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd180-169">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Data Lake Store.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="fd180-170">Implantação de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="fd180-170">Commands toorun deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="fd180-171">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd180-171">PowerShell</span></span>

<span data-ttu-id="fd180-172">Implante seu tooenable modelo capturar de Hubs de evento no armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="fd180-172">Deploy your template tooenable Event Hubs Capture into Azure Storage:</span></span>
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

<span data-ttu-id="fd180-173">Implante seu tooenable modelo capturar de Hubs de evento no repositório Azure Data Lake:</span><span class="sxs-lookup"><span data-stu-id="fd180-173">Deploy your template tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="fd180-174">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="fd180-174">Azure CLI</span></span>

<span data-ttu-id="fd180-175">Escolhendo o Armazenamento de Blobs do Azure como destino:</span><span class="sxs-lookup"><span data-stu-id="fd180-175">Choosing Azure Blob Storage as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

<span data-ttu-id="fd180-176">Escolhendo o Azure Data Lake Store como destino:</span><span class="sxs-lookup"><span data-stu-id="fd180-176">Choosing Azure Data Lake Store as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="fd180-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fd180-177">Next steps</span></span>

<span data-ttu-id="fd180-178">Você também pode configurar a captura de Hubs de eventos por meio de saudação [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd180-178">You can also configure Event Hubs Capture via hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fd180-179">Para obter mais informações, consulte [habilitar a captura de Hubs de evento usando Olá portal do Azure](event-hubs-capture-enable-through-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd180-179">For more information, see [Enable Event Hubs Capture using hello Azure portal](event-hubs-capture-enable-through-portal.md).</span></span>

<span data-ttu-id="fd180-180">Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd180-180">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="fd180-181">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="fd180-181">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="fd180-182">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="fd180-182">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="fd180-183">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="fd180-183">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
