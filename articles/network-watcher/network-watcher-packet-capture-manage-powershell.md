---
title: captura de pacote aaaManage com observador de rede do Azure - PowerShell | Microsoft Docs
description: "Esta página explica como o pacote de saudação toomanage capturar recurso do observador de rede usando o PowerShell"
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
ms.openlocfilehash: 77a522a1b05e020a73ba7140c1410615eb8761da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="60492-103">Gerenciar as capturas de pacotes com o Observador de Rede do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="60492-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="60492-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="60492-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="60492-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="60492-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="60492-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="60492-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="60492-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="60492-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="60492-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="60492-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="60492-109">Captura de pacote do Inspetor de rede permite que você toocreate captura sessões tootrack tráfego tooand de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="60492-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="60492-110">Filtros são fornecidos para Olá tooensure de sessão de captura que somente o tráfego de saudação que você deseja capturar.</span><span class="sxs-lookup"><span data-stu-id="60492-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="60492-111">Captura de pacote ajuda anomalias de rede toodiagnose reativo e proativo.</span><span class="sxs-lookup"><span data-stu-id="60492-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="60492-112">Outros usos incluem a coleta de estatísticas de rede, obtenção de informações de invasões de rede, toodebug cliente-servidor comunicações e muito mais.</span><span class="sxs-lookup"><span data-stu-id="60492-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="60492-113">Sendo tooremotely capaz de captura de pacote de gatilho, esse recurso facilita a carga de saudação da execução de uma captura de pacote e manualmente no computador desejado hello, que economiza tempo.</span><span class="sxs-lookup"><span data-stu-id="60492-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="60492-114">Este artigo o orienta por Olá diversas tarefas de gerenciamento que estão atualmente disponíveis para captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="60492-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="60492-115">**Iniciar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="60492-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="60492-116">**Parar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="60492-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="60492-117">**Excluir uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="60492-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="60492-118">**Baixar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="60492-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="60492-119">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="60492-119">Before you begin</span></span>

<span data-ttu-id="60492-120">Este artigo pressupõe que você tenha Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="60492-120">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="60492-121">Uma instância do observador de rede na região Olá deseja toocreate uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="60492-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>

* <span data-ttu-id="60492-122">Uma máquina virtual com o pacote de saudação capturar extensão habilitada.</span><span class="sxs-lookup"><span data-stu-id="60492-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60492-123">A captura de pacotes requer uma extensão da máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="60492-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="60492-124">Para instalar a extensão de saudação em uma VM do Windows, visite [extensão de máquina virtual do agente do Inspetor de rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para a visita de VM do Linux [extensão de máquina virtual do agente do Inspetor de rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="60492-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="60492-125">Instalar a extensão de VM</span><span class="sxs-lookup"><span data-stu-id="60492-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="60492-126">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="60492-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="60492-127">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="60492-127">Step 2</span></span>

<span data-ttu-id="60492-128">exemplo a seguir recupera informações de extensão de Olá Olá necessário Olá toorun `Set-AzureRmVMExtension` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="60492-128">hello following example retrieves hello extension information needed toorun hello `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="60492-129">Este cmdlet instala o agente de captura de pacote de saudação na máquina de virtual do convidado hello.</span><span class="sxs-lookup"><span data-stu-id="60492-129">This cmdlet installs hello packet capture agent on hello guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="60492-130">Olá `Set-AzureRmVMExtension` cmdlet pode levar vários toocomplete de minutos.</span><span class="sxs-lookup"><span data-stu-id="60492-130">hello `Set-AzureRmVMExtension` cmdlet may take several minutes toocomplete.</span></span>

<span data-ttu-id="60492-131">Para máquinas virtuais do Windows:</span><span class="sxs-lookup"><span data-stu-id="60492-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="60492-132">Para máquinas virtuais Linux:</span><span class="sxs-lookup"><span data-stu-id="60492-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="60492-133">Olá exemplo a seguir é uma resposta bem-sucedida após a execução Olá `Set-AzureRmVMExtension` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="60492-133">hello following example is a successful response after running hello `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="60492-134">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="60492-134">Step 3</span></span>

<span data-ttu-id="60492-135">tooensure que Olá agente estiver instalado, execute Olá `Get-AzureRmVMExtension` cmdlet e passe o nome da máquina virtual Olá Olá nome e extensão.</span><span class="sxs-lookup"><span data-stu-id="60492-135">tooensure that hello agent is installed, run hello `Get-AzureRmVMExtension` cmdlet and pass it hello virtual machine name and hello extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="60492-136">saudação de exemplo a seguir é um exemplo de resposta de saudação em execução`Get-AzureRmVMExtension`</span><span class="sxs-lookup"><span data-stu-id="60492-136">hello following sample is an example of hello response from running `Get-AzureRmVMExtension`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="60492-137">Iniciar uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="60492-137">Start a packet capture</span></span>

