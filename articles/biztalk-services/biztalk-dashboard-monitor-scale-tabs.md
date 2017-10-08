---
title: "aaaDashboard, Monitor, escala, configurar e conexões híbridas nos Serviços BizTalk | Microsoft Docs"
description: "Saiba mais sobre os controles de saudação e monitorar o desempenho em guias de portal clássico Olá para Serviços BizTalk: painel, Monitor, escala, configurar e conexões híbridas. MABS, WABS"
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
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="1c4e7-104">Examine Olá guias painel, Monitor, escala, configurar e Conexão híbrida</span><span class="sxs-lookup"><span data-stu-id="1c4e7-104">Review hello Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="1c4e7-105">Depois de criar o BizTalk Service e implantar seu aplicativo, você pode alterar algumas das configurações de serviço BizTalk hello e monitorar o desempenho do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-105">After you create your BizTalk Service and deploy your application, you can change some of hello BizTalk Service settings and monitor hello application performance.</span></span> 

<span data-ttu-id="1c4e7-106">Quando você abre Olá portal clássico do Azure, são colocados automaticamente em hello **todos os itens** guia tooview Service o BizTalk, selecione o BizTalk Service no hello **todos os itens** guia ou selecione hello **Serviços BIZTALK** guia; e, em seguida, selecione o nome do BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-106">When you open hello Azure classic portal, you are automatically placed at hello **ALL ITEMS** tab. tooview your BizTalk Service, select your BizTalk Service in hello **ALL ITEMS** tab or select hello **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="1c4e7-107">Isso abre uma nova janela com hello guias a seguir.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-107">This opens a new window with hello following tabs.</span></span> <span data-ttu-id="1c4e7-108">Este tópico descreve essas guias.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-108">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="1c4e7-109">Início rápido (</span><span class="sxs-lookup"><span data-stu-id="1c4e7-109">Quickstart (</span></span>![Início rápido][Quickstart]<span data-ttu-id="1c4e7-111">)</span><span class="sxs-lookup"><span data-stu-id="1c4e7-111">)</span></span>
<span data-ttu-id="1c4e7-112">Dependendo da saudação BizTalk Services Edition, todas as opções listadas podem não estar disponíveis.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-112">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="1c4e7-113"><strong>Obter ferramentas Olá</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-113"><strong>Get hello tools</strong></span></span></td>
        <td><span data-ttu-id="1c4e7-114">Baixe Olá SDK dos Serviços BizTalk tooinstall Olá projeto modelos do Visual Studio no computador de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-114">Download hello BizTalk Services SDK tooinstall hello Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="1c4e7-115">Esses modelos criam Olá <strong>Serviços BizTalk</strong> (ponte) e hello <strong>artefatos do serviço BizTalk</strong> projetos do Visual Studio de (transformação) que são implantado tooyour BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-115">These templates create hello <strong>BizTalk Services</strong> (bridge) and hello <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed tooyour BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="1c4e7-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Como posso começar a usar Olá SDK dos Serviços BizTalk do Azure </a> e <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">instalando Olá SDK dos Serviços BizTalk do Azure</a> listas Olá etapas tooget iniciado.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using hello Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing hello Azure BizTalk Services SDK</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="1c4e7-117"><strong>Criar contratos de parceiro</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-117"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="1c4e7-118">Abre Olá Portal de serviços do Azure BizTalk hospedado no Azure, onde você pode adicionar parceiros e cria X12, AS2 e EDIFACT EDI contratos.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-118">Opens hello Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="1c4e7-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurar os componentes para mensagens EDI no Portal de Serviços BizTalk</a> listas Olá etapas tooget iniciado.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="1c4e7-120"><strong>Saiba mais sobre os Serviços BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-120"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="1c4e7-121">Vá toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">Central de informações</a> toolearn mais sobre os Serviços BizTalk do Azure.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-121">Go toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> toolearn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="1c4e7-122">Na barra de tarefas de saudação na parte inferior do hello, você pode:</span><span class="sxs-lookup"><span data-stu-id="1c4e7-122">In hello task bar at hello bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="1c4e7-123"><strong>Gerenciar</strong> a implantação de seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1c4e7-123"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="1c4e7-124">Abre o portal de Serviços BizTalk do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-124">Opens hello Azure BizTalk Services portal.</span></span> <span data-ttu-id="1c4e7-125">Olá Portal de Serviços BizTalk é a configuração de tooEDI de entrada hello, inclusive adicionar parceiros e criar X12, AS2 e acordos de EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-125">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="1c4e7-126">Isso é Olá igual <strong>criar acordos de parceiro</strong> em Olá <strong>início rápido</strong> guia.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-126">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="1c4e7-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurar os componentes para mensagens EDI no Portal de Serviços BizTalk</a> fornece mais informações sobre Olá Portal de Serviços BizTalk.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="1c4e7-128"><strong>Informações de Conexão</strong> de saudação Namespace de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="1c4e7-128"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="1c4e7-129">Quando você seleciona as informações de Conexão, em seguida, Olá Namespace de controle de acesso, emissor padrão, e chave padrão são exibidos.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-129">When you select Connection Information, then hello Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="1c4e7-130">Você pode copiar esses valores.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-130">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="1c4e7-131">Você também pode abrir Olá Portal de controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-131">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="1c4e7-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Criar um Namespace de controle de acesso</a> fornece mais informações sobre Olá Portal de controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="1c4e7-133"><strong>Sincronizar chaves</strong> em Olá conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="1c4e7-133"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="1c4e7-134">Quando você cria uma Conta de Armazenamento, uma chave primária e uma chave secundária são criadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-134">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="1c4e7-135">Essas chaves de criptografia controlam acesso tooyour conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-135">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="1c4e7-136">O BizTalk Service usa automaticamente Olá chave primária.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-136">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="1c4e7-137"><strong>Sincronizar chaves</strong> habilitar usuários tooswitch entre hello chave primária e chave secundária da saudação sem interromper Olá BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-137"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="1c4e7-138">Por exemplo, convém Olá BizTalk Service toouse uma nova chave primária para Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-138">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="1c4e7-139">toodo isso:</span><span class="sxs-lookup"><span data-stu-id="1c4e7-139">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="1c4e7-140">Selecione o Serviço do BizTalk e selecione <strong>Sincronizar Chaves</strong>.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-140">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="1c4e7-141">Selecione Olá chave secundária.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-141">Select hello Secondary Key.</span></span> <span data-ttu-id="1c4e7-142">Quando você fizer isso, Olá BizTalk Service inicia usando Olá chave secundária.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-142">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="1c4e7-143">Em Olá portal clássico do Azure, selecione sua conta de armazenamento e regenerar a chave primária da saudação.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-143">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="1c4e7-144">Lembre-se de que o BizTalk Service está usando Olá chave secundária.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-144">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="1c4e7-145">Selecione o Serviço do BizTalk e selecione <strong>Sincronizar Chaves</strong>.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-145">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="1c4e7-146">Agora, selecione Olá chave primária.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-146">Now, select hello Primary Key.</span></span> <span data-ttu-id="1c4e7-147">Isso é Olá nova chave primária você regenerado.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-147">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="1c4e7-148">Em Olá portal clássico do Azure, selecione sua conta de armazenamento e regenerar a chave secundária da saudação.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-148">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="1c4e7-149">Esse processo é chamado de "chaves de substituição".</span><span class="sxs-lookup"><span data-stu-id="1c4e7-149">This process is called "rollover keys".</span></span> <span data-ttu-id="1c4e7-150">finalidade de saudação é tooenable usuários tooswitch entre hello chave primária e chave secundária da saudação sem interromper Olá BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-150">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="1c4e7-151"><strong>Excluir</strong> seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1c4e7-151"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="1c4e7-152">Quando você seleciona excluir, o BizTalk Service e tooit de todos os itens implantados são removidos.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-152">When you select Delete, your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="1c4e7-153">Painel</span><span class="sxs-lookup"><span data-stu-id="1c4e7-153">Dashboard</span></span>
