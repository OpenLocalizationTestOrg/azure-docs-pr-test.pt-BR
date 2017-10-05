---
title: "Visualização de logs de fluxo do grupo de segurança de rede do Azure com o Power BI | Microsoft Docs"
description: "Esta página descreve como visualizar logs de fluxo NSG com o Power BI."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d8c61ca2a3bd5affe02e8f9500655db6699a245f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="d8e1d-103">Visualização de logs de fluxo do grupo de segurança de rede com o Power BI</span><span class="sxs-lookup"><span data-stu-id="d8e1d-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="d8e1d-104">Os logs de fluxo do grupo de segurança de rede permitem que você exiba informações sobre o tráfego IP de entrada e saída em grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-104">Network Security Group flow logs allow you to view information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="d8e1d-105">Esses logs de fluxo exibem os fluxos de entrada e saída baseados por regras. A NIC de fluxo se aplica às informações de 5 tuplas sobre o fluxo (IP de origem/destino, porta de origem/destino e protocolo) e se o tráfego foi permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-105">These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="d8e1d-106">Não é fácil aprofundar-se sobre dados de registro em log de fluxo pesquisando manualmente os arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-106">It can be difficult to gain insights into flow logging data by manually searching the log files.</span></span> <span data-ttu-id="d8e1d-107">Neste artigo, fornecemos uma solução para visualizar os logs de fluxo mais recentes e as informações sobre o tráfego na sua rede.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-107">In this article, we provide a solution to visualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="d8e1d-108">Cenário</span><span class="sxs-lookup"><span data-stu-id="d8e1d-108">Scenario</span></span>

<span data-ttu-id="d8e1d-109">No cenário a seguir, conectamos a área de trabalho do Power BI com a conta de armazenamento que havíamos configurado como o coletor para nossos dados de registro em log de fluxo de NSG.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-109">In the following scenario, we connect Power BI desktop to the storage account we have configured as the sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="d8e1d-110">Depois de nos conectarmos com nossa conta de armazenamento, o Power BI baixa e analisa os logs para fornecer uma representação visual do tráfego registrado por grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-110">After we connect to our storage account, Power BI downloads and parses the logs to provide a visual representation of the traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="d8e1d-111">Ao usar os visuais fornecidos no modelo, você pode examinar:</span><span class="sxs-lookup"><span data-stu-id="d8e1d-111">Using the visuals supplied in the template you can examine:</span></span>

* <span data-ttu-id="d8e1d-112">Os principais locutores</span><span class="sxs-lookup"><span data-stu-id="d8e1d-112">Top Talkers</span></span>
* <span data-ttu-id="d8e1d-113">Dados de fluxo de série temporal por decisão de regra e direção</span><span class="sxs-lookup"><span data-stu-id="d8e1d-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="d8e1d-114">Fluxos de endereço MAC da interface de rede</span><span class="sxs-lookup"><span data-stu-id="d8e1d-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="d8e1d-115">Fluxos de NSG e regra</span><span class="sxs-lookup"><span data-stu-id="d8e1d-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="d8e1d-116">Fluxos de porta de destino</span><span class="sxs-lookup"><span data-stu-id="d8e1d-116">Flows by Destination Port</span></span>

<span data-ttu-id="d8e1d-117">O modelo fornecido é editável para que possa modificá-lo e adicionar elementos visuais ou dados novos ou editar consultas para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-117">The template provided is editable so you can modify it to add new data, visuals, or edit queries to suit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="d8e1d-118">Configuração</span><span class="sxs-lookup"><span data-stu-id="d8e1d-118">Setup</span></span>

<span data-ttu-id="d8e1d-119">Antes de começar, você deve habilitar o registro em log de fluxo do grupo de segurança de rede em um ou mais grupos de segurança de rede em sua conta.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="d8e1d-120">Confira o artigo: [Introdução ao registro em log de fluxo para grupos de segurança de rede](network-watcher-nsg-flow-logging-overview.md) para obter instruções sobre como habilitar os logs de fluxo da segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-120">For instructions on enabling Network Security flow logs, refer to the following article: [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="d8e1d-121">Você também deve ter o cliente de desktop do Power BI instalado no seu computador e espaço livre suficiente para baixar e carregar os dados de log que existem em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-121">You must also have the Power BI Desktop client installed on your machine, and enough free space on your machine to download and load the log data that exists in your storage account.</span></span>

![Diagrama do Visio][1]

### <a name="steps"></a><span data-ttu-id="d8e1d-123">Etapas</span><span class="sxs-lookup"><span data-stu-id="d8e1d-123">Steps</span></span>

