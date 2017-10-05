---
title: Microsoft Dynamics CRM e Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: a9593d5f198e05db80451a599428a296ed02e781
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="c2ce1-104">Passo a passo: Ativar a telemetria para o Microsoft Dynamics CRM Online usando o Application Insights</span><span class="sxs-lookup"><span data-stu-id="c2ce1-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="c2ce1-105">Este artigo mostra como obter dados de telemetria no [Microsoft Dynamics CRM Online](https://www.dynamics.com/) usando o [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="c2ce1-105">This article shows you how to get telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="c2ce1-106">Percorreremos o processo completo de adição de um script do Application Insights ao seu aplicativo, captura de dados e visualização de dados.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-106">We’ll walk through the complete process of adding Application Insights script to your application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="c2ce1-107">[Procurar a solução de exemplo](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="c2ce1-107">[Browse the sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-to-new-or-existing-crm-online-instance"></a><span data-ttu-id="c2ce1-108">Adicionar o Application Insights a uma instância nova ou existente do CRM Online</span><span class="sxs-lookup"><span data-stu-id="c2ce1-108">Add Application Insights to new or existing CRM Online instance</span></span>
<span data-ttu-id="c2ce1-109">Para monitorar seu aplicativo, você adiciona um SDK do Application Insights a ele.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-109">To monitor your application, you add an Application Insights SDK to your application.</span></span> <span data-ttu-id="c2ce1-110">O SDK envia a telemetria para o [Portal do Application Insights](https://portal.azure.com), no qual você pode usar nossas potentes ferramentas de análise e diagnóstico ou exportar os dados para o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-110">The SDK sends telemetry to the [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export the data to storage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="c2ce1-111">Criar um recurso do Application Insights no Azure</span><span class="sxs-lookup"><span data-stu-id="c2ce1-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="c2ce1-112">Obtenha [uma conta no Microsoft Azure](http://azure.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="c2ce1-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="c2ce1-113">Entre no [Portal do Azure](https://portal.azure.com) e adicione um novo recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-113">Sign into the [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="c2ce1-114">Este é o local em que os dados serão processados e exibidos.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-114">This is where your data will be processed and displayed.</span></span>
   
    ![Clique em +, Serviços de Desenvolvedor, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="c2ce1-116">Escolha ASP.NET como o tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-116">Choose ASP.NET as the application type.</span></span>
3. <span data-ttu-id="c2ce1-117">Abra a página de Introdução e abra "Monitorar e diagnosticar aplicativos do lado do cliente".</span><span class="sxs-lookup"><span data-stu-id="c2ce1-117">Open the Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![Trecho de código para inserção na sua página da Web](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="c2ce1-119">**Mantenha a página de código aberta** enquanto realiza a próxima etapa na outra janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-119">**Keep the code page open** while you do the next step in another browser window.</span></span> <span data-ttu-id="c2ce1-120">Você precisará do código em breve.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-120">You'll need the code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="c2ce1-121">Criar um recurso da Web em JavaScript no Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="c2ce1-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="c2ce1-122">Abra sua instância do CRM Online e faça logon com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="c2ce1-123">Abra o Microsoft Dynamics CRM Configurações, Personalizações, Personalizar o Sistema</span><span class="sxs-lookup"><span data-stu-id="c2ce1-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize the System</span></span>
   
    ![Configurações do Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Configurações > Personalizações](./media/app-insights-sample-mscrm/05.png)

    ![Personalizar a opção do sistema](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="c2ce1-127">Crie um recurso de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-127">Create a JavaScript resource.</span></span>
   
    ![Caixa de diálogo Novo Recurso da Web](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="c2ce1-129">Atribua um nome, selecione **Script (JScript)** e abra o editor de texto.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-129">Give it a name, select **Script (JScript)** and open the text editor.</span></span>
   
    ![Abrir o editor de texto](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="c2ce1-131">Copie o código do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-131">Copy the code from Application Insights.</span></span> <span data-ttu-id="c2ce1-132">Ao copiar, certifique-se de ignorar marcas de script.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-132">While copying make sure to ignore script tags.</span></span> <span data-ttu-id="c2ce1-133">Consulte a captura de tela abaixo:</span><span class="sxs-lookup"><span data-stu-id="c2ce1-133">Refer below screenshot:</span></span>
   
    ![Configurar sua chave de instrumentação](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="c2ce1-135">O código inclui a chave de instrumentação que identifica seu recurso do Application insights.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-135">The code includes the instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="c2ce1-136">Salve e publique.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-136">Save and publish.</span></span>
   
    ![Salvar e publicar](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="c2ce1-138">Formulários de instrumento</span><span class="sxs-lookup"><span data-stu-id="c2ce1-138">Instrument Forms</span></span>
1. <span data-ttu-id="c2ce1-139">No Microsoft CRM Online, abra o formulário Conta</span><span class="sxs-lookup"><span data-stu-id="c2ce1-139">In Microsoft CRM Online, open the Account form</span></span>
   
    ![Formulário da Conta](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="c2ce1-141">Abra as propriedades do formulário</span><span class="sxs-lookup"><span data-stu-id="c2ce1-141">Open the form Properties</span></span>
   
    ![Propriedades do formulário](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="c2ce1-143">Adicione o recurso da Web de JavaScript que você criou</span><span class="sxs-lookup"><span data-stu-id="c2ce1-143">Add the JavaScript web resource that you created</span></span>
   
    ![Adicionar menu](./media/app-insights-sample-mscrm/13.png)
   
    ![Adicionar recurso da Web](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="c2ce1-146">Salve e publique as personalizações do formulário.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="c2ce1-147">Métricas capturadas</span><span class="sxs-lookup"><span data-stu-id="c2ce1-147">Metrics captured</span></span>
<span data-ttu-id="c2ce1-148">Agora você configurou a captura de telemetria do formulário.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-148">You have now set up telemetry capture for the form.</span></span> <span data-ttu-id="c2ce1-149">Sempre que ele for usado, os dados serão enviados ao recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-149">Whenever it is used, data will be sent to your Application Insights resource.</span></span>

<span data-ttu-id="c2ce1-150">Aqui estão exemplos dos dados que você verá.</span><span class="sxs-lookup"><span data-stu-id="c2ce1-150">Here are samples of the data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="c2ce1-151">Integridade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="c2ce1-151">Application health</span></span>
![Tempo de carregamento de página de exemplo](./media/app-insights-sample-mscrm/15.png)

![Gráfico de exibições de página de exemplo](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="c2ce1-154">Exceções de navegador:</span><span class="sxs-lookup"><span data-stu-id="c2ce1-154">Browser exceptions:</span></span>

![Gráfico de exceções de navegador](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="c2ce1-156">Clique no gráfico para obter mais detalhes:</span><span class="sxs-lookup"><span data-stu-id="c2ce1-156">Click the chart to get more detail:</span></span>

![Lista de exceções](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="c2ce1-158">Uso</span><span class="sxs-lookup"><span data-stu-id="c2ce1-158">Usage</span></span>
![Usuários, seções e exibição de página](./media/app-insights-sample-mscrm/19.png)

![Gráficos de sessão](./media/app-insights-sample-mscrm/20.png)

![Versões do navegador](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="c2ce1-162">Navegadores</span><span class="sxs-lookup"><span data-stu-id="c2ce1-162">Browsers</span></span>
![Divisão de tempo de carregamento de página](./media/app-insights-sample-mscrm/22.png)

![Contagem de sessões por versão do navegador](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="c2ce1-165">Geolocalização</span><span class="sxs-lookup"><span data-stu-id="c2ce1-165">Geolocation</span></span>
![Contagem de sessões por país](./media/app-insights-sample-mscrm/24.png)

![Sessões e usuários por país](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="c2ce1-168">Solicitação de exibição de página interna</span><span class="sxs-lookup"><span data-stu-id="c2ce1-168">Inside page view request</span></span>
![Resumo de exibição de página](./media/app-insights-sample-mscrm/26.png)

![Pesquisar em eventos de exibição de página](./media/app-insights-sample-mscrm/27.png)

![Exibições de páginas semelhantes](./media/app-insights-sample-mscrm/28.png)

![Propriedades de exibição de página](./media/app-insights-sample-mscrm/29.png)

![Páginas por sessão](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="c2ce1-174">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="c2ce1-174">Sample code</span></span>
<span data-ttu-id="c2ce1-175">[Procurar no código de amostra](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="c2ce1-175">[Browse the sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="c2ce1-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="c2ce1-176">Power BI</span></span>
<span data-ttu-id="c2ce1-177">Você pode fazer análises ainda mais profundas se [exportar os dados para o Microsoft Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="c2ce1-177">You can do even deeper analysis if you [export the data to Microsoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="c2ce1-178">Exemplo de Solução para o Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="c2ce1-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="c2ce1-179">[Veja a solução do exemplo implementada no Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="c2ce1-179">[Here is the sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="c2ce1-180">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="c2ce1-180">Learn more</span></span>
* [<span data-ttu-id="c2ce1-181">O que é o Application Insights?</span><span class="sxs-lookup"><span data-stu-id="c2ce1-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="c2ce1-182">Application Insights para páginas da Web</span><span class="sxs-lookup"><span data-stu-id="c2ce1-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="c2ce1-183">Mais exemplos e explicações passo a passo</span><span class="sxs-lookup"><span data-stu-id="c2ce1-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
