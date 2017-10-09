---
title: pacote aaaManage captura com o observador de rede do Azure - API REST | Microsoft Docs
description: "Esta página explica como toomanage Olá recurso de captura de pacote do observador de rede usando a API REST do Azure"
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
ms.openlocfilehash: 7a531fbe796e85e94961bd192d171defb299be05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="bb852-103">Gerenciar as capturas de pacotes com o Observador de Rede do Azure usando a API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="bb852-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="bb852-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bb852-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="bb852-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb852-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="bb852-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bb852-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="bb852-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bb852-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="bb852-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="bb852-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="bb852-109">Captura de pacote do Inspetor de rede permite que você toocreate captura sessões tootrack tráfego tooand de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bb852-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="bb852-110">Filtros são fornecidos para Olá tooensure de sessão de captura que somente o tráfego de saudação que você deseja capturar.</span><span class="sxs-lookup"><span data-stu-id="bb852-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="bb852-111">Captura de pacote ajuda anomalias de rede toodiagnose reativo e proativo.</span><span class="sxs-lookup"><span data-stu-id="bb852-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="bb852-112">Outros usos incluem a coleta de estatísticas de rede, obtenção de informações de invasões de rede, toodebug cliente-servidor comunicações e muito mais.</span><span class="sxs-lookup"><span data-stu-id="bb852-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="bb852-113">Sendo tooremotely capaz de captura de pacote de gatilho, esse recurso facilita a carga de saudação da execução de uma captura de pacote e manualmente no computador desejado hello, que economiza tempo.</span><span class="sxs-lookup"><span data-stu-id="bb852-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="bb852-114">Este artigo o orienta por Olá diversas tarefas de gerenciamento que estão atualmente disponíveis para captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="bb852-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="bb852-115">**Obter uma captura de pacotes**</span><span class="sxs-lookup"><span data-stu-id="bb852-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="bb852-116">**Listar todas as capturas de pacotes**</span><span class="sxs-lookup"><span data-stu-id="bb852-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="bb852-117">**Olá consultar o status de uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="bb852-117">**Query hello status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="bb852-118">**Iniciar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="bb852-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="bb852-119">**Parar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="bb852-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="bb852-120">**Excluir uma captura de pacotes**</span><span class="sxs-lookup"><span data-stu-id="bb852-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="bb852-121">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="bb852-121">Before you begin</span></span>

<span data-ttu-id="bb852-122">Nesse cenário, você deve chamar hello toorun de API de Rest do Inspetor de rede IP fluxo verificar.</span><span class="sxs-lookup"><span data-stu-id="bb852-122">In this scenario, you call hello Network Watcher Rest API toorun IP Flow Verify.</span></span> <span data-ttu-id="bb852-123">ARMclient é toocall usado Olá REST API usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb852-123">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="bb852-124">O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="bb852-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="bb852-125">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="bb852-125">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> <span data-ttu-id="bb852-126">A captura de pacotes requer uma extensão da máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="bb852-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="bb852-127">Para instalar a extensão de saudação em uma VM do Windows, visite [extensão de máquina virtual do agente do Inspetor de rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para a visita de VM do Linux [extensão de máquina virtual do agente do Inspetor de rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="bb852-127">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="bb852-128">Fazer logon com o ARMClient</span><span class="sxs-lookup"><span data-stu-id="bb852-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="bb852-129">Recuperar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bb852-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="bb852-130">Execute Olá tooreturn de script a seguir em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bb852-130">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="bb852-131">Essas informações são necessárias para iniciar uma captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="bb852-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="bb852-132">Olá variáveis de necessidades de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb852-132">hello following code needs variables:</span></span>

- <span data-ttu-id="bb852-133">**subscriptionId** -id da assinatura Olá também pode ser recuperado com hello **AzureRMSubscription Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bb852-133">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="bb852-134">**resourceGroupName** - Olá nome de um grupo de recursos que contém máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="bb852-134">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="bb852-135">De saída a seguir hello, id de saudação da máquina virtual de saudação é usada no exemplo a seguir hello.</span><span class="sxs-lookup"><span data-stu-id="bb852-135">From hello following output, hello id of hello virtual machine is used in hello next example.</span></span>

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


