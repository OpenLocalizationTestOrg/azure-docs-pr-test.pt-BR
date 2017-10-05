---
title: "Gerenciar capturas de pacote com o Observador de Rede do Azure – CLI 1.0 do Azure | Microsoft Docs"
description: "Esta página explica como gerenciar o recurso de captura de pacote do Observador de Rede usando a CLI 1.0 do Azure"
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
ms.openlocfilehash: 91588910334859c1ea77186674d5bfb31b311b36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="8c6c8-103">Gerenciar as capturas de pacote com o Observador de Rede do Azure usando a CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="8c6c8-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8c6c8-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8c6c8-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="8c6c8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c6c8-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="8c6c8-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8c6c8-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="8c6c8-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8c6c8-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="8c6c8-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="8c6c8-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="8c6c8-109">Captura de pacote do Observador de Rede permite que você crie sessões de captura para controlar o tráfego em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="8c6c8-110">Os filtros são fornecidos para a sessão de captura garantir que somente o tráfego que você deseja capturar.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="8c6c8-111">Captura de pacote ajuda a diagnosticar problemas de rede reativo e proativo.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="8c6c8-112">Outros usos incluem a coleta de estatísticas de rede, obter informações sobre as invasões de rede, para depurar comunicações cliente-servidor e muito mais.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="8c6c8-113">Por poder remotamente disparar a captura de pacote, esse recurso alivia a carga da execução de uma captura de pacote e manualmente no computador desejado, o que economiza tempo.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="8c6c8-114">Este artigo usa a CLI 1.0 do Azure para plataforma cruzada, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="8c6c8-115">Este artigo o guiará durante as tarefas de gerenciamento diferentes que estão atualmente disponíveis para captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-115">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="8c6c8-116">**Iniciar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="8c6c8-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="8c6c8-117">**Parar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="8c6c8-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="8c6c8-118">**Excluir uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="8c6c8-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="8c6c8-119">**Baixar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="8c6c8-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="8c6c8-120">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="8c6c8-120">Before you begin</span></span>

