---
title: "padrões de tráfego de rede aaaVisualize com ferramentas de software livre e o observador de rede do Azure | Microsoft Docs"
description: "Esta página descreve como de captura de pacote de rede Inspetor toouse com tooand de padrões de tráfego Capanalysis toovisualize de suas VMs."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a><span data-ttu-id="4dbe2-103">Visualizar tooand de padrões de tráfego de rede de suas VMs usando ferramentas de software livre</span><span class="sxs-lookup"><span data-stu-id="4dbe2-103">Visualize network traffic patterns tooand from your VMs using open source tools</span></span>

<span data-ttu-id="4dbe2-104">Captura de pacote contém dados de rede que permitem a análise forense tooperform e inspeções profundas de pacote.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-104">Packet captures contain network data that allow you tooperform network forensics and deep packet inspection.</span></span> <span data-ttu-id="4dbe2-105">Há abre muitas ferramentas de origem, você pode usar tooanalyze pacote capturas toogain informações sobre a sua rede.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-105">There are many opens source tools you can use tooanalyze packet captures toogain insights about your network.</span></span> <span data-ttu-id="4dbe2-106">Uma dessas ferramentas é a CapAnalysis, uma ferramenta de visualização de captura de pacote de software livre.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="4dbe2-107">Visualização de dados de captura de pacote é uma maneira importante que tooquickly derivar ideias sobre padrões e as anomalias dentro de sua rede.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-107">Visualizing packet capture data is a valuable way tooquickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="4dbe2-108">As visualizações também fornecem um meio de compartilhar essas informações de maneira facilmente consumível.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="4dbe2-109">Observador de rede do Azure fornece que Olá capacidade toocapture captura dados valiosos, permitindo que o pacote de tooperform em sua rede.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-109">Azure’s Network Watcher provides you hello ability toocapture this valuable data by allowing you tooperform packet captures on your network.</span></span> <span data-ttu-id="4dbe2-110">Neste artigo, fornecemos um passo a passo de como toovisualize e obtenha informações do pacote de captura usando CapAnalysis com o observador de rede.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-110">In this article, we provide a walkthrough of how toovisualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="4dbe2-111">Cenário</span><span class="sxs-lookup"><span data-stu-id="4dbe2-111">Scenario</span></span>

<span data-ttu-id="4dbe2-112">Você tem um aplicativo da web simples implantado em uma máquina virtual no Azure deseja toouse código-fonte aberto ferramentas toovisualize seu tooquickly de tráfego de rede identificar padrões de fluxo e todas as anomalias possíveis.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-112">You have a simple web application deployed on a VM in Azure want toouse open source tools toovisualize its network traffic tooquickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="4dbe2-113">Com o observador de rede, você poderá obter uma captura de pacote de seu ambiente de rede e armazená-lo diretamente em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="4dbe2-114">CapAnalysis, captura de pacote do hello diretamente saudação do blob de armazenamento de ingestão e visualizar o seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-114">CapAnalysis can then ingest hello packet capture directly from hello storage blob and visualize its contents.</span></span>

![cenário][1]

## <a name="steps"></a><span data-ttu-id="4dbe2-116">Etapas</span><span class="sxs-lookup"><span data-stu-id="4dbe2-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="4dbe2-117">Instale o CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="4dbe2-117">Install CapAnalysis</span></span>

<span data-ttu-id="4dbe2-118">tooinstall CapAnalysis em uma máquina virtual, você pode consultar instruções oficial toohello https://www.capanalysis.net/ca/how-to-install-capanalysis aqui.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-118">tooinstall CapAnalysis on a virtual machine, you can refer toohello official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="4dbe2-119">Acessar CapAnalysis remotamente, precisamos tooopen porta 9877 na sua VM, adicionando uma nova regra de segurança de entrada.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-119">In order access CapAnalysis remotely, we need tooopen port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="4dbe2-120">Para obter mais informações sobre como criar regras em grupos de segurança de rede, consulte muito[criar regras em um NSG existente](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span><span class="sxs-lookup"><span data-stu-id="4dbe2-120">For more about creating rules in Network Security Groups, refer too[Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="4dbe2-121">Depois que a regra de saudação foi adicionada com êxito, você deve ser capaz de tooaccess CapAnalysis de`http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="4dbe2-121">Once hello rule has been successfully added, you should be able tooaccess CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a><span data-ttu-id="4dbe2-122">Use o observador de rede do Azure toostart sessão de captura de um pacote</span><span class="sxs-lookup"><span data-stu-id="4dbe2-122">Use Azure Network Watcher toostart a packet capture session</span></span>

