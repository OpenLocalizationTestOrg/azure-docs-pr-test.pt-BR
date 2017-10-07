---
title: captura de pacote aaaManage com observador de rede do Azure - portal do Azure | Microsoft Docs
description: "Esta página explica como toomanage Olá recurso de captura de pacote do observador de rede usando o portal do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="d19a9-103">Gerenciar capturas de pacote com o observador de rede do Azure usando o portal de saudação</span><span class="sxs-lookup"><span data-stu-id="d19a9-103">Manage packet captures with Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d19a9-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d19a9-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="d19a9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d19a9-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="d19a9-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d19a9-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="d19a9-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d19a9-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="d19a9-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="d19a9-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="d19a9-109">Captura de pacote do Inspetor de rede permite que você toocreate captura sessões tootrack tráfego tooand de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d19a9-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="d19a9-110">Filtros são fornecidos para Olá tooensure de sessão de captura que somente o tráfego de saudação que você deseja capturar.</span><span class="sxs-lookup"><span data-stu-id="d19a9-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="d19a9-111">Captura de pacote ajuda anomalias de rede toodiagnose reativo e proativo.</span><span class="sxs-lookup"><span data-stu-id="d19a9-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="d19a9-112">Outros usos incluem a coleta de estatísticas de rede, obtenção de informações de invasões de rede, toodebug cliente-servidor comunicações e muito mais.</span><span class="sxs-lookup"><span data-stu-id="d19a9-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="d19a9-113">Sendo tooremotely capaz de captura de pacote de gatilho, esse recurso facilita a carga de saudação da execução de uma captura de pacote e manualmente no computador desejado hello, que economiza tempo.</span><span class="sxs-lookup"><span data-stu-id="d19a9-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="d19a9-114">Este artigo o orienta por Olá diversas tarefas de gerenciamento que estão atualmente disponíveis para captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="d19a9-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="d19a9-115">**Iniciar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="d19a9-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="d19a9-116">**Parar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="d19a9-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="d19a9-117">**Excluir uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="d19a9-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="d19a9-118">**Baixar uma captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="d19a9-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="d19a9-119">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="d19a9-119">Before you begin</span></span>

<span data-ttu-id="d19a9-120">Este artigo pressupõe que você tenha Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d19a9-120">This article assumes that you have hello following resources:</span></span>

