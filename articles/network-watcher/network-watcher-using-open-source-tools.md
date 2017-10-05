---
title: "Como visualizar os padrões de tráfego de rede com ferramentas de software livre e observador de rede do Azure | Microsoft Docs"
description: "Esta página descreve como usar a captura de pacote do observador de rede com CapAnalysis para visualizar os padrões de tráfego para e de suas VMs."
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
ms.openlocfilehash: e27bb694d0cbcf1ff7c9d8ca4682a79c8b5c5cb1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-network-traffic-patterns-to-and-from-your-vms-using-open-source-tools"></a><span data-ttu-id="c3e2b-103">Como visualizar padrões de tráfego de rede de e para suas VMs usando ferramentas de software livre</span><span class="sxs-lookup"><span data-stu-id="c3e2b-103">Visualize network traffic patterns to and from your VMs using open source tools</span></span>

<span data-ttu-id="c3e2b-104">As capturas de pacote contêm dados de rede que permitem que você execute análise forense e inspeções profundas.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-104">Packet captures contain network data that allow you to perform network forensics and deep packet inspection.</span></span> <span data-ttu-id="c3e2b-105">Você pode usar muitas das ferramentas de softwares livres disponíveis para analisar as capturas de pacote para aprofundar-se sobre a sua rede.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-105">There are many opens source tools you can use to analyze packet captures to gain insights about your network.</span></span> <span data-ttu-id="c3e2b-106">Uma dessas ferramentas é a CapAnalysis, uma ferramenta de visualização de captura de pacote de software livre.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="c3e2b-107">Visualizar dados de captura de pacote é uma maneira valiosa para aprofundar-se rapidamente sobre os padrões e anomalias na rede.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-107">Visualizing packet capture data is a valuable way to quickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="c3e2b-108">As visualizações também fornecem um meio de compartilhar essas informações de maneira facilmente consumível.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="c3e2b-109">O observador de rede do Azure fornece a capacidade de capturar esses dados valiosos, permitindo que você execute as capturas de pacote na sua rede.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-109">Azure’s Network Watcher provides you the ability to capture this valuable data by allowing you to perform packet captures on your network.</span></span> <span data-ttu-id="c3e2b-110">Neste artigo, fornecemos um passo a passo sobre como visualizar e aprofundar-se sobre as capturas de pacote usando CapAnalysis com o observador de rede.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-110">In this article, we provide a walkthrough of how to visualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="c3e2b-111">Cenário</span><span class="sxs-lookup"><span data-stu-id="c3e2b-111">Scenario</span></span>

<span data-ttu-id="c3e2b-112">Você tem um aplicativo simples da web implantado em uma VM no Azure para usar ferramentas de software livre para visualizar seu tráfego de rede para identificar rapidamente os padrões de fluxo e anomalias possíveis.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-112">You have a simple web application deployed on a VM in Azure want to use open source tools to visualize its network traffic to quickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="c3e2b-113">Com o observador de rede, você poderá obter uma captura de pacote de seu ambiente de rede e armazená-lo diretamente em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="c3e2b-114">O CapAnalysis pode incluir a captura de pacote diretamente do armazenamento de blobs e visualizar seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-114">CapAnalysis can then ingest the packet capture directly from the storage blob and visualize its contents.</span></span>

![cenário][1]

## <a name="steps"></a><span data-ttu-id="c3e2b-116">Etapas</span><span class="sxs-lookup"><span data-stu-id="c3e2b-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="c3e2b-117">Instale o CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="c3e2b-117">Install CapAnalysis</span></span>