1. <span data-ttu-id="d8e1d-124">Baixe e abra o seguinte modelo do Power BI no aplicativo de área de trabalho do Power BI: [modelo de logs de fluxo do Power BI do observador de rede](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span><span class="sxs-lookup"><span data-stu-id="d8e1d-124">Download and open the following Power BI template in the Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="d8e1d-125">Insira os parâmetros de consulta necessários</span><span class="sxs-lookup"><span data-stu-id="d8e1d-125">Enter the required Query parameters</span></span>
    1. <span data-ttu-id="d8e1d-126">**StorageAccountName** – Especifica o nome da conta de armazenamento que contém os logs de fluxo NSG que você gostaria de carregar e visualizar.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-126">**StorageAccountName** – Specifies to the name of the storage account containing the NSG flow logs that you would like to load and visualize.</span></span>
    1. <span data-ttu-id="d8e1d-127">**NumberOfLogFiles** – Especifica o número de arquivos de log que você gostaria de baixar e visualizar no Power BI.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-127">**NumberOfLogFiles** – Specifies the number of log files that you would like to download and visualize in Power BI.</span></span> <span data-ttu-id="d8e1d-128">Por exemplo: se especificar 50, serão baixados e disponibilizados para visualização os 50 arquivos de log mais recentes.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-128">For example, if 50 is specified, the 50 latest log files.</span></span> <span data-ttu-id="d8e1d-129">Olhando à frente, temos 2 NSGs habilitados e configurados para enviar logs de fluxo NSG para esta conta, desta forma, as 25 horas de logs podem ser visualizadas.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-129">Ff we have 2 NSGs enabled and configured to send NSG flow logs to this account, then the past 25 hours of logs can be viewed.</span></span>

    ![principal do Power BI][2]

1. <span data-ttu-id="d8e1d-131">Insira a chave de acesso da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-131">Enter the Access Key for your storage account.</span></span> <span data-ttu-id="d8e1d-132">Para encontrar as chaves de acesso válidas, acesse a sua conta de armazenamento no portal do Azure e selecione: **Chaves de Acesso** no menu Configurações.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-132">You can find valid access keys by navigating to your storage account in the Azure portal and selecting **Access Keys** from the Settings menu.</span></span> <span data-ttu-id="d8e1d-133">Clique em **Conectar** e, em seguida, aplique as alterações.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-133">Click **Connect** then apply changes.</span></span>

    ![teclas de acesso][3]

    ![chave de acesso 2][4]

4.  <span data-ttu-id="d8e1d-136">Depois de baixar e analisar os logs, você pode utilizar os visuais criados previamente.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-136">Your logs are download and parsed and you can now utilize the pre-created visuals.</span></span>

## <a name="understanding-the-visuals"></a><span data-ttu-id="d8e1d-137">Noções básicas sobre os elementos visuais</span><span class="sxs-lookup"><span data-stu-id="d8e1d-137">Understanding the visuals</span></span>

<span data-ttu-id="d8e1d-138">No modelo, é fornecido um conjunto de visuais que ajuda no entendimento dos dados do Log de Fluxo do NSG.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-138">Provided in the template are a set of visuals that help make sense of the NSG Flow Log data.</span></span> <span data-ttu-id="d8e1d-139">As imagens a seguir mostram um exemplo da aparência de um painel populado com dados.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-139">The following images show a sample of what the dashboard looks like when populated with data.</span></span> <span data-ttu-id="d8e1d-140">Confira a seguir as informações detalhadas sobre cada visual</span><span class="sxs-lookup"><span data-stu-id="d8e1d-140">Below we examine each visual in greater detail</span></span> 

![powerbi][5]
 
<span data-ttu-id="d8e1d-142">O visual dos principais locutores mostra os IPs que iniciaram a maioria das conexões durante o período especificado.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-142">The Top Talkers visual shows the IPs that have initiated the most connections over the period specified.</span></span> <span data-ttu-id="d8e1d-143">O tamanho das caixas corresponde ao número relativo de conexões.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-143">The size of the boxes corresponds to the relative number of connections.</span></span> 

![toptalkers][6]

<span data-ttu-id="d8e1d-145">Os gráficos de série de tempo a seguir mostram o número de fluxos durante o período.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-145">The following time series graphs show the number of flows over the period.</span></span> <span data-ttu-id="d8e1d-146">O gráfico superior é segmentado pelo sentido do fluxo, enquanto o inferior é segmentado pela decisão tomada (permitir ou negar).</span><span class="sxs-lookup"><span data-stu-id="d8e1d-146">The upper graph is segmented by the flow direction, and the lower is segmented by the decision made (allow or deny).</span></span> <span data-ttu-id="d8e1d-147">Com esse visual, é possível examinar as tendências do tráfego ao longo do tempo e identificar picos anormais ou quedas no tráfego ou na segmentação de tráfego.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flowsoverperiod][7]

<span data-ttu-id="d8e1d-149">Os gráficos a seguir mostram os fluxos por interface de rede, com a parte superior segmentada por sentido do fluxo, e a inferior segmentada por decisão tomada.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-149">The following graphs show the flows per Network interface, with the upper segmented by flow direction and the lower segmented by decision made.</span></span> <span data-ttu-id="d8e1d-150">Com essas informações, você saberá qual das suas VMs comunicou-se mais em relação às outras, e se o tráfego para uma VM específica está sendo permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-150">With this information, you can gain insights into which of your VMs communicated the most relative to others, and if traffic to a specific VM is being allowed or denied.</span></span>

![flowspernic][8]

<span data-ttu-id="d8e1d-152">O gráfico de rosca a seguir mostra uma divisão de fluxos de porta de destino.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-152">The following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="d8e1d-153">Com essas informações, você pode exibir as portas de destino mais usadas dentro do período especificado.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-153">With this information, you can view the most commonly used destination ports used within the specified period.</span></span>

![donut][9]

<span data-ttu-id="d8e1d-155">O gráfico de barras a seguir mostra o fluxo de NSG e a regra.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-155">The following bar chart shows the Flow by NSG and Rule.</span></span> <span data-ttu-id="d8e1d-156">Com essas informações, você pode conferir os NSGs responsáveis pela maioria do tráfego e a análise de tráfego em um NSG por regra.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-156">With this information, you can see the NSGs responsible for the most traffic, and the breakdown of traffic on an NSG by rule.</span></span>

![barchart][10]
 
<span data-ttu-id="d8e1d-158">Os gráficos informativos a seguir exibem informações sobre os NSGs presentes nos logs, o número de fluxos capturados ao longo do período e os dados do log capturado mais antigo.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-158">The following informational charts display information about the NSGs present in the logs, the number of Flows captured over the period, and the date of the earliest log captured.</span></span> <span data-ttu-id="d8e1d-159">Com essas informações, você terá uma ideia sobre quais NSGs estão sendo registrados e qual é a extensão de dados dos fluxos.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-159">This information gives you an idea of what NSGs are being logged and the date range of flows.</span></span>

![infochart1][11]

![infochart2][12]

<span data-ttu-id="d8e1d-162">As segmentações exibidas no modelo a seguir, permitem que você visualize somente os dados que quiser.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-162">This template includes the following slicers to allow you to view only the data you are most interested in.</span></span> <span data-ttu-id="d8e1d-163">Você pode filtrar seus grupos de recursos, NSGs e regras.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="d8e1d-164">Além disso, você também pode filtrar as informações de 5 tuplas, a decisão e o momento em que o log foi gravado.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-164">You can also filter on 5-tuple information, decision, and the time the log was written.</span></span>

![slicers][13]

## <a name="conclusion"></a><span data-ttu-id="d8e1d-166">Conclusão</span><span class="sxs-lookup"><span data-stu-id="d8e1d-166">Conclusion</span></span>

<span data-ttu-id="d8e1d-167">Mostramos neste cenário que somos capazes de visualizar e compreender o tráfego se usarmos os logs de fluxo do grupo de segurança de rede fornecidos pelo Observador de rede e o Power BI.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able to visualize and understand the traffic.</span></span> <span data-ttu-id="d8e1d-168">Usando o modelo fornecido, o Power BI baixa os logs diretamente do armazenamento e os processa localmente.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-168">Using the provided template, Power BI downloads the logs directly from storage and processes them locally.</span></span> <span data-ttu-id="d8e1d-169">O tempo necessário para carregar o modelo varia de acordo com o número de arquivos solicitados e o tamanho total dos arquivos baixados.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-169">Time taken to load the template varies depending on the number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="d8e1d-170">Fique à vontade para personalizar esse modelo para adequá-lo às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-170">Feel free to customize this template for your needs.</span></span> <span data-ttu-id="d8e1d-171">Há várias maneiras de usar o Power BI com logs de fluxo do grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="d8e1d-172">Observações</span><span class="sxs-lookup"><span data-stu-id="d8e1d-172">Notes</span></span>

* <span data-ttu-id="d8e1d-173">Os logs, por padrão, são armazenados em `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span><span class="sxs-lookup"><span data-stu-id="d8e1d-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="d8e1d-174">Se houver outros dados em outro diretório, as consultas para executar o pull e os processos de dados deverão ser modificados.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-174">If other data exists in another directory they the queries to pull and process the data must be modified.</span></span>

* <span data-ttu-id="d8e1d-175">Não é recomendado usar o modelo fornecido quando há mais de 1 GB de logs.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-175">The provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="d8e1d-176">Se você tiver uma quantidade grande de logs, recomendamos que estude uma solução que use outro tipo de armazenamento de dados, como o Data Lake ou o SQL server.</span><span class="sxs-lookup"><span data-stu-id="d8e1d-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8e1d-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8e1d-177">Next Steps</span></span>

<span data-ttu-id="d8e1d-178">Para saber como visualizar os logs de fluxo NSG com a pilha elástica, confira: [Como visualizar padrões de tráfego de rede de e para suas VMs usando ferramentas de software livre](network-watcher-using-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="d8e1d-178">Learn how to visualize your NSG flow logs with the Elastick Stack by visiting [Visualize network traffic patterns to and from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
