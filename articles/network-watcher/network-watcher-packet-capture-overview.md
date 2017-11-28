---
title: "Introdução à captura de pacote no Observador de Rede do Azure | Microsoft Docs"
description: "Esta página fornece uma visão geral do recurso de captura de pacote do Observador de Rede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4fdd007c2cfad7b42f26ab2cacfba06d95c8dad3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-variable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="26937-103">Introdução à captura de pacote de varáveis no Observador de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="26937-103">Introduction to variable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="26937-104">A captura de pacote de variáveis do Observador de Rede permite que você crie sessões de captura de pacote para controlar o tráfego em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="26937-104">Network Watcher variable packet capture allows you to create packet capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="26937-105">A captura de pacote ajuda a diagnosticar anomalias de rede reativas e proativas.</span><span class="sxs-lookup"><span data-stu-id="26937-105">Packet capture helps to diagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="26937-106">Outros usos incluem a coleta de estatísticas de rede, obter informações sobre as invasões de rede, para depurar comunicações cliente-servidor e muito mais.</span><span class="sxs-lookup"><span data-stu-id="26937-106">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span>

<span data-ttu-id="26937-107">A captura de pacote é uma extensão de máquina virtual iniciada remotamente por meio do Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="26937-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="26937-108">Esse recurso alivia o transtorno que é executar manualmente uma captura de pacote na máquina virtual desejada, o que economiza um tempo precioso.</span><span class="sxs-lookup"><span data-stu-id="26937-108">This capability eases the burden of running a packet capture manually on the desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="26937-109">A captura de pacote pode ser disparada por meio do portal, do PowerShell, da CLI ou da API REST.</span><span class="sxs-lookup"><span data-stu-id="26937-109">Packet capture can be triggered through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="26937-110">Os alertas de Máquina Virtual são um exemplo de como a captura de pacote pode ser disparada.</span><span class="sxs-lookup"><span data-stu-id="26937-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="26937-111">Os filtros são fornecidos para a sessão de captura a fim de garantir que somente o tráfego que você deseja monitorar seja capturado.</span><span class="sxs-lookup"><span data-stu-id="26937-111">Filters are provided for the capture session to ensure you capture traffic you want to monitor.</span></span> <span data-ttu-id="26937-112">Os filtros têm base em informações de cinco tuplas (protocolo, endereço IP local, endereço IP remoto, porta local e porta remota).</span><span class="sxs-lookup"><span data-stu-id="26937-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="26937-113">Os dados capturados são armazenados no disco local ou um blob de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="26937-113">The captured data is stored in the local disk or a storage blob.</span></span> <span data-ttu-id="26937-114">Há um limite de 10 sessões de captura de pacote por região e assinatura.</span><span class="sxs-lookup"><span data-stu-id="26937-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="26937-115">Esse limite se aplica somente às sessões e não aos arquivos de captura de pacote salvos localmente na VM ou em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="26937-115">This limit applies only to the sessions and does not apply to the saved packet capture files either locally on the VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26937-116">A captura de pacotes requer uma extensão da máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="26937-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="26937-117">Para instalar a extensão em uma VM do Windows, visite [Extensão da máquina virtual do Agente do Observador de Rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para a VM do Linux, visite [Extensão da máquina virtual do Agente do Observador de Rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="26937-117">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="26937-118">Para reduzir as informações capturadas apenas às informações desejadas, as opções a seguir estão disponíveis para uma sessão de captura de pacote:</span><span class="sxs-lookup"><span data-stu-id="26937-118">To reduce the information you capture to only the information you want, the following options are available for a packet capture session:</span></span>

<span data-ttu-id="26937-119">**Configuração da captura**</span><span class="sxs-lookup"><span data-stu-id="26937-119">**Capture configuration**</span></span>

|<span data-ttu-id="26937-120">Propriedade</span><span class="sxs-lookup"><span data-stu-id="26937-120">Property</span></span>|<span data-ttu-id="26937-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="26937-121">Description</span></span>|
|---|---|
|<span data-ttu-id="26937-122">**Máximo de bytes por pacote (bytes)**</span><span class="sxs-lookup"><span data-stu-id="26937-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="26937-123">O número de bytes capturados de cada pacote; todos os bytes serão capturados se deixado em branco.</span><span class="sxs-lookup"><span data-stu-id="26937-123">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="26937-124">O número de bytes capturados de cada pacote; todos os bytes serão capturados se deixado em branco.</span><span class="sxs-lookup"><span data-stu-id="26937-124">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="26937-125">Se você precisar apenas do cabeçalho IPv4 – indique 34 aqui</span><span class="sxs-lookup"><span data-stu-id="26937-125">If you need only the IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="26937-126">**Máximo de bytes por sessão (bytes)**</span><span class="sxs-lookup"><span data-stu-id="26937-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="26937-127">Número total de bytes capturados, quando o valor for atingido, a sessão terminará.</span><span class="sxs-lookup"><span data-stu-id="26937-127">Total number of bytes in that are captured, once the value is reached the session ends.</span></span>|
|<span data-ttu-id="26937-128">**Tempo limite (segundos)**</span><span class="sxs-lookup"><span data-stu-id="26937-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="26937-129">Define uma restrição de tempo na sessão de captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="26937-129">Sets a time constraint on the packet capture session.</span></span> <span data-ttu-id="26937-130">O valor padrão é 18000 segundos, ou cinco horas.</span><span class="sxs-lookup"><span data-stu-id="26937-130">The default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="26937-131">**Filtragem (opcional)**</span><span class="sxs-lookup"><span data-stu-id="26937-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="26937-132">Propriedade</span><span class="sxs-lookup"><span data-stu-id="26937-132">Property</span></span>|<span data-ttu-id="26937-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="26937-133">Description</span></span>|
|---|---|
|<span data-ttu-id="26937-134">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="26937-134">**Protocol**</span></span> | <span data-ttu-id="26937-135">O protocolo de filtragem da captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="26937-135">The protocol to filter for the packet capture.</span></span> <span data-ttu-id="26937-136">Os valores disponíveis são TCP, UDP e Todos.</span><span class="sxs-lookup"><span data-stu-id="26937-136">The available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="26937-137">**Endereço IP local**</span><span class="sxs-lookup"><span data-stu-id="26937-137">**Local IP address**</span></span> | <span data-ttu-id="26937-138">Esse valor filtra a captura de pacotes para os pacotes cujo endereço IP local corresponde ao valor do filtro.</span><span class="sxs-lookup"><span data-stu-id="26937-138">This value filters the packet capture to packets where the local IP address matches this filter value.</span></span>|
|<span data-ttu-id="26937-139">**Porta local**</span><span class="sxs-lookup"><span data-stu-id="26937-139">**Local port**</span></span> | <span data-ttu-id="26937-140">Esse valor filtra a captura de pacotes para os pacotes cuja porta local corresponde ao valor do filtro.</span><span class="sxs-lookup"><span data-stu-id="26937-140">This value filters the packet capture to packets where the local port matches this filter value.</span></span>|
|<span data-ttu-id="26937-141">**Endereço IP remoto**</span><span class="sxs-lookup"><span data-stu-id="26937-141">**Remote IP address**</span></span> | <span data-ttu-id="26937-142">Esse valor filtra a captura de pacotes para os pacotes cujo IP remoto corresponde ao valor do filtro.</span><span class="sxs-lookup"><span data-stu-id="26937-142">This value filters the packet capture to packets where the remote IP matches this filter value.</span></span>|
|<span data-ttu-id="26937-143">**Porta remota**</span><span class="sxs-lookup"><span data-stu-id="26937-143">**Remote port**</span></span> | <span data-ttu-id="26937-144">Esse valor filtra a captura de pacotes para os pacotes cuja porta remota corresponde ao valor do filtro.</span><span class="sxs-lookup"><span data-stu-id="26937-144">This value filters the packet capture to packets where the remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="26937-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="26937-145">Next steps</span></span>

<span data-ttu-id="26937-146">Saiba como você pode gerenciar as capturas de pacote no portal visitando [Gerenciar captura de pacote no Portal do Azure](network-watcher-packet-capture-manage-portal.md) ou com o PowerShell visitando [Gerenciar captura de pacote com o PowerShell](network-watcher-packet-capture-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="26937-146">Learn how you can manage packet captures through the portal by visiting [Manage packet capture in the Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="26937-147">Saiba como criar capturas de pacote proativas com base em alertas de máquina virtual visitando [Criar uma captura de pacote disparada por alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="26937-147">Learn how to create proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