<span data-ttu-id="c3e2b-118">Para instalar o CapAnalysis em uma máquina virtual, confira as instruções oficiais: https://www.capanalysis.net/ca/how-to-install-capanalysis.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-118">To install CapAnalysis on a virtual machine, you can refer to the official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="c3e2b-119">Para acessar o CapAnalysis remotamente, é preciso abrir a porta 9877 na sua VM, adicionando uma nova regra de segurança de entrada.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-119">In order access CapAnalysis remotely, we need to open port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="c3e2b-120">Para obter mais informações sobre como criar regras em grupos de segurança de rede, veja [Como criar regras em uma NSG existente](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span><span class="sxs-lookup"><span data-stu-id="c3e2b-120">For more about creating rules in Network Security Groups, refer to [Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="c3e2b-121">Depois de adicionar a regra com êxito, você pode acessar o CapAnalysis em `http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="c3e2b-121">Once the rule has been successfully added, you should be able to access CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-to-start-a-packet-capture-session"></a><span data-ttu-id="c3e2b-122">Como usar o observador de rede do Azure para iniciar uma sessão de captura de pacote</span><span class="sxs-lookup"><span data-stu-id="c3e2b-122">Use Azure Network Watcher to start a packet capture session</span></span>

<span data-ttu-id="c3e2b-123">O observador de rede permite que você capture pacotes para acompanhar o tráfego de entrada e saída de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-123">Network Watcher allows you to capture packets to track traffic in and out of a virtual machine.</span></span> <span data-ttu-id="c3e2b-124">Confira as instruções em: [Capturas de pacote de gerenciamento com o observador de rede](network-watcher-packet-capture-manage-portal.md) para iniciar uma sessão de captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-124">You can refer to the instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) to start a packet capture session.</span></span> <span data-ttu-id="c3e2b-125">Esta captura de pacote pode ser armazenada em um armazenamento de blobs para ser acessada pelo CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-125">This packet capture can be stored in a storage blob to be accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-to-capanalysis"></a><span data-ttu-id="c3e2b-126">Como carregar uma captura de pacote no CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="c3e2b-126">Upload a packet capture to CapAnalysis</span></span>
<span data-ttu-id="c3e2b-127">Você pode carregar diretamente uma captura de pacote realizada pelo observador de rede usando a guia "Importação de URL" e fornecer um link para o armazenamento de blobs onde a captura de pacote é armazenada.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-127">You can directly upload a packet capture taken by network watcher using the “Import from URL” tab and providing a link to the storage blob where the packet capture is stored.</span></span>

<span data-ttu-id="c3e2b-128">Ao fornecer um link para o CapAnalysis, não deixe de acrescentar um token SAS à URL do armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-128">When providing a link to CapAnalysis, make sure to append a SAS token to the storage blob URL.</span></span>  <span data-ttu-id="c3e2b-129">Para fazer isso, navegue até a assinatura de acesso compartilhado da conta de armazenamento, designe as permissões permitidas e pressione o botão Gerar SAS para criar um token.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-129">To do this, navigate to Shared access signature from the storage account, designate the allowed permissions, and press the Generate SAS button to create a token.</span></span> <span data-ttu-id="c3e2b-130">Em seguida, você pode acrescentar esse token SAS para a URL do armazenamento de blobs de captura de pacote.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-130">You can then append this SAS token to the packet capture storage blob URL.</span></span>

<span data-ttu-id="c3e2b-131">A URL resultante será algo parecido com isto: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="c3e2b-131">The resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="c3e2b-132">Análise de capturas de pacote</span><span class="sxs-lookup"><span data-stu-id="c3e2b-132">Analyzing packet captures</span></span>

<span data-ttu-id="c3e2b-133">O CapAnalysis oferece várias opções para visualizar sua captura de pacote, cada uma fornece análise de uma perspectiva diferente.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-133">CapAnalysis offers various options to visualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="c3e2b-134">Com esses resumos visuais, você pode entender as tendências do tráfego de rede e identificar rapidamente qualquer atividade incomum.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="c3e2b-135">Alguns desses recursos são mostrados na lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="c3e2b-135">A few of these features are shown in the following list:</span></span>

1. <span data-ttu-id="c3e2b-136">Tabelas de fluxo</span><span class="sxs-lookup"><span data-stu-id="c3e2b-136">Flow Tables</span></span>

    <span data-ttu-id="c3e2b-137">Esta tabela fornece a lista de fluxos de dados de pacote, o carimbo de hora associado com os fluxos, vários protocolos associados ao fluxo e o IP de origem e destino.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-137">This table gives you the list of flows in the packet data, the time stamp associated with the flows and the various protocols associated with the flow, as well as source and destination IP.</span></span>

    ![página de fluxo do capanalysis][5]

