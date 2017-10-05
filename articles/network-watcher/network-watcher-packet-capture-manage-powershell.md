---
title: Gerenciar as capturas de pacotes com o Observador de Rede do Azure - PowerShell | Microsoft Docs
description: "Esta página explica como gerenciar o recurso de captura de pacotes do Observador de Rede usando o PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04d82085-c9ea-4ea1-b050-a3dd4960f3aa
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abd3b3641da80ee835fac85b4bde68594449e451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="51344-103">Gerenciar as capturas de pacotes com o Observador de Rede do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="51344-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="51344-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="51344-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="51344-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51344-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="51344-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="51344-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="51344-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="51344-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="51344-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="51344-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="51344-109">Captura de pacote do Observador de Rede permite que você crie sessões de captura para controlar o tráfego em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="51344-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="51344-110">Os filtros são fornecidos para a sessão de captura garantir que somente o tráfego que você deseja capturar.</span><span class="sxs-lookup"><span data-stu-id="51344-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="51344-111">Captura de pacote ajuda a diagnosticar problemas de rede reativo e proativo.</span><span class="sxs-lookup"><span data-stu-id="51344-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="51344-112">Outros usos incluem a coleta de estatísticas de rede, obter informações sobre as invasões de rede, para depurar comunicações cliente-servidor e muito mais.</span><span class="sxs-lookup"><span data-stu-id="51344-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="51344-113">Por poder remotamente disparar a captura de pacote, esse recurso alivia a carga da execução de uma captura de pacote e manualmente no computador desejado, o que economiza tempo.</span><span class="sxs-lookup"><span data-stu-id="51344-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="51344-114">Este artigo o guiará durante as tarefas de gerenciamento diferentes que estão atualmente disponíveis para captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="51344-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="51344-115">**Iniciar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="51344-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="51344-116">**Parar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="51344-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="51344-117">**Excluir uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="51344-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="51344-118">**Baixar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="51344-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="51344-119">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="51344-119">Before you begin</span></span>

<span data-ttu-id="51344-120">Este artigo pressupõe que você tenha os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="51344-120">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="51344-121">Uma instância do Observador de Rede na região que você deseja criar uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="51344-121">An instance of Network Watcher in the region you want to create a packet capture</span></span>

