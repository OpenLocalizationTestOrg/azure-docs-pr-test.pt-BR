---
title: Criar um namespace de Hubs de Eventos do Azure e habilitar a Captura usando um modelo | Microsoft Docs
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
ms.openlocfilehash: 19bbb51868e767aa1d15f4574628b7fd36607207
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a><span data-ttu-id="15b95-103">Criar um namespace de Hubs de Eventos com o hub de eventos e habilitar a Captura usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="15b95-103">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>

<span data-ttu-id="15b95-104">Este artigo mostra como usar um modelo do Azure Resource Manager que cria um namespace de Hubs de Eventos, com uma instância de hub de eventos e também habilita o [recurso Captura](event-hubs-capture-overview.md) no hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="15b95-104">This article shows how to use an Azure Resource Manager template that creates an Event Hubs namespace, with one event hub instance, and also enables the [Capture feature](event-hubs-capture-overview.md) on the event hub.</span></span> <span data-ttu-id="15b95-105">O artigo descreve como definir quais recursos são implantados e como definir os parâmetros que são especificados quando a implantação é executada.</span><span class="sxs-lookup"><span data-stu-id="15b95-105">The article describes how to define which resources are deployed, and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="15b95-106">Você pode usar este modelo para suas próprias implantações ou personalizá-lo para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="15b95-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="15b95-107">Este artigo também mostra como especificar que os eventos sejam capturados em Blobs de Armazenamento do Azure ou em um Azure Data Lake Store com base no destino escolhido.</span><span class="sxs-lookup"><span data-stu-id="15b95-107">This article also shows how to specify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on the destination you choose.</span></span>

<span data-ttu-id="15b95-108">Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="15b95-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="15b95-109">Para saber mais sobre as práticas e os padrões de convenções de nomenclatura de Recursos do Azure, confira [Convenções de nomenclatura de funcionalidade do Azure][Azure Resources naming conventions].</span><span class="sxs-lookup"><span data-stu-id="15b95-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span></span>

<span data-ttu-id="15b95-110">Para obter os modelos completos, clique nos seguintes links do GitHub:</span><span class="sxs-lookup"><span data-stu-id="15b95-110">For the complete templates, click the following GitHub links:</span></span>

- <span data-ttu-id="15b95-111">[Hub de eventos e habilitar a Captura no modelo de Armazenamento][Event Hub and enable Capture to Storage template]</span><span class="sxs-lookup"><span data-stu-id="15b95-111">[Event hub and enable Capture to Storage template][Event Hub and enable Capture to Storage template]</span></span> 
- <span data-ttu-id="15b95-112">[Hub de eventos e habilitar a Captura no modelo do Azure Data Lake Store][Event Hub and enable Capture to Azure Data Lake Store template]</span><span class="sxs-lookup"><span data-stu-id="15b95-112">[Event hub and enable Capture to Azure Data Lake Store template][Event Hub and enable Capture to Azure Data Lake Store template]</span></span>

> [!NOTE]
> <span data-ttu-id="15b95-113">Para verificar os modelos mais recentes, visite a galeria [Modelos de Início Rápido do Azure][Azure Quickstart Templates] e procure por Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="15b95-113">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="15b95-114">O que você implantará?</span><span class="sxs-lookup"><span data-stu-id="15b95-114">What will you deploy?</span></span>

<span data-ttu-id="15b95-115">Com esse modelo, você implanta um namespace de Hub de Eventos com um hub de eventos e também habilita a [Captura dos Hubs de Eventos](event-hubs-capture-overview.md).</span><span class="sxs-lookup"><span data-stu-id="15b95-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span></span>

<span data-ttu-id="15b95-116">[Hubs de Eventos](event-hubs-what-is-event-hubs.md) é um serviço de processamento de eventos usado para fornecer entrada a telemetria e eventos para o Azure em grande escala, com baixa latência e alta confiabilidade.</span><span class="sxs-lookup"><span data-stu-id="15b95-116">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used to provide event and telemetry ingress to Azure at massive scale, with low latency and high reliability.</span></span> <span data-ttu-id="15b95-117">A Captura dos Hubs de Eventos permite que você forneça automaticamente os dados de streaming em Hubs de Eventos para o Armazenamento de Blobs do Azure ou Azure Data Lake Store, dentro de um período especificado ou do intervalo de tamanho de sua preferência.</span><span class="sxs-lookup"><span data-stu-id="15b95-117">Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to Azure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span></span>