<span data-ttu-id="4dbe2-123">Observador de rede permite tráfego de tootrack toocapture pacotes dentro e fora de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-123">Network Watcher allows you toocapture packets tootrack traffic in and out of a virtual machine.</span></span> <span data-ttu-id="4dbe2-124">Você pode consultar as instruções de toohello em [captura de pacote de gerenciamento com o observador de rede](network-watcher-packet-capture-manage-portal.md) toostart uma sessão de captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-124">You can refer toohello instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) toostart a packet capture session.</span></span> <span data-ttu-id="4dbe2-125">Esta captura de pacote pode ser armazenada em um toobe de blob de armazenamento acessado por CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-125">This packet capture can be stored in a storage blob toobe accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-toocapanalysis"></a><span data-ttu-id="4dbe2-126">Carregar um tooCapAnalysis de captura de pacote</span><span class="sxs-lookup"><span data-stu-id="4dbe2-126">Upload a packet capture tooCapAnalysis</span></span>
<span data-ttu-id="4dbe2-127">Diretamente, você pode carregar uma captura de pacote utilizada pelo observador de rede usando o guia de "Da URL de importação" hello e fornecendo um blob de armazenamento do link toohello onde a captura de pacote de saudação é armazenada.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-127">You can directly upload a packet capture taken by network watcher using hello “Import from URL” tab and providing a link toohello storage blob where hello packet capture is stored.</span></span>

<span data-ttu-id="4dbe2-128">Ao fornecer um link tooCapAnalysis, verifique se tooappend uma URL de blob de armazenamento de toohello token SAS.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-128">When providing a link tooCapAnalysis, make sure tooappend a SAS token toohello storage blob URL.</span></span>  <span data-ttu-id="4dbe2-129">toodo isso, navegue tooShared assinatura de acesso da conta de armazenamento hello, designar Olá permissões concedida e pressione Olá gerar SAS botão toocreate um token.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-129">toodo this, navigate tooShared access signature from hello storage account, designate hello allowed permissions, and press hello Generate SAS button toocreate a token.</span></span> <span data-ttu-id="4dbe2-130">Em seguida, você pode acrescentar essa URL de blob de armazenamento SAS token toohello pacote captura.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-130">You can then append this SAS token toohello packet capture storage blob URL.</span></span>

<span data-ttu-id="4dbe2-131">Olá URL resultante será parecida com isto: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="4dbe2-131">hello resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="4dbe2-132">Análise de capturas de pacote</span><span class="sxs-lookup"><span data-stu-id="4dbe2-132">Analyzing packet captures</span></span>

<span data-ttu-id="4dbe2-133">CapAnalysis oferece várias toovisualize de opções sua captura de pacote, cada fornecendo análise de uma perspectiva diferente.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-133">CapAnalysis offers various options toovisualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="4dbe2-134">Com esses resumos visuais, você pode entender as tendências do tráfego de rede e identificar rapidamente qualquer atividade incomum.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="4dbe2-135">Alguns desses recursos são mostrados na Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="4dbe2-135">A few of these features are shown in hello following list:</span></span>

1. <span data-ttu-id="4dbe2-136">Tabelas de fluxo</span><span class="sxs-lookup"><span data-stu-id="4dbe2-136">Flow Tables</span></span>

    <span data-ttu-id="4dbe2-137">Fornece essa tabela Olá lista de fluxos de dados do pacote de saudação, Olá associado Olá fluxos de carimbo de hora e Olá vários protocolos associados fluxo hello, assim como o IP de origem e de destino.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-137">This table gives you hello list of flows in hello packet data, hello time stamp associated with hello flows and hello various protocols associated with hello flow, as well as source and destination IP.</span></span>

    ![página de fluxo do capanalysis][5]

