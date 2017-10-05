---
title: Gerenciar capturas de pacotes com o Observador de Rede do Azure - API REST | Microsoft Docs
description: "Esta página explica como gerenciar o recurso de captura de pacotes do Observador de Rede usando a API REST do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 53fe0324-835f-4005-afc8-145eeb314aeb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 49ec20802a252258d8493eb26510270b925e851a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="4a832-103">Gerenciar as capturas de pacotes com o Observador de Rede do Azure usando a API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="4a832-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="4a832-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4a832-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="4a832-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a832-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="4a832-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4a832-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="4a832-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4a832-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="4a832-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="4a832-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="4a832-109">Captura de pacote do Observador de Rede permite que você crie sessões de captura para controlar o tráfego em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4a832-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="4a832-110">Os filtros são fornecidos para a sessão de captura garantir que somente o tráfego que você deseja capturar.</span><span class="sxs-lookup"><span data-stu-id="4a832-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="4a832-111">Captura de pacote ajuda a diagnosticar problemas de rede reativo e proativo.</span><span class="sxs-lookup"><span data-stu-id="4a832-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="4a832-112">Outros usos incluem a coleta de estatísticas de rede, obter informações sobre as invasões de rede, para depurar comunicações cliente-servidor e muito mais.</span><span class="sxs-lookup"><span data-stu-id="4a832-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="4a832-113">Por poder remotamente disparar a captura de pacote, esse recurso alivia a carga da execução de uma captura de pacote e manualmente no computador desejado, o que economiza tempo.</span><span class="sxs-lookup"><span data-stu-id="4a832-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="4a832-114">Este artigo o guiará durante as tarefas de gerenciamento diferentes que estão atualmente disponíveis para captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="4a832-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="4a832-115">**Obter uma captura de pacotes**</span><span class="sxs-lookup"><span data-stu-id="4a832-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="4a832-116">**Listar todas as capturas de pacotes**</span><span class="sxs-lookup"><span data-stu-id="4a832-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="4a832-117">**Consultar o status de uma captura de pacotes**</span><span class="sxs-lookup"><span data-stu-id="4a832-117">**Query the status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="4a832-118">**Iniciar uma captura de pacotes**</span><span class="sxs-lookup"><span data-stu-id="4a832-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="4a832-119">**Parar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="4a832-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="4a832-120">**Excluir uma captura de pacotes**</span><span class="sxs-lookup"><span data-stu-id="4a832-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="4a832-121">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="4a832-121">Before you begin</span></span>

<span data-ttu-id="4a832-122">Nesse cenário, você chama a API Rest do Observador de Rede para executar a Verificação de Fluxo de IP.</span><span class="sxs-lookup"><span data-stu-id="4a832-122">In this scenario, you call the Network Watcher Rest API to run IP Flow Verify.</span></span> <span data-ttu-id="4a832-123">O ARMclient é usado para chamar a API REST usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a832-123">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="4a832-124">O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="4a832-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="4a832-125">Este cenário pressupõe que você já tenha seguido as etapas em [Criar um Observador de Rede](network-watcher-create.md) para criar um Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="4a832-125">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> <span data-ttu-id="4a832-126">A captura de pacotes exige uma extensão de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="4a832-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="4a832-127">Para instalar a extensão em uma VM do Windows, visite [Extensão da máquina virtual do Agente do Observador de Rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para a VM do Linux, visite [Extensão da máquina virtual do Agente do Observador de Rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="4a832-127">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="4a832-128">Fazer logon com o ARMClient</span><span class="sxs-lookup"><span data-stu-id="4a832-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="4a832-129">Recuperar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4a832-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="4a832-130">Execute o script a seguir para retornar para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4a832-130">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="4a832-131">Essas informações são necessárias para iniciar uma captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="4a832-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="4a832-132">O código a seguir precisa de variáveis:</span><span class="sxs-lookup"><span data-stu-id="4a832-132">The following code needs variables:</span></span>

