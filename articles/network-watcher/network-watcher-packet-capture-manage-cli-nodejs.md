---
title: captura de pacote aaaManage com observador de rede do Azure - 1.0 da CLI do Azure | Microsoft Docs
description: "Esta página explica como toomanage Olá recurso de captura de pacote do observador de rede usando o Azure CLI 1.0"
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
ms.openlocfilehash: c4b710a8d82ccaaf65876a8c2ef845aa97b5f831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="a3077-103">Gerenciar as capturas de pacote com o Observador de Rede do Azure usando a CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="a3077-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a3077-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a3077-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="a3077-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3077-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="a3077-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a3077-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="a3077-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a3077-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="a3077-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="a3077-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="a3077-109">Captura de pacote do Inspetor de rede permite que você toocreate captura sessões tootrack tráfego tooand de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a3077-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="a3077-110">Filtros são fornecidos para Olá tooensure de sessão de captura que somente o tráfego de saudação que você deseja capturar.</span><span class="sxs-lookup"><span data-stu-id="a3077-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="a3077-111">Captura de pacote ajuda anomalias de rede toodiagnose reativo e proativo.</span><span class="sxs-lookup"><span data-stu-id="a3077-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="a3077-112">Outros usos incluem a coleta de estatísticas de rede, obtenção de informações de invasões de rede, toodebug cliente-servidor comunicações e muito mais.</span><span class="sxs-lookup"><span data-stu-id="a3077-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="a3077-113">Sendo tooremotely capaz de captura de pacote de gatilho, esse recurso facilita a carga de saudação da execução de uma captura de pacote e manualmente no computador desejado hello, que economiza tempo.</span><span class="sxs-lookup"><span data-stu-id="a3077-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="a3077-114">Este artigo usa a CLI 1.0 do Azure para plataforma cruzada, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="a3077-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="a3077-115">Este artigo o orienta por Olá diversas tarefas de gerenciamento que estão atualmente disponíveis para captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="a3077-115">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="a3077-116">**Iniciar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="a3077-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="a3077-117">**Parar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="a3077-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="a3077-118">**Excluir uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="a3077-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="a3077-119">**Baixar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="a3077-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="a3077-120">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="a3077-120">Before you begin</span></span>

<span data-ttu-id="a3077-121">Este artigo pressupõe que você tenha Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3077-121">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="a3077-122">Uma instância do observador de rede na região Olá deseja toocreate uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="a3077-122">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="a3077-123">Uma máquina virtual com o pacote de saudação capturar extensão habilitada.</span><span class="sxs-lookup"><span data-stu-id="a3077-123">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3077-124">Captura de pacote requer um toobe de agente em execução na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3077-124">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="a3077-125">Olá agente é instalado como uma extensão.</span><span class="sxs-lookup"><span data-stu-id="a3077-125">hello Agent is installed as an extension.</span></span> <span data-ttu-id="a3077-126">Para obter instruções sobre extensões de VM, visite [recursos e extensões de máquina Virtual](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="a3077-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="a3077-127">Instalar a extensão de VM</span><span class="sxs-lookup"><span data-stu-id="a3077-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="a3077-128">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="a3077-128">Step 1</span></span>

<span data-ttu-id="a3077-129">Executar Olá `azure vm extension set` agente de captura de pacote do cmdlet tooinstall Olá na máquina de virtual do convidado hello.</span><span class="sxs-lookup"><span data-stu-id="a3077-129">Run hello `azure vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="a3077-130">Para máquinas virtuais do Windows:</span><span class="sxs-lookup"><span data-stu-id="a3077-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="a3077-131">Para máquinas virtuais Linux:</span><span class="sxs-lookup"><span data-stu-id="a3077-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="a3077-132">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="a3077-132">Step 2</span></span>

<span data-ttu-id="a3077-133">tooensure que Olá agente estiver instalado, execute Olá `vm extension get` cmdlet e passá-lo a grupo de recursos de saudação e o nome da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a3077-133">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="a3077-134">Verifique a saudação resultante lista tooensure Olá agente está instalado.</span><span class="sxs-lookup"><span data-stu-id="a3077-134">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="a3077-135">saudação de exemplo a seguir é um exemplo de resposta de saudação em execução`azure vm extension get`</span><span class="sxs-lookup"><span data-stu-id="a3077-135">hello following sample is an example of hello response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="a3077-136">Iniciar uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="a3077-136">Start a packet capture</span></span>

<span data-ttu-id="a3077-137">Depois de hello a etapas anteriores forem concluídas, agente de captura de pacote de saudação é instalado na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3077-137">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="a3077-138">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="a3077-138">Step 1</span></span>

<span data-ttu-id="a3077-139">Olá próxima etapa é a instância do tooretrieve Olá observador de rede.</span><span class="sxs-lookup"><span data-stu-id="a3077-139">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="a3077-140">Essa variável é passada toohello `network watcher show` cmdlet na etapa 4.</span><span class="sxs-lookup"><span data-stu-id="a3077-140">This variable is passed toohello `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="a3077-141">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="a3077-141">Step 2</span></span>