<span data-ttu-id="60492-138">Depois de hello a etapas anteriores forem concluídas, agente de captura de pacote de saudação é instalado na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="60492-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="60492-139">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="60492-139">Step 1</span></span>

<span data-ttu-id="60492-140">Olá próxima etapa é a instância do tooretrieve Olá observador de rede.</span><span class="sxs-lookup"><span data-stu-id="60492-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="60492-141">Essa variável é passada toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet na etapa 4.</span><span class="sxs-lookup"><span data-stu-id="60492-141">This variable is passed toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="60492-142">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="60492-142">Step 2</span></span>

<span data-ttu-id="60492-143">Recupere uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="60492-143">Retrieve a storage account.</span></span> <span data-ttu-id="60492-144">Esta conta de armazenamento é um arquivo de captura de pacote usado toostore hello.</span><span class="sxs-lookup"><span data-stu-id="60492-144">This storage account is used toostore hello packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="60492-145">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="60492-145">Step 3</span></span>

<span data-ttu-id="60492-146">Filtros podem ser dados de saudação toolimit usado armazenado por captura de pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="60492-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="60492-147">Olá exemplo a seguir define dois filtros.</span><span class="sxs-lookup"><span data-stu-id="60492-147">hello following example sets up two filters.</span></span>  <span data-ttu-id="60492-148">Coleta de um filtro TCP de saída de tráfego somente do local IP 10.0.0.3 toodestination portas 20, 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="60492-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="60492-149">filtro de segundo Olá coleta somente o tráfego UDP.</span><span class="sxs-lookup"><span data-stu-id="60492-149">hello second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="60492-150">Vários filtros podem ser definidos para uma captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="60492-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="60492-151">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="60492-151">Step 4</span></span>

<span data-ttu-id="60492-152">Executar Olá `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart Olá pacote processo de captura, passar valores hello necessário recuperados Olá etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="60492-152">Run hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart hello packet capture process, passing hello required values retrieved in hello preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="60492-153">Olá, exemplo a seguir é saída de hello esperada da execução de saudação `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="60492-153">hello following example is hello expected output from running hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="60492-154">Obter uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="60492-154">Get a packet capture</span></span>

<span data-ttu-id="60492-155">Executando Olá `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, recupera o status de saudação de uma captura de pacote em execução no momento ou foi concluída.</span><span class="sxs-lookup"><span data-stu-id="60492-155">Running hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="60492-156">Olá, exemplo a seguir é saída Olá Olá `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="60492-156">hello following example is hello output from hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="60492-157">Olá exemplo a seguir é após a conclusão da captura de saudação.</span><span class="sxs-lookup"><span data-stu-id="60492-157">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="60492-158">Olá valor PacketCaptureStatus for interrompido, com um StopReason de TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="60492-158">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="60492-159">Esse valor mostra que a captura de pacote de saudação foi bem-sucedida e executou seu tempo.</span><span class="sxs-lookup"><span data-stu-id="60492-159">This value shows that hello packet capture was successful and ran its time.</span></span>
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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="60492-160">Parar uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="60492-160">Stop a packet capture</span></span>

<span data-ttu-id="60492-161">Executando Olá `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, se uma sessão de captura está em andamento ele é interrompido.</span><span class="sxs-lookup"><span data-stu-id="60492-161">By running hello `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="60492-162">Olá cmdlet não retorna resposta quando executado em uma sessão de captura atualmente em execução ou uma sessão existente que já foi interrompido.</span><span class="sxs-lookup"><span data-stu-id="60492-162">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="60492-163">Excluir uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="60492-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="60492-164">Excluir uma captura de pacote não exclui o arquivo hello na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="60492-164">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="60492-165">Baixar um pacote de capturas</span><span class="sxs-lookup"><span data-stu-id="60492-165">Download a packet capture</span></span>

<span data-ttu-id="60492-166">Depois de concluído, a sessão de captura de pacote hello captura arquivo pode ser carregado tooblob tooa ou armazenamento local arquivo em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="60492-166">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="60492-167">local de armazenamento de saudação de captura de pacote de saudação é definido no momento da criação da sessão de saudação.</span><span class="sxs-lookup"><span data-stu-id="60492-167">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="60492-168">Uma ferramenta conveniente tooaccess esses capturar os arquivos salvos tooa conta de armazenamento é o Microsoft Azure Storage Explorer, que pode ser baixado em: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="60492-168">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="60492-169">Se uma conta de armazenamento for especificada, os arquivos de captura de pacote são salvos tooa conta de armazenamento no hello local a seguir:</span><span class="sxs-lookup"><span data-stu-id="60492-169">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="60492-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="60492-170">Next steps</span></span>

<span data-ttu-id="60492-171">Saiba como o pacote tooautomate captura com alertas de máquina Virtual por meio da exibição [criar uma captura de pacote de disparo de alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="60492-171">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="60492-172">Localizar se determinado tráfego é permitido dentro ou fora de sua VM visitando [Verificar o fluxo de IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="60492-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