<span data-ttu-id="15b95-118">Clique no botão abaixo para habilitar a Captura de Hubs de Eventos no Armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="15b95-118">Click the following button to enable Event Hubs Capture into Azure Storage:</span></span>

<span data-ttu-id="15b95-119">[![Implantar no Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="15b95-119">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span></span>

<span data-ttu-id="15b95-120">Clique no botão abaixo para habilitar a Captura de Hubs de Eventos no Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="15b95-120">Click the following button to enable Event Hubs Capture into Azure Data Lake Store:</span></span>

<span data-ttu-id="15b95-121">[![Implantar no Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="15b95-121">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="15b95-122">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="15b95-122">Parameters</span></span>

<span data-ttu-id="15b95-123">Com o Gerenciador de Recursos do Azure, você define parâmetros para os valores que deseja especificar quando o modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="15b95-123">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="15b95-124">O modelo inclui uma seção chamada `Parameters` , que contém todos os valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="15b95-124">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="15b95-125">Você deve definir um parâmetro para os valores que variam de acordo com o projeto que você está implantando ou com o ambiente em que a implantação ocorre.</span><span class="sxs-lookup"><span data-stu-id="15b95-125">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="15b95-126">Não defina parâmetros para valores que permanecem sempre os mesmos.</span><span class="sxs-lookup"><span data-stu-id="15b95-126">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="15b95-127">Cada valor de parâmetro é usado no modelo para definir os recursos que são implantados.</span><span class="sxs-lookup"><span data-stu-id="15b95-127">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="15b95-128">O modelo define os parâmetros a seguir.</span><span class="sxs-lookup"><span data-stu-id="15b95-128">The template defines the following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="15b95-129">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="15b95-129">eventHubNamespaceName</span></span>

<span data-ttu-id="15b95-130">O nome do [namespace Hubs de Evento](event-hubs-create.md) a criar.</span><span class="sxs-lookup"><span data-stu-id="15b95-130">The name of the [Event Hubs namespace](event-hubs-create.md) to create.</span></span>

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of the EventHub namespace"
      }
}
```

### <a name="eventhubname"></a><span data-ttu-id="15b95-131">eventHubName</span><span class="sxs-lookup"><span data-stu-id="15b95-131">eventHubName</span></span>

<span data-ttu-id="15b95-132">O nome do hub de eventos criado no [namespace Hubs de Eventos](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="15b95-132">The name of the event hub created in the [Event Hubs namespace](event-hubs-create.md).</span></span>

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of the event hub"
    }
}
```

### <a name="messageretentionindays"></a><span data-ttu-id="15b95-133">messageRetentionInDays</span><span class="sxs-lookup"><span data-stu-id="15b95-133">messageRetentionInDays</span></span>

<span data-ttu-id="15b95-134">O número de dias para manter as mensagens no hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="15b95-134">The number of days to retain the messages in the event hub.</span></span> 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long to retain the data in event hub"
     }
 }
```

### <a name="partitioncount"></a><span data-ttu-id="15b95-135">partitionCount</span><span class="sxs-lookup"><span data-stu-id="15b95-135">partitionCount</span></span>

<span data-ttu-id="15b95-136">O número de partições a serem criadas no hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="15b95-136">The number of partitions to create in the event hub.</span></span>

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

### <a name="captureenabled"></a><span data-ttu-id="15b95-137">captureEnabled</span><span class="sxs-lookup"><span data-stu-id="15b95-137">captureEnabled</span></span>

<span data-ttu-id="15b95-138">Habilite a Captura no hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="15b95-138">Enable Capture on the event hub.</span></span>

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable the Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a><span data-ttu-id="15b95-139">captureEncodingFormat</span><span class="sxs-lookup"><span data-stu-id="15b95-139">captureEncodingFormat</span></span>

<span data-ttu-id="15b95-140">O formato de codificação que você especifica para serializar os dados do evento.</span><span class="sxs-lookup"><span data-stu-id="15b95-140">The encoding format you specify to serialize the event data.</span></span>

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"The encoding format in which Capture serializes the EventData"
    }
}
```

### <a name="capturetime"></a><span data-ttu-id="15b95-141">captureTime</span><span class="sxs-lookup"><span data-stu-id="15b95-141">captureTime</span></span>

