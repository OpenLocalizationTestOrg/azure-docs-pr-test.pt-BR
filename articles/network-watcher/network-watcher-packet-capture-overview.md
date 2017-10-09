---
title: captura de tooPacket aaaIntroduction no Inspetor de rede do Azure | Microsoft Docs
description: "Esta página fornece uma visão geral do recurso de captura de pacote hello observador de rede"
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
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="3e451-103">Captura de pacote toovariable introdução em observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="3e451-103">Introduction toovariable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="3e451-104">Captura de pacote de variável do Inspetor de rede permite que você toocreate pacote captura sessões tootrack tooand de tráfego de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3e451-104">Network Watcher variable packet capture allows you toocreate packet capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="3e451-105">Captura de pacote ajuda toodiagnose anomalias na rede ambos os reativa e proactivity.</span><span class="sxs-lookup"><span data-stu-id="3e451-105">Packet capture helps toodiagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="3e451-106">Outros usos incluem a coleta de estatísticas de rede, obtenção de informações de invasões de rede, toodebug cliente-servidor comunicações e muito mais.</span><span class="sxs-lookup"><span data-stu-id="3e451-106">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span>

<span data-ttu-id="3e451-107">A captura de pacote é uma extensão de máquina virtual iniciada remotamente por meio do Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="3e451-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="3e451-108">Esse recurso facilita a carga Olá da execução de uma captura de pacote manualmente na máquina virtual Olá desejado, o que economiza tempo.</span><span class="sxs-lookup"><span data-stu-id="3e451-108">This capability eases hello burden of running a packet capture manually on hello desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="3e451-109">Captura de pacote pode ser acionada por meio do portal de saudação, o PowerShell, CLI ou API REST.</span><span class="sxs-lookup"><span data-stu-id="3e451-109">Packet capture can be triggered through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="3e451-110">Os alertas de Máquina Virtual são um exemplo de como a captura de pacote pode ser disparada.</span><span class="sxs-lookup"><span data-stu-id="3e451-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="3e451-111">Os filtros são fornecidos para tooensure de sessão de captura Olá você capturar o tráfego que você deseja toomonitor.</span><span class="sxs-lookup"><span data-stu-id="3e451-111">Filters are provided for hello capture session tooensure you capture traffic you want toomonitor.</span></span> <span data-ttu-id="3e451-112">Os filtros têm base em informações de cinco tuplas (protocolo, endereço IP local, endereço IP remoto, porta local e porta remota).</span><span class="sxs-lookup"><span data-stu-id="3e451-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="3e451-113">Olá capturado dados são armazenados no disco local hello ou um blob de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3e451-113">hello captured data is stored in hello local disk or a storage blob.</span></span> <span data-ttu-id="3e451-114">Há um limite de 10 sessões de captura de pacote por região e assinatura.</span><span class="sxs-lookup"><span data-stu-id="3e451-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="3e451-115">Esse limite se aplica somente a sessões de toohello e não se aplica a toohello salva arquivos de captura de pacote localmente no hello VM ou em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3e451-115">This limit applies only toohello sessions and does not apply toohello saved packet capture files either locally on hello VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e451-116">A captura de pacotes requer uma extensão da máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="3e451-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="3e451-117">Para instalar a extensão de saudação em uma VM do Windows, visite [extensão de máquina virtual do agente do Inspetor de rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para a visita de VM do Linux [extensão de máquina virtual do agente do Inspetor de rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="3e451-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="3e451-118">informações de saudação tooreduce capturar informações de saudação tooonly desejado, Olá as opções a seguir está disponível para uma sessão de captura de pacote:</span><span class="sxs-lookup"><span data-stu-id="3e451-118">tooreduce hello information you capture tooonly hello information you want, hello following options are available for a packet capture session:</span></span>

<span data-ttu-id="3e451-119">**Configuração da captura**</span><span class="sxs-lookup"><span data-stu-id="3e451-119">**Capture configuration**</span></span>

|<span data-ttu-id="3e451-120">Propriedade</span><span class="sxs-lookup"><span data-stu-id="3e451-120">Property</span></span>|<span data-ttu-id="3e451-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="3e451-121">Description</span></span>|
|---|---|
|<span data-ttu-id="3e451-122">**Máximo de bytes por pacote (bytes)**</span><span class="sxs-lookup"><span data-stu-id="3e451-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="3e451-123">Olá o número de bytes de cada pacote que são capturadas, todos os bytes são capturados se deixado em branco.</span><span class="sxs-lookup"><span data-stu-id="3e451-123">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="3e451-124">Olá o número de bytes de cada pacote que são capturadas, todos os bytes são capturados se deixado em branco.</span><span class="sxs-lookup"><span data-stu-id="3e451-124">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="3e451-125">Se você precisar somente cabeçalho de IPv4 hello – indicar 34 aqui</span><span class="sxs-lookup"><span data-stu-id="3e451-125">If you need only hello IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="3e451-126">**Máximo de bytes por sessão (bytes)**</span><span class="sxs-lookup"><span data-stu-id="3e451-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="3e451-127">Número total de bytes em que é capturado, quando o valor de saudação é atingido Olá término da sessão.</span><span class="sxs-lookup"><span data-stu-id="3e451-127">Total number of bytes in that are captured, once hello value is reached hello session ends.</span></span>|
|<span data-ttu-id="3e451-128">**Tempo limite (segundos)**</span><span class="sxs-lookup"><span data-stu-id="3e451-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="3e451-129">Define uma restrição de tempo no pacote de saudação capturar a sessão.</span><span class="sxs-lookup"><span data-stu-id="3e451-129">Sets a time constraint on hello packet capture session.</span></span> <span data-ttu-id="3e451-130">valor padrão de saudação é 18000 segundos ou cinco horas.</span><span class="sxs-lookup"><span data-stu-id="3e451-130">hello default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="3e451-131">**Filtragem (opcional)**</span><span class="sxs-lookup"><span data-stu-id="3e451-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="3e451-132">Propriedade</span><span class="sxs-lookup"><span data-stu-id="3e451-132">Property</span></span>|<span data-ttu-id="3e451-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="3e451-133">Description</span></span>|
|---|---|
|<span data-ttu-id="3e451-134">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="3e451-134">**Protocol**</span></span> | <span data-ttu-id="3e451-135">Olá toofilter de protocolo para o pacote de saudação de captura.</span><span class="sxs-lookup"><span data-stu-id="3e451-135">hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="3e451-136">os valores disponíveis Olá são TCP, UDP e todos.</span><span class="sxs-lookup"><span data-stu-id="3e451-136">hello available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="3e451-137">**Endereço IP local**</span><span class="sxs-lookup"><span data-stu-id="3e451-137">**Local IP address**</span></span> | <span data-ttu-id="3e451-138">Esse valor filtra Olá toopackets de captura de pacote em que o endereço IP local Olá corresponde esse valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="3e451-138">This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>|
|<span data-ttu-id="3e451-139">**Porta local**</span><span class="sxs-lookup"><span data-stu-id="3e451-139">**Local port**</span></span> | <span data-ttu-id="3e451-140">Este pacote de saudação do valor filtros capturar toopackets onde porta local Olá corresponde a esse valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="3e451-140">This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>|
|<span data-ttu-id="3e451-141">**Endereço IP remoto**</span><span class="sxs-lookup"><span data-stu-id="3e451-141">**Remote IP address**</span></span> | <span data-ttu-id="3e451-142">Este pacote de saudação do valor filtros capturar toopackets onde IP remoto Olá corresponde a esse valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="3e451-142">This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>|
|<span data-ttu-id="3e451-143">**Porta remota**</span><span class="sxs-lookup"><span data-stu-id="3e451-143">**Remote port**</span></span> | <span data-ttu-id="3e451-144">Este pacote de saudação do valor filtros capturar toopackets onde porta remota Olá corresponde a esse valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="3e451-144">This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="3e451-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3e451-145">Next steps</span></span>

<span data-ttu-id="3e451-146">Saiba como você pode gerenciar a captura de pacote por meio do portal Olá visitando [gerenciar captura de pacote no portal do Azure de saudação](network-watcher-packet-capture-manage-portal.md) ou com o PowerShell visitando [gerenciar de captura de pacote com o PowerShell](network-watcher-packet-capture-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3e451-146">Learn how you can manage packet captures through hello portal by visiting [Manage packet capture in hello Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="3e451-147">Saiba como o pacote pró-ativo toocreate captura com base em alertas de máquina virtual visitando [criar uma captura de pacote de disparo de alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="3e451-147">Learn how toocreate proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













