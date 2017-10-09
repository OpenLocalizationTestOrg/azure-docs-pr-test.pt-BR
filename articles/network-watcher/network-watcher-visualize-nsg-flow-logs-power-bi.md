---
title: "logs de aaaVisualizing fluxo de grupo de segurança de rede do Azure com o Power BI | Microsoft Docs"
description: "Esta página descreve como o fluxo NSG toovisualize registra com o Power BI."
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
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="6444a-103">Visualização de logs de fluxo do grupo de segurança de rede com o Power BI</span><span class="sxs-lookup"><span data-stu-id="6444a-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="6444a-104">Os logs de fluxo de grupo de segurança de rede permitem tooview a informações sobre o tráfego IP de entrada e saída em grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="6444a-104">Network Security Group flow logs allow you tooview information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="6444a-105">Esses logs de fluxo Mostrar saídas e fluxos de entrada em uma base por regra, Olá fluxo de saudação do NIC se aplica, 5-tupla informações sobre o fluxo de saudação (origem/destino IP, porta de origem/destino, protocolo), e se o tráfego de saudação é permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="6444a-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="6444a-106">Pode ser difícil toogain insights em fluxo de log de dados pesquisando manualmente os arquivos de log de saudação.</span><span class="sxs-lookup"><span data-stu-id="6444a-106">It can be difficult toogain insights into flow logging data by manually searching hello log files.</span></span> <span data-ttu-id="6444a-107">Neste artigo, fornecemos um toovisualize solução seu fluxo mais recente logs e saiba mais sobre o tráfego na rede.</span><span class="sxs-lookup"><span data-stu-id="6444a-107">In this article, we provide a solution toovisualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="6444a-108">Cenário</span><span class="sxs-lookup"><span data-stu-id="6444a-108">Scenario</span></span>

<span data-ttu-id="6444a-109">Olá cenário a seguir, conectamos conta de armazenamento do Power BI desktop toohello que configuramos como coletor Olá para nossos dados NSG fluxo de log.</span><span class="sxs-lookup"><span data-stu-id="6444a-109">In hello following scenario, we connect Power BI desktop toohello storage account we have configured as hello sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="6444a-110">Depois de nos conectarmos tooour conta de armazenamento, Power BI baixa e analisa Olá logs tooprovide uma representação visual do tráfego de saudação que é registrado por grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="6444a-110">After we connect tooour storage account, Power BI downloads and parses hello logs tooprovide a visual representation of hello traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="6444a-111">Usando visuais Olá fornecidos no modelo de saudação, que você pode examinar:</span><span class="sxs-lookup"><span data-stu-id="6444a-111">Using hello visuals supplied in hello template you can examine:</span></span>

* <span data-ttu-id="6444a-112">Os principais locutores</span><span class="sxs-lookup"><span data-stu-id="6444a-112">Top Talkers</span></span>
* <span data-ttu-id="6444a-113">Dados de fluxo de série temporal por decisão de regra e direção</span><span class="sxs-lookup"><span data-stu-id="6444a-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="6444a-114">Fluxos de endereço MAC da interface de rede</span><span class="sxs-lookup"><span data-stu-id="6444a-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="6444a-115">Fluxos de NSG e regra</span><span class="sxs-lookup"><span data-stu-id="6444a-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="6444a-116">Fluxos de porta de destino</span><span class="sxs-lookup"><span data-stu-id="6444a-116">Flows by Destination Port</span></span>

<span data-ttu-id="6444a-117">modelo de saudação fornecido é editável para que você pode modificá-lo tooadd novos dados, visuais, ou editar consultas toosuit suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="6444a-117">hello template provided is editable so you can modify it tooadd new data, visuals, or edit queries toosuit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="6444a-118">Configuração</span><span class="sxs-lookup"><span data-stu-id="6444a-118">Setup</span></span>