<span data-ttu-id="15b95-142">O intervalo de tempo no qual a Captura de Hubs de Eventos inicia a captura de dados.</span><span class="sxs-lookup"><span data-stu-id="15b95-142">The time interval in which Event Hubs Capture starts capturing the data.</span></span>

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"the time window in seconds for the capture"
    }
}
```

### <a name="capturesize"></a><span data-ttu-id="15b95-143">captureSize</span><span class="sxs-lookup"><span data-stu-id="15b95-143">captureSize</span></span>
<span data-ttu-id="15b95-144">O intervalo de tamanho no qual a Captura inicia a captura de dados.</span><span class="sxs-lookup"><span data-stu-id="15b95-144">The size interval at which Capture starts capturing the data.</span></span>

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"The size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a><span data-ttu-id="15b95-145">captureNameFormat</span><span class="sxs-lookup"><span data-stu-id="15b95-145">captureNameFormat</span></span>

<span data-ttu-id="15b95-146">O formato de nome usado pela Captura de Hubs de Eventos para gravar os arquivos Avro.</span><span class="sxs-lookup"><span data-stu-id="15b95-146">The name format used by Event Hubs Capture to write the Avro files.</span></span> <span data-ttu-id="15b95-147">Observe que um formato de nome de Captura deve conter os campos `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` e `{Second}`.</span><span class="sxs-lookup"><span data-stu-id="15b95-147">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span></span> <span data-ttu-id="15b95-148">Eles podem ficar organizados em qualquer ordem, com ou sem delimitadores.</span><span class="sxs-lookup"><span data-stu-id="15b95-148">These can be arranged in any order, with or without delimiters.</span></span>
 
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

### <a name="apiversion"></a><span data-ttu-id="15b95-149">apiVersion</span><span class="sxs-lookup"><span data-stu-id="15b95-149">apiVersion</span></span>

<span data-ttu-id="15b95-150">A versão da API do modelo.</span><span class="sxs-lookup"><span data-stu-id="15b95-150">The API version of the template.</span></span>

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by the template"
    }
 }
```

<span data-ttu-id="15b95-151">Use os parâmetros a seguir se você escolher o Armazenamento do Azure como destino.</span><span class="sxs-lookup"><span data-stu-id="15b95-151">Use the following parameters if you choose Azure Storage as your destination.</span></span>

### <a name="destinationstorageaccountresourceid"></a><span data-ttu-id="15b95-152">destinationStorageAccountResourceId</span><span class="sxs-lookup"><span data-stu-id="15b95-152">destinationStorageAccountResourceId</span></span>

<span data-ttu-id="15b95-153">A Captura exige uma ID de recurso da conta de Armazenamento do Azure para habilitar a captura na sua conta de armazenamento desejada.</span><span class="sxs-lookup"><span data-stu-id="15b95-153">Capture requires an Azure Storage account resource ID to enable capturing to your desired Storage account.</span></span>

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want the blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a><span data-ttu-id="15b95-154">blobContainerName</span><span class="sxs-lookup"><span data-stu-id="15b95-154">blobContainerName</span></span>