* <span data-ttu-id="51344-122">Uma máquina virtual com a extensão da captura de pacotes habilitada.</span><span class="sxs-lookup"><span data-stu-id="51344-122">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51344-123">A captura de pacotes requer uma extensão da máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="51344-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="51344-124">Para instalar a extensão em uma VM do Windows, visite [Extensão da máquina virtual do Agente do Observador de Rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para a VM do Linux, visite [Extensão da máquina virtual do Agente do Observador de Rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="51344-124">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="51344-125">Instalar a extensão da VM</span><span class="sxs-lookup"><span data-stu-id="51344-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="51344-126">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="51344-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="51344-127">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="51344-127">Step 2</span></span>

<span data-ttu-id="51344-128">O exemplo a seguir recupera as informações da extensão necessárias para executar o cmdlet `Set-AzureRmVMExtension`.</span><span class="sxs-lookup"><span data-stu-id="51344-128">The following example retrieves the extension information needed to run the `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="51344-129">Esse cmdlet instala o agente de captura de pacotes na máquina virtual convidada.</span><span class="sxs-lookup"><span data-stu-id="51344-129">This cmdlet installs the packet capture agent on the guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="51344-130">O cmdlet `Set-AzureRmVMExtension` pode levar vários minutos para concluir.</span><span class="sxs-lookup"><span data-stu-id="51344-130">The `Set-AzureRmVMExtension` cmdlet may take several minutes to complete.</span></span>

<span data-ttu-id="51344-131">Para as máquinas virtuais do Windows:</span><span class="sxs-lookup"><span data-stu-id="51344-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="51344-132">Para as máquinas virtuais do Linux:</span><span class="sxs-lookup"><span data-stu-id="51344-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="51344-133">O exemplo a seguir é uma resposta bem-sucedida após executar o cmdlet `Set-AzureRmVMExtension`.</span><span class="sxs-lookup"><span data-stu-id="51344-133">The following example is a successful response after running the `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="51344-134">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="51344-134">Step 3</span></span>

<span data-ttu-id="51344-135">Para garantir que o agente está instalado, execute o cmdlet `Get-AzureRmVMExtension` e passe o nome da máquina virtual e o nome da extensão.</span><span class="sxs-lookup"><span data-stu-id="51344-135">To ensure that the agent is installed, run the `Get-AzureRmVMExtension` cmdlet and pass it the virtual machine name and the extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="51344-136">A seguir está um exemplo de resposta ao executar `Get-AzureRmVMExtension`</span><span class="sxs-lookup"><span data-stu-id="51344-136">The following sample is an example of the response from running `Get-AzureRmVMExtension`</span></span>

```
ResourceGroupName       : testrg
VMName                  : testvm1
Name                    : AzureNetworkWatcherExtension
Location                : westcentralus
Etag                    : null
Publisher               : Microsoft.Azure.NetworkWatcher
ExtensionType           : NetworkWatcherAgentWindows
TypeHandlerVersion      : 1.4
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1/
                          extensions/AzureNetworkWatcherExtension
PublicSettings          : 
ProtectedSettings       : 
ProvisioningState       : Succeeded
Statuses                : 
SubStatuses             : 
AutoUpgradeMinorVersion : True
ForceUpdateTag          : 
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="51344-137">Iniciar uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="51344-137">Start a packet capture</span></span>

<span data-ttu-id="51344-138">Depois que as etapas anteriores forem concluídas, o agente de captura de pacote está instalado na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="51344-138">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="51344-139">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="51344-139">Step 1</span></span>

<span data-ttu-id="51344-140">A próxima etapa é recuperar a instância do Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="51344-140">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="51344-141">Essa variável é passada para o cmdlet `New-AzureRmNetworkWatcherPacketCapture` na etapa 4.</span><span class="sxs-lookup"><span data-stu-id="51344-141">This variable is passed to the `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="51344-142">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="51344-142">Step 2</span></span>

<span data-ttu-id="51344-143">Recupere uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="51344-143">Retrieve a storage account.</span></span> <span data-ttu-id="51344-144">Essa conta de armazenamento é usada para armazenar o arquivo de captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="51344-144">This storage account is used to store the packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="51344-145">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="51344-145">Step 3</span></span>

<span data-ttu-id="51344-146">Os filtros podem ser usados para limitar os dados armazenados pela captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="51344-146">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="51344-147">O exemplo a seguir configura dois filtros.</span><span class="sxs-lookup"><span data-stu-id="51344-147">The following example sets up two filters.</span></span>  <span data-ttu-id="51344-148">Um filtro coleta o tráfego de saída TCP somente do IP local 10.0.0.3 até as portas de destino 20, 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="51344-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="51344-149">O segundo filtro coleta apenas o tráfego UDP.</span><span class="sxs-lookup"><span data-stu-id="51344-149">The second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="51344-150">Vários filtros podem ser definidos para uma captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="51344-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="51344-151">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="51344-151">Step 4</span></span>

<span data-ttu-id="51344-152">Execute o cmdlet `New-AzureRmNetworkWatcherPacketCapture` para iniciar o processo de captura de pacotes, passando os valores necessários recuperados nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="51344-152">Run the `New-AzureRmNetworkWatcherPacketCapture` cmdlet to start the packet capture process, passing the required values retrieved in the preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="51344-153">O exemplo a seguir é a saída esperada ao executar o cmdlet `New-AzureRmNetworkWatcherPacketCapture`.</span><span class="sxs-lookup"><span data-stu-id="51344-153">The following example is the expected output from running the `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"3bf27278-8251-4651-9546-c7f369855e4e"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]


```

## <a name="get-a-packet-capture"></a><span data-ttu-id="51344-154">Obter uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="51344-154">Get a packet capture</span></span>

<span data-ttu-id="51344-155">Executando o `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, recupera o status de uma captura de pacote atualmente em execução ou concluído.</span><span class="sxs-lookup"><span data-stu-id="51344-155">Running the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="51344-156">O exemplo a seguir é a saída do cmdlet `Get-AzureRmNetworkWatcherPacketCapture`.</span><span class="sxs-lookup"><span data-stu-id="51344-156">The following example is the output from the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="51344-157">O exemplo a seguir é após a conclusão da captura.</span><span class="sxs-lookup"><span data-stu-id="51344-157">The following example is after the capture is complete.</span></span> <span data-ttu-id="51344-158">O valor de PacketCaptureStatus é Parado, com um StopReason de TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="51344-158">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="51344-159">Esse valor mostra que a captura de pacote foi bem-sucedida e executou seu tempo.</span><span class="sxs-lookup"><span data-stu-id="51344-159">This value shows that the packet capture was successful and ran its time.</span></span>
```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"4b9a81ed-dc63-472e-869e-96d7166ccb9b"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]
CaptureStartTime        : 2/1/2017 10:43:01 PM
PacketCaptureStatus     : Stopped
StopReason              : TimeExceeded
PacketCaptureError      : []
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="51344-160">Parar uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="51344-160">Stop a packet capture</span></span>

<span data-ttu-id="51344-161">Ao executar o cmdlet `Stop-AzureRmNetworkWatcherPacketCapture`, se uma sessão de captura estiver em andamento, será interrompida.</span><span class="sxs-lookup"><span data-stu-id="51344-161">By running the `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="51344-162">O cmdlet retorna sem resposta quando executado em uma sessão de captura atualmente em execução ou uma sessão existente que já foi interrompido.</span><span class="sxs-lookup"><span data-stu-id="51344-162">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="51344-163">Excluir uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="51344-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="51344-164">Excluir uma captura de pacote não exclui o arquivo da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="51344-164">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="51344-165">Baixar uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="51344-165">Download a packet capture</span></span>

<span data-ttu-id="51344-166">Quando a sessão de captura de pacote for concluído, o arquivo de captura pode ser carregado no Armazenamento de Blobs ou em um arquivo local na VM.</span><span class="sxs-lookup"><span data-stu-id="51344-166">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="51344-167">O local de armazenamento da captura de pacote é definido no momento da criação da sessão.</span><span class="sxs-lookup"><span data-stu-id="51344-167">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="51344-168">Uma ferramenta conveniente para acessar esses arquivos de captura salvos em uma conta de armazenamento é o Gerenciador de Armazenamento do Microsoft Azure, que pode ser baixado aqui: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="51344-168">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="51344-169">Se uma conta de armazenamento for especificada, os arquivos de captura de pacote serão salvos em uma conta de armazenamento no seguinte local:</span><span class="sxs-lookup"><span data-stu-id="51344-169">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="51344-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="51344-170">Next steps</span></span>

<span data-ttu-id="51344-171">Saiba como automatizar a captura de pacote com alertas de máquina Virtual por meio da exibição [criar uma captura de pacote acionado alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="51344-171">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="51344-172">Localizar se determinado tráfego é permitido dentro ou fora de sua VM visitando [Verificar o fluxo de IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="51344-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