<span data-ttu-id="a3077-142">Recupere uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a3077-142">Retrieve a storage account.</span></span> <span data-ttu-id="a3077-143">Esta conta de armazenamento é um arquivo de captura de pacote usado toostore hello.</span><span class="sxs-lookup"><span data-stu-id="a3077-143">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="a3077-144">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="a3077-144">Step 3</span></span>

<span data-ttu-id="a3077-145">Filtros podem ser dados de saudação toolimit usado armazenado por captura de pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3077-145">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="a3077-146">Olá exemplo a seguir configura um pacote de captura com vários filtros.</span><span class="sxs-lookup"><span data-stu-id="a3077-146">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="a3077-147">Olá três primeiros filtros coletam tráfego de TCP de saída somente local IP 10.0.0.3 toodestination portas 20, 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="a3077-147">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="a3077-148">filtro de última Olá coleta somente o tráfego UDP.</span><span class="sxs-lookup"><span data-stu-id="a3077-148">hello last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="a3077-149">Vários filtros podem ser definidos para uma captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="a3077-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="a3077-150">Se você estiver usando uma estrutura de filtro complexas, é melhor filtros de toouse como um erro de sintaxe de tooavoid de arquivo json.</span><span class="sxs-lookup"><span data-stu-id="a3077-150">If you are using a complex filter structure, it is better toouse filters as a json file tooavoid syntax errors.</span></span> <span data-ttu-id="a3077-151">Por exemplo, use o sinalizador de hello "-r" (em vez de "-f") e passar Olá local de um arquivo json que contém a saudação filtros a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3077-151">For example, use hello flag "-r" (instead of "-f") and pass hello location of a json file containing hello following filters:</span></span>

```json
[
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"20"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"80"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"443"
    },
    {
        "protocol":"UDP"
    }
]
```


<span data-ttu-id="a3077-152">Olá, exemplo a seguir é saída de hello esperada da execução de saudação `network watcher packet-capture create` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a3077-152">hello following example is hello expected output from running hello `network watcher packet-capture create` cmdlet.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="a3077-153">Obter uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="a3077-153">Get a packet capture</span></span>

<span data-ttu-id="a3077-154">Executando Olá `network watcher packet-capture show` cmdlet, recupera o status de saudação de uma captura de pacote em execução no momento ou foi concluída.</span><span class="sxs-lookup"><span data-stu-id="a3077-154">Running hello `network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="a3077-155">Olá, exemplo a seguir é saída Olá Olá `network watcher packet-capture show` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a3077-155">hello following example is hello output from hello `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="a3077-156">Olá exemplo a seguir é após a conclusão da captura de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3077-156">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="a3077-157">Olá valor PacketCaptureStatus for interrompido, com um StopReason de TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="a3077-157">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="a3077-158">Esse valor mostra que a captura de pacote de saudação foi bem-sucedida e executou seu tempo.</span><span class="sxs-lookup"><span data-stu-id="a3077-158">This value shows that hello packet capture was successful and ran its time.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="a3077-159">Parar uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="a3077-159">Stop a packet capture</span></span>

<span data-ttu-id="a3077-160">Executando Olá `network watcher packet-capture stop` cmdlet, se uma sessão de captura está em andamento ele é interrompido.</span><span class="sxs-lookup"><span data-stu-id="a3077-160">By running hello `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="a3077-161">Olá cmdlet não retorna resposta quando executado em uma sessão de captura atualmente em execução ou uma sessão existente que já foi interrompido.</span><span class="sxs-lookup"><span data-stu-id="a3077-161">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="a3077-162">Excluir uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="a3077-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="a3077-163">Excluir uma captura de pacote não exclui o arquivo hello na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="a3077-163">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="a3077-164">Baixar um pacote de capturas</span><span class="sxs-lookup"><span data-stu-id="a3077-164">Download a packet capture</span></span>

<span data-ttu-id="a3077-165">Depois de concluído, a sessão de captura de pacote hello captura arquivo pode ser carregado tooblob tooa ou armazenamento local arquivo em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="a3077-165">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="a3077-166">local de armazenamento de saudação de captura de pacote de saudação é definido no momento da criação da sessão de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3077-166">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="a3077-167">Uma ferramenta conveniente tooaccess esses capturar os arquivos salvos tooa conta de armazenamento é o Microsoft Azure Storage Explorer, que pode ser baixado em: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="a3077-167">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="a3077-168">Se uma conta de armazenamento for especificada, os arquivos de captura de pacote são salvos tooa conta de armazenamento no hello local a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3077-168">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="a3077-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a3077-169">Next steps</span></span>

<span data-ttu-id="a3077-170">Saiba como o pacote tooautomate captura com alertas de máquina Virtual por meio da exibição [criar uma captura de pacote de disparo de alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="a3077-170">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="a3077-171">Localize se determinado tráfego é permitido dentro ou fora de sua VM visitando [Verificar o fluxo do IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a3077-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