- <span data-ttu-id="d19a9-121">Uma instância do observador de rede na região Olá deseja toocreate uma captura de pacote</span><span class="sxs-lookup"><span data-stu-id="d19a9-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="d19a9-122">Uma máquina virtual com o pacote de saudação capturar extensão habilitada.</span><span class="sxs-lookup"><span data-stu-id="d19a9-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d19a9-123">A captura de pacotes requer uma extensão da máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="d19a9-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="d19a9-124">Para instalar a extensão de saudação em uma VM do Windows, visite [extensão de máquina virtual do agente do Inspetor de rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para a visita de VM do Linux [extensão de máquina virtual do agente do Inspetor de rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="d19a9-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

### <a name="packet-capture-agent-extension-through-hello-portal"></a><span data-ttu-id="d19a9-125">Extensão do agente de captura de pacote por meio do portal Olá</span><span class="sxs-lookup"><span data-stu-id="d19a9-125">Packet Capture agent extension through hello portal</span></span>

<span data-ttu-id="d19a9-126">captura de pacote de saudação tooinstall agente da VM por meio do portal hello, navegar tooyour virtual machine, clique em **extensões** > **adicionar** e procure **rede Inspetor de agente para Windows**</span><span class="sxs-lookup"><span data-stu-id="d19a9-126">tooinstall hello packet capture VM agent through hello portal, navigate tooyour virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span></span>

![exibição de agentes][agent]

## <a name="packet-capture-overview"></a><span data-ttu-id="d19a9-128">visão geral da Captura de Pacotes</span><span class="sxs-lookup"><span data-stu-id="d19a9-128">Packet Capture overview</span></span>

<span data-ttu-id="d19a9-129">Navegue toohello [portal do Azure](https://portal.azure.com) e clique em **rede** > **observador de rede** > **de captura de pacote**</span><span class="sxs-lookup"><span data-stu-id="d19a9-129">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span></span>

<span data-ttu-id="d19a9-130">página de visão geral de saudação mostra a que captura de uma lista de todos os pacotes existentes, independentemente do estado de saudação.</span><span class="sxs-lookup"><span data-stu-id="d19a9-130">hello overview page shows a list of all packet captures that exist no matter hello state.</span></span>

> [!NOTE]
> <span data-ttu-id="d19a9-131">Captura de pacote requer a conta de armazenamento toohello conectividade pela porta 443.</span><span class="sxs-lookup"><span data-stu-id="d19a9-131">Packet capture requires connectivity toohello storage account over port 443.</span></span>

![tela de visão geral da captura de pacotes][1]

## <a name="start-a-packet-capture"></a><span data-ttu-id="d19a9-133">Iniciar uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="d19a9-133">Start a packet capture</span></span>

<span data-ttu-id="d19a9-134">Clique em **adicionar** toocreate uma captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="d19a9-134">Click **Add** toocreate a packet capture.</span></span>

<span data-ttu-id="d19a9-135">Olá propriedades que podem ser definidas em uma captura de pacote são:</span><span class="sxs-lookup"><span data-stu-id="d19a9-135">hello properties that can be defined on a packet capture are:</span></span>

<span data-ttu-id="d19a9-136">**Configurações principais**</span><span class="sxs-lookup"><span data-stu-id="d19a9-136">**Main settings**</span></span>

- <span data-ttu-id="d19a9-137">**Assinatura** -este valor é a assinatura de saudação que é usada, uma instância do observador de rede é necessária em cada assinatura.</span><span class="sxs-lookup"><span data-stu-id="d19a9-137">**Subscription** - This value is hello subscription that is used, an instance of network watcher is needed in each subscription.</span></span>
- <span data-ttu-id="d19a9-138">**Grupo de recursos** -grupo de recursos de saudação da máquina virtual hello está sendo direcionada.</span><span class="sxs-lookup"><span data-stu-id="d19a9-138">**Resource group** - hello resource group of hello virtual machine that is being targeted.</span></span>
- <span data-ttu-id="d19a9-139">**Máquina virtual de destino** -Olá máquina de virtual que está executando a captura de pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="d19a9-139">**Target virtual machine** - hello virtual machine that is running hello packet capture</span></span>
- <span data-ttu-id="d19a9-140">**Nome de captura de pacote** -esse valor é o nome de saudação da captura de pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="d19a9-140">**Packet capture name** - This value is hello name of hello packet capture.</span></span>

<span data-ttu-id="d19a9-141">**Configuração da captura**</span><span class="sxs-lookup"><span data-stu-id="d19a9-141">**Capture configuration**</span></span>

- <span data-ttu-id="d19a9-142">**Conta de Armazenamento** - Determina se a captura do pacote é salva em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d19a9-142">**Storage Account** - Determines if packet capture is saved in a storage account.</span></span>
- <span data-ttu-id="d19a9-143">**Arquivo** -determina se uma captura de pacote é salvo localmente na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="d19a9-143">**File** - Determines if a packet capture is saved locally on hello virtual machine.</span></span>
- <span data-ttu-id="d19a9-144">**Contas de armazenamento** -Olá selecionado captura de pacote de saudação do armazenamento conta toosave no.</span><span class="sxs-lookup"><span data-stu-id="d19a9-144">**Storage Accounts** - hello selected storage account toosave hello packet capture in.</span></span> <span data-ttu-id="d19a9-145">O local padrão é https://{nome da conta de armazenamento}.blob.core.windows.net/network-watcher-logs/subscriptions/{id assinatura}/resourcegroups/{nome do grupo de recursos}/providers/microsoft.compute/virtualmachines/{nome máquina virtual}/{AA}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span><span class="sxs-lookup"><span data-stu-id="d19a9-145">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span></span> <span data-ttu-id="d19a9-146">(Habilitado somente se o **Armazenamento** estiver selecionado)</span><span class="sxs-lookup"><span data-stu-id="d19a9-146">(Only enabled if **Storage** is selected)</span></span>
- <span data-ttu-id="d19a9-147">**Caminho de arquivo local** -caminho de local de saudação em uma captura de pacote de saudação de toosave de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d19a9-147">**Local file path** - hello local path on a virtual machine toosave hello packet capture.</span></span> <span data-ttu-id="d19a9-148">(Habilitado somente se o **Arquivo** estiver selecionado).</span><span class="sxs-lookup"><span data-stu-id="d19a9-148">(Only enabled if **File** is selected).</span></span> <span data-ttu-id="d19a9-149">Um caminho válido deve ser fornecido</span><span class="sxs-lookup"><span data-stu-id="d19a9-149">A Valid path must be supplied</span></span>
- <span data-ttu-id="d19a9-150">**Máximo de bytes por pacote** -Olá o número de bytes de cada pacote que são capturadas, todos os bytes são capturados se deixado em branco.</span><span class="sxs-lookup"><span data-stu-id="d19a9-150">**Maximum bytes per packet** - hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span>
- <span data-ttu-id="d19a9-151">**Máximo de bytes por sessão** - Total número de bytes que são capturadas, quando o valor de saudação é atingido Olá paradas de captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="d19a9-151">**Maximum bytes per session** - Total number of bytes that are captured, once hello value is reached hello packet capture stops.</span></span>
- <span data-ttu-id="d19a9-152">**Tempo limite (segundos)** -define um limite de tempo para Olá toostop de captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="d19a9-152">**Time limit (seconds)** - Sets a time limit for hello packet capture toostop.</span></span> <span data-ttu-id="d19a9-153">O padrão é 18.000 segundos.</span><span class="sxs-lookup"><span data-stu-id="d19a9-153">Default is 18000 seconds.</span></span>

> [!NOTE]
> <span data-ttu-id="d19a9-154">As contas de armazenamento Premium atualmente não têm suporte para armazenar as capturas de pacotes.</span><span class="sxs-lookup"><span data-stu-id="d19a9-154">Premium storage accounts are currently not supported for storing packet captures.</span></span>

<span data-ttu-id="d19a9-155">**Filtragem (Opcional)**</span><span class="sxs-lookup"><span data-stu-id="d19a9-155">**Filtering (Optional)**</span></span>

- <span data-ttu-id="d19a9-156">**Protocolo** -Olá toofilter de protocolo para captura de pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="d19a9-156">**Protocol** - hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="d19a9-157">os valores disponíveis Olá são TCP, UDP e qualquer.</span><span class="sxs-lookup"><span data-stu-id="d19a9-157">hello available values are TCP, UDP, and Any.</span></span>
- <span data-ttu-id="d19a9-158">**Endereço IP local** -esse valor filtra Olá toopackets de captura de pacote em que o endereço IP local Olá corresponde esse valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="d19a9-158">**Local IP address** - This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>
- <span data-ttu-id="d19a9-159">**Porta local** -esse valor filtra Olá toopackets de captura de pacote em que a porta local Olá corresponde esse valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="d19a9-159">**Local port** - This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>
- <span data-ttu-id="d19a9-160">**Endereço IP remoto** -esse valor filtra Olá toopackets de captura de pacote onde IP remoto Olá corresponde a esse valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="d19a9-160">**Remote IP address** - This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>
- <span data-ttu-id="d19a9-161">**Porta remota** -esse valor filtra Olá toopackets de captura de pacote em que a porta remota Olá corresponde esse valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="d19a9-161">**Remote port** - This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>

> [!NOTE]
> <span data-ttu-id="d19a9-162">Os valores da porta e do endereço IP podem ser um único valor, um intervalo de valores ou um conjunto.</span><span class="sxs-lookup"><span data-stu-id="d19a9-162">Port and IP address values can be a single value, range of values, or a set.</span></span> <span data-ttu-id="d19a9-163">(ou seja, 80-1024 para a porta) Você pode definir quantos filtros quiser.</span><span class="sxs-lookup"><span data-stu-id="d19a9-163">(that is, 80-1024 for port) You can define as many filters as you want.</span></span>

<span data-ttu-id="d19a9-164">Depois de preencher valores hello, clique em **Okey** toocreate captura de pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="d19a9-164">Once hello values are filled out, click **OK** toocreate hello packet capture.</span></span>

![criar uma captura de pacotes][2]

<span data-ttu-id="d19a9-166">Depois de definir o limite de tempo de saudação em captura de pacote de saudação expirou, captura de pacote de saudação será interrompida e pode ser examinada.</span><span class="sxs-lookup"><span data-stu-id="d19a9-166">After hello time limit set on hello packet capture has expired, hello packet capture will stop and can be reviewed.</span></span> <span data-ttu-id="d19a9-167">Manualmente, você pode interromper sessões de captura de pacote hello.</span><span class="sxs-lookup"><span data-stu-id="d19a9-167">You can also manually stop hello packet captures sessions.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="d19a9-168">Excluir uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="d19a9-168">Delete a packet capture</span></span>

<span data-ttu-id="d19a9-169">No pacote de saudação capturar o modo de exibição, clique em Olá **menu de contexto** (...) ou o botão direito do mouse e clique em **excluir** toostop captura de pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="d19a9-169">In hello packet capture view, click hello **context menu** (...) or right click, and click **delete** toostop hello packet capture</span></span>

![excluir uma captura de pacotes][3]

> [!NOTE]
> <span data-ttu-id="d19a9-171">Excluir uma captura de pacote não exclui o arquivo hello na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="d19a9-171">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

<span data-ttu-id="d19a9-172">Você será solicitado tooconfirm deseja toodelete captura de pacote de saudação, clique em **Sim**</span><span class="sxs-lookup"><span data-stu-id="d19a9-172">You are asked tooconfirm you want toodelete hello packet capture, click **Yes**</span></span>

![confirmação][4]

## <a name="stop-a-packet-capture"></a><span data-ttu-id="d19a9-174">Parar uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="d19a9-174">Stop a packet capture</span></span>

<span data-ttu-id="d19a9-175">No pacote de saudação capturar o modo de exibição, clique em Olá **menu de contexto** (...) ou o botão direito do mouse e clique em **parar** toostop captura de pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="d19a9-175">In hello packet capture view, click hello **context menu** (...) or right click, and click **Stop** toostop hello packet capture</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="d19a9-176">Baixar um pacote de capturas</span><span class="sxs-lookup"><span data-stu-id="d19a9-176">Download a packet capture</span></span>

<span data-ttu-id="d19a9-177">Depois de concluído, a sessão de captura de pacote hello captura arquivo é carregado tooblob armazenamento ou tooa local em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d19a9-177">Once your packet capture session has completed, hello capture file is uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="d19a9-178">local de armazenamento de saudação de captura de pacote de saudação é definido no momento da criação da sessão de saudação.</span><span class="sxs-lookup"><span data-stu-id="d19a9-178">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="d19a9-179">Uma ferramenta conveniente tooaccess esses capturar os arquivos salvos tooa conta de armazenamento é o Microsoft Azure Storage Explorer, que pode ser baixado em: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="d19a9-179">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="d19a9-180">Se uma conta de armazenamento for especificada, os arquivos de captura de pacote são salvos tooa conta de armazenamento no hello local a seguir:</span><span class="sxs-lookup"><span data-stu-id="d19a9-180">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="d19a9-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d19a9-181">Next steps</span></span>

<span data-ttu-id="d19a9-182">Saiba como o pacote tooautomate captura com alertas de máquina Virtual por meio da exibição [criar uma captura de pacote de disparo de alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="d19a9-182">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="d19a9-183">Localize se determinado tráfego é permitido dentro ou fora de sua VM visitando [Verificar o fluxo do IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d19a9-183">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