<span data-ttu-id="1c4e7-154">Dependendo da saudação BizTalk Services Edition, todas as opções listadas podem não estar disponíveis.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-154">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="1c4e7-155">Quando você seleciona o nome do BizTalk Service, o guia do painel de saudação é exibido.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-155">When you select your BizTalk Service name, hello Dashboard tab is displayed.</span></span> <span data-ttu-id="1c4e7-156">No Painel, você pode:</span><span class="sxs-lookup"><span data-stu-id="1c4e7-156">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a><span data-ttu-id="1c4e7-157">Visão geral de uso: Mostra o número de saudação de usadas as conexões híbridas</span><span class="sxs-lookup"><span data-stu-id="1c4e7-157">Usage Overview: Shows hello number of used Hybrid Connections</span></span>
<span data-ttu-id="1c4e7-158">Também exibe o uso de dados de saudação em GB.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-158">Also displays hello data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="1c4e7-159">Gráfico de métrica: mostra uma lista fixa de métricas de desempenho</span><span class="sxs-lookup"><span data-stu-id="1c4e7-159">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="1c4e7-160">Essas métricas fornecem valores em tempo real sobre a integridade de saudação do hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-160">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="1c4e7-161">Você também pode escolher Olá **relativo** ou **absoluto** hello e valores de intervalo de tempo **intervalo** de métricas de saudação que são exibidas no gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-161">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed in hello graph.</span></span> 