1. <span data-ttu-id="4dbe2-139">Visão geral do protocolo</span><span class="sxs-lookup"><span data-stu-id="4dbe2-139">Protocol Overview</span></span>

    <span data-ttu-id="4dbe2-140">Este painel permite que você tooquickly ver distribuição de saudação do tráfego de rede ao longo do hello diversos protocolos e regiões geográficas.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-140">This pane allows you tooquickly see hello distribution of network traffic over hello various protocols and geographies.</span></span>

    ![visão geral do protocolo do capanalysis][6]

1. <span data-ttu-id="4dbe2-142">Estatísticas</span><span class="sxs-lookup"><span data-stu-id="4dbe2-142">Statistics</span></span>

    <span data-ttu-id="4dbe2-143">Este painel permite que você tooview estatísticas de tráfego de rede – bytes enviados e recebidos da origem e destino IPs, fluxos para cada fonte hello e destino IPs, o protocolo usado para vários fluxos e a duração de saudação de fluxos.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-143">This pane allows you tooview network traffic statistics – bytes sent and received from source and destination IPs, flows for each of hello source and destination IPs, protocol used for various flows, and hello duration of flows.</span></span>

    ![estatísticas do capanalysis][7]

1. <span data-ttu-id="4dbe2-145">Geomap</span><span class="sxs-lookup"><span data-stu-id="4dbe2-145">Geomap</span></span>

    <span data-ttu-id="4dbe2-146">Este painel fornece uma exibição de mapa de seu tráfego de rede com cores dimensionamento toohello volume de tráfego de cada país.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-146">This pane provides you with a map view of your network traffic, with colors scaling toohello volume of traffic from each country.</span></span> <span data-ttu-id="4dbe2-147">Você pode selecionar países realçados tooview fluxo adicional estatísticas, como a proporção de saudação de dados enviados e recebidos de IPs esse país.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-147">You can select highlighted countries tooview additional flow statistics such as hello proportion of data sent and received from IPs in that country.</span></span>

    ![geomap][8]

1. <span data-ttu-id="4dbe2-149">Filtros</span><span class="sxs-lookup"><span data-stu-id="4dbe2-149">Filters</span></span>

    <span data-ttu-id="4dbe2-150">O CapAnalysis fornece um conjunto de filtros para análise rápida dos pacotes específicos.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="4dbe2-151">Por exemplo, você pode escolher dados de saudação toofilter por informações específicas do protocolo toogain nesse subconjunto de tráfego.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-151">For example, you can choose toofilter hello data by protocol toogain specific insights on that subset of traffic.</span></span>

    ![filtros][11]

    <span data-ttu-id="4dbe2-153">Visite [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn mais sobre os recursos dos todos os CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="4dbe2-154">Conclusão</span><span class="sxs-lookup"><span data-stu-id="4dbe2-154">Conclusion</span></span>

<span data-ttu-id="4dbe2-155">O recurso de captura de pacote do observador de rede permite que você toocapture Olá dados tooperform necessário análise forense e entender melhor o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-155">Network Watcher’s packet capture feature allows you toocapture hello data necessary tooperform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="4dbe2-156">Nesse cenário, mostramos como as capturas de pacote do observador de rede podem ser facilmente integradas a ferramentas de visualização de software livre.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="4dbe2-157">Usando ferramentas de software livre, como captura CapAnalysis toovisualize pacotes, você pode executar a inspeção profunda de pacotes e identificar rapidamente as tendências em seu tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="4dbe2-157">By using open source tools such as CapAnalysis toovisualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dbe2-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4dbe2-158">Next steps</span></span>

<span data-ttu-id="4dbe2-159">toolearn mais informações sobre logs de fluxo do NSG, visite [NSG fluxo logs](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="4dbe2-159">toolearn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="4dbe2-160">Saiba como toovisualize seu fluxo NSG registra com o Power BI visitando [visualizar NSG fluxos de logs com o Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="4dbe2-160">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
