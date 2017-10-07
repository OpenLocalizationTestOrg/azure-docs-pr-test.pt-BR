---
title: captura de pacote aaaManage com observador de rede do Azure - 2.0 do CLI do Azure | Microsoft Docs
description: "Esta página explica como toomanage Olá recurso de captura de pacote do observador de rede usando o Azure CLI 2.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d19cb7d0ca3b7a9bc0546859e07ef6d4df4f42d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="be1f2-103">Gerenciar as capturas de pacote com o Observador de Rede do Azure usando a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="be1f2-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="be1f2-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="be1f2-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="be1f2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be1f2-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="be1f2-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="be1f2-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="be1f2-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="be1f2-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="be1f2-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="be1f2-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="be1f2-109">Captura de pacote do Inspetor de rede permite que você toocreate captura sessões tootrack tráfego tooand de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="be1f2-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="be1f2-110">Filtros são fornecidos para Olá tooensure de sessão de captura que somente o tráfego de saudação que você deseja capturar.</span><span class="sxs-lookup"><span data-stu-id="be1f2-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="be1f2-111">Captura de pacote ajuda anomalias de rede toodiagnose reativo e proativo.</span><span class="sxs-lookup"><span data-stu-id="be1f2-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="be1f2-112">Outros usos incluem a coleta de estatísticas de rede, obtenção de informações de invasões de rede, toodebug cliente-servidor comunicações e muito mais.</span><span class="sxs-lookup"><span data-stu-id="be1f2-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="be1f2-113">Sendo tooremotely capaz de captura de pacote de gatilho, esse recurso facilita a carga de saudação da execução de uma captura de pacote e manualmente no computador desejado hello, que economiza tempo.</span><span class="sxs-lookup"><span data-stu-id="be1f2-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="be1f2-114">Este artigo usa nossa próxima geração CLI para o modelo de implantação de gerenciamento de recursos do hello, 2.0 do CLI do Azure, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="be1f2-114">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="be1f2-115">Olá tooperform as etapas neste artigo, é necessário muito[instalar Olá Interface de linha de comando do Azure para Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="be1f2-115">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="be1f2-116">Este artigo o orienta por Olá diversas tarefas de gerenciamento que estão atualmente disponíveis para captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="be1f2-116">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="be1f2-117">**Iniciar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="be1f2-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="be1f2-118">**Parar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="be1f2-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="be1f2-119">**Excluir uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="be1f2-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="be1f2-120">**Baixar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="be1f2-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="be1f2-121">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="be1f2-121">Before you begin</span></span>

<span data-ttu-id="be1f2-122">Este artigo pressupõe que você tenha Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="be1f2-122">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="be1f2-123">Uma instância do observador de rede na região Olá deseja toocreate uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="be1f2-123">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="be1f2-124">Uma máquina virtual com o pacote de saudação capturar extensão habilitada.</span><span class="sxs-lookup"><span data-stu-id="be1f2-124">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="be1f2-125">Captura de pacote requer um toobe de agente em execução na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="be1f2-125">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="be1f2-126">Olá agente é instalado como uma extensão.</span><span class="sxs-lookup"><span data-stu-id="be1f2-126">hello Agent is installed as an extension.</span></span> <span data-ttu-id="be1f2-127">Para obter instruções sobre extensões de VM, visite [recursos e extensões de máquina Virtual](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="be1f2-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="be1f2-128">Instalar a extensão de VM</span><span class="sxs-lookup"><span data-stu-id="be1f2-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="be1f2-129">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="be1f2-129">Step 1</span></span>

<span data-ttu-id="be1f2-130">Executar Olá `az vm extension set` agente de captura de pacote do cmdlet tooinstall Olá na máquina de virtual do convidado hello.</span><span class="sxs-lookup"><span data-stu-id="be1f2-130">Run hello `az vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="be1f2-131">Para máquinas virtuais do Windows:</span><span class="sxs-lookup"><span data-stu-id="be1f2-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="be1f2-132">Para máquinas virtuais Linux:</span><span class="sxs-lookup"><span data-stu-id="be1f2-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="be1f2-133">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="be1f2-133">Step 2</span></span>

<span data-ttu-id="be1f2-134">tooensure que Olá agente estiver instalado, execute Olá `vm extension get` cmdlet e passá-lo a grupo de recursos de saudação e o nome da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="be1f2-134">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="be1f2-135">Verifique a saudação resultante lista tooensure Olá agente está instalado.</span><span class="sxs-lookup"><span data-stu-id="be1f2-135">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="be1f2-136">saudação de exemplo a seguir é um exemplo de resposta de saudação em execução`az vm extension show`</span><span class="sxs-lookup"><span data-stu-id="be1f2-136">hello following sample is an example of hello response from running `az vm extension show`</span></span>

```json
{
  "autoUpgradeMinorVersion": true,
  "forceUpdateTag": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/NetworkWatcherAgentWindows",
  "instanceView": null,
  "location": "westcentralus",
  "name": "NetworkWatcherAgentWindows",
  "protectedSettings": null,
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.NetworkWatcher",
  "resourceGroup": "{resourceGroupName}",
  "settings": null,
  "tags": null,
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "1.4",
  "virtualMachineExtensionType": "NetworkWatcherAgentWindows"
}
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="be1f2-137">Iniciar uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="be1f2-137">Start a packet capture</span></span>

<span data-ttu-id="be1f2-138">Depois de hello a etapas anteriores forem concluídas, agente de captura de pacote de saudação é instalado na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="be1f2-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="be1f2-139">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="be1f2-139">Step 1</span></span>

<span data-ttu-id="be1f2-140">Olá próxima etapa é a instância do tooretrieve Olá observador de rede.</span><span class="sxs-lookup"><span data-stu-id="be1f2-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="be1f2-141">Nome da seção de saudação observador de rede é passado toohello `az network watcher show` cmdlet na etapa 4.</span><span class="sxs-lookup"><span data-stu-id="be1f2-141">TThe name of hello Network Watcher is passed toohello `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="be1f2-142">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="be1f2-142">Step 2</span></span>

<span data-ttu-id="be1f2-143">Recupere uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="be1f2-143">Retrieve a storage account.</span></span> <span data-ttu-id="be1f2-144">Esta conta de armazenamento é um arquivo de captura de pacote usado toostore hello.</span><span class="sxs-lookup"><span data-stu-id="be1f2-144">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="be1f2-145">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="be1f2-145">Step 3</span></span>

<span data-ttu-id="be1f2-146">Filtros podem ser dados de saudação toolimit usado armazenado por captura de pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="be1f2-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="be1f2-147">Olá exemplo a seguir configura um pacote de captura com vários filtros.</span><span class="sxs-lookup"><span data-stu-id="be1f2-147">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="be1f2-148">Olá três primeiros filtros coletam tráfego de TCP de saída somente local IP 10.0.0.3 toodestination portas 20, 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="be1f2-148">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="be1f2-149">filtro de última Olá coleta somente o tráfego UDP.</span><span class="sxs-lookup"><span data-stu-id="be1f2-149">hello last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="be1f2-150">Olá, exemplo a seguir é saída de hello esperada da execução de saudação `az network watcher packet-capture create` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="be1f2-150">hello following example is hello expected output from running hello `az network watcher packet-capture create` cmdlet.</span></span>

```json
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/pa
cketCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/p
roviders/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapture_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="be1f2-151">Obter uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="be1f2-151">Get a packet capture</span></span>

<span data-ttu-id="be1f2-152">Executando Olá `az network watcher packet-capture show` cmdlet, recupera o status de saudação de uma captura de pacote em execução no momento ou foi concluída.</span><span class="sxs-lookup"><span data-stu-id="be1f2-152">Running hello `az network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="be1f2-153">Olá, exemplo a seguir é saída Olá Olá `az network watcher packet-capture show` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="be1f2-153">hello following example is hello output from hello `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="be1f2-154">Olá exemplo a seguir é após a conclusão da captura de saudação.</span><span class="sxs-lookup"><span data-stu-id="be1f2-154">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="be1f2-155">Olá valor PacketCaptureStatus for interrompido, com um StopReason de TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="be1f2-155">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="be1f2-156">Esse valor mostra que a captura de pacote de saudação foi bem-sucedida e executou seu tempo.</span><span class="sxs-lookup"><span data-stu-id="be1f2-156">This value shows that hello packet capture was successful and ran its time.</span></span>

```
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/providers/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapt
ure_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="be1f2-157">Parar uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="be1f2-157">Stop a packet capture</span></span>

<span data-ttu-id="be1f2-158">Executando Olá `az network watcher packet-capture stop` cmdlet, se uma sessão de captura está em andamento ele é interrompido.</span><span class="sxs-lookup"><span data-stu-id="be1f2-158">By running hello `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="be1f2-159">Olá cmdlet não retorna resposta quando executado em uma sessão de captura atualmente em execução ou uma sessão existente que já foi interrompido.</span><span class="sxs-lookup"><span data-stu-id="be1f2-159">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="be1f2-160">Excluir uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="be1f2-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="be1f2-161">Excluir uma captura de pacote não exclui o arquivo hello na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="be1f2-161">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="be1f2-162">Baixar um pacote de capturas</span><span class="sxs-lookup"><span data-stu-id="be1f2-162">Download a packet capture</span></span>

<span data-ttu-id="be1f2-163">Depois de concluído, a sessão de captura de pacote hello captura arquivo pode ser carregado tooblob tooa ou armazenamento local arquivo em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="be1f2-163">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="be1f2-164">local de armazenamento de saudação de captura de pacote de saudação é definido no momento da criação da sessão de saudação.</span><span class="sxs-lookup"><span data-stu-id="be1f2-164">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="be1f2-165">Uma ferramenta conveniente tooaccess esses capturar os arquivos salvos tooa conta de armazenamento é o Microsoft Azure Storage Explorer, que pode ser baixado em: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="be1f2-165">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="be1f2-166">Se uma conta de armazenamento for especificada, os arquivos de captura de pacote são salvos tooa conta de armazenamento no hello local a seguir:</span><span class="sxs-lookup"><span data-stu-id="be1f2-166">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="be1f2-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="be1f2-167">Next steps</span></span>

<span data-ttu-id="be1f2-168">Saiba como o pacote tooautomate captura com alertas de máquina Virtual por meio da exibição [criar uma captura de pacote de disparo de alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="be1f2-168">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="be1f2-169">Localize se determinado tráfego é permitido dentro ou fora de sua VM visitando [Verificar o fluxo do IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="be1f2-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