<span data-ttu-id="1c4e7-162">Para obter uma descrição dessas métricas de desempenho, vá muito[métricas disponíveis](#Metrics) neste tópico.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-162">For a description of these performance metrics, go too[Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="1c4e7-163">Visão Rápida: lista as propriedades do Serviço BizTalk</span><span class="sxs-lookup"><span data-stu-id="1c4e7-163">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="1c4e7-164"><strong>Atualizar as credenciais do banco de dados de acompanhamento</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-164"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="1c4e7-165">Olá de alterações de nome de usuário e senha usados toolog em Olá banco de dados de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-165">Changes hello user name and password used toolog into hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-166"><strong>Atualizar o certificado de SSL</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-166"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="1c4e7-167">Pode atualizar Olá BizTalk Service toouse um certificado SSL diferente.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-167">Can update hello BizTalk Service toouse a different SSL certificate.</span></span> <span data-ttu-id="1c4e7-168">Um certificado SSL autoassinado é automaticamente criado quando você <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">criar hello BizTalk Service</a>.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-168">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create hello BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-169"><strong>Baixar certificado</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-169"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="1c4e7-170">Você pode baixar o certificado SSL Olá usado pelo computador local tooa BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-170">You can download hello SSL certificate used by your BizTalk Service tooa local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-171"><strong>Status</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-171"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="1c4e7-172">Exibe o status atual de saudação do BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-172">Displays hello current status of your BizTalk Service.</span></span> <span data-ttu-id="1c4e7-173">Consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">Serviços BizTalk: gráfico de estado do serviço</a>.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-173">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-174"><strong>URL do serviço</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-174"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="1c4e7-175">Olá URL para o BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-175">hello URL for your BizTalk Service.</span></span> <span data-ttu-id="1c4e7-176">Isso é Olá mesmo como Olá <strong>URL do domínio</strong> inserido quando o BizTalk Service é criado.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-176">This is hello same as hello <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-177"><strong>Endereço VIP (IP virtual público)</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-177"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="1c4e7-178">endereço IP de saudação atribuído tooyour BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-178">hello IP address assigned tooyour BizTalk Service.</span></span> <span data-ttu-id="1c4e7-179">Ele é usado para todos os pontos de extremidade de entrada e é o endereço de origem Olá para tráfego de saída.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-179">It is used for all input endpoints and is hello source address for outbound traffic.</span></span> <span data-ttu-id="1c4e7-180">Esse endereço IP pertence tooyour BizTalk Service desde que ele é criado.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-180">This IP address belongs tooyour BizTalk Service as long as it is created.</span></span> <span data-ttu-id="1c4e7-181">Se você excluir Olá BizTalk Service, o endereço IP de saudação é atribuído tooanother BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-181">If you delete hello BizTalk Service, hello IP address is assigned tooanother BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-182"><strong>Namespace do ACS</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-182"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="1c4e7-183">Autentica com hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-183">Authenticates with hello BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-184"><strong>Edição</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-184"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="1c4e7-185">Lista Olá que edição inserida quando Olá BizTalk Service é criado.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-185">Lists hello Edition entered when hello BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-186"><strong>Localidade</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-186"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="1c4e7-187">Exibe Olá região geográfica que hospeda o BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-187">Displays hello geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-188"><strong>Criado</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-188"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="1c4e7-189">Olá Olá de data e hora exibe o BizTalk Service foi criado.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-189">Displays hello date and time hello BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-190"><strong>Banco de dados de acompanhamento</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-190"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="1c4e7-191">nome de banco de dados do Azure SQL Olá que armazena Olá controle tabelas usadas pelo seu BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-191">hello Azure SQL Database name that stores hello tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="1c4e7-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requisitos Explained</a> fornece detalhes sobre Olá banco de dados de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-193"><strong>Armazenamento de monitoramento/arquivamento</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-193"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="1c4e7-194">Olá armazenamento do Azure nome da conta que armazena Olá monitoramento saída o BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-194">hello Azure Storage account name that stores hello monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="1c4e7-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requisitos Explained</a> fornece detalhes sobre Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-196"><strong>Nome da assinatura</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-196"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="1c4e7-197">Lista de assinatura de saudação que hospeda o BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-197">Lists hello subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="1c4e7-198">assinatura de saudação controla acesso toohello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-198">hello subscription governs access toohello Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-199"><strong>ID da assinatura</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-199"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="1c4e7-200">Quando uma assinatura é criada, uma ID da assinatura é gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-200">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="1c4e7-201">Ao usar APIs REST, talvez seja necessário Olá tooenter ID de assinatura.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-201">When using REST APIs, you may need tooenter hello Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="1c4e7-202">[Serviços BizTalk: Portal clássico do Azure usando o provisionamento](http://go.microsoft.com/fwlink/p/?LinkID=302280) listas Olá etapas toocreate um BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-202">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists hello steps toocreate a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a><span data-ttu-id="1c4e7-203">Gerenciar informações de Conexão, sincronizar as chaves e excluir na barra de tarefas de saudação:</span><span class="sxs-lookup"><span data-stu-id="1c4e7-203">Manage, Connection Information, Sync Keys, and Delete in hello task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="1c4e7-204"><strong>Gerenciar</strong> a implantação de seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1c4e7-204"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="1c4e7-205">Abre Olá Portal de Serviços BizTalk do Azure.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-205">Opens hello Azure BizTalk Services Portal.</span></span> <span data-ttu-id="1c4e7-206">Olá Portal de Serviços BizTalk é a configuração de tooEDI de entrada hello, inclusive adicionar parceiros e criar X12, AS2 e acordos de EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-206">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="1c4e7-207">Isso é Olá igual <strong>criar acordos de parceiro</strong> em Olá <strong>início rápido</strong> guia.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-207">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="1c4e7-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurar os componentes para mensagens EDI no Portal de Serviços BizTalk</a> fornece mais informações sobre Olá Portal de Serviços BizTalk.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-209"><strong>Informações de Conexão</strong> de saudação Namespace de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="1c4e7-209"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="1c4e7-210">Exibe Olá Namespace de controle de acesso, o emissor padrão e valores de chave padrão. que podem ser copiado.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-210">Displays hello Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="1c4e7-211">Você também pode abrir Olá Portal de controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-211">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="1c4e7-212">Este Portal de controle de acesso é Olá mesmo que usar a opção do Active Directory de saudação no painel de navegação esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-212">This Access Control Portal is hello same as using hello Active Directory option in hello left navigation pane.</span></span>
<br/><br/><span data-ttu-id="1c4e7-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Gerenciando seu Namespace do ACS</a> fornece mais informações sobre Olá Portal de controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-214"><strong>Sincronizar chaves</strong> em Olá conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="1c4e7-214"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="1c4e7-215">Quando você cria uma Conta de Armazenamento, uma chave primária e uma chave secundária são criadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-215">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="1c4e7-216">Essas chaves de criptografia controlam acesso tooyour conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-216">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="1c4e7-217">O BizTalk Service usa automaticamente Olá chave primária.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-217">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="1c4e7-218"><strong>Sincronizar chaves</strong> habilitar usuários tooswitch entre hello chave primária e chave secundária da saudação sem interromper Olá BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-218"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="1c4e7-219">Por exemplo, convém Olá BizTalk Service toouse uma nova chave primária para Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-219">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="1c4e7-220">toodo isso:</span><span class="sxs-lookup"><span data-stu-id="1c4e7-220">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="1c4e7-221">Selecione o Serviço do BizTalk e selecione <strong>Sincronizar Chaves</strong>.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-221">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="1c4e7-222">Selecione Olá chave secundária.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-222">Select hello Secondary Key.</span></span> <span data-ttu-id="1c4e7-223">Quando você fizer isso, Olá BizTalk Service inicia usando Olá chave secundária.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-223">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="1c4e7-224">Em Olá portal clássico do Azure, selecione sua conta de armazenamento e regenerar a chave primária da saudação.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-224">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="1c4e7-225">Lembre-se de que o BizTalk Service está usando Olá chave secundária.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-225">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="1c4e7-226">Selecione o Serviço do BizTalk e selecione <strong>Sincronizar Chaves</strong>.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-226">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="1c4e7-227">Agora, selecione Olá chave primária.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-227">Now, select hello Primary Key.</span></span> <span data-ttu-id="1c4e7-228">Isso é Olá nova chave primária você regenerado.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-228">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="1c4e7-229">Em Olá portal clássico do Azure, selecione sua conta de armazenamento e regenerar a chave secundária da saudação.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-229">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="1c4e7-230">Esse processo é chamado de "chaves de substituição".</span><span class="sxs-lookup"><span data-stu-id="1c4e7-230">This process is called "rollover keys".</span></span> <span data-ttu-id="1c4e7-231">finalidade de saudação é tooenable usuários tooswitch entre hello chave primária e chave secundária da saudação sem interromper Olá BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-231">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="1c4e7-232"><strong>Excluir</strong> seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1c4e7-232"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="1c4e7-233">O BizTalk Service e tooit de todos os itens serão removidos.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-233">Your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="1c4e7-234">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="1c4e7-234">Monitor</span></span>
<span data-ttu-id="1c4e7-235">Não se aplica a toohello edição gratuita.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-235">Does not apply toohello Free Edition.</span></span>

<span data-ttu-id="1c4e7-236">Quando você seleciona o nome do BizTalk Service, da guia monitorar hello está disponível e exibe Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="1c4e7-236">When you select your BizTalk Service name, hello Monitor tab is available and displays hello following:</span></span>

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a><span data-ttu-id="1c4e7-237">Gráfico de métrico: Olá exibe selecionado métricas de desempenho</span><span class="sxs-lookup"><span data-stu-id="1c4e7-237">Metric Graph: Displays hello selected performance metrics</span></span>
<span data-ttu-id="1c4e7-238">Essas métricas fornecem valores em tempo real sobre a integridade de saudação do hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-238">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="1c4e7-239">Você escolhe quais métricas de desempenho são exibidas.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-239">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="1c4e7-240">No máximo seis métricas de desempenho podem ser exibidas simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-240">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="1c4e7-241">Você também pode escolher Olá **relativo** ou **absoluto** hello e valores de intervalo de tempo **intervalo** das métricas de saudação que são exibidas.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-241">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed.</span></span> 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a><span data-ttu-id="1c4e7-242">tooremove ou exibir as métricas no gráfico de saudação:</span><span class="sxs-lookup"><span data-stu-id="1c4e7-242">tooremove or display metrics in hello graph:</span></span>
1. <span data-ttu-id="1c4e7-243">Selecione Olá **Monitor** guia.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-243">Select hello **Monitor** tab.</span></span>
2. <span data-ttu-id="1c4e7-244">Selecione **adicionar métricas** na barra de tarefas de saudação:</span><span class="sxs-lookup"><span data-stu-id="1c4e7-244">Select **Add Metrics** in hello task bar:</span></span>  
   <span data-ttu-id="1c4e7-245">![Selecione Adicionar Métricas][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="1c4e7-245">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="1c4e7-246">Verifique se deseja toodisplay de métricas de desempenho de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-246">Check hello performance metrics you want toodisplay.</span></span>
4. <span data-ttu-id="1c4e7-247">Selecione Olá marca de seleção tooreturn toohello **Monitor** guia.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-247">Select hello checkmark tooreturn toohello **Monitor** tab.</span></span>
5. <span data-ttu-id="1c4e7-248">Selecione Olá círculo próxima toohello métrica toodisplay valor da métrica no gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-248">Select hello circle next toohello metric toodisplay that metric's value in hello graph.</span></span>  
   
    <span data-ttu-id="1c4e7-249">Por exemplo, Olá **uso da CPU** métrica está esmaecida; sua saída não é exibida no gráfico de saudação:</span><span class="sxs-lookup"><span data-stu-id="1c4e7-249">For example, hello **CPU Usage** metric is grayed out; its output is not displayed in hello graph:</span></span>  
   <span data-ttu-id="1c4e7-250">![A métrica Uso de CPU fica esmaecida][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="1c4e7-250">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="1c4e7-251">Selecione Olá esmaecidas saudação do círculo tooenable **uso da CPU** toodisplay métrica sua saída em gráfico hello:</span><span class="sxs-lookup"><span data-stu-id="1c4e7-251">Select hello grayed out circle tooenable hello **CPU Usage** metric toodisplay its output in hello graph:</span></span>  
   <span data-ttu-id="1c4e7-252">![A métrica Uso de CPU está habilitada][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="1c4e7-252">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="1c4e7-253">Selecione tooremove uma métrica do gráfico de exibição hello e lista hello, **excluir métrica** na barra de tarefas de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-253">tooremove a metric from hello display graph and hello list, select **Delete Metric** in hello task bar.</span></span> <span data-ttu-id="1c4e7-254">lista de métrica toohello back Olá tooadd, selecione **adicionar métricas** na barra de tarefas hello, verificar métrica hello e selecione Olá marca de seleção tooreturn toohello **Monitor** guia. Selecione Olá esmaecidas métrica de saudação do círculo tooenable.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-254">tooadd hello metric back toohello list, select **Add Metrics** in hello task bar, check hello metric, and select hello checkmark tooreturn toohello **Monitor** tab. Select hello grayed out circle tooenable hello metric.</span></span>

## <span data-ttu-id="1c4e7-255"><a name="Metrics"></a>Métricas disponíveis</span><span class="sxs-lookup"><span data-stu-id="1c4e7-255"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="1c4e7-256">Olá, contadores de desempenho/métricas a seguir está disponível:</span><span class="sxs-lookup"><span data-stu-id="1c4e7-256">hello following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="1c4e7-257"><strong>Latência de viagem de ida e volta</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-257"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="1c4e7-258">Exibe o saudação tempo médio em milissegundos (ms) tooprocess que é recebida uma mensagem da mensagem de saudação do hello tempo até que a mensagem de saudação é totalmente processada pelo Olá BizTalk Service em todas as pontes.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-258">Displays hello average time taken in milliseconds (ms) tooprocess a message from hello time hello message is received until hello message is fully processed by hello BizTalk Service across all bridges.</span></span> <span data-ttu-id="1c4e7-259">São contadas apenas mensagens processadas com êxito.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-259">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="1c4e7-260">Quando ocorre Olá eventos a seguir, um carimbo de hora é criado:</span><span class="sxs-lookup"><span data-stu-id="1c4e7-260">When hello following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="1c4e7-261">Mensagem entrar gateway Olá</span><span class="sxs-lookup"><span data-stu-id="1c4e7-261">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="1c4e7-262">Mensagem é roteada toohello destino</span><span class="sxs-lookup"><span data-stu-id="1c4e7-262">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="1c4e7-263">A resposta do destino é recebida</span><span class="sxs-lookup"><span data-stu-id="1c4e7-263">Destination response is received</span></span></li>
<li><span data-ttu-id="1c4e7-264">Gateway de toohello de resposta enviada de confirmação de destino</span><span class="sxs-lookup"><span data-stu-id="1c4e7-264">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="1c4e7-265">Esta métrica mostra o resultado de saudação de saudação cálculo a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c4e7-265">This metric shows hello result of hello following calculation:</span></span>
<br/><br/>
<span data-ttu-id="1c4e7-266">[Destino confirmação resposta enviada toohello gateway] - [mensagem entrar gateway Olá]</span><span class="sxs-lookup"><span data-stu-id="1c4e7-266">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-267"><strong>Falhas na origem</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-267"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="1c4e7-268">Exibe o número total de saudação de mensagens que falharam por Olá BizTalk Service quando recebendo mensagens de pontos de extremidade de origem hello.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-268">Displays hello total number of messages that failed by hello BizTalk Service when pulling messages from hello source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-269"><strong>Uso da CPU</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-269"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="1c4e7-270">Lista Olá % tempo do processador médio de todas as instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-270">Lists hello average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-271"><strong>Latência de processamento</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-271"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="1c4e7-272">Exibe o saudação tempo médio em milissegundos (ms) tooprocess uma mensagem de saudação BizTalk Service em todas as pontes, excluindo o tempo de saudação gasto em destinos.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-272">Displays hello average time taken In milliseconds (ms) tooprocess a message by hello BizTalk Service across all bridges, excluding hello time spent in destinations.</span></span> <span data-ttu-id="1c4e7-273">São contadas apenas mensagens processadas com êxito.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-273">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="1c4e7-274">Quando cada Olá eventos a seguir ocorrem, é criado um carimbo de hora:</span><span class="sxs-lookup"><span data-stu-id="1c4e7-274">When each of hello following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="1c4e7-275">Mensagem entrar gateway Olá</span><span class="sxs-lookup"><span data-stu-id="1c4e7-275">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="1c4e7-276">Mensagem é roteada toohello destino</span><span class="sxs-lookup"><span data-stu-id="1c4e7-276">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="1c4e7-277">A resposta do destino é recebida</span><span class="sxs-lookup"><span data-stu-id="1c4e7-277">Destination response is received</span></span></li>
<li><span data-ttu-id="1c4e7-278">Gateway de toohello de resposta enviada de confirmação de destino</span><span class="sxs-lookup"><span data-stu-id="1c4e7-278">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/><span data-ttu-id="1c4e7-279">Esta métrica mostra o resultado de saudação de saudação cálculo a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c4e7-279">This metric shows hello result of hello following calculation:</span></span><br/><br/>
<span data-ttu-id="1c4e7-280">[Destino confirmação resposta enviada toohello gateway] - [mensagem entrar gateway Olá] - [resposta de destino é recebida] + [mensagem é roteada toohello destino]</span><span class="sxs-lookup"><span data-stu-id="1c4e7-280">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway] - [Destination response is received] + [Message is routed toohello destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-281"><strong>Falhas no processo</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-281"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="1c4e7-282">Exibe o número total de saudação de mensagens que falharam durante o processamento por Olá BizTalk Service em todas as pontes de saudação em um intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-282">Displays hello total number of messages that failed during processing by hello BizTalk Service across all hello bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-283"><strong>Mensagens Enviadas</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-283"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="1c4e7-284">Exibe Olá o número total de mensagens enviadas por Olá BizTalk Service em todas as pontes dentro de um intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-284">Displays hello total number of messages sent by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="1c4e7-285">Essa métrica é incrementada quando uma mensagem enviada de um pipeline alcança o destino da rota hello.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-285">This metric is incremented when a message sent from a pipeline reaches hello route destination.</span></span> <span data-ttu-id="1c4e7-286">Essa métrica não indica se uma mensagem foi processada com êxito.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-286">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="1c4e7-287">Em um cenário de solicitação-resposta, a métrica de saudação é incrementada quando o destino da rota Olá envia um pipeline de toohello voltar de confirmação de recebimento.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-287">In a Request-Reply scenario, hello metric is incremented when hello route destination sends a receipt acknowledgement back toohello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-288"><strong>Mensagens recebidas</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-288"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="1c4e7-289">Exibe Olá o número total de mensagens recebidas por Olá BizTalk Service em todas as pontes dentro de um intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-289">Displays hello total number of messages received by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="1c4e7-290">Essa métrica é incrementada quando uma nova mensagem é recebida pelo pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-290">This metric is incremented when a new message is received by hello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-291"><strong>Mensagens em processamento</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-291"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="1c4e7-292">Exibe Olá número total de mensagens que estão sendo processadas pelo Olá BizTalk Service dentro de um intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-292">Displays hello total number of messages currently being processed by hello BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="1c4e7-293"><strong>Mensagens processadas</strong></span><span class="sxs-lookup"><span data-stu-id="1c4e7-293"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="1c4e7-294">Exibe Olá número total de mensagens processadas com êxito pelo Olá BizTalk Service em todas as pontes dentro de um intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-294">Displays hello total number of messages successfully processed by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="1c4e7-295">Essa métrica é incrementada quando uma mensagem é recebida com êxito pelo pipeline hello e destino toohello roteado com êxito.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-295">This metric is incremented when a message is successfully received by hello pipeline and successfully routed toohello destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="1c4e7-296">Escala</span><span class="sxs-lookup"><span data-stu-id="1c4e7-296">Scale</span></span>
<span data-ttu-id="1c4e7-297">Na guia dimensionamento de saudação, você pode adicionar ou subtrair Olá número de unidades usadas pelo seu BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-297">In hello Scale tab, you can add or subtract hello number of units used by your BizTalk Service.</span></span> <span data-ttu-id="1c4e7-298">Por padrão, há uma unidade configurada.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-298">By default, there is one Unit configured.</span></span> <span data-ttu-id="1c4e7-299">Unidades adicionais podem ser adicionadas tooscale o BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-299">Additional Units can be added tooscale your BizTalk Service.</span></span> <span data-ttu-id="1c4e7-300">Quando você aumenta a escala hello, você está aumentando a taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-300">When you increase hello scale, you are increasing throughput.</span></span> <span data-ttu-id="1c4e7-301">Olá quantidade de recursos também aumenta, incluindo pontes implantadas, contratos, conexões de LOB e a capacidade de processamento.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-301">hello amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="1c4e7-302">Por exemplo, você aumentar a escala de saudação de unidades de 1 unidade too2.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-302">For example, you increase hello scale from 1 Unit too2 Units.</span></span> <span data-ttu-id="1c4e7-303">Nessa situação, você pode implantar Olá duplo número de pontes, double contratos hello, double Olá LOB conexões e potência de processamento de saudação duplo.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-303">In this situation, you can deploy double hello number of bridges, double hello agreements, double hello LOB connections, and double hello processing power.</span></span>

<span data-ttu-id="1c4e7-304">Algumas edições do BizTalk não oferecem uma opção de escala.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-304">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="1c4e7-305">Nesta situação, uma unidade é permitida.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-305">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="1c4e7-306">toodetermine quantas unidades sua edição pode ser dimensionada, consulte muito[Serviços BizTalk: gráfico de edições](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="1c4e7-306">toodetermine how many units your edition can be scaled, refer too[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="1c4e7-307">Aumentar Olá número de unidades pode afetar os preços.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-307">Increasing hello number of units may impact pricing.</span></span> <span data-ttu-id="1c4e7-308">Se você aumentar Olá unidades, selecionando **salvar** exibe uma mensagem que informa se a cobrança é afetada.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-308">If you increase hello Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="1c4e7-309">Você, em seguida, escolha toocontinue.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-309">You then choose toocontinue.</span></span> <span data-ttu-id="1c4e7-310">Quando você aumenta o número de saudação de unidades, Olá status do BizTalk Service muda de ativo tooUpdating.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-310">When you increase hello number of Units, hello BizTalk Service status changes from Active tooUpdating.</span></span> <span data-ttu-id="1c4e7-311">Olá estado de atualização, o BizTalk Service continua toorun.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-311">In hello Updating state, your BizTalk Service continues toorun.</span></span>

<span data-ttu-id="1c4e7-312">[Serviços BizTalk: gráfico de edições](biztalk-editions-feature-chart.md) define uma “Unidade”.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-312">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="1c4e7-313">Configurar</span><span class="sxs-lookup"><span data-stu-id="1c4e7-313">Configure</span></span>
<span data-ttu-id="1c4e7-314">Não se aplica a conexões de tooHybrid.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-314">Does not apply tooHybrid Connections.</span></span>

<span data-ttu-id="1c4e7-315">Define Olá tooNone de Status de Backup ou automático.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-315">Sets hello Backup Status tooNone or Automatic.</span></span> <span data-ttu-id="1c4e7-316">Quando definido como tooNone, não há backups são criados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-316">When set tooNone, no backups are automatically created.</span></span> <span data-ttu-id="1c4e7-317">Quando definido como tooAutomatic, configurar o local de backup hello, frequência de saudação de backup hello e quanto tempo tookeep Olá os arquivos de backup.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-317">When set tooAutomatic, you configure hello backup location, hello frequency of hello backup, and how long tookeep hello backup files.</span></span> 

<span data-ttu-id="1c4e7-318">[Serviços BizTalk: Backup e restauração](biztalk-backup-restore.md) fornece detalhes de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-318">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides hello details.</span></span> 

## <span data-ttu-id="1c4e7-319"><a name="HybridConnections"></a>Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="1c4e7-319"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="1c4e7-320">As conexões híbridas conectam a um aplicativo do Azure, como aplicativos Web ou aplicativos móveis no serviço de aplicativo do Azure, recurso de local de tooan que usa uma porta TCP estática, como SQL Server, MySQL, APIs da Web de HTTP e mais serviços da Web personalizados.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-320">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, tooan on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="1c4e7-321">Conexões híbridas são gerenciadas nos Serviços BizTalk no hello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="1c4e7-321">Hybrid Connections are managed in  BizTalk Services in hello Azure classic portal.</span></span>

<span data-ttu-id="1c4e7-322">toocreate conexões híbridas no serviço de aplicativo do Azure, consulte [acessar recursos usando conexões híbridas no serviço de aplicativo do Azure locais](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1c4e7-322">toocreate Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="1c4e7-323">toocreate ou gerenciar conexões híbridas Serviços BizTalk do Azure, consulte [conexões híbridas](integration-hybrid-connection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1c4e7-323">toocreate or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="1c4e7-324">Avançar</span><span class="sxs-lookup"><span data-stu-id="1c4e7-324">Next</span></span>
<span data-ttu-id="1c4e7-325">Agora que você está familiarizado com guias diferentes hello, você pode aprender mais sobre os recursos de Serviços BizTalk do Azure hello:</span><span class="sxs-lookup"><span data-stu-id="1c4e7-325">Now that you're familiar with hello different tabs, you can learn more about hello Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="1c4e7-326">Serviços BizTalk: limitação</span><span class="sxs-lookup"><span data-stu-id="1c4e7-326">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="1c4e7-327">Serviços BizTalk: nome e chave do emissor</span><span class="sxs-lookup"><span data-stu-id="1c4e7-327">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="1c4e7-328">Serviços BizTalk: backup e restauração</span><span class="sxs-lookup"><span data-stu-id="1c4e7-328">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="1c4e7-329">Consulte também</span><span class="sxs-lookup"><span data-stu-id="1c4e7-329">See Also</span></span>
* [<span data-ttu-id="1c4e7-330">Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="1c4e7-330">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="1c4e7-331">Serviços BizTalk: gráfico das edições Developer, Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="1c4e7-331">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="1c4e7-332">Serviços BizTalk: provisionamento usando o portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="1c4e7-332">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="1c4e7-333">Serviços BizTalk: gráfico de estado do Serviço do BizTalk (a página pode estar em inglês)</span><span class="sxs-lookup"><span data-stu-id="1c4e7-333">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="1c4e7-334">Como posso começar a usar Olá SDK dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="1c4e7-334">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