- <span data-ttu-id="4a832-133">**subscriptionId** - a id da assinatura também pode ser recuperada com o cmdlet **Get-AzureRMSubscription**.</span><span class="sxs-lookup"><span data-stu-id="4a832-133">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="4a832-134">**resourceGroupName** - o nome de um grupo de recursos que contém as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="4a832-134">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="4a832-135">Na saída a seguir, a id da máquina virtual é usada no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="4a832-135">From the following output, the id of the virtual machine is used in the next example.</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```


## <a name="get-a-packet-capture"></a><span data-ttu-id="4a832-136">Obter uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="4a832-136">Get a packet capture</span></span>

<span data-ttu-id="4a832-137">O exemplo a seguir obtém o status de uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="4a832-137">The following example gets the status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="4a832-138">As respostas a seguir são exemplos de uma resposta típica retornada ao consultar o status de uma captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="4a832-138">The following responses are examples of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Running",
  "packetCaptureError": []
}
```

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Stopped",
  "stopReason": "TimeExceeded",
  "packetCaptureError": []
}
```

## <a name="list-all-packet-captures"></a><span data-ttu-id="4a832-139">Listar todas as capturas de pacotes</span><span class="sxs-lookup"><span data-stu-id="4a832-139">List all packet captures</span></span>

<span data-ttu-id="4a832-140">O exemplo a seguir obtém todas as sessões de captura de pacotes em uma região.</span><span class="sxs-lookup"><span data-stu-id="4a832-140">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="4a832-141">A resposta a seguir é um exemplo de uma resposta típica retornada ao obter todas as capturas de pacotes</span><span class="sxs-lookup"><span data-stu-id="4a832-141">The following response is an example of a typical response returned when getting all packet captures</span></span>

```json
{
  "value": [
    {
      "name": "TestPacketCapture6",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Succeeded",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_19_53_056.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    },
    {
      "name": "TestPacketCapture7",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture7",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Failed",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_23_15_364.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    }
  ]
}
```

## <a name="query-packet-capture-status"></a><span data-ttu-id="4a832-142">Consultar o status da captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="4a832-142">Query packet capture status</span></span>

<span data-ttu-id="4a832-143">O exemplo a seguir obtém todas as sessões de captura de pacotes em uma região.</span><span class="sxs-lookup"><span data-stu-id="4a832-143">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="4a832-144">A resposta a seguir é um exemplo de uma resposta típica retornada ao consultar o status de uma captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="4a832-144">The following response is an example of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="4a832-145">Iniciar captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="4a832-145">Start packet capture</span></span>

<span data-ttu-id="4a832-146">O exemplo a seguir cria uma captura de pacotes em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4a832-146">The following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="4a832-147">O exemplo é parametrizado para permitir flexibilidade ao criar um exemplo.</span><span class="sxs-lookup"><span data-stu-id="4a832-147">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
$storageaccountname = "contosoexamplergdiag374"
$vmName = "ContosoVM"
$bytestoCaptureperPacket = "0"
$bytesPerSession = "1073741824"
$captureTimeinSeconds = "60"
$localIP = ""
$localPort = "" # Examples are: 80, or 80-120
$remoteIP = ""
$remotePort = "" # Examples are: 80, or 80-120
$protocol = "" # Valid values are TCP, UDP and Any.
$targetUri = "" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName
$storageId = "" # Example: "https://mytestaccountname.blob.core.windows.net/capture/vm1Capture.cap"
$storagePath = ""
$localFilePath = "c:\\temp\\packetcapture.cap" # Example: "d:\capture\vm1Capture.cap"

$requestBody = @"
{
    'properties':  {
                       'target':  '/${targetUri}',
                       'bytesToCapturePerPacket':  '${bytestoCaptureperPacket}',
                       'totalBytesPerSession':  '${bytesPerSession}',
                       'timeLimitinSeconds':  '${captureTimeinSeconds}',
                       'storageLocation':  {
                                               'storageId':  '${storageId}',
                                               'storagePath':  '${storagePath}',
                                               'filePath':  '${localFilePath}'
                                           },
                       'filters':  [
                                       {
                                           'protocol':  '${protocol}',
                                           'localIPAddress':  '${localIP}',
                                           'localPort':  '${localPort}',
                                           'remoteIPAddress':  '${remoteIP}',
                                           'remotePort':  '${remotePort}'
                                       }
                                   ]
                   }
}
"@

armclient PUT "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-07-01" $requestbody
```

## <a name="stop-packet-capture"></a><span data-ttu-id="4a832-148">Parar uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="4a832-148">Stop packet capture</span></span>

<span data-ttu-id="4a832-149">O exemplo a seguir para uma captura de pacotes em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4a832-149">The following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="4a832-150">O exemplo é parametrizado para permitir flexibilidade ao criar um exemplo.</span><span class="sxs-lookup"><span data-stu-id="4a832-150">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="4a832-151">Excluir a captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="4a832-151">Delete packet capture</span></span>

<span data-ttu-id="4a832-152">O exemplo a seguir excluir uma captura de pacotes em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4a832-152">The following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="4a832-153">O exemplo é parametrizado para permitir flexibilidade ao criar um exemplo.</span><span class="sxs-lookup"><span data-stu-id="4a832-153">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="4a832-154">Excluir uma captura de pacotes não exclui o arquivo na conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="4a832-154">Deleting a packet capture does not delete the file in the storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a832-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4a832-155">Next steps</span></span>

<span data-ttu-id="4a832-156">Para obter instruções sobre como baixar os arquivos das contas de armazenamento do Azure, consulte [Introdução ao armazenamento de Blobs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="4a832-156">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="4a832-157">Outra ferramenta que pode ser usada é o Gerenciador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4a832-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="4a832-158">Mais informações sobre o Gerenciador de Armazenamento podem ser encontradas aqui no link a seguir: [Gerenciador de Armazenamento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="4a832-158">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="4a832-159">Saiba como automatizar as capturas de pacotes com alertas da Máquina Virtual exibindo [Criar uma captura de pacotes disparada por alertas](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="4a832-159">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













