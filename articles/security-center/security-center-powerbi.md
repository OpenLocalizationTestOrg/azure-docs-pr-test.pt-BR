---
title: "Obter percepções de dados da Central de Segurança do Azure com o Power BI | Microsoft Docs"
description: "O pacote de conteúdo do Power BI da Central de Segurança do Azure facilita a localização de alertas de segurança, recomendações, recursos atacados e tendências, com base em um conjunto de dados que foi criado para o relatório."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 0ded6bc7-52e8-43b4-8940-0bee137526e3
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: 10f7b8f20cc41a5ebb1b1376e2bf17be02600ae4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-insights-from-azure-security-center-data-with-power-bi"></a><span data-ttu-id="2de7e-103">Obtenha percepções de dados da Central de Segurança do Azure com o Power BI</span><span class="sxs-lookup"><span data-stu-id="2de7e-103">Get insights from Azure Security Center data with Power BI</span></span>
<span data-ttu-id="2de7e-104">O [Painel do Power BI](http://aka.ms/azure-security-center-power-bi) para a Central de Segurança do Azure o habilita a visualizar, analisar e filtrar recomendações e alertas de segurança de qualquer lugar, incluindo seu dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="2de7e-104">The [Power BI Dashboard](http://aka.ms/azure-security-center-power-bi) for Azure Security Center enables you to visualize, analyze, and filter recommendations and security alerts from anywhere, including your mobile device.</span></span> <span data-ttu-id="2de7e-105">Use o painel do Power BI para revelar tendências e padrões, exibir alertas de segurança por recurso ou endereço IP de origem e riscos de segurança não tratados por recurso ou idade.</span><span class="sxs-lookup"><span data-stu-id="2de7e-105">Use the Power BI dashboard to reveal trends and attack patterns - view security alerts by resource or source IP address and unaddressed security risks by resource or age.</span></span>

<span data-ttu-id="2de7e-106">Você também pode combinar recomendações e alertas de segurança do Security Center com outros dados de maneiras interessantes, por exemplo, usando dados dos [Logs de auditoria do Azure](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) e da [Auditoria do Banco de Dados SQL do Azure](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="2de7e-106">You can also mash up Security Center recommendations and security alerts with other data in interesting ways, for example using data from [Azure Audit Logs](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) and [Azure SQL Database Auditing](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/).</span></span> <span data-ttu-id="2de7e-107">Ambos oferecem Painéis do Power BI, e você também pode exportar esses dados para o Excel para produzir relatórios facilmente sobre o estado de segurança de seus recursos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="2de7e-107">Both offer Power BI Dashboards, and you can also export this data to Excel for easy reporting on the security state of your cloud resources.</span></span>

## <a name="using-azure-security-center-dashboard-to-access-power-bi"></a><span data-ttu-id="2de7e-108">Como usar o painel da Central de Segurança do Azure para acessar o Power BI</span><span class="sxs-lookup"><span data-stu-id="2de7e-108">Using Azure Security Center dashboard to access Power BI</span></span>
<span data-ttu-id="2de7e-109">Você também pode usar o painel da Central de Segurança do Azure para acessar relatórios do Power BI.</span><span class="sxs-lookup"><span data-stu-id="2de7e-109">You can also use the Azure Security Center dashboard to access Power BI reports.</span></span> <span data-ttu-id="2de7e-110">Siga as etapas abaixo para executar esta tarefa:</span><span class="sxs-lookup"><span data-stu-id="2de7e-110">Follow the steps to perform this task:</span></span>

1. <span data-ttu-id="2de7e-111">No painel **Central de Segurança do Azure**, clique no botão **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="2de7e-111">In the **Azure Security Center** dashboard, click **Power BI** button.</span></span>

    ![Conectar-se a Central de Segurança do Azure usando o Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-1-newUI-2017.png)
2. <span data-ttu-id="2de7e-113">A folha **Power BI** será aberta no lado direito, como mostrado na tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="2de7e-113">The **Power BI** blade opens on the right side as shown in the following screen:</span></span>

    ![Conectar-se a Central de Segurança do Azure usando o Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new11-2017.png)
3. <span data-ttu-id="2de7e-115">Se você estiver criando o painel do Power BI pela primeira vez, poderá escolher uma das seguintes opções na folha **Explorar no Power BI** :</span><span class="sxs-lookup"><span data-stu-id="2de7e-115">If you are creating the Power BI dashboard for the first time, you can choose one of the following options in the **Explore in Power BI** blade:</span></span>

   * <span data-ttu-id="2de7e-116">**Painel de informações da segurança**: escolha essa opção se você quiser criar um painel que inclua o status de segurança, threads e detecções.</span><span class="sxs-lookup"><span data-stu-id="2de7e-116">**Security insights dashboard**: choose this option if you want to create a dashboard that includes security status, threads, and detections.</span></span> <span data-ttu-id="2de7e-117">Esta opção é a mais comum para a função DevOps responsável pela análise de seu status de proteção e alertas detectados nas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="2de7e-117">This option is a more common for DevOps role that is responsible for analyzing their protection status and detected alerts across subscriptions.</span></span>
   * <span data-ttu-id="2de7e-118">**Painel de gerenciamento da política**: escolha essa opção se você quiser explorar o gerenciamento e a imposição da política.</span><span class="sxs-lookup"><span data-stu-id="2de7e-118">**Policy management dashboard**: choose this option if you want to explore management and enforcement policy.</span></span>  <span data-ttu-id="2de7e-119">Esta opção é a mais comum para a TI Central, que está mais focada na governança.</span><span class="sxs-lookup"><span data-stu-id="2de7e-119">This option is a more common for Central IT who are more focused on governance.</span></span> <span data-ttu-id="2de7e-120">Ela pode usar esse painel para ganhar visibilidade e ter ideias sobre a conformidade da política de segurança em toda a organização.</span><span class="sxs-lookup"><span data-stu-id="2de7e-120">They can use this dashboard to gain visibility and insights on security policy adherence across their organization.</span></span>
   * <span data-ttu-id="2de7e-121">Se você já tiver um painel do Power BI, clique em **Ir para o painel do Power BI atual**.</span><span class="sxs-lookup"><span data-stu-id="2de7e-121">If you already have a Power BI dashboard, click **Go to your current Power BI dashboard**.</span></span>
4. <span data-ttu-id="2de7e-122">Neste exemplo, clique na opção **Painel de informações de segurança** .</span><span class="sxs-lookup"><span data-stu-id="2de7e-122">For this example, click **Security insights dashboard** option.</span></span> <span data-ttu-id="2de7e-123">Se esta for a primeira vez que você estiver criando um painel do Power BI para a Central de Segurança, será solicitada a instalação do pacote de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="2de7e-123">If this is the first time, you are creating a Power BI dashboard for Security Center you are prompted to install the content pack.</span></span> <span data-ttu-id="2de7e-124">Clique no botão **Obter** na janela **Pacotes de conteúdo do Power BI** como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="2de7e-124">Click **Get** button in the **Content packs for Power BI** window as shown in the following screen:</span></span>

    ![Painel de Informações de Segurança da Central de Segurança do Azure](./media/security-center-powerbi/security-center-powerbi-fig1-new3.png)
5. <span data-ttu-id="2de7e-126">A janela **Conectar ao Azure Security Center Security Insights** é exibida.</span><span class="sxs-lookup"><span data-stu-id="2de7e-126">The **Connect to Azure Security Center Security Insights** window appear.</span></span> <span data-ttu-id="2de7e-127">Verifique se o Método de **autenticação** é **oAuth2**, como mostrado abaixo, e clique no botão **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="2de7e-127">Make sure the **Authentication** method is **oAuth2** as shown below and click **Sign in** button.</span></span>

    ![Autenticação](./media/security-center-powerbi/security-center-powerbi-fig1-new4.png)
6. <span data-ttu-id="2de7e-129">Você pode ser solicitado a autenticar novamente com suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="2de7e-129">You may be asked to authenticate again with your Azure credentials.</span></span> <span data-ttu-id="2de7e-130">Depois de autenticar, seu painel será criado.</span><span class="sxs-lookup"><span data-stu-id="2de7e-130">After authenticating your dashboard will be created.</span></span> <span data-ttu-id="2de7e-131">Depois de criar o painel, você verá um relatório com uma estrutura semelhante à mostrada na tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="2de7e-131">Once the dashboard is created you see a report with the similar structure as shown in the following screen:</span></span>

    ![Painel do Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new5.png)

> [!NOTE]
> <span data-ttu-id="2de7e-133">Uma atualização do relatório é agendada para ocorrer diariamente.</span><span class="sxs-lookup"><span data-stu-id="2de7e-133">A refresh of the report is scheduled to take place on a daily basis.</span></span> <span data-ttu-id="2de7e-134">Se houver uma falha dessa atualização, leia [Possíveis problemas de atualização com o Power BI da Central de Segurança do Azure](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/)para saber mais sobre como solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="2de7e-134">In case you experience a failure on this refresh, read [Potential Refresh Issues with the Azure Security Center Power BI](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), for more information on how to troubleshoot.</span></span>
>
>

<span data-ttu-id="2de7e-135">Aqui, você pode ver o número de alertas de segurança e recomendações, além do número de VMs, bancos de dados SQL do Azure e recursos da rede que estão sendo monitorados pela Central de Segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="2de7e-135">Here you can see the number of security alerts and recommendations, as well as the number of VMs, Azure SQL databases, and network resources being monitored by Azure Security Center.</span></span>

<span data-ttu-id="2de7e-136">Um link para a Central de Segurança do Azure o redirecionará para o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2de7e-136">A link to Azure Security Center redirects you to the Azure portal.</span></span> <span data-ttu-id="2de7e-137">Os gráficos facilitam a visualização de informações sobre recomendações de segurança e alertas, incluindo:</span><span class="sxs-lookup"><span data-stu-id="2de7e-137">The charts make it easy to visualize information about security recommendations and alerts, including:</span></span>

* <span data-ttu-id="2de7e-138">Estado da Segurança de Recursos</span><span class="sxs-lookup"><span data-stu-id="2de7e-138">Resource Security State</span></span>
* <span data-ttu-id="2de7e-139">Recomendações Pendentes</span><span class="sxs-lookup"><span data-stu-id="2de7e-139">Pending Recommendations</span></span>
* <span data-ttu-id="2de7e-140">Recomendações de VM</span><span class="sxs-lookup"><span data-stu-id="2de7e-140">VM Recommendations</span></span>
* <span data-ttu-id="2de7e-141">Alertas ao Longo do Tempo</span><span class="sxs-lookup"><span data-stu-id="2de7e-141">Alerts over Time</span></span>
* <span data-ttu-id="2de7e-142">Recursos Atacados</span><span class="sxs-lookup"><span data-stu-id="2de7e-142">Attacked Resources</span></span>
* <span data-ttu-id="2de7e-143">IPs Atacados</span><span class="sxs-lookup"><span data-stu-id="2de7e-143">Attacked IPs</span></span>

<span data-ttu-id="2de7e-144">Por trás de cada gráfico, há percepções adicionais.</span><span class="sxs-lookup"><span data-stu-id="2de7e-144">Behind each chart, there are additional insights.</span></span> <span data-ttu-id="2de7e-145">Selecione um bloco para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="2de7e-145">Select a tile to see more information.</span></span> <span data-ttu-id="2de7e-146">Por exemplo, o bloco **Estado de Segurança do Recurso** mostra detalhes adicionais sobre as recomendações pendentes pelos recursos, como mostrado na tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="2de7e-146">For example, the **Resource Security State** tile shows you additional details about pending recommendations by resources as shown in the following screen:</span></span>

![Recomendações](./media/security-center-powerbi/security-center-powerbi-fig1-new6.png)

<span data-ttu-id="2de7e-148">Se você clicar em qualquer linha do gráfico, as outras ficarão acinzentadas e você focará apenas na selecionada.</span><span class="sxs-lookup"><span data-stu-id="2de7e-148">If you click on any line of this graph, the others are going to gray out and you focus only on the one you selected.</span></span> <span data-ttu-id="2de7e-149">Para retornar ao painel, clique em **Central de Segurança do Azure** na opção **Painéis** no painel esquerdo dessa página.</span><span class="sxs-lookup"><span data-stu-id="2de7e-149">To return to the dashboard, click **Azure Security Center** under the **Dashboards** option on the left pane of this page.</span></span>

> [!NOTE]
> <span data-ttu-id="2de7e-150">Se você quiser personalizar seus relatórios adicionando campos extras ou alterando os visuais existentes, poderá editar o relatório.</span><span class="sxs-lookup"><span data-stu-id="2de7e-150">If you’d like to customize your reports by adding additional fields or changing existing visuals, you can edit the report.</span></span> <span data-ttu-id="2de7e-151">Leia [Interagir com um relatório no Modo de Edição no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="2de7e-151">Read [Interact with a report in Editing View in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) for more information.</span></span>
>
>

<span data-ttu-id="2de7e-152">Os blocos **Alertas ao Longo do Tempo, Recursos Atacados** e **IPs do Invasor** terão resultados semelhante ao clicar em cada um deles.</span><span class="sxs-lookup"><span data-stu-id="2de7e-152">The **Alerts over Time, Attacked Resources** and **Attacker IPs** tiles will have the similar output when you click on each one of it.</span></span> <span data-ttu-id="2de7e-153">Isso ocorre porque o relatório agrega informações sobre essas três variáveis e chama-as de **Recursos sob Ataque** , como mostrado na tela abaixo:</span><span class="sxs-lookup"><span data-stu-id="2de7e-153">This happens because the report aggregates information regarding all those three variables and calls it **Resources under Attack** as shown in the following screen:</span></span>

![Recursos sob Ataque](./media/security-center-powerbi/security-center-powerbi-fig1-new7.png)

<span data-ttu-id="2de7e-155">Nesse ponto, você pode também salvar uma cópia do relatório, imprimi-lo ou publicá-lo na Web usando as opções disponíveis no menu **Arquivo** .</span><span class="sxs-lookup"><span data-stu-id="2de7e-155">At this point you can also save a copy of this report, print it or publish it on the web by using the options available in the **File** menu.</span></span>

![Menu Arquivo](./media/security-center-powerbi/security-center-powerbi-fig8.png)

## <a name="exploring-your-azure-security-center-data-with-power-bi-services"></a><span data-ttu-id="2de7e-157">Como explorar seus dados da Central de Segurança do Azure com serviços do Power BI</span><span class="sxs-lookup"><span data-stu-id="2de7e-157">Exploring your Azure Security Center data with Power BI services</span></span>
<span data-ttu-id="2de7e-158">Conecte os [Serviços do Pacote de Conteúdo do Power BI](https://msit.powerbi.com/groups/me/getdata/services) no Power BI e siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2de7e-158">Connect to the [Power BI Content Pack Services](https://msit.powerbi.com/groups/me/getdata/services) in Power BI and execute the following steps:</span></span>

1. <span data-ttu-id="2de7e-159">Na janela **Pacote de Conteúdo do Power BI** , você verá duas opções, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="2de7e-159">In the **Content Pack for Power BI** window you will see two options as shown below.</span></span>

    ![Pacote de Conteúdo do Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new.png)

   > [!NOTE]
   > <span data-ttu-id="2de7e-161">Se já executou a primeira parte deste artigo, você verá somente uma opção, o que é Gerenciamento de Política da Central de Segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="2de7e-161">If already executed the first part of this article you will see only one option, which is Azure Security Center Policy Management.</span></span>
   >
   >
2. <span data-ttu-id="2de7e-162">Para este exemplo, clique em **Obter** no bloco **Gerenciamento de Política da Central de Segurança do Azure**.</span><span class="sxs-lookup"><span data-stu-id="2de7e-162">For the purpose of this example, click **Get** in the **Azure Security Center Policy Management** tile.</span></span>
3. <span data-ttu-id="2de7e-163">Na janela **Conectar Gerenciamento de Política da Central de Segurança do Azure**, selecione **oAuth2** no menu suspenso **Método de Autenticação**, como mostrado abaixo e clique no botão **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="2de7e-163">In the **Connect to Azure Security Center Policy Management** window, make sure to select **oAuth2** under **Authentication Method** drop down as shown below and click **Sign in** button.</span></span>

    ![Janela de Gerenciamento de Política](./media/security-center-powerbi/security-center-powerbi-fig1-new8.png)
4. <span data-ttu-id="2de7e-165">Você será redirecionado para uma página de autenticação, na qual deverá digitar as credenciais que está usando para conectar a Central de Segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="2de7e-165">You will be redirected to an authentication page where you should type the credentials that you are using to connect to Azure Security Center.</span></span> <span data-ttu-id="2de7e-166">Após o processo de autenticação ser concluído, o Power BI iniciará a importação dos dados para criar seus relatórios.</span><span class="sxs-lookup"><span data-stu-id="2de7e-166">After the authentication process is complete, Power BI will start importing data to build your reports.</span></span> <span data-ttu-id="2de7e-167">Durante esse período, você verá a seguinte mensagem no canto direito do navegador:</span><span class="sxs-lookup"><span data-stu-id="2de7e-167">During this time you may see the following message on the right corner of your browser:</span></span>

    ![Conectar-se a Central de Segurança do Azure usando o Power BI](./media/security-center-powerbi/security-center-powerbi-fig4.png)

   > [!NOTE]
   > <span data-ttu-id="2de7e-169">Quando o painel estiver sendo criado pela primeira vez, isso poderá demorar um pouco mais, principalmente para os cenários nos quais você tem várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="2de7e-169">when the dashboard is being created for the first time it can take longer than usual, mainly for scenarios where you have multiple subscriptions.</span></span>
   >
   >
5. <span data-ttu-id="2de7e-170">Com o processo concluído, o painel Power BI da Central de Segurança do Azure carregará o relatório **Gerenciamento de Política** semelhante ao mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="2de7e-170">Once the process is finished, your Azure Security Center Power BI dashboard will load with the **Policy Management** report similar to the one shown below:</span></span>

    ![Painel de gerenciamento da política](./media/security-center-powerbi/security-center-powerbi-fig1-new9.png)

## <a name="see-also"></a><span data-ttu-id="2de7e-172">Confira também</span><span class="sxs-lookup"><span data-stu-id="2de7e-172">See also</span></span>
<span data-ttu-id="2de7e-173">Neste documento, você aprendeu a usar o Power BI na Central de Segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="2de7e-173">In this document, you learned how to use Power BI in Azure Security Center.</span></span> <span data-ttu-id="2de7e-174">Para saber mais sobre a Central de Segurança do Azure, veja o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2de7e-174">To learn more about Azure Security Center, see the following:</span></span>

* <span data-ttu-id="2de7e-175">[Guia de Operações e Planejamento da Central de Segurança do Azure](security-center-planning-and-operations-guide.md) : saiba como planejar a adoção da Central de Segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="2de7e-175">[Azure Security Center Planning and Operations Guide](security-center-planning-and-operations-guide.md) — Learn how to plan Azure Security Center adoption.</span></span>
* <span data-ttu-id="2de7e-176">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md) : saiba como configurar políticas de segurança na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="2de7e-176">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security settings in Azure Security Center</span></span>
* <span data-ttu-id="2de7e-177">[Gerenciando e respondendo aos alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) : aprenda a gerenciar e responder aos alertas de segurança</span><span class="sxs-lookup"><span data-stu-id="2de7e-177">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts</span></span>
* <span data-ttu-id="2de7e-178">[Perguntas frequentes da Central de Segurança do Azure](security-center-faq.md) : encontre as perguntas frequentes sobre como usar o serviço</span><span class="sxs-lookup"><span data-stu-id="2de7e-178">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service</span></span>
* <span data-ttu-id="2de7e-179">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre postagens no blog sobre conformidade e segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="2de7e-179">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance</span></span>