<span data-ttu-id="15b95-155">O contêiner de blob no qual deseja capturar os dados de evento.</span><span class="sxs-lookup"><span data-stu-id="15b95-155">The blob container in which to capture your event data.</span></span>

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want the blobs captured"
    }
}
```

<span data-ttu-id="15b95-156">Use os parâmetros a seguir se você escolher o Azure Data Lake Store como destino.</span><span class="sxs-lookup"><span data-stu-id="15b95-156">Use the following parameters if you choose Azure Data Lake Store as your destination.</span></span> <span data-ttu-id="15b95-157">Você deve definir permissões no caminho do Data Lake Store no qual deseja capturar o evento.</span><span class="sxs-lookup"><span data-stu-id="15b95-157">You must set permissions on your Data Lake Store path, in which you want to Capture the event.</span></span> <span data-ttu-id="15b95-158">Para definir permissões, confira [este artigo](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="15b95-158">To set permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span></span>

###<a name="subscriptionid"></a><span data-ttu-id="15b95-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="15b95-159">subscriptionId</span></span>

<span data-ttu-id="15b95-160">ID de assinatura para o namespace de Hubs de Eventos e o Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="15b95-160">Subscription ID for the Event Hubs namespace and Azure Data Lake Store.</span></span> <span data-ttu-id="15b95-161">Os dois recursos devem estar na mesma ID de assinatura.</span><span class="sxs-lookup"><span data-stu-id="15b95-161">Both these resources must be under the same subscription ID.</span></span>

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a><span data-ttu-id="15b95-162">dataLakeAccountName</span><span class="sxs-lookup"><span data-stu-id="15b95-162">dataLakeAccountName</span></span>

<span data-ttu-id="15b95-163">O nome do Azure Data Lake Store para os eventos capturados.</span><span class="sxs-lookup"><span data-stu-id="15b95-163">The Azure Data Lake Store name for the captured events.</span></span>

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a><span data-ttu-id="15b95-164">dataLakeFolderPath</span><span class="sxs-lookup"><span data-stu-id="15b95-164">dataLakeFolderPath</span></span>

<span data-ttu-id="15b95-165">O caminho da pasta de destino para os eventos capturados.</span><span class="sxs-lookup"><span data-stu-id="15b95-165">The destination folder path for the captured events.</span></span>

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-to-deploy-for-azure-storage-as-destination-to-captured-events"></a><span data-ttu-id="15b95-166">Recursos a serem implantados no Armazenamento do Azure como destino dos eventos capturados</span><span class="sxs-lookup"><span data-stu-id="15b95-166">Resources to deploy for Azure Storage as destination to captured events</span></span>

<span data-ttu-id="15b95-167">Cria um namespace do tipo **EventHubs** com um hub de eventos, e também habilita a Captura para o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="15b95-167">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture to Azure Blob Storage.</span></span>

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

## <a name="resources-to-deploy-for-azure-data-lake-store-as-destination"></a><span data-ttu-id="15b95-168">Recursos a serem implantados no Azure Data Lake Store como destino</span><span class="sxs-lookup"><span data-stu-id="15b95-168">Resources to deploy for Azure Data Lake Store as destination</span></span>

<span data-ttu-id="15b95-169">Cria um namespace do tipo **EventHubs**, com um hub de eventos, e também habilita a Captura para o Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="15b95-169">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture to Azure Data Lake Store.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="15b95-170">Comandos para executar a implantação</span><span class="sxs-lookup"><span data-stu-id="15b95-170">Commands to run deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="15b95-171">PowerShell</span><span class="sxs-lookup"><span data-stu-id="15b95-171">PowerShell</span></span>

<span data-ttu-id="15b95-172">Implante o modelo para habilitar a captura de Hubs de Eventos no Armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="15b95-172">Deploy your template to enable Event Hubs Capture into Azure Storage:</span></span>
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

<span data-ttu-id="15b95-173">Implante o modelo para habilitar a captura de Hubs de Eventos no Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="15b95-173">Deploy your template to enable Event Hubs Capture into Azure Data Lake Store:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="15b95-174">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="15b95-174">Azure CLI</span></span>

<span data-ttu-id="15b95-175">Escolhendo o Armazenamento de Blobs do Azure como destino:</span><span class="sxs-lookup"><span data-stu-id="15b95-175">Choosing Azure Blob Storage as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

<span data-ttu-id="15b95-176">Escolhendo o Azure Data Lake Store como destino:</span><span class="sxs-lookup"><span data-stu-id="15b95-176">Choosing Azure Data Lake Store as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="15b95-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="15b95-177">Next steps</span></span>

<span data-ttu-id="15b95-178">Você também pode configurar a Captura de Hubs de Eventos por meio do [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="15b95-178">You can also configure Event Hubs Capture via the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="15b95-179">Para saber mais, confira [Habilitar a Captura de Hubs de Eventos usando o portal do Azure](event-hubs-capture-enable-through-portal.md).</span><span class="sxs-lookup"><span data-stu-id="15b95-179">For more information, see [Enable Event Hubs Capture using the Azure portal](event-hubs-capture-enable-through-portal.md).</span></span>

<span data-ttu-id="15b95-180">Você pode saber mais sobre Hubs de Eventos visitando os links abaixo:</span><span class="sxs-lookup"><span data-stu-id="15b95-180">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="15b95-181">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="15b95-181">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="15b95-182">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="15b95-182">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="15b95-183">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="15b95-183">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture to Storage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture to Azure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls