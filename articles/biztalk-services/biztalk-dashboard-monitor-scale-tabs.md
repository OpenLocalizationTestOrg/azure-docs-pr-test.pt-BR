---
title: "Painel, Monitor, Escala, Configuração e Conexões Híbridas nos Serviços BizTalk | Microsoft Docs"
description: "Saiba mais sobre os controles e monitore o desempenho nas guias do portal clássico para os Serviços BizTalk: Painel, Monitor, Escala, Configurar e Conexões Híbridas MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 4ec88d9a681a5692b31f7e3990d1c153296b18ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="review-the-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="e5714-104">Examine as guias Painel, Monitor, Escala, Configurar e Conexão Híbrid</span><span class="sxs-lookup"><span data-stu-id="e5714-104">Review the Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="e5714-105">Depois de criar o Serviço BizTalk e implantar seu aplicativo, você pode alterar algumas configurações do Serviço BizTalk e monitorar o desempenho do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e5714-105">After you create your BizTalk Service and deploy your application, you can change some of the BizTalk Service settings and monitor the application performance.</span></span> 

<span data-ttu-id="e5714-106">Ao abrir o portal clássico do Azure, você será levado automaticamente para a guia **TODOS OS ITENS** .</span><span class="sxs-lookup"><span data-stu-id="e5714-106">When you open the Azure classic portal, you are automatically placed at the **ALL ITEMS** tab.</span></span> <span data-ttu-id="e5714-107">Para exibir seu Serviço BizTalk, selecione o Serviço do BizTalk na guia **TODOS OS ITENS** ou selecione a guia **SERVIÇOS BIZTALK** e selecione o nome do seu Serviço BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-107">To view your BizTalk Service, select your BizTalk Service in the **ALL ITEMS** tab or select the **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="e5714-108">Isso abre uma nova janela com as seguintes guias:</span><span class="sxs-lookup"><span data-stu-id="e5714-108">This opens a new window with the following tabs.</span></span> <span data-ttu-id="e5714-109">Este tópico descreve essas guias.</span><span class="sxs-lookup"><span data-stu-id="e5714-109">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="e5714-110">Início rápido (</span><span class="sxs-lookup"><span data-stu-id="e5714-110">Quickstart (</span></span>![Início rápido][Quickstart]<span data-ttu-id="e5714-112">)</span><span class="sxs-lookup"><span data-stu-id="e5714-112">)</span></span>
<span data-ttu-id="e5714-113">Dependendo da Edição dos Serviços do BizTalk, é possível que não todas as opções listadas estejam disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e5714-113">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="e5714-114"><strong>Obter as ferramentas</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-114"><strong>Get the tools</strong></span></span></td>
        <td><span data-ttu-id="e5714-115">Baixe o SDK dos Serviços BizTalk para instalar os modelos do projeto do Visual Studio em seu computador de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="e5714-115">Download the BizTalk Services SDK to install the Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="e5714-116">Esses modelos criam os projetos do Visual Studio <strong>Serviços BizTalk</strong> (ponte) e <strong>Artefatos do Serviço BizTalk</strong> (Transformação), que são implantados em seu Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-116">These templates create the <strong>BizTalk Services</strong> (bridge) and the <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed to your BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="e5714-117">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> Como faço para começar a usar o SDK dos Serviços BizTalk do Azure </a> e <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Instalando o SDK dos Serviços BizTalk do Azure</a> listam as etapas para começar.</span><span class="sxs-lookup"><span data-stu-id="e5714-117">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using the Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing the Azure BizTalk Services SDK</a> lists the steps to get started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="e5714-118"><strong>Criar contratos de parceiro</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-118"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="e5714-119">Abre o Portal dos Serviços BizTalk hospedados no Azure onde você adiciona parceiros e cria contratos EDI X12, AS2 e EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="e5714-119">Opens the Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="e5714-120">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurando componentes para mensagens EDI no Portal dos Serviços BizTalk</a> lista as etapas para começar.</span><span class="sxs-lookup"><span data-stu-id="e5714-120">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists the steps to get started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="e5714-121"><strong>Saiba mais sobre os Serviços BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-121"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="e5714-122">Acesse o <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">centro de aprendizado</a> para saber mais sobre os Serviços BizTalk do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5714-122">Go to the <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> to learn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="e5714-123">Na barra de tarefas na parte inferior, você pode:</span><span class="sxs-lookup"><span data-stu-id="e5714-123">In the task bar at the bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="e5714-124"><strong>Gerenciar</strong> a implantação de seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="e5714-124"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="e5714-125">Abre o Portal dos Serviços do BizTalk do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5714-125">Opens the Azure BizTalk Services portal.</span></span> <span data-ttu-id="e5714-126">O Portal dos Serviços do BizTalk é a entrada para a configuração de EDI, inclusive a adição de parceiros e criação de acordos AS2 e X12 e EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="e5714-126">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="e5714-127">É igual à opção <strong>Criar contratos de parceiros</strong> na guia <strong>Início Rápido</strong>.</span><span class="sxs-lookup"><span data-stu-id="e5714-127">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="e5714-128">A página 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurando componentes para mensagens de EDI no Portal de Serviços BizTalk</a> fornece mais informações sobre o Portal de Serviços BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-128">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="e5714-129"><strong>Informação da conexão</strong> do Namespace de Controle de Acesso</span><span class="sxs-lookup"><span data-stu-id="e5714-129"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="e5714-130">Quando você seleciona Informações de Conexão, o Namespace do Controle de Acesso, o Emissor Padrão e a Chave Padrão são exibidos.</span><span class="sxs-lookup"><span data-stu-id="e5714-130">When you select Connection Information, then the Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="e5714-131">Você pode copiar esses valores.</span><span class="sxs-lookup"><span data-stu-id="e5714-131">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="e5714-132">Você também pode abrir o Portal de Controle de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e5714-132">You can also open the Access Control Portal.</span></span> <span data-ttu-id="e5714-133"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Criar um namespace do Controle de Acesso</a> fornece mais informações sobre o Portal de Controle de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e5714-133"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="e5714-134"><strong>Chaves de sincronização</strong> na conta de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="e5714-134"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="e5714-135">Quando você cria uma Conta de Armazenamento, uma chave primária e uma chave secundária são criadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e5714-135">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="e5714-136">Essas chaves de criptografia controlam o acesso à sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e5714-136">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="e5714-137">Seu Serviço do BizTalk usa automaticamente a chave primária.</span><span class="sxs-lookup"><span data-stu-id="e5714-137">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="e5714-138">A opção <strong>Sincronizar Chaves</strong> permite que os usuários alternem entre as chaves primária e secundária sem interromper o Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-138"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="e5714-139">Por exemplo, você deseja que o Serviço do BizTalk use uma nova Chave Primária para a Conta de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e5714-139">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="e5714-140">Para fazer isso:</span><span class="sxs-lookup"><span data-stu-id="e5714-140">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="e5714-141">Selecione o Serviço do BizTalk e selecione <strong>Sincronizar Chaves</strong>.</span><span class="sxs-lookup"><span data-stu-id="e5714-141">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="e5714-142">Selecione a chave secundária.</span><span class="sxs-lookup"><span data-stu-id="e5714-142">Select the Secondary Key.</span></span> <span data-ttu-id="e5714-143">Quando você faz isso, o Serviço do BizTalk começa a usar a chave secundária.</span><span class="sxs-lookup"><span data-stu-id="e5714-143">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="e5714-144">No portal clássico do Azure, selecione sua Conta de Armazenamento e regenere a Chave Primária.</span><span class="sxs-lookup"><span data-stu-id="e5714-144">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="e5714-145">Lembre-se que seu Serviço do BizTalk está usando a chave secundária.</span><span class="sxs-lookup"><span data-stu-id="e5714-145">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="e5714-146">Selecione o Serviço do BizTalk e selecione <strong>Sincronizar Chaves</strong>.</span><span class="sxs-lookup"><span data-stu-id="e5714-146">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="e5714-147">Agora, selecione a chave primário.</span><span class="sxs-lookup"><span data-stu-id="e5714-147">Now, select the Primary Key.</span></span> <span data-ttu-id="e5714-148">Esta é a nova chave primária que você regenerou.</span><span class="sxs-lookup"><span data-stu-id="e5714-148">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="e5714-149">No portal clássico do Azure, selecione sua Conta de Armazenamento e Regenerar a Chave Secundária.</span><span class="sxs-lookup"><span data-stu-id="e5714-149">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="e5714-150">Esse processo é chamado de "chaves de substituição".</span><span class="sxs-lookup"><span data-stu-id="e5714-150">This process is called "rollover keys".</span></span> <span data-ttu-id="e5714-151">O propósito é permitir que os usuários alternem entre as chaves primária e secundária sem interromper o Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-151">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="e5714-152"><strong>Excluir</strong> seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="e5714-152"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="e5714-153">Quando você seleciona Excluir, seu Serviço do BizTalk e todos os itens implantados nele são removidos.</span><span class="sxs-lookup"><span data-stu-id="e5714-153">When you select Delete, your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="e5714-154">Painel</span><span class="sxs-lookup"><span data-stu-id="e5714-154">Dashboard</span></span>