## <a name="get-a-packet-capture"></a><span data-ttu-id="bb852-136">Obter uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="bb852-136">Get a packet capture</span></span>

<span data-ttu-id="bb852-137">exemplo a seguir Hello obtém status de saudação de uma captura de pacote único</span><span class="sxs-lookup"><span data-stu-id="bb852-137">hello following example gets hello status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="bb852-138">Olá respostas seguintes são exemplos de uma resposta típica retornados ao consultar o status de saudação de uma captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="bb852-138">hello following responses are examples of a typical response returned when querying hello status of a packet capture.</span></span>

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

## <a name="list-all-packet-captures"></a><span data-ttu-id="bb852-139">Listar todas as capturas de pacotes</span><span class="sxs-lookup"><span data-stu-id="bb852-139">List all packet captures</span></span>

<span data-ttu-id="bb852-140">saudação de exemplo a seguir obtém todas as sessões de captura de pacote em uma região.</span><span class="sxs-lookup"><span data-stu-id="bb852-140">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="bb852-141">Olá resposta a seguir é um exemplo de uma resposta típica retornado ao obter todos os pacotes de captura</span><span class="sxs-lookup"><span data-stu-id="bb852-141">hello following response is an example of a typical response returned when getting all packet captures</span></span>

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

## <a name="query-packet-capture-status"></a><span data-ttu-id="bb852-142">Consultar o status da captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="bb852-142">Query packet capture status</span></span>

<span data-ttu-id="bb852-143">saudação de exemplo a seguir obtém todas as sessões de captura de pacote em uma região.</span><span class="sxs-lookup"><span data-stu-id="bb852-143">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="bb852-144">Olá, resposta a seguir é um exemplo de uma resposta típica retornado ao consultar o status de saudação de uma captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="bb852-144">hello following response is an example of a typical response returned when querying hello status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="bb852-145">Iniciar captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="bb852-145">Start packet capture</span></span>

<span data-ttu-id="bb852-146">saudação de exemplo a seguir cria uma captura de pacote em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bb852-146">hello following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="bb852-147">exemplo Hello é parametrizada tooallow flexibilidade na criação de um exemplo.</span><span class="sxs-lookup"><span data-stu-id="bb852-147">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

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

## <a name="stop-packet-capture"></a><span data-ttu-id="bb852-148">Parar uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="bb852-148">Stop packet capture</span></span>

<span data-ttu-id="bb852-149">saudação de exemplo a seguir interrompe uma captura de pacote em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bb852-149">hello following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="bb852-150">exemplo Hello é parametrizada tooallow flexibilidade na criação de um exemplo.</span><span class="sxs-lookup"><span data-stu-id="bb852-150">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="bb852-151">Excluir a captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="bb852-151">Delete packet capture</span></span>

<span data-ttu-id="bb852-152">saudação de exemplo a seguir exclui uma captura de pacote em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bb852-152">hello following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="bb852-153">exemplo Hello é parametrizada tooallow flexibilidade na criação de um exemplo.</span><span class="sxs-lookup"><span data-stu-id="bb852-153">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="bb852-154">Excluir uma captura de pacote não exclui o arquivo hello na conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="bb852-154">Deleting a packet capture does not delete hello file in hello storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb852-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bb852-155">Next steps</span></span>

<span data-ttu-id="bb852-156">Para obter instruções sobre como baixar os arquivos de contas de armazenamento do azure, consulte muito[Introdução ao armazenamento de BLOBs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="bb852-156">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="bb852-157">Outra ferramenta que pode ser usada é o Gerenciador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bb852-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="bb852-158">Para obter mais informações sobre o Gerenciador de armazenamento podem ser encontradas aqui em Olá link a seguir: [Gerenciador de armazenamento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="bb852-158">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="bb852-159">Saiba como o pacote tooautomate captura com alertas de máquina Virtual por meio da exibição [criar uma captura de pacote de disparo de alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="bb852-159">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













