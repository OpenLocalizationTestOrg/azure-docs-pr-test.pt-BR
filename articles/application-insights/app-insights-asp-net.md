---
title: "aaaSet a análise de aplicativo web do ASP.NET com o Azure Application Insights | Microsoft Docs"
description: "Configurar análise de desempenho, disponibilidade e uso para seu site ASP.NET, hospedado no local ou no Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 61a3cdce68da48bfb9450b1d296acc1535f50a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a><span data-ttu-id="d69cd-103">Configurar o Application Insights para seu site ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d69cd-103">Set up Application Insights for your ASP.NET website</span></span>

<span data-ttu-id="d69cd-104">Este procedimento configura o ASP.NET web aplicativo toosend telemetria toohello [Azure Application Insights](app-insights-overview.md) serviço.</span><span class="sxs-lookup"><span data-stu-id="d69cd-104">This procedure configures your ASP.NET web app toosend telemetry toohello [Azure Application Insights](app-insights-overview.md) service.</span></span> <span data-ttu-id="d69cd-105">Ele funciona para aplicativos ASP.NET que estão hospedados em seu próprio servidor IIS ou na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="d69cd-105">It works for ASP.NET apps that are hosted either in your own IIS server or in hello Cloud.</span></span> <span data-ttu-id="d69cd-106">Obter gráficos e uma linguagem de consulta eficiente que ajudam você entender o desempenho de saudação do aplicativo e quantas pessoas estão usando mais alertas automáticos falhas ou problemas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="d69cd-106">You get charts and a powerful query language that help you understand hello performance of your app and how people are using it, plus automatic alerts on failures or performance issues.</span></span> <span data-ttu-id="d69cd-107">Muitos desenvolvedores consideram esses recursos excelentes como estão, mas você também pode estender e personalizar a telemetria de saudação se for necessário.</span><span class="sxs-lookup"><span data-stu-id="d69cd-107">Many developers find these features great as they are, but you can also extend and customize hello telemetry if you need to.</span></span>

<span data-ttu-id="d69cd-108">A instalação leva apenas alguns cliques no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d69cd-108">Setup takes just a few clicks in Visual Studio.</span></span> <span data-ttu-id="d69cd-109">Você tem encargos de tooavoid opção Olá limitando volume Olá de telemetria.</span><span class="sxs-lookup"><span data-stu-id="d69cd-109">You have hello option tooavoid charges by limiting hello volume of telemetry.</span></span> <span data-ttu-id="d69cd-110">Isso permite que você tooexperiment e depuração ou toomonitor um site com não muitos usuários.</span><span class="sxs-lookup"><span data-stu-id="d69cd-110">This allows you tooexperiment and debug, or toomonitor a site with not many users.</span></span> <span data-ttu-id="d69cd-111">Quando você decidir que deseja toogo em frente e monitorar o seu site de produção, é fácil tooraise limite de hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="d69cd-111">When you decide you want toogo ahead and monitor your production site, it's easy tooraise hello limit later.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="d69cd-112">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="d69cd-112">Before you start</span></span>
<span data-ttu-id="d69cd-113">Você precisa de:</span><span class="sxs-lookup"><span data-stu-id="d69cd-113">You need:</span></span>