<span data-ttu-id="e5714-155">Dependendo da Edição dos Serviços do BizTalk, é possível que não todas as opções listadas estejam disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e5714-155">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="e5714-156">Quando você seleciona o nome do Serviço do BizTalk, a guia de Painel é exibida.</span><span class="sxs-lookup"><span data-stu-id="e5714-156">When you select your BizTalk Service name, the Dashboard tab is displayed.</span></span> <span data-ttu-id="e5714-157">No Painel, você pode:</span><span class="sxs-lookup"><span data-stu-id="e5714-157">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-the-number-of-used-hybrid-connections"></a><span data-ttu-id="e5714-158">Visão geral do usuário: mostra o número de Conexões Híbridas usadas</span><span class="sxs-lookup"><span data-stu-id="e5714-158">Usage Overview: Shows the number of used Hybrid Connections</span></span>
<span data-ttu-id="e5714-159">Também mostra os dados usados em GB.</span><span class="sxs-lookup"><span data-stu-id="e5714-159">Also displays the data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="e5714-160">Gráfico de métrica: mostra uma lista fixa de métricas de desempenho</span><span class="sxs-lookup"><span data-stu-id="e5714-160">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="e5714-161">Essas métricas fornecem valores em tempo real relacionados à integridade do Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-161">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="e5714-162">Você também pode especificar os valores **Relativo** ou **Absoluto** e o **Intervalo** de tempo das métricas que são mostradas no gráfico.</span><span class="sxs-lookup"><span data-stu-id="e5714-162">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed in the graph.</span></span> 