<span data-ttu-id="6444a-119">Antes de começar, você deve habilitar o registro em log de fluxo do grupo de segurança de rede em um ou mais grupos de segurança de rede em sua conta.</span><span class="sxs-lookup"><span data-stu-id="6444a-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="6444a-120">Para obter instruções sobre como habilitar a segurança de rede de fluxo de logs, consulte toohello artigo a seguir: [registro em log tooflow de Introdução para grupos de segurança de rede](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6444a-120">For instructions on enabling Network Security flow logs, refer toohello following article: [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="6444a-121">Você também deve ter o cliente do Power BI Desktop saudação instalado em seu computador e suficiente liberar espaço em sua máquina toodownload e carga Olá dados de log que existe na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6444a-121">You must also have hello Power BI Desktop client installed on your machine, and enough free space on your machine toodownload and load hello log data that exists in your storage account.</span></span>

![Diagrama do Visio][1]

### <a name="steps"></a><span data-ttu-id="6444a-123">Etapas</span><span class="sxs-lookup"><span data-stu-id="6444a-123">Steps</span></span>

1. <span data-ttu-id="6444a-124">Baixe e abra Olá seguindo o modelo do Power BI no hello aplicativo de área de trabalho do Power BI [fluxo de rede Inspetor PowerBI logs de modelo](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span><span class="sxs-lookup"><span data-stu-id="6444a-124">Download and open hello following Power BI template in hello Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="6444a-125">Digite os parâmetros de consulta Olá necessária</span><span class="sxs-lookup"><span data-stu-id="6444a-125">Enter hello required Query parameters</span></span>
    1. <span data-ttu-id="6444a-126">**StorageAccountName** – toohello Especifica o nome da conta de armazenamento Olá fluxo NSG Olá contém logs que você deseja tooload e visualizar.</span><span class="sxs-lookup"><span data-stu-id="6444a-126">**StorageAccountName** – Specifies toohello name of hello storage account containing hello NSG flow logs that you would like tooload and visualize.</span></span>
    1. <span data-ttu-id="6444a-127">**NumberOfLogFiles** – Especifica o número de saudação de arquivos de log que você deseja toodownload e visualizar no Power BI.</span><span class="sxs-lookup"><span data-stu-id="6444a-127">**NumberOfLogFiles** – Specifies hello number of log files that you would like toodownload and visualize in Power BI.</span></span> <span data-ttu-id="6444a-128">Por exemplo, se for especificada a 50, Olá 50 arquivos de log mais recentes.</span><span class="sxs-lookup"><span data-stu-id="6444a-128">For example, if 50 is specified, hello 50 latest log files.</span></span> <span data-ttu-id="6444a-129">FF temos 2 NSGs habilitado e configurado a conta de toothis toosend NSG fluxo de logs, hello últimas 25 horas de logs pode ser exibidas.</span><span class="sxs-lookup"><span data-stu-id="6444a-129">Ff we have 2 NSGs enabled and configured toosend NSG flow logs toothis account, then hello past 25 hours of logs can be viewed.</span></span>

    ![principal do Power BI][2]

1. <span data-ttu-id="6444a-131">Digite hello chave de acesso para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6444a-131">Enter hello Access Key for your storage account.</span></span> <span data-ttu-id="6444a-132">Você pode encontrar as chaves de acesso válido navegando tooyour conta de armazenamento hello Azure portal e selecionando **chaves de acesso** no menu de configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="6444a-132">You can find valid access keys by navigating tooyour storage account in hello Azure portal and selecting **Access Keys** from hello Settings menu.</span></span> <span data-ttu-id="6444a-133">Clique em **Conectar** e, em seguida, aplique as alterações.</span><span class="sxs-lookup"><span data-stu-id="6444a-133">Click **Connect** then apply changes.</span></span>

    ![teclas de acesso][3]

    ![chave de acesso 2][4]

4.  <span data-ttu-id="6444a-136">Os logs são baixar e analisada e agora você pode utilizar visuais pré-criados hello.</span><span class="sxs-lookup"><span data-stu-id="6444a-136">Your logs are download and parsed and you can now utilize hello pre-created visuals.</span></span>

## <a name="understanding-hello-visuals"></a><span data-ttu-id="6444a-137">Noções básicas sobre visuais Olá</span><span class="sxs-lookup"><span data-stu-id="6444a-137">Understanding hello visuals</span></span>

<span data-ttu-id="6444a-138">Fornecido em Olá modelo são um conjunto de elementos visuais que ajudam faz sentido de saudação dados NSG fluxo de Log.</span><span class="sxs-lookup"><span data-stu-id="6444a-138">Provided in hello template are a set of visuals that help make sense of hello NSG Flow Log data.</span></span> <span data-ttu-id="6444a-139">Olá imagens a seguir mostram um exemplo de qual painel Olá aparência quando preenchida com dados.</span><span class="sxs-lookup"><span data-stu-id="6444a-139">hello following images show a sample of what hello dashboard looks like when populated with data.</span></span> <span data-ttu-id="6444a-140">Confira a seguir as informações detalhadas sobre cada visual</span><span class="sxs-lookup"><span data-stu-id="6444a-140">Below we examine each visual in greater detail</span></span> 

![powerbi][5]
 
<span data-ttu-id="6444a-142">Talkers de parte superior do Hello visual mostra Olá IPs que iniciou Olá a maioria das conexões pela Olá período especificado.</span><span class="sxs-lookup"><span data-stu-id="6444a-142">hello Top Talkers visual shows hello IPs that have initiated hello most connections over hello period specified.</span></span> <span data-ttu-id="6444a-143">tamanho de saudação das caixas Olá corresponde número relativo de toohello de conexões.</span><span class="sxs-lookup"><span data-stu-id="6444a-143">hello size of hello boxes corresponds toohello relative number of connections.</span></span> 

![toptalkers][6]

<span data-ttu-id="6444a-145">Hello, seguir gráficos de série de tempo mostram Olá número de fluxos em período de saudação.</span><span class="sxs-lookup"><span data-stu-id="6444a-145">hello following time series graphs show hello number of flows over hello period.</span></span> <span data-ttu-id="6444a-146">gráfico superior Olá segmentado por direção do fluxo de saudação e Olá inferior é segmentada por decisão Olá feita (permitir ou negar).</span><span class="sxs-lookup"><span data-stu-id="6444a-146">hello upper graph is segmented by hello flow direction, and hello lower is segmented by hello decision made (allow or deny).</span></span> <span data-ttu-id="6444a-147">Com esse visual, é possível examinar as tendências do tráfego ao longo do tempo e identificar picos anormais ou quedas no tráfego ou na segmentação de tráfego.</span><span class="sxs-lookup"><span data-stu-id="6444a-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flowsoverperiod][7]

<span data-ttu-id="6444a-149">Olá gráficos a seguir mostram Olá fluxos por interface de rede, com hello superior segmentadas por direção do fluxo e Olá inferior segmentadas por decisão tomada.</span><span class="sxs-lookup"><span data-stu-id="6444a-149">hello following graphs show hello flows per Network interface, with hello upper segmented by flow direction and hello lower segmented by decision made.</span></span> <span data-ttu-id="6444a-150">Com essas informações, você pode obter ideias sobre que suas VMs comunicadas Olá tooothers relativo a maioria das e se o tráfego tooa VM específica está sendo permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="6444a-150">With this information, you can gain insights into which of your VMs communicated hello most relative tooothers, and if traffic tooa specific VM is being allowed or denied.</span></span>

![flowspernic][8]

<span data-ttu-id="6444a-152">Olá gráfico de roda de rosca a seguir mostra uma divisão de fluxos de porta de destino.</span><span class="sxs-lookup"><span data-stu-id="6444a-152">hello following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="6444a-153">Com essas informações, você pode exibir as portas de destino Olá usado mais comumente usadas em Olá especificado período.</span><span class="sxs-lookup"><span data-stu-id="6444a-153">With this information, you can view hello most commonly used destination ports used within hello specified period.</span></span>

![donut][9]

<span data-ttu-id="6444a-155">Olá seguinte gráfico de barras mostra Olá fluxo NSG e regra.</span><span class="sxs-lookup"><span data-stu-id="6444a-155">hello following bar chart shows hello Flow by NSG and Rule.</span></span> <span data-ttu-id="6444a-156">Com essas informações, você pode ver Olá NSGs responsáveis por hello mais tráfego e divisão de saudação do tráfego em um NSG pela regra.</span><span class="sxs-lookup"><span data-stu-id="6444a-156">With this information, you can see hello NSGs responsible for hello most traffic, and hello breakdown of traffic on an NSG by rule.</span></span>

![barchart][10]
 
<span data-ttu-id="6444a-158">Hello seguintes gráficos informativos exibe informações sobre Olá NSGs presente nos logs de saudação, Olá número de fluxos capturados por período hello e data de saudação de log mais antigo de Olá capturado.</span><span class="sxs-lookup"><span data-stu-id="6444a-158">hello following informational charts display information about hello NSGs present in hello logs, hello number of Flows captured over hello period, and hello date of hello earliest log captured.</span></span> <span data-ttu-id="6444a-159">Essas informações lhe dá uma ideia do que os NSGs estão sendo registradas em log e Olá intervalo de datas de fluxos.</span><span class="sxs-lookup"><span data-stu-id="6444a-159">This information gives you an idea of what NSGs are being logged and hello date range of flows.</span></span>

![infochart1][11]

![infochart2][12]

<span data-ttu-id="6444a-162">Esse modelo inclui Olá tooallow segmentações de dados a seguir você tooview somente Olá os dados que está mais interessados em.</span><span class="sxs-lookup"><span data-stu-id="6444a-162">This template includes hello following slicers tooallow you tooview only hello data you are most interested in.</span></span> <span data-ttu-id="6444a-163">Você pode filtrar seus grupos de recursos, NSGs e regras.</span><span class="sxs-lookup"><span data-stu-id="6444a-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="6444a-164">Você também pode filtrar em informações de 5 tuplas, a decisão e a hora de Olá Olá log foi gravado.</span><span class="sxs-lookup"><span data-stu-id="6444a-164">You can also filter on 5-tuple information, decision, and hello time hello log was written.</span></span>

![slicers][13]

## <a name="conclusion"></a><span data-ttu-id="6444a-166">Conclusão</span><span class="sxs-lookup"><span data-stu-id="6444a-166">Conclusion</span></span>

<span data-ttu-id="6444a-167">Mostramos neste cenário que usando logs de fluxo de grupo de segurança de rede fornecidas pelo observador de rede e o Power BI, estamos toovisualize capaz e entender o tráfego de saudação.</span><span class="sxs-lookup"><span data-stu-id="6444a-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able toovisualize and understand hello traffic.</span></span> <span data-ttu-id="6444a-168">Usando o modelo de saudação fornecido, o Power BI baixa os logs de saudação diretamente do armazenamento e processa-os localmente.</span><span class="sxs-lookup"><span data-stu-id="6444a-168">Using hello provided template, Power BI downloads hello logs directly from storage and processes them locally.</span></span> <span data-ttu-id="6444a-169">Modelo de saudação do tempo gasto tooload varia dependendo do número de saudação de arquivos solicitados e o tamanho total dos arquivos baixados.</span><span class="sxs-lookup"><span data-stu-id="6444a-169">Time taken tooload hello template varies depending on hello number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="6444a-170">Se sentir livre toocustomize este modelo para suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="6444a-170">Feel free toocustomize this template for your needs.</span></span> <span data-ttu-id="6444a-171">Há várias maneiras de usar o Power BI com logs de fluxo do grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="6444a-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="6444a-172">Observações</span><span class="sxs-lookup"><span data-stu-id="6444a-172">Notes</span></span>

* <span data-ttu-id="6444a-173">Os logs, por padrão, são armazenados em `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span><span class="sxs-lookup"><span data-stu-id="6444a-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="6444a-174">Se houver outros dados em outro diretório eles Olá toopull consultas e dados de saudação do processo devem ser modificados.</span><span class="sxs-lookup"><span data-stu-id="6444a-174">If other data exists in another directory they hello queries toopull and process hello data must be modified.</span></span>

* <span data-ttu-id="6444a-175">modelo de saudação fornecido não é recomendado para uso com mais de 1 GB de logs.</span><span class="sxs-lookup"><span data-stu-id="6444a-175">hello provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="6444a-176">Se você tiver uma quantidade grande de logs, recomendamos que estude uma solução que use outro tipo de armazenamento de dados, como o Data Lake ou o SQL server.</span><span class="sxs-lookup"><span data-stu-id="6444a-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6444a-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6444a-177">Next Steps</span></span>

<span data-ttu-id="6444a-178">Saiba como toovisualize seu fluxo NSG registra com hello Elastick pilha visitando [visualizar tooand de padrões de tráfego de rede de suas VMs usando ferramentas de software livre](network-watcher-using-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="6444a-178">Learn how toovisualize your NSG flow logs with hello Elastick Stack by visiting [Visualize network traffic patterns tooand from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

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