* <span data-ttu-id="d69cd-114">Atualização 3 ou mais recente do Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="d69cd-114">Visual Studio 2013 update 3 or later.</span></span> <span data-ttu-id="d69cd-115">Mais tarde é melhor.</span><span class="sxs-lookup"><span data-stu-id="d69cd-115">Later is better.</span></span>
* <span data-ttu-id="d69cd-116">Uma assinatura muito[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="d69cd-116">A subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="d69cd-117">Se sua equipe ou organização tiver uma assinatura do Azure, Olá proprietário pode adicionar você tooit, usando o [conta da Microsoft](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="d69cd-117">If your team or organization has an Azure subscription, hello owner can add you tooit, by using your [Microsoft account](http://live.com).</span></span>

<span data-ttu-id="d69cd-118">Há tópicos alternativo toolook em se você estiver interessado em:</span><span class="sxs-lookup"><span data-stu-id="d69cd-118">There are alternative topics toolook at if you are interested in:</span></span>

* [<span data-ttu-id="d69cd-119">Instrumentar um aplicativo Web em tempo de execução</span><span class="sxs-lookup"><span data-stu-id="d69cd-119">Instrumenting a web app at runtime</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="d69cd-120">Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="d69cd-120">Azure Cloud Services</span></span>](app-insights-cloudservices.md)

## <span data-ttu-id="d69cd-121"><a name="ide"></a>Etapa 1: Adicionar Olá SDK do Application Insights</span><span class="sxs-lookup"><span data-stu-id="d69cd-121"><a name="ide"></a> Step 1: Add hello Application Insights SDK</span></span>

<span data-ttu-id="d69cd-122">Clique com o botão direito do mouse no projeto de aplicativo Web no Gerenciador de Soluções e escolha **Adicionar** > **Application Insights Telemetry...** ou **Configurar o Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="d69cd-122">Right-click your web app project in Solution Explorer, and choose **Add** > **Application Insights Telemetry...** or **Configure Application Insights**.</span></span>

![Captura de tela do Gerenciador de soluções, com adicionar o Application Insights Telemetry realçado](./media/app-insights-asp-net/appinsights-03-addExisting.png)

<span data-ttu-id="d69cd-124">(No Visual Studio 2015, há também uma opção tooadd Application Insights na caixa de diálogo de novo projeto de saudação.)</span><span class="sxs-lookup"><span data-stu-id="d69cd-124">(In Visual Studio 2015, there's also an option tooadd Application Insights in hello New Project dialog.)</span></span>

<span data-ttu-id="d69cd-125">Continue a página de configuração do Application Insights toohello:</span><span class="sxs-lookup"><span data-stu-id="d69cd-125">Continue toohello Application Insights configuration page:</span></span>

![Captura de tela de registrar seu aplicativo com o Application Insights](./media/app-insights-asp-net/visual-studio-register-dialog.png)

<span data-ttu-id="d69cd-127">**a.**</span><span class="sxs-lookup"><span data-stu-id="d69cd-127">**a.**</span></span> <span data-ttu-id="d69cd-128">Selecione a conta de saudação e assinatura que você use tooaccess do Azure.</span><span class="sxs-lookup"><span data-stu-id="d69cd-128">Select hello account and subscription that you use tooaccess Azure.</span></span>

<span data-ttu-id="d69cd-129">**b.**</span><span class="sxs-lookup"><span data-stu-id="d69cd-129">**b.**</span></span> <span data-ttu-id="d69cd-130">Selecione o recurso de saudação do Azure onde deseja que os dados de saudação toosee de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d69cd-130">Select hello resource in Azure where you want toosee hello data from your app.</span></span> <span data-ttu-id="d69cd-131">Normalmente:</span><span class="sxs-lookup"><span data-stu-id="d69cd-131">Usually:</span></span>

* <span data-ttu-id="d69cd-132">Use um [único recurso para diferentes componentes](app-insights-monitor-multi-role-apps.md) de um único aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d69cd-132">Use a [single resource for different components](app-insights-monitor-multi-role-apps.md) of a single application.</span></span> 
* <span data-ttu-id="d69cd-133">Crie recursos separados para aplicativos não relacionados.</span><span class="sxs-lookup"><span data-stu-id="d69cd-133">Create separate resources for unrelated applications.</span></span>
 
<span data-ttu-id="d69cd-134">Se você quiser tooset Olá Olá ou grupo local do recurso em que os dados estão armazenados, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="d69cd-134">If you want tooset hello resource group or hello location where your data is stored, click **Configure settings**.</span></span> <span data-ttu-id="d69cd-135">Grupos de recursos são usados toocontrol toodata de acesso.</span><span class="sxs-lookup"><span data-stu-id="d69cd-135">Resource groups are used toocontrol access toodata.</span></span> <span data-ttu-id="d69cd-136">Por exemplo, se você tiver vários aplicativos que fazem parte do hello mesmo sistema, você pode colocar seus dados do Application Insights hello mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d69cd-136">For example, if you have several apps that form part of hello same system, you might put their Application Insights data in hello same resource group.</span></span>

<span data-ttu-id="d69cd-137">**c.**</span><span class="sxs-lookup"><span data-stu-id="d69cd-137">**c.**</span></span> <span data-ttu-id="d69cd-138">Defina um limite no limite de volume de dados livre hello, tooavoid encargos.</span><span class="sxs-lookup"><span data-stu-id="d69cd-138">Set a cap at hello free data volume limit, tooavoid charges.</span></span> <span data-ttu-id="d69cd-139">O Application Insights é liberar tooa determinados volume de telemetria.</span><span class="sxs-lookup"><span data-stu-id="d69cd-139">Application Insights is free up tooa certain volume of telemetry.</span></span> <span data-ttu-id="d69cd-140">Após Olá recurso for criado, você pode alterar sua seleção no portal de saudação abrindo **recursos + preços** > **gerenciamento do volume de dados** > **diário limite de volume**.</span><span class="sxs-lookup"><span data-stu-id="d69cd-140">After hello resource is created, you can change your selection in hello portal by opening  **Features + pricing** > **Data volume management** > **Daily volume cap**.</span></span>

<span data-ttu-id="d69cd-141">**d.**</span><span class="sxs-lookup"><span data-stu-id="d69cd-141">**d.**</span></span> <span data-ttu-id="d69cd-142">Clique em **registrar** toogo em frente e configurar o Application Insights para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="d69cd-142">Click **Register** toogo ahead and configure Application Insights for your web app.</span></span> <span data-ttu-id="d69cd-143">Telemetria será enviada toohello [portal do Azure](https://portal.azure.com), durante a depuração e depois de publicar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d69cd-143">Telemetry will be sent toohello [Azure portal](https://portal.azure.com), both during debugging and after you have published your app.</span></span>

<span data-ttu-id="d69cd-144">**e.**</span><span class="sxs-lookup"><span data-stu-id="d69cd-144">**e.**</span></span> <span data-ttu-id="d69cd-145">Se você não quiser portal de toohello de telemetria toosend durante a depuração, basta adicionar Olá SDK do Application Insights tooyour aplicativo mas não configurar um recurso no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="d69cd-145">If you don't want toosend telemetry toohello portal while you're debugging, just add hello Application Insights SDK tooyour app but don't configure a resource in hello portal.</span></span> <span data-ttu-id="d69cd-146">Você será capaz de toosee telemetria no Visual Studio enquanto você está depurando.</span><span class="sxs-lookup"><span data-stu-id="d69cd-146">You will be able toosee telemetry in Visual Studio while you are debugging.</span></span> <span data-ttu-id="d69cd-147">Posteriormente, você pode retornar a página de configuração de toothis ou você pode esperar até depois de implantar seu aplicativo e [ative telemetria em tempo de execução](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="d69cd-147">Later, you can return toothis configuration page, or you could wait until after you have deployed your app and [switch on telemetry at run time](app-insights-monitor-performance-live-website-now.md).</span></span>


## <span data-ttu-id="d69cd-148"><a name="run"></a>Etapa 2: Executar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="d69cd-148"><a name="run"></a> Step 2: Run your app</span></span>
<span data-ttu-id="d69cd-149">Execute o aplicativo com F5.</span><span class="sxs-lookup"><span data-stu-id="d69cd-149">Run your app with F5.</span></span> <span data-ttu-id="d69cd-150">Abra páginas diferentes toogenerate alguns telemetria.</span><span class="sxs-lookup"><span data-stu-id="d69cd-150">Open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="d69cd-151">No Visual Studio, você vê uma contagem de eventos de saudação que foram registrados.</span><span class="sxs-lookup"><span data-stu-id="d69cd-151">In Visual Studio, you see a count of hello events that have been logged.</span></span>

![Captura de tela do Visual Studio.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a><span data-ttu-id="d69cd-154">Etapa 3: conferir sua telemetria</span><span class="sxs-lookup"><span data-stu-id="d69cd-154">Step 3: See your telemetry</span></span>
<span data-ttu-id="d69cd-155">Você pode ver sua telemetria no Visual Studio ou no portal de web do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="d69cd-155">You can see your telemetry either in Visual Studio or in hello Application Insights web portal.</span></span> <span data-ttu-id="d69cd-156">Pesquisar telemetria no Visual Studio toohelp depurar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d69cd-156">Search telemetry in Visual Studio toohelp you debug your app.</span></span> <span data-ttu-id="d69cd-157">Monitorar o desempenho e uso no portal da web de saudação quando o sistema está ativo.</span><span class="sxs-lookup"><span data-stu-id="d69cd-157">Monitor performance and usage in hello web portal when your system is live.</span></span> 

### <a name="see-your-telemetry-in-visual-studio"></a><span data-ttu-id="d69cd-158">Confira sua telemetria no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d69cd-158">See your telemetry in Visual Studio</span></span>

<span data-ttu-id="d69cd-159">No Visual Studio, abra a janela do Application Insights Olá.</span><span class="sxs-lookup"><span data-stu-id="d69cd-159">In Visual Studio, open hello Application Insights window.</span></span> <span data-ttu-id="d69cd-160">Clique em Olá **Application Insights** botão ou em seu projeto no Gerenciador de soluções, selecione **Application Insights**e, em seguida, clique em **pesquisa Live telemetria**.</span><span class="sxs-lookup"><span data-stu-id="d69cd-160">Either click hello **Application Insights** button, or right-click your project in Solution Explorer, select **Application Insights**, and then click **Search Live Telemetry**.</span></span>

<span data-ttu-id="d69cd-161">Na janela de pesquisa do Visual Studio Application Insights hello, consulte Olá **dados da sessão de depuração** exibição de telemetria gerada no lado do servidor de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d69cd-161">In hello Visual Studio Application Insights Search window, see hello **Data from Debug session** view for telemetry generated in hello server side of your app.</span></span> <span data-ttu-id="d69cd-162">Fazer experiências com filtros de saudação e clique em qualquer evento toosee mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="d69cd-162">Experiment with hello filters, and click any event toosee more detail.</span></span>

![Captura de tela de saudação de exibição de dados da sessão de depuração na janela do Application Insights hello.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> <span data-ttu-id="d69cd-164">Se você não vir todos os dados, certifique-se de intervalo de tempo de saudação está correto e clique Olá ícone de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d69cd-164">If you don't see any data, make sure hello time range is correct, and click hello Search icon.</span></span>

<span data-ttu-id="d69cd-165">[Saiba mais sobre as ferramentas do Application Insights no Visual Studio](app-insights-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="d69cd-165">[Learn more about Application Insights tools in Visual Studio](app-insights-visual-studio.md).</span></span>

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a><span data-ttu-id="d69cd-166">Conferir telemetria no portal da Web</span><span class="sxs-lookup"><span data-stu-id="d69cd-166">See telemetry in web portal</span></span>

<span data-ttu-id="d69cd-167">Você também pode ver a telemetria no portal de web do Application Insights hello (a menos que você escolheu tooinstall somente Olá SDK).</span><span class="sxs-lookup"><span data-stu-id="d69cd-167">You can also see telemetry in hello Application Insights web portal (unless you chose tooinstall only hello SDK).</span></span> <span data-ttu-id="d69cd-168">portal de saudação tem mais exibições de entre componentes do Visual Studio, ferramentas analíticas e gráficos.</span><span class="sxs-lookup"><span data-stu-id="d69cd-168">hello portal has more charts, analytic tools, and cross-component views than Visual Studio.</span></span> <span data-ttu-id="d69cd-169">portal de saudação também fornece alertas.</span><span class="sxs-lookup"><span data-stu-id="d69cd-169">hello portal also provides alerts.</span></span>

<span data-ttu-id="d69cd-170">Abra seu recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d69cd-170">Open your Application Insights resource.</span></span> <span data-ttu-id="d69cd-171">O entrar toohello [portal do Azure](https://portal.azure.com/) e localize-lo ou projeto de saudação do botão direito do mouse no Visual Studio e permitir que ele levá-lo lá.</span><span class="sxs-lookup"><span data-stu-id="d69cd-171">Either sign in toohello [Azure portal](https://portal.azure.com/) and find it there, or right-click hello project in Visual Studio, and let it take you there.</span></span>

![Captura de tela do Visual Studio, mostrando como tooopen Olá portal do Application Insights](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> <span data-ttu-id="d69cd-173">Se você receber um erro de acesso: você tem mais de um conjunto de credenciais do Microsoft e você tiver entrado com conjunto errado Olá?</span><span class="sxs-lookup"><span data-stu-id="d69cd-173">If you get an access error: Do you have more than one set of Microsoft credentials, and are you signed in with hello wrong set?</span></span> <span data-ttu-id="d69cd-174">No portal de hello, sair e entrar novamente.</span><span class="sxs-lookup"><span data-stu-id="d69cd-174">In hello portal, sign out and sign in again.</span></span>

<span data-ttu-id="d69cd-175">portal de saudação é aberto em uma exibição de telemetria de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d69cd-175">hello portal opens on a view of hello telemetry from your app.</span></span>

![Captura de tela da página de visão geral do Application Insights](./media/app-insights-asp-net/66.png)

<span data-ttu-id="d69cd-177">No portal de hello, clique em qualquer bloco ou gráfico toosee mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="d69cd-177">In hello portal, click any tile or chart toosee more detail.</span></span>

<span data-ttu-id="d69cd-178">[Saiba mais sobre como usar o Application Insights no portal do Azure de saudação](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="d69cd-178">[Learn more about using Application Insights in hello Azure portal](app-insights-dashboards.md).</span></span>

## <a name="step-4-publish-your-app"></a><span data-ttu-id="d69cd-179">Etapa 4: Publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="d69cd-179">Step 4: Publish your app</span></span>
<span data-ttu-id="d69cd-180">Publica seu servidor do IIS do aplicativo tooyour ou tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d69cd-180">Publish your app tooyour IIS server or tooAzure.</span></span> <span data-ttu-id="d69cd-181">Inspecionar [fluxo ao vivo de métricas](app-insights-metrics-explorer.md#live-metrics-stream) toomake-se de que tudo está funcionando normalmente.</span><span class="sxs-lookup"><span data-stu-id="d69cd-181">Watch [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) toomake sure everything is running smoothly.</span></span>

<span data-ttu-id="d69cd-182">A telemetria cria no portal do Application Insights hello, onde você pode monitorar as métricas, pesquisar a telemetria e configurar [painéis](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="d69cd-182">Your telemetry builds up in hello Application Insights portal, where you can monitor metrics, search your telemetry, and set up [dashboards](app-insights-dashboards.md).</span></span> <span data-ttu-id="d69cd-183">Você também pode usar Olá poderoso [linguagem de consulta de análise de Log](https://docs.loganalytics.io/) tooanalyze uso e desempenho ou toofind eventos específicos.</span><span class="sxs-lookup"><span data-stu-id="d69cd-183">You can also use hello powerful [Log Analytics query language](https://docs.loganalytics.io/) tooanalyze usage and performance, or toofind specific events.</span></span>

<span data-ttu-id="d69cd-184">Você também pode continuar tooanalyze sua telemetria em [Visual Studio](app-insights-visual-studio.md), com ferramentas como pesquisa de diagnóstica e [tendências](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="d69cd-184">You can also continue tooanalyze your telemetry in [Visual Studio](app-insights-visual-studio.md), with tools such as diagnostic search and [trends](app-insights-visual-studio-trends.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d69cd-185">Se seu aplicativo envia suficiente Olá tooapproach de telemetria [limitação limites](app-insights-pricing.md#limits-summary)automática [amostragem](app-insights-sampling.md) switches em.</span><span class="sxs-lookup"><span data-stu-id="d69cd-185">If your app sends enough telemetry tooapproach hello [throttling limits](app-insights-pricing.md#limits-summary), automatic [sampling](app-insights-sampling.md) switches on.</span></span> <span data-ttu-id="d69cd-186">Amostragem reduz a quantidade de saudação de telemetria enviada do seu aplicativo, preservando dados correlacionados para fins de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="d69cd-186">Sampling reduces hello quantity of telemetry sent from your app, while preserving correlated data for diagnostic purposes.</span></span>
>
>

## <span data-ttu-id="d69cd-187"><a name="land"></a> Você está pronto</span><span class="sxs-lookup"><span data-stu-id="d69cd-187"><a name="land"></a> You're all set</span></span>

<span data-ttu-id="d69cd-188">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d69cd-188">Congratulations!</span></span> <span data-ttu-id="d69cd-189">Você instalou o pacote do Application Insights Olá em seu aplicativo e ele toosend telemetria toohello Application Insights serviço configurado no Azure.</span><span class="sxs-lookup"><span data-stu-id="d69cd-189">You installed hello Application Insights package in your app, and configured it toosend telemetry toohello Application Insights service on Azure.</span></span>

![Diagrama de movimentação de telemetria](./media/app-insights-asp-net/01-scheme.png)

<span data-ttu-id="d69cd-191">Olá recursos do Azure que recebe a telemetria do aplicativo é identificado por um *chave de instrumentação*.</span><span class="sxs-lookup"><span data-stu-id="d69cd-191">hello Azure resource that receives your app's telemetry is identified by an *instrumentation key*.</span></span> <span data-ttu-id="d69cd-192">Você encontrará esta chave no arquivo applicationinsights. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="d69cd-192">You'll find this key in hello ApplicationInsights.config file.</span></span>


## <a name="upgrade-toofuture-sdk-versions"></a><span data-ttu-id="d69cd-193">Atualizar versões SDK toofuture</span><span class="sxs-lookup"><span data-stu-id="d69cd-193">Upgrade toofuture SDK versions</span></span>
<span data-ttu-id="d69cd-194">tooupgrade tooa [nova versão do SDK do hello](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), abra Olá **Gerenciador de pacotes do NuGet** novamente e o filtro de pacotes instalados.</span><span class="sxs-lookup"><span data-stu-id="d69cd-194">tooupgrade tooa [new release of hello SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), open hello **NuGet package manager** again, and filter on installed packages.</span></span> <span data-ttu-id="d69cd-195">Selecione **Microsoft.ApplicationInsights.Web** e escolha **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="d69cd-195">Select **Microsoft.ApplicationInsights.Web**, and choose **Upgrade**.</span></span>

<span data-ttu-id="d69cd-196">Se você fez tooApplicationInsights.config quaisquer personalizações, salve uma cópia dele antes de atualizar.</span><span class="sxs-lookup"><span data-stu-id="d69cd-196">If you made any customizations tooApplicationInsights.config, save a copy of it before you upgrade.</span></span> <span data-ttu-id="d69cd-197">Em seguida, mescle suas alterações na nova versão de hello.</span><span class="sxs-lookup"><span data-stu-id="d69cd-197">Then, merge your changes into hello new version.</span></span>

## <a name="video"></a><span data-ttu-id="d69cd-198">Vídeo</span><span class="sxs-lookup"><span data-stu-id="d69cd-198">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="d69cd-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d69cd-199">Next steps</span></span>

### <a name="more-telemetry"></a><span data-ttu-id="d69cd-200">Mais telemetria</span><span class="sxs-lookup"><span data-stu-id="d69cd-200">More telemetry</span></span>

* <span data-ttu-id="d69cd-201">**[Navegador e página carregam dados](app-insights-javascript.md)**  -insira um trecho de código em suas páginas da Web.</span><span class="sxs-lookup"><span data-stu-id="d69cd-201">**[Browser and page load data](app-insights-javascript.md)** - Insert a code snippet in your web pages.</span></span>
* <span data-ttu-id="d69cd-202">**[Obtenha monitoramento de dependência e de exceção mais detalhado](app-insights-monitor-performance-live-website-now.md)**  -instale o Monitor de Status no seu servidor.</span><span class="sxs-lookup"><span data-stu-id="d69cd-202">**[Get more detailed dependency and exception monitoring](app-insights-monitor-performance-live-website-now.md)** - Install Status Monitor on your server.</span></span>
* <span data-ttu-id="d69cd-203">**[Eventos personalizados de código](app-insights-api-custom-events-metrics.md)**  toocount, hora ou medir a ações do usuário.</span><span class="sxs-lookup"><span data-stu-id="d69cd-203">**[Code custom events](app-insights-api-custom-events-metrics.md)** toocount, time, or measure user actions.</span></span>
* <span data-ttu-id="d69cd-204">**[Obter dados de log](app-insights-asp-net-trace-logs.md)**  - correlacionar dados de log com a telemetria.</span><span class="sxs-lookup"><span data-stu-id="d69cd-204">**[Get log data](app-insights-asp-net-trace-logs.md)** - Correlate log data with your telemetry.</span></span>

### <a name="analysis"></a><span data-ttu-id="d69cd-205">Análise</span><span class="sxs-lookup"><span data-stu-id="d69cd-205">Analysis</span></span>

* <span data-ttu-id="d69cd-206">**[Trabalhar com o Application Insights no Visual Studio](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="d69cd-206">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="d69cd-207">Inclui informações sobre como depurar com a telemetria, pesquisa de diagnóstica e drill-through toocode.</span><span class="sxs-lookup"><span data-stu-id="d69cd-207">Includes information about debugging with telemetry, diagnostic search, and drill through toocode.</span></span>
* <span data-ttu-id="d69cd-208">**[Trabalhando com o portal do Application Insights Olá](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="d69cd-208">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/> <span data-ttu-id="d69cd-209">Inclui informações sobre painéis, poderosas ferramentas de diagnóstico e análise, alertas, um mapa de dependências em tempo real de seu aplicativo e a exportação de telemetria.</span><span class="sxs-lookup"><span data-stu-id="d69cd-209">Includes information about dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span>
* <span data-ttu-id="d69cd-210">**[Análise de](app-insights-analytics-tour.md)**  -Olá poderosa linguagem de consulta.</span><span class="sxs-lookup"><span data-stu-id="d69cd-210">**[Analytics](app-insights-analytics-tour.md)** - hello powerful query language.</span></span>

### <a name="alerts"></a><span data-ttu-id="d69cd-211">Alertas</span><span class="sxs-lookup"><span data-stu-id="d69cd-211">Alerts</span></span>

* <span data-ttu-id="d69cd-212">[Testes de disponibilidade](app-insights-monitor-web-app-availability.md): criar testes toomake se seu site está visível na web hello.</span><span class="sxs-lookup"><span data-stu-id="d69cd-212">[Availability tests](app-insights-monitor-web-app-availability.md): Create tests toomake sure your site is visible on hello web.</span></span>
* <span data-ttu-id="d69cd-213">[Inteligente diagnóstico](app-insights-proactive-diagnostics.md): esses testes são executados automaticamente, para que você não tenha toodo nada tooset-los para cima.</span><span class="sxs-lookup"><span data-stu-id="d69cd-213">[Smart diagnostics](app-insights-proactive-diagnostics.md): These tests run automatically, so you don't have toodo anything tooset them up.</span></span> <span data-ttu-id="d69cd-214">Eles informam se o aplicativo tem uma taxa incomum de solicitações com falha.</span><span class="sxs-lookup"><span data-stu-id="d69cd-214">They tell you if your app has an unusual rate of failed requests.</span></span>
* <span data-ttu-id="d69cd-215">[Alertas de métrica](app-insights-alerts.md): definir esses toowarn se uma métrica exceder um limite.</span><span class="sxs-lookup"><span data-stu-id="d69cd-215">[Metric alerts](app-insights-alerts.md): Set these toowarn you if a metric crosses a threshold.</span></span> <span data-ttu-id="d69cd-216">Você pode defini-los em métricas personalizadas que você codifica em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d69cd-216">You can set them on custom metrics that you code into your app.</span></span>

### <a name="automation"></a><span data-ttu-id="d69cd-217">Automação</span><span class="sxs-lookup"><span data-stu-id="d69cd-217">Automation</span></span>

* [<span data-ttu-id="d69cd-218">Automatizar a criação de um recurso adicional do Application Insights</span><span class="sxs-lookup"><span data-stu-id="d69cd-218">Automate creating an Application Insights resource</span></span>](app-insights-powershell.md)