<span data-ttu-id="8c6c8-121">Este artigo pressupõe que você tenha os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="8c6c8-121">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="8c6c8-122">Uma instância do Observador de Rede na região que você deseja criar uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="8c6c8-122">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="8c6c8-123">Uma máquina virtual com a extensão de captura de pacote habilitada.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-123">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c6c8-124">Captura de pacote requer um agente está em execução na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-124">Packet capture requires an agent to be running on the virtual machine.</span></span> <span data-ttu-id="8c6c8-125">O agente é instalado como uma extensão.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-125">The Agent is installed as an extension.</span></span> <span data-ttu-id="8c6c8-126">Para obter instruções sobre extensões de VM, visite [recursos e extensões de máquina Virtual](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="8c6c8-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="8c6c8-127">Instalar a extensão de VM</span><span class="sxs-lookup"><span data-stu-id="8c6c8-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="8c6c8-128">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="8c6c8-128">Step 1</span></span>

<span data-ttu-id="8c6c8-129">Execute o `azure vm extension set` cmdlet para instalar o agente de captura de pacote na máquina virtual convidada.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-129">Run the `azure vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="8c6c8-130">Para máquinas virtuais do Windows:</span><span class="sxs-lookup"><span data-stu-id="8c6c8-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="8c6c8-131">Para máquinas virtuais Linux:</span><span class="sxs-lookup"><span data-stu-id="8c6c8-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="8c6c8-132">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="8c6c8-132">Step 2</span></span>

<span data-ttu-id="8c6c8-133">Para garantir que o agente está instalado, execute o `vm extension get` cmdlet e passe o nome de máquina virtual e o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-133">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="8c6c8-134">Verifique a lista resultante para garantir que o agente está instalado.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-134">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="8c6c8-135">O exemplo a seguir é um exemplo de resposta de execução`azure vm extension get`</span><span class="sxs-lookup"><span data-stu-id="8c6c8-135">The following sample is an example of the response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up the VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="8c6c8-136">Iniciar uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="8c6c8-136">Start a packet capture</span></span>

<span data-ttu-id="8c6c8-137">Depois que as etapas anteriores forem concluídas, o agente de captura de pacote está instalado na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-137">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="8c6c8-138">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="8c6c8-138">Step 1</span></span>

<span data-ttu-id="8c6c8-139">A próxima etapa é recuperar a instância do Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-139">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="8c6c8-140">Essa variável é passada para o cmdlet `network watcher show` na etapa 4.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-140">This variable is passed to the `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="8c6c8-141">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="8c6c8-141">Step 2</span></span>

<span data-ttu-id="8c6c8-142">Recupere uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-142">Retrieve a storage account.</span></span> <span data-ttu-id="8c6c8-143">Essa conta de armazenamento é usada para armazenar o arquivo de captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-143">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="8c6c8-144">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="8c6c8-144">Step 3</span></span>

<span data-ttu-id="8c6c8-145">Filtros podem ser usados para limitar os dados armazenados por pacote de captura.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-145">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="8c6c8-146">O exemplo a seguir configura uma captura de pacote com vários filtros.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-146">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="8c6c8-147">Os três primeiros filtros coletam tráfego de saída TCP apenas de IP local 10.0.0.3 para portas de destino de 20, 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-147">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="8c6c8-148">O último filtro coleta apenas o tráfego UDP.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-148">The last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="8c6c8-149">Vários filtros podem ser definidos para uma captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="8c6c8-150">Se você estiver usando uma estrutura de filtro complexas, é melhor usar filtros como um arquivo json para evitar erros de sintaxe.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-150">If you are using a complex filter structure, it is better to use filters as a json file to avoid syntax errors.</span></span> <span data-ttu-id="8c6c8-151">Por exemplo, use o sinalizador "-r" (em vez de "-f") e passar o local de um arquivo json que contém os seguintes filtros:</span><span class="sxs-lookup"><span data-stu-id="8c6c8-151">For example, use the flag "-r" (instead of "-f") and pass the location of a json file containing the following filters:</span></span>

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


<span data-ttu-id="8c6c8-152">O exemplo a seguir é a saída esperada executem o cmdlet `network watcher packet-capture create`.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-152">The following example is the expected output from running the `network watcher packet-capture create` cmdlet.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="8c6c8-153">Obter uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="8c6c8-153">Get a packet capture</span></span>

<span data-ttu-id="8c6c8-154">Executando o `network watcher packet-capture show` cmdlet, recupera o status de uma captura de pacote atualmente em execução ou concluído.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-154">Running the `network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="8c6c8-155">O exemplo a seguir é a saída do cmdlet `network watcher packet-capture show`.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-155">The following example is the output from the `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="8c6c8-156">O exemplo a seguir é após a conclusão da captura.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-156">The following example is after the capture is complete.</span></span> <span data-ttu-id="8c6c8-157">O valor de PacketCaptureStatus é Parado, com um StopReason de TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-157">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="8c6c8-158">Esse valor mostra que a captura de pacote foi bem-sucedida e executou seu tempo.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-158">This value shows that the packet capture was successful and ran its time.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="8c6c8-159">Parar uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="8c6c8-159">Stop a packet capture</span></span>

<span data-ttu-id="8c6c8-160">Ao executar o cmdlet `network watcher packet-capture stop`, se uma sessão de captura estiver em andamento, será interrompida.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-160">By running the `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="8c6c8-161">O cmdlet retorna sem resposta quando executado em uma sessão de captura atualmente em execução ou uma sessão existente que já foi interrompido.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-161">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="8c6c8-162">Excluir uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="8c6c8-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="8c6c8-163">Excluir uma captura de pacote não exclui o arquivo da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-163">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="8c6c8-164">Baixar uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="8c6c8-164">Download a packet capture</span></span>

<span data-ttu-id="8c6c8-165">Quando a sessão de captura de pacote for concluído, o arquivo de captura pode ser carregado no Armazenamento de Blobs ou em um arquivo local na VM.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-165">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="8c6c8-166">O local de armazenamento da captura de pacote é definido no momento da criação da sessão.</span><span class="sxs-lookup"><span data-stu-id="8c6c8-166">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="8c6c8-167">Uma ferramenta conveniente para acessar esses arquivos de captura salvos em uma conta de armazenamento é o Gerenciador de Armazenamento do Microsoft Azure, que pode ser baixado aqui: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="8c6c8-167">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="8c6c8-168">Se uma conta de armazenamento for especificada, os arquivos de captura de pacote serão salvos em uma conta de armazenamento no seguinte local:</span><span class="sxs-lookup"><span data-stu-id="8c6c8-168">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="8c6c8-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8c6c8-169">Next steps</span></span>

<span data-ttu-id="8c6c8-170">Saiba como automatizar as capturas de pacotes com alertas da Máquina Virtual exibindo [Criar uma captura de pacotes disparada por alertas](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="8c6c8-170">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="8c6c8-171">Localize se determinado tráfego é permitido dentro ou fora de sua VM visitando [Verificar o fluxo do IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="8c6c8-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