<span data-ttu-id="e5714-163">Para obter uma descrição dessas métricas de desempenho, acesse [Métricas disponíveis](#Metrics) neste tópico.</span><span class="sxs-lookup"><span data-stu-id="e5714-163">For a description of these performance metrics, go to [Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="e5714-164">Visão Rápida: lista as propriedades do Serviço BizTalk</span><span class="sxs-lookup"><span data-stu-id="e5714-164">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="e5714-165"><strong>Atualizar as credenciais do banco de dados de acompanhamento</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-165"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="e5714-166">Altera o nome de usuário e senha usado para fazer logon no banco de dados de acompanhamento.</span><span class="sxs-lookup"><span data-stu-id="e5714-166">Changes the user name and password used to log into the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-167"><strong>Atualizar o certificado de SSL</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-167"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="e5714-168">É possível atualizar o Serviço BizTalk para usar um certificado SSL diferente.</span><span class="sxs-lookup"><span data-stu-id="e5714-168">Can update the BizTalk Service to use a different SSL certificate.</span></span> <span data-ttu-id="e5714-169">Um Certificado SSL autoassinado é criado automaticamente ao <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">criar o Serviço do BizTalk</a>.</span><span class="sxs-lookup"><span data-stu-id="e5714-169">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create the BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-170"><strong>Baixar certificado</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-170"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="e5714-171">Você pode baixar o certificado SSL usado pelo Serviço de BizTalk em uma máquina local.</span><span class="sxs-lookup"><span data-stu-id="e5714-171">You can download the SSL certificate used by your BizTalk Service to a local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-172"><strong>Status</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-172"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="e5714-173">Mostra o status atual do Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-173">Displays the current status of your BizTalk Service.</span></span> <span data-ttu-id="e5714-174">Consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">Serviços BizTalk: gráfico de estado do serviço</a>.</span><span class="sxs-lookup"><span data-stu-id="e5714-174">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="e5714-175"><strong>URL do serviço</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-175"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="e5714-176">A URL para o seu Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-176">The URL for your BizTalk Service.</span></span> <span data-ttu-id="e5714-177">É igual à <strong>URL do Domínio</strong> inserida quando o Serviço do BizTalk é criado.</span><span class="sxs-lookup"><span data-stu-id="e5714-177">This is the same as the <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-178"><strong>Endereço VIP (IP virtual público)</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-178"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="e5714-179">O endereço IP atribuído ao seu Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-179">The IP address assigned to your BizTalk Service.</span></span> <span data-ttu-id="e5714-180">Ele é usado para todos os pontos de extremidade de entrada e é o endereço de origem para o tráfego de saída.</span><span class="sxs-lookup"><span data-stu-id="e5714-180">It is used for all input endpoints and is the source address for outbound traffic.</span></span> <span data-ttu-id="e5714-181">Esse endereço IP pertence ao seu Serviço BizTalk contanto que ele seja criado.</span><span class="sxs-lookup"><span data-stu-id="e5714-181">This IP address belongs to your BizTalk Service as long as it is created.</span></span> <span data-ttu-id="e5714-182">Se você excluir o Serviço do BizTalk, o endereço IP será atribuído a outro Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-182">If you delete the BizTalk Service, the IP address is assigned to another BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-183"><strong>Namespace do ACS</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-183"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="e5714-184">Autenticados com o Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-184">Authenticates with the BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-185"><strong>Edição</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-185"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="e5714-186">Lista a Edição inserida quando o Serviço do BizTalk é criado.</span><span class="sxs-lookup"><span data-stu-id="e5714-186">Lists the Edition entered when the BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-187"><strong>Localidade</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-187"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="e5714-188">Mostra a região geográfica que hospeda seu Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-188">Displays the geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-189"><strong>Criado</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-189"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="e5714-190">Mostra a data e a hora em que o Serviço do BizTalk foi criado.</span><span class="sxs-lookup"><span data-stu-id="e5714-190">Displays the date and time the BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-191"><strong>Banco de dados de acompanhamento</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-191"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="e5714-192">O nome do Banco de Dados SQL que armazena as tabelas de acompanhamento usadas pelo Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-192">The Azure SQL Database name that stores the tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="e5714-193">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requisitos explicados</a> fornece detalhes sobre o Banco de Dados de Acompanhamento.</span><span class="sxs-lookup"><span data-stu-id="e5714-193">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-194"><strong>Armazenamento de monitoramento/arquivamento</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-194"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="e5714-195">O nome da conta de Armazenamento do Azure que armazena a saída do monitoramento de seu Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-195">The Azure Storage account name that stores the monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="e5714-196">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requisitos explicados</a> fornece detalhes sobre a conta de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e5714-196">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-197"><strong>Nome da assinatura</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-197"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="e5714-198">Lista a assinatura que hospeda seu Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-198">Lists the subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="e5714-199">A assinatura rege o acesso ao portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5714-199">The subscription governs access to the Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-200"><strong>ID da assinatura</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-200"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="e5714-201">Quando uma assinatura é criada, uma ID da assinatura é gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e5714-201">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="e5714-202">Ao usar APIs REST, talvez seja necessário inserir a ID da assinatura.</span><span class="sxs-lookup"><span data-stu-id="e5714-202">When using REST APIs, you may need to enter the Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="e5714-203">[Serviços BizTalk: provisionamento usando o portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280) lista as etapas para criar um Serviço BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-203">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists the steps to create a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-the-task-bar"></a><span data-ttu-id="e5714-204">Gerenciar, Informação de Conexão, Chaves de sincronização, e Excluir na barra de tarefas:</span><span class="sxs-lookup"><span data-stu-id="e5714-204">Manage, Connection Information, Sync Keys, and Delete in the task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="e5714-205"><strong>Gerenciar</strong> a implantação de seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="e5714-205"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="e5714-206">Abre o Portal dos Serviços do BizTalk do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5714-206">Opens the Azure BizTalk Services Portal.</span></span> <span data-ttu-id="e5714-207">O Portal dos Serviços do BizTalk é a entrada para a configuração de EDI, inclusive a adição de parceiros e criação de acordos AS2 e X12 e EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="e5714-207">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="e5714-208">É igual à opção <strong>Criar contratos de parceiros</strong> na guia <strong>Início Rápido</strong>.</span><span class="sxs-lookup"><span data-stu-id="e5714-208">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="e5714-209">A página 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurando componentes para mensagens de EDI no Portal de Serviços BizTalk</a> fornece mais informações sobre o Portal de Serviços BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-209">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-210"><strong>Informação da conexão</strong> do Namespace de Controle de Acesso</span><span class="sxs-lookup"><span data-stu-id="e5714-210"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="e5714-211">Mostra o Namespace do Controle de Acesso, Emissor Padrão, e valores de Chave Padrão; que podem ser copiados.</span><span class="sxs-lookup"><span data-stu-id="e5714-211">Displays the Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="e5714-212">Você também pode abrir o Portal de Controle de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e5714-212">You can also open the Access Control Portal.</span></span> <span data-ttu-id="e5714-213">Esse Portal de Controle de Acesso é igual ao uso da opção Active Directory no painel de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="e5714-213">This Access Control Portal is the same as using the Active Directory option in the left navigation pane.</span></span>
<br/><br/><span data-ttu-id="e5714-214">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Gerenciando o namespace do ACS</a> fornece mais informações sobre o Portal de Controle de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e5714-214">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-215"><strong>Chaves de sincronização</strong> na conta de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="e5714-215"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="e5714-216">Quando você cria uma Conta de Armazenamento, uma chave primária e uma chave secundária são criadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e5714-216">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="e5714-217">Essas chaves de criptografia controlam o acesso à sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e5714-217">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="e5714-218">Seu Serviço do BizTalk usa automaticamente a chave primária.</span><span class="sxs-lookup"><span data-stu-id="e5714-218">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="e5714-219">A opção <strong>Sincronizar Chaves</strong> permite que os usuários alternem entre as chaves primária e secundária sem interromper o Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-219"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="e5714-220">Por exemplo, você deseja que o Serviço do BizTalk use uma nova Chave Primária para a Conta de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e5714-220">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="e5714-221">Para fazer isso:</span><span class="sxs-lookup"><span data-stu-id="e5714-221">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="e5714-222">Selecione o Serviço do BizTalk e selecione <strong>Sincronizar Chaves</strong>.</span><span class="sxs-lookup"><span data-stu-id="e5714-222">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="e5714-223">Selecione a chave secundária.</span><span class="sxs-lookup"><span data-stu-id="e5714-223">Select the Secondary Key.</span></span> <span data-ttu-id="e5714-224">Quando você faz isso, o Serviço do BizTalk começa a usar a chave secundária.</span><span class="sxs-lookup"><span data-stu-id="e5714-224">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="e5714-225">No portal clássico do Azure, selecione sua Conta de Armazenamento e regenere a Chave Primária.</span><span class="sxs-lookup"><span data-stu-id="e5714-225">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="e5714-226">Lembre-se que seu Serviço do BizTalk está usando a chave secundária.</span><span class="sxs-lookup"><span data-stu-id="e5714-226">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="e5714-227">Selecione o Serviço do BizTalk e selecione <strong>Sincronizar Chaves</strong>.</span><span class="sxs-lookup"><span data-stu-id="e5714-227">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="e5714-228">Agora, selecione a chave primário.</span><span class="sxs-lookup"><span data-stu-id="e5714-228">Now, select the Primary Key.</span></span> <span data-ttu-id="e5714-229">Esta é a nova chave primária que você regenerou.</span><span class="sxs-lookup"><span data-stu-id="e5714-229">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="e5714-230">No portal clássico do Azure, selecione sua Conta de Armazenamento e Regenerar a Chave Secundária.</span><span class="sxs-lookup"><span data-stu-id="e5714-230">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="e5714-231">Esse processo é chamado de "chaves de substituição".</span><span class="sxs-lookup"><span data-stu-id="e5714-231">This process is called "rollover keys".</span></span> <span data-ttu-id="e5714-232">O propósito é permitir que os usuários alternem entre as chaves primária e secundária sem interromper o Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-232">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="e5714-233"><strong>Excluir</strong> seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="e5714-233"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="e5714-234">Seu Serviço do BizTalk e todos os itens implantados a ele são removidos.</span><span class="sxs-lookup"><span data-stu-id="e5714-234">Your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="e5714-235">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="e5714-235">Monitor</span></span>
<span data-ttu-id="e5714-236">Não é aplicado à Edição Gratuita.</span><span class="sxs-lookup"><span data-stu-id="e5714-236">Does not apply to the Free Edition.</span></span>

<span data-ttu-id="e5714-237">Ao selecionar o nome do seu Serviço do BizTalk, a guia do Monitor está disponível e mostra o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e5714-237">When you select your BizTalk Service name, the Monitor tab is available and displays the following:</span></span>

##### <a name="metric-graph-displays-the-selected-performance-metrics"></a><span data-ttu-id="e5714-238">Gráfico de Métricas: exibe as métricas de desempenho selecionadas</span><span class="sxs-lookup"><span data-stu-id="e5714-238">Metric Graph: Displays the selected performance metrics</span></span>
<span data-ttu-id="e5714-239">Essas métricas fornecem valores em tempo real relacionados à integridade do Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-239">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="e5714-240">Você escolhe quais métricas de desempenho são exibidas.</span><span class="sxs-lookup"><span data-stu-id="e5714-240">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="e5714-241">No máximo seis métricas de desempenho podem ser exibidas simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="e5714-241">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="e5714-242">Você também pode especificar os valores **Relativo** ou **Absoluto** e o **Intervalo** de tempo das métricas mostradas.</span><span class="sxs-lookup"><span data-stu-id="e5714-242">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed.</span></span> 

##### <a name="to-remove-or-display-metrics-in-the-graph"></a><span data-ttu-id="e5714-243">Para remover ou exibir métricas no gráfico:</span><span class="sxs-lookup"><span data-stu-id="e5714-243">To remove or display metrics in the graph:</span></span>
1. <span data-ttu-id="e5714-244">Selecione a guia **Processo** .</span><span class="sxs-lookup"><span data-stu-id="e5714-244">Select the **Monitor** tab.</span></span>
2. <span data-ttu-id="e5714-245">Selecione **Adicionar Métricas** na barra de tarefas:</span><span class="sxs-lookup"><span data-stu-id="e5714-245">Select **Add Metrics** in the task bar:</span></span>  
   <span data-ttu-id="e5714-246">![Selecione Adicionar Métricas][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="e5714-246">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="e5714-247">Verifique as métricas de desempenho que você deseja mostrar.</span><span class="sxs-lookup"><span data-stu-id="e5714-247">Check the performance metrics you want to display.</span></span>
4. <span data-ttu-id="e5714-248">Selecione a marca de seleção para retornar à guia **Monitoramento** .</span><span class="sxs-lookup"><span data-stu-id="e5714-248">Select the checkmark to return to the **Monitor** tab.</span></span>
5. <span data-ttu-id="e5714-249">Selecione o círculo ao lado de métrica para exibir o valor dela no gráfico.</span><span class="sxs-lookup"><span data-stu-id="e5714-249">Select the circle next to the metric to display that metric's value in the graph.</span></span>  
   
    <span data-ttu-id="e5714-250">Por exemplo, a métrica **Uso de CPU** fica esmaecida; sua saída não é exibida no gráfico:</span><span class="sxs-lookup"><span data-stu-id="e5714-250">For example, the **CPU Usage** metric is grayed out; its output is not displayed in the graph:</span></span>  
   <span data-ttu-id="e5714-251">![A métrica Uso de CPU fica esmaecida][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="e5714-251">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="e5714-252">Clique no círculo esmaecido para habilitar a métrica **Uso de CPU** e mostrar sua saída no gráfico:</span><span class="sxs-lookup"><span data-stu-id="e5714-252">Select the grayed out circle to enable the **CPU Usage** metric to display its output in the graph:</span></span>  
   <span data-ttu-id="e5714-253">![A métrica Uso de CPU está habilitada][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="e5714-253">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="e5714-254">Para remover uma métrica do gráfico de exibição e da lista, selecione **Excluir Métricas** na barra de tarefas.</span><span class="sxs-lookup"><span data-stu-id="e5714-254">To remove a metric from the display graph and the list, select **Delete Metric** in the task bar.</span></span> <span data-ttu-id="e5714-255">Para adicionar a métrica à lista novamente, selecione **Adicionar Métricas** na barra de tarefas, selecione a métrica e clique na marca de seleção para retornar para a guia **Monitorar**.</span><span class="sxs-lookup"><span data-stu-id="e5714-255">To add the metric back to the list, select **Add Metrics** in the task bar, check the metric, and select the checkmark to return to the **Monitor** tab.</span></span> <span data-ttu-id="e5714-256">Selecione o círculo esmaecido para habilitar a métrica.</span><span class="sxs-lookup"><span data-stu-id="e5714-256">Select the grayed out circle to enable the metric.</span></span>

## <span data-ttu-id="e5714-257"><a name="Metrics"></a>Métricas disponíveis</span><span class="sxs-lookup"><span data-stu-id="e5714-257"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="e5714-258">As contagens/métricas de desempenho a seguir estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="e5714-258">The following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="e5714-259"><strong>Latência de viagem de ida e volta</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-259"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="e5714-260">Mostra a média do tempo em milissegundos (ms) que leva para processar uma mensagem a partir do tempo em que a mensagem é recebida até que a mensagem seja completamente processada pelo Serviço do BizTalk através de todas as pontes.</span><span class="sxs-lookup"><span data-stu-id="e5714-260">Displays the average time taken in milliseconds (ms) to process a message from the time the message is received until the message is fully processed by the BizTalk Service across all bridges.</span></span> <span data-ttu-id="e5714-261">São contadas apenas mensagens processadas com êxito.</span><span class="sxs-lookup"><span data-stu-id="e5714-261">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="e5714-262">Quando os eventos a seguir ocorrerem, será criado um carimbo de data/hora:</span><span class="sxs-lookup"><span data-stu-id="e5714-262">When the following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="e5714-263">A mensagem entra no gateway</span><span class="sxs-lookup"><span data-stu-id="e5714-263">Message enters the gateway</span></span></li>
<li><span data-ttu-id="e5714-264">A mensagem é roteada ao destino</span><span class="sxs-lookup"><span data-stu-id="e5714-264">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="e5714-265">A resposta do destino é recebida</span><span class="sxs-lookup"><span data-stu-id="e5714-265">Destination response is received</span></span></li>
<li><span data-ttu-id="e5714-266">A resposta da confirmação do destino é enviada ao gateway</span><span class="sxs-lookup"><span data-stu-id="e5714-266">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="e5714-267">Esta métrica mostra o resultado do seguinte cálculo:</span><span class="sxs-lookup"><span data-stu-id="e5714-267">This metric shows the result of the following calculation:</span></span>
<br/><br/>
<span data-ttu-id="e5714-268">[Resposta de confirmação do destino enviada ao gateway] - [Mensagem entra no gateway]</span><span class="sxs-lookup"><span data-stu-id="e5714-268">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-269"><strong>Falhas na origem</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-269"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="e5714-270">Exibe o número total de mensagens que falharam quando o Serviço do BizTalk puxa as mensagens nos pontos de extremidade de origem.</span><span class="sxs-lookup"><span data-stu-id="e5714-270">Displays the total number of messages that failed by the BizTalk Service when pulling messages from the source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-271"><strong>Uso da CPU</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-271"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="e5714-272">Lista a média da % de Tempo do Processador para todas as instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="e5714-272">Lists the average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-273"><strong>Latência de processamento</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-273"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="e5714-274">Exibe o tempo médio para processar uma mensagem pelo Serviço do BizTalk em todas as pontes, exceto o tempo gasto nos destinos.</span><span class="sxs-lookup"><span data-stu-id="e5714-274">Displays the average time taken In milliseconds (ms) to process a message by the BizTalk Service across all bridges, excluding the time spent in destinations.</span></span> <span data-ttu-id="e5714-275">São contadas apenas mensagens processadas com êxito.</span><span class="sxs-lookup"><span data-stu-id="e5714-275">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="e5714-276">Quando cada um dos eventos a seguir ocorre, é criado um carimbo de data/hora:</span><span class="sxs-lookup"><span data-stu-id="e5714-276">When each of the following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="e5714-277">A mensagem entra no gateway</span><span class="sxs-lookup"><span data-stu-id="e5714-277">Message enters the gateway</span></span></li>
<li><span data-ttu-id="e5714-278">A mensagem é roteada ao destino</span><span class="sxs-lookup"><span data-stu-id="e5714-278">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="e5714-279">A resposta do destino é recebida</span><span class="sxs-lookup"><span data-stu-id="e5714-279">Destination response is received</span></span></li>
<li><span data-ttu-id="e5714-280">A resposta da confirmação do destino é enviada ao gateway</span><span class="sxs-lookup"><span data-stu-id="e5714-280">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/><span data-ttu-id="e5714-281">Esta métrica mostra o resultado do seguinte cálculo:</span><span class="sxs-lookup"><span data-stu-id="e5714-281">This metric shows the result of the following calculation:</span></span><br/><br/>
<span data-ttu-id="e5714-282">[Resposta da confirmação do destino enviada ao gateway] – [Mensagem entra no gateway] – [A resposta do destino é recebida] + [A mensagem é roteada ao destino]</span><span class="sxs-lookup"><span data-stu-id="e5714-282">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway] - [Destination response is received] + [Message is routed to the destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-283"><strong>Falhas no processo</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-283"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="e5714-284">Exibe o número total de mensagens que falharam durante o processamento pelo Serviço do BizTalk em todas as pontes em um intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="e5714-284">Displays the total number of messages that failed during processing by the BizTalk Service across all the bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-285"><strong>Mensagens Enviadas</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-285"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="e5714-286">Exibe o número total de mensagens enviadas pelo Serviço do BizTalk por todas as pontes dentro em um intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="e5714-286">Displays the total number of messages sent by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="e5714-287">Essa métrica é incrementada quando uma mensagem enviada de uma pipeline alcança o destino da rota.</span><span class="sxs-lookup"><span data-stu-id="e5714-287">This metric is incremented when a message sent from a pipeline reaches the route destination.</span></span> <span data-ttu-id="e5714-288">Essa métrica não indica se uma mensagem foi processada com êxito.</span><span class="sxs-lookup"><span data-stu-id="e5714-288">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="e5714-289">Em um cenário de solicitação-resposta, a métrica é incrementada quando o destino de rota envia uma confirmação de recebimento de volta à pipeline.</span><span class="sxs-lookup"><span data-stu-id="e5714-289">In a Request-Reply scenario, the metric is incremented when the route destination sends a receipt acknowledgement back to the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-290"><strong>Mensagens recebidas</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-290"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="e5714-291">Exibe o número total de mensagens recebidas pelo Serviço do BizTalk por todas as pontes dentro em um intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="e5714-291">Displays the total number of messages received by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="e5714-292">Essa métrica é incrementada quando uma nova mensagem é recebida pela pipeline.</span><span class="sxs-lookup"><span data-stu-id="e5714-292">This metric is incremented when a new message is received by the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-293"><strong>Mensagens em processamento</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-293"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="e5714-294">Exibe o número total de mensagens sendo processadas no momento pelo Serviço do BizTalk em um intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="e5714-294">Displays the total number of messages currently being processed by the BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e5714-295"><strong>Mensagens processadas</strong></span><span class="sxs-lookup"><span data-stu-id="e5714-295"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="e5714-296">Exibe o número total de mensagens processadas com êxito pelo Serviço do BizTalk por todas as pontes dentro em um intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="e5714-296">Displays the total number of messages successfully processed by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="e5714-297">Essa métrica é incrementada quando uma mensagem é recebida com êxito pela pipeline e roteada com êxito ao destino.</span><span class="sxs-lookup"><span data-stu-id="e5714-297">This metric is incremented when a message is successfully received by the pipeline and successfully routed to the destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="e5714-298">Escala</span><span class="sxs-lookup"><span data-stu-id="e5714-298">Scale</span></span>
<span data-ttu-id="e5714-299">Na guia Escala, você pode adicionar ou subtrair o número de unidades usadas pelo Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-299">In the Scale tab, you can add or subtract the number of units used by your BizTalk Service.</span></span> <span data-ttu-id="e5714-300">Por padrão, há uma unidade configurada.</span><span class="sxs-lookup"><span data-stu-id="e5714-300">By default, there is one Unit configured.</span></span> <span data-ttu-id="e5714-301">Unidades adicionais podem ser adicionadas para dimensionar seu Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e5714-301">Additional Units can be added to scale your BizTalk Service.</span></span> <span data-ttu-id="e5714-302">Quando você aumenta a escala, você está aumentando a produção.</span><span class="sxs-lookup"><span data-stu-id="e5714-302">When you increase the scale, you are increasing throughput.</span></span> <span data-ttu-id="e5714-303">A quantidade de recursos também aumenta, inclusive as pontes implantadas, os acordos, as conexões de LOB e a capacidade de processamento.</span><span class="sxs-lookup"><span data-stu-id="e5714-303">The amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="e5714-304">Por exemplo, você aumenta a escala de uma unidade para duas.</span><span class="sxs-lookup"><span data-stu-id="e5714-304">For example, you increase the scale from 1 Unit to 2 Units.</span></span> <span data-ttu-id="e5714-305">Nessa situação, você pode implantar duas vezes mais pontes, contratos, conexões de LOB e a capacidade de processamento.</span><span class="sxs-lookup"><span data-stu-id="e5714-305">In this situation, you can deploy double the number of bridges, double the agreements, double the LOB connections, and double the processing power.</span></span>

<span data-ttu-id="e5714-306">Algumas edições do BizTalk não oferecem uma opção de escala.</span><span class="sxs-lookup"><span data-stu-id="e5714-306">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="e5714-307">Nesta situação, uma unidade é permitida.</span><span class="sxs-lookup"><span data-stu-id="e5714-307">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="e5714-308">Para determinar a quantidade de unidades de dimensionamento da sua edição, consulte [Serviços BizTalk: gráfico de edições](biztalk-editions-feature-chart.md)</span><span class="sxs-lookup"><span data-stu-id="e5714-308">To determine how many units your edition can be scaled, refer to [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="e5714-309">Aumentar o número de unidades pode afetar os preços.</span><span class="sxs-lookup"><span data-stu-id="e5714-309">Increasing the number of units may impact pricing.</span></span> <span data-ttu-id="e5714-310">Se você aumentar as unidades, selecione **Salvar** para exibir uma mensagem que informa se a cobrança é afetada.</span><span class="sxs-lookup"><span data-stu-id="e5714-310">If you increase the Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="e5714-311">Você escolhe continuar.</span><span class="sxs-lookup"><span data-stu-id="e5714-311">You then choose to continue.</span></span> <span data-ttu-id="e5714-312">Quando você aumenta o número de unidades, o status do Serviço do BizTalk é alterado de Ativo para Atualizando.</span><span class="sxs-lookup"><span data-stu-id="e5714-312">When you increase the number of Units, the BizTalk Service status changes from Active to Updating.</span></span> <span data-ttu-id="e5714-313">Durante o estado Atualizando, seu Serviço do BizTalk continua funcionando.</span><span class="sxs-lookup"><span data-stu-id="e5714-313">In the Updating state, your BizTalk Service continues to run.</span></span>

<span data-ttu-id="e5714-314">[Serviços BizTalk: gráfico de edições](biztalk-editions-feature-chart.md) define uma “Unidade”.</span><span class="sxs-lookup"><span data-stu-id="e5714-314">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="e5714-315">Configurar</span><span class="sxs-lookup"><span data-stu-id="e5714-315">Configure</span></span>
<span data-ttu-id="e5714-316">Não é aplicado para Conexões Híbridas.</span><span class="sxs-lookup"><span data-stu-id="e5714-316">Does not apply to Hybrid Connections.</span></span>

<span data-ttu-id="e5714-317">Define o Status de Backup para Nenhum ou Automático.</span><span class="sxs-lookup"><span data-stu-id="e5714-317">Sets the Backup Status to None or Automatic.</span></span> <span data-ttu-id="e5714-318">Quando estiver definido para Nenhum, nenhum backup será criado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e5714-318">When set to None, no backups are automatically created.</span></span> <span data-ttu-id="e5714-319">Quando estiver definido para Automático, você configura o local do backup, a frequência do backup, e por quanto tempo manter os arquivos de backup.</span><span class="sxs-lookup"><span data-stu-id="e5714-319">When set to Automatic, you configure the backup location, the frequency of the backup, and how long to keep the backup files.</span></span> 

<span data-ttu-id="e5714-320">[Serviços BizTalk: backup e restauração](biztalk-backup-restore.md) fornece os detalhes.</span><span class="sxs-lookup"><span data-stu-id="e5714-320">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides the details.</span></span> 

## <span data-ttu-id="e5714-321"><a name="HybridConnections"></a>Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="e5714-321"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="e5714-322">As Conexões Híbridas conectam um aplicativo do Azure, como aplicativos Web ou Aplicativos Móveis no Serviço de Aplicativo do Azure, a um recurso local que utilize uma porta TCP estática, como SQL Server, MySQL, APIs Web HTTP e os serviços Web mais personalizados.</span><span class="sxs-lookup"><span data-stu-id="e5714-322">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, to an on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="e5714-323">As Conexões Híbridas são gerenciadas nos Serviços BizTalk, no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5714-323">Hybrid Connections are managed in  BizTalk Services in the Azure classic portal.</span></span>

<span data-ttu-id="e5714-324">Para criar conexões híbridas no Serviço de Aplicativo do Azure, confira [Acessar recursos locais usando conexões híbridas no Serviço de Aplicativo do Azure](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e5714-324">To create Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="e5714-325">Para criar ou gerenciar as Conexões Híbridas nos Serviços do BizTalk do Azure, consulte [Conexões Híbridas](integration-hybrid-connection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e5714-325">To create or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="e5714-326">Avançar</span><span class="sxs-lookup"><span data-stu-id="e5714-326">Next</span></span>
<span data-ttu-id="e5714-327">Agora que está familiarizado com as diferentes guias, você pode obter mais informações sobre os recursos dos Serviços BizTalk do Azure:</span><span class="sxs-lookup"><span data-stu-id="e5714-327">Now that you're familiar with the different tabs, you can learn more about the Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="e5714-328">Serviços BizTalk: limitação</span><span class="sxs-lookup"><span data-stu-id="e5714-328">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="e5714-329">Serviços BizTalk: nome e chave do emissor</span><span class="sxs-lookup"><span data-stu-id="e5714-329">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="e5714-330">Serviços BizTalk: backup e restauração</span><span class="sxs-lookup"><span data-stu-id="e5714-330">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="e5714-331">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e5714-331">See Also</span></span>
* [<span data-ttu-id="e5714-332">Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="e5714-332">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="e5714-333">Serviços BizTalk: gráfico das edições Developer, Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="e5714-333">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="e5714-334">Serviços BizTalk: provisionamento usando o portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="e5714-334">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="e5714-335">Serviços BizTalk: gráfico de estado do Serviço do BizTalk (a página pode estar em inglês)</span><span class="sxs-lookup"><span data-stu-id="e5714-335">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="e5714-336">Como começar a usar o SDK dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="e5714-336">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