1. <span data-ttu-id="c3e2b-139">Visão geral do protocolo</span><span class="sxs-lookup"><span data-stu-id="c3e2b-139">Protocol Overview</span></span>

    <span data-ttu-id="c3e2b-140">Este painel permite que você veja rapidamente a distribuição do tráfego de rede em diferentes protocolos e regiões geográficas.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-140">This pane allows you to quickly see the distribution of network traffic over the various protocols and geographies.</span></span>

    ![visão geral do protocolo do capanalysis][6]

1. <span data-ttu-id="c3e2b-142">Estatísticas</span><span class="sxs-lookup"><span data-stu-id="c3e2b-142">Statistics</span></span>

    <span data-ttu-id="c3e2b-143">Este painel permite exibir estatísticas de tráfego de rede — bytes enviados e IPs de origem e destino, fluxos de cada IP de origem e destino, o protocolo usado para vários fluxos e a duração de fluxos.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-143">This pane allows you to view network traffic statistics – bytes sent and received from source and destination IPs, flows for each of the source and destination IPs, protocol used for various flows, and the duration of flows.</span></span>

    ![estatísticas do capanalysis][7]

1. <span data-ttu-id="c3e2b-145">Geomap</span><span class="sxs-lookup"><span data-stu-id="c3e2b-145">Geomap</span></span>

    <span data-ttu-id="c3e2b-146">Este painel fornece uma exibição de mapa de seu tráfego de rede, com cores de dimensionamento para o volume de tráfego de cada país.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-146">This pane provides you with a map view of your network traffic, with colors scaling to the volume of traffic from each country.</span></span> <span data-ttu-id="c3e2b-147">Você pode selecionar os países destacados para exibir estatísticas de fluxo adicionais, assim como a proporção dos dados enviados e recebidos pelos IPs nesse país.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-147">You can select highlighted countries to view additional flow statistics such as the proportion of data sent and received from IPs in that country.</span></span>

    ![geomap][8]

1. <span data-ttu-id="c3e2b-149">Filtros</span><span class="sxs-lookup"><span data-stu-id="c3e2b-149">Filters</span></span>

    <span data-ttu-id="c3e2b-150">O CapAnalysis fornece um conjunto de filtros para análise rápida dos pacotes específicos.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="c3e2b-151">Por exemplo, você pode optar por filtrar os dados por protocolo para obter informações específicas sobre esse subconjunto de tráfego.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-151">For example, you can choose to filter the data by protocol to gain specific insights on that subset of traffic.</span></span>

    ![filtros][11]

    <span data-ttu-id="c3e2b-153">Acesse [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) para saber mais sobre os recursos do CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) to learn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="c3e2b-154">Conclusão</span><span class="sxs-lookup"><span data-stu-id="c3e2b-154">Conclusion</span></span>

<span data-ttu-id="c3e2b-155">O recurso de captura de pacote do observador de rede e permite que você capture os dados necessários para executar uma análise forense e compreender melhor o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-155">Network Watcher’s packet capture feature allows you to capture the data necessary to perform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="c3e2b-156">Nesse cenário, mostramos como as capturas de pacote do observador de rede podem ser facilmente integradas a ferramentas de visualização de software livre.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="c3e2b-157">Usando ferramentas de software livre, como o CapAnalysis, para visualizar a captura de pacotes, você pode realizar inspeções de pacotes minuciosas e identificar rapidamente as tendências do seu tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="c3e2b-157">By using open source tools such as CapAnalysis to visualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3e2b-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c3e2b-158">Next steps</span></span>

<span data-ttu-id="c3e2b-159">Para saber mais sobre logs de fluxo NSG, acesse [Logs de fluxo NSG](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c3e2b-159">To learn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="c3e2b-160">Para saber como visualizar os logs de fluxo NSG com o Power BI, veja [Como visualizar logs de fluxos NSG com Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="c3e2b-160">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
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
