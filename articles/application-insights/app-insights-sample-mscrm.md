---
title: "aaaMicrosoft Dynamics CRM e informações de aplicativo do Azure | Microsoft Docs"
description: "Obtenha a telemetria do Microsoft Dynamics CRM Online usando o Application Insights. Passo a passo da instalação, obtenção de dados, visualização e exportação."
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="ee947-104">Passo a passo: Ativar a telemetria para o Microsoft Dynamics CRM Online usando o Application Insights</span><span class="sxs-lookup"><span data-stu-id="ee947-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="ee947-105">Este artigo mostra como os dados de telemetria tooget do [Microsoft Dynamics CRM Online](https://www.dynamics.com/) usando [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="ee947-105">This article shows you how tooget telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="ee947-106">Vamos examinar o processo completo de saudação de adicionar Application Insights script tooyour aplicativo, a captura de dados e visualização de dados.</span><span class="sxs-lookup"><span data-stu-id="ee947-106">We’ll walk through hello complete process of adding Application Insights script tooyour application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="ee947-107">[Procurar a solução de exemplo hello](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="ee947-107">[Browse hello sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a><span data-ttu-id="ee947-108">Adicionar Application Insights toonew ou instância do CRM Online</span><span class="sxs-lookup"><span data-stu-id="ee947-108">Add Application Insights toonew or existing CRM Online instance</span></span>
<span data-ttu-id="ee947-109">toomonitor seu aplicativo, você adiciona um aplicativo de tooyour do SDK do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ee947-109">toomonitor your application, you add an Application Insights SDK tooyour application.</span></span> <span data-ttu-id="ee947-110">Olá SDK envia telemetria toohello [portal do Application Insights](https://portal.azure.com), onde você pode usar nossa análise avançada e ferramentas de diagnóstico ou exportar Olá toostorage de dados.</span><span class="sxs-lookup"><span data-stu-id="ee947-110">hello SDK sends telemetry toohello [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export hello data toostorage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="ee947-111">Criar um recurso do Application Insights no Azure</span><span class="sxs-lookup"><span data-stu-id="ee947-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="ee947-112">Obtenha [uma conta no Microsoft Azure](http://azure.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="ee947-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="ee947-113">O logon no hello [portal do Azure](https://portal.azure.com) e adicionar um novo recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ee947-113">Sign into hello [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="ee947-114">Este é o local em que os dados serão processados e exibidos.</span><span class="sxs-lookup"><span data-stu-id="ee947-114">This is where your data will be processed and displayed.</span></span>
   
    ![Clique em +, Serviços de Desenvolvedor, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="ee947-116">Escolha o ASP.NET como o tipo de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ee947-116">Choose ASP.NET as hello application type.</span></span>
3. <span data-ttu-id="ee947-117">Abra a página de introdução de saudação e "Monitor e o diagnóstico do lado do cliente".</span><span class="sxs-lookup"><span data-stu-id="ee947-117">Open hello Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![Trecho de código para inserção na sua página da Web](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="ee947-119">**Manter a página de código Olá aberta** enquanto Olá próxima etapa em outra janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="ee947-119">**Keep hello code page open** while you do hello next step in another browser window.</span></span> <span data-ttu-id="ee947-120">Você precisará código Olá em breve.</span><span class="sxs-lookup"><span data-stu-id="ee947-120">You'll need hello code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="ee947-121">Criar um recurso da Web em JavaScript no Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="ee947-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="ee947-122">Abra sua instância do CRM Online e faça logon com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="ee947-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="ee947-123">Abra o Microsoft Dynamics CRM configurações, as personalizações, personalizar Olá sistema</span><span class="sxs-lookup"><span data-stu-id="ee947-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize hello System</span></span>
   
    ![Configurações do Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Configurações > Personalizações](./media/app-insights-sample-mscrm/05.png)

    ![Personalizar a opção de saudação do sistema](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="ee947-127">Crie um recurso de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ee947-127">Create a JavaScript resource.</span></span>
   
    ![Caixa de diálogo Novo Recurso da Web](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="ee947-129">Dê a ele um nome, selecione **Script (JScript)** e Olá abrir editor de texto.</span><span class="sxs-lookup"><span data-stu-id="ee947-129">Give it a name, select **Script (JScript)** and open hello text editor.</span></span>
   
    ![Editor de texto de saudação aberto](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="ee947-131">Copie o código de saudação do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ee947-131">Copy hello code from Application Insights.</span></span> <span data-ttu-id="ee947-132">Ao copiar Verifique tooignore certeza de marcas de script.</span><span class="sxs-lookup"><span data-stu-id="ee947-132">While copying make sure tooignore script tags.</span></span> <span data-ttu-id="ee947-133">Consulte a captura de tela abaixo:</span><span class="sxs-lookup"><span data-stu-id="ee947-133">Refer below screenshot:</span></span>
   
    ![Configurar sua chave de instrumentação](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="ee947-135">código de saudação inclui a chave de instrumentação Olá que identifica o recurso do Application insights.</span><span class="sxs-lookup"><span data-stu-id="ee947-135">hello code includes hello instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="ee947-136">Salve e publique.</span><span class="sxs-lookup"><span data-stu-id="ee947-136">Save and publish.</span></span>
   
    ![Salvar e publicar](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="ee947-138">Formulários de instrumento</span><span class="sxs-lookup"><span data-stu-id="ee947-138">Instrument Forms</span></span>
1. <span data-ttu-id="ee947-139">No Microsoft CRM Online, abra o formulário de conta de saudação</span><span class="sxs-lookup"><span data-stu-id="ee947-139">In Microsoft CRM Online, open hello Account form</span></span>
   
    ![Formulário da Conta](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="ee947-141">Abrir o formulário de saudação propriedades</span><span class="sxs-lookup"><span data-stu-id="ee947-141">Open hello form Properties</span></span>
   
    ![Propriedades do formulário](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="ee947-143">Adicionar Olá recurso da web de JavaScript que você criou</span><span class="sxs-lookup"><span data-stu-id="ee947-143">Add hello JavaScript web resource that you created</span></span>
   
    ![Adicionar menu](./media/app-insights-sample-mscrm/13.png)
   
    ![Adicionar recurso da web de saudação](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="ee947-146">Salve e publique as personalizações do formulário.</span><span class="sxs-lookup"><span data-stu-id="ee947-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="ee947-147">Métricas capturadas</span><span class="sxs-lookup"><span data-stu-id="ee947-147">Metrics captured</span></span>
<span data-ttu-id="ee947-148">Você já configurou a captura de telemetria para o formulário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee947-148">You have now set up telemetry capture for hello form.</span></span> <span data-ttu-id="ee947-149">Sempre que for usado, dados serão enviados recurso do Application Insights tooyour.</span><span class="sxs-lookup"><span data-stu-id="ee947-149">Whenever it is used, data will be sent tooyour Application Insights resource.</span></span>

<span data-ttu-id="ee947-150">Aqui estão exemplos de dados de saudação que você verá.</span><span class="sxs-lookup"><span data-stu-id="ee947-150">Here are samples of hello data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="ee947-151">Integridade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="ee947-151">Application health</span></span>
![Tempo de carregamento de página de exemplo](./media/app-insights-sample-mscrm/15.png)

![Gráfico de exibições de página de exemplo](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="ee947-154">Exceções de navegador:</span><span class="sxs-lookup"><span data-stu-id="ee947-154">Browser exceptions:</span></span>

![Gráfico de exceções de navegador](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="ee947-156">Clique em Olá gráfico tooget mais detalhes:</span><span class="sxs-lookup"><span data-stu-id="ee947-156">Click hello chart tooget more detail:</span></span>

![Lista de exceções](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="ee947-158">Uso</span><span class="sxs-lookup"><span data-stu-id="ee947-158">Usage</span></span>
![Usuários, seções e exibição de página](./media/app-insights-sample-mscrm/19.png)

![Gráficos de sessão](./media/app-insights-sample-mscrm/20.png)

![Versões do navegador](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="ee947-162">Navegadores</span><span class="sxs-lookup"><span data-stu-id="ee947-162">Browsers</span></span>
![Divisão de tempo de carregamento de página](./media/app-insights-sample-mscrm/22.png)

![Contagem de sessões por versão do navegador](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="ee947-165">Geolocalização</span><span class="sxs-lookup"><span data-stu-id="ee947-165">Geolocation</span></span>
![Contagem de sessões por país](./media/app-insights-sample-mscrm/24.png)

![Sessões e usuários por país](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="ee947-168">Solicitação de exibição de página interna</span><span class="sxs-lookup"><span data-stu-id="ee947-168">Inside page view request</span></span>
![Resumo de exibição de página](./media/app-insights-sample-mscrm/26.png)

![Pesquisar em eventos de exibição de página](./media/app-insights-sample-mscrm/27.png)

![Exibições de páginas semelhantes](./media/app-insights-sample-mscrm/28.png)

![Propriedades de exibição de página](./media/app-insights-sample-mscrm/29.png)

![Páginas por sessão](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="ee947-174">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="ee947-174">Sample code</span></span>
<span data-ttu-id="ee947-175">[Procurar o código de exemplo hello](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="ee947-175">[Browse hello sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="ee947-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="ee947-176">Power BI</span></span>
<span data-ttu-id="ee947-177">Você pode fazer uma análise mais profunda mesmo se você [exportar Olá dados tooMicrosoft Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="ee947-177">You can do even deeper analysis if you [export hello data tooMicrosoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="ee947-178">Exemplo de Solução para o Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="ee947-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="ee947-179">[Aqui está a solução de exemplo hello implementada no Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="ee947-179">[Here is hello sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="ee947-180">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="ee947-180">Learn more</span></span>
* [<span data-ttu-id="ee947-181">O que é o Application Insights?</span><span class="sxs-lookup"><span data-stu-id="ee947-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="ee947-182">Application Insights para páginas da Web</span><span class="sxs-lookup"><span data-stu-id="ee947-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="ee947-183">Mais exemplos e explicações passo a passo</span><span class="sxs-lookup"><span data-stu-id="ee947-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
