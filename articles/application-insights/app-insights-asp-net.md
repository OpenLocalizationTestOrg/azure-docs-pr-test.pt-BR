---
title: "Configurar análise de aplicativo Web do ASP.NET com o Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: cb247ee68da88265f7c51258644064463d44f8b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a><span data-ttu-id="909b1-103">Configurar o Application Insights para seu site ASP.NET</span><span class="sxs-lookup"><span data-stu-id="909b1-103">Set up Application Insights for your ASP.NET website</span></span>

<span data-ttu-id="909b1-104">Este procedimento configura seu aplicativo da Web ASP.NET para enviar telemetria para o serviço [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="909b1-104">This procedure configures your ASP.NET web app to send telemetry to the [Azure Application Insights](app-insights-overview.md) service.</span></span> <span data-ttu-id="909b1-105">Ele funciona para aplicativos ASP.NET hospedados em seu próprio servidor IIS ou na nuvem.</span><span class="sxs-lookup"><span data-stu-id="909b1-105">It works for ASP.NET apps that are hosted either in your own IIS server or in the Cloud.</span></span> <span data-ttu-id="909b1-106">Você obtém gráficos e uma linguagem de consulta eficiente que ajudarão a compreender o desempenho de seu aplicativo e como as pessoas estão usando-o, além de alertas automáticos sobre falhas ou problemas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="909b1-106">You get charts and a powerful query language that help you understand the performance of your app and how people are using it, plus automatic alerts on failures or performance issues.</span></span> <span data-ttu-id="909b1-107">Muitos desenvolvedores acham esses recursos excelentes como estão, mas você também pode estender e personalizar a telemetria se for necessário.</span><span class="sxs-lookup"><span data-stu-id="909b1-107">Many developers find these features great as they are, but you can also extend and customize the telemetry if you need to.</span></span>

<span data-ttu-id="909b1-108">A instalação leva apenas alguns cliques no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="909b1-108">Setup takes just a few clicks in Visual Studio.</span></span> <span data-ttu-id="909b1-109">Você tem a opção de evitar cobranças limitando o volume de telemetria.</span><span class="sxs-lookup"><span data-stu-id="909b1-109">You have the option to avoid charges by limiting the volume of telemetry.</span></span> <span data-ttu-id="909b1-110">Isso permite testar e depurar ou monitorar um site com poucos usuários.</span><span class="sxs-lookup"><span data-stu-id="909b1-110">This allows you to experiment and debug, or to monitor a site with not many users.</span></span> <span data-ttu-id="909b1-111">Quando você decidir que deseja prosseguir e monitorar seu site de produção, é fácil aumentar o limite mais tarde.</span><span class="sxs-lookup"><span data-stu-id="909b1-111">When you decide you want to go ahead and monitor your production site, it's easy to raise the limit later.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="909b1-112">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="909b1-112">Before you start</span></span>
<span data-ttu-id="909b1-113">Você precisa de:</span><span class="sxs-lookup"><span data-stu-id="909b1-113">You need:</span></span>

* <span data-ttu-id="909b1-114">Atualização 3 ou mais recente do Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="909b1-114">Visual Studio 2013 update 3 or later.</span></span> <span data-ttu-id="909b1-115">Mais tarde é melhor.</span><span class="sxs-lookup"><span data-stu-id="909b1-115">Later is better.</span></span>
* <span data-ttu-id="909b1-116">Uma assinatura do [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="909b1-116">A subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="909b1-117">Se sua equipe ou organização tem uma assinatura do Azure, o proprietário pode adicioná-lo a ela, usando sua [conta da Microsoft](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="909b1-117">If your team or organization has an Azure subscription, the owner can add you to it, by using your [Microsoft account](http://live.com).</span></span>

<span data-ttu-id="909b1-118">Há tópicos alternativos para conferir se você está interessado em:</span><span class="sxs-lookup"><span data-stu-id="909b1-118">There are alternative topics to look at if you are interested in:</span></span>

* [<span data-ttu-id="909b1-119">Instrumentar um aplicativo Web em tempo de execução</span><span class="sxs-lookup"><span data-stu-id="909b1-119">Instrumenting a web app at runtime</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="909b1-120">Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="909b1-120">Azure Cloud Services</span></span>](app-insights-cloudservices.md)

## <span data-ttu-id="909b1-121"><a name="ide"></a>Etapa 1: Adicionar o SDK do Application Insights</span><span class="sxs-lookup"><span data-stu-id="909b1-121"><a name="ide"></a> Step 1: Add the Application Insights SDK</span></span>

<span data-ttu-id="909b1-122">Clique com o botão direito do mouse no projeto de aplicativo Web no Gerenciador de Soluções e escolha **Adicionar** > **Application Insights Telemetry...** ou **Configurar o Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="909b1-122">Right-click your web app project in Solution Explorer, and choose **Add** > **Application Insights Telemetry...** or **Configure Application Insights**.</span></span>

![Captura de tela do Gerenciador de soluções, com adicionar o Application Insights Telemetry realçado](./media/app-insights-asp-net/appinsights-03-addExisting.png)

<span data-ttu-id="909b1-124">(No Visual Studio 2015, há também uma opção adicioná-lo na caixa de diálogo Novo projeto.)</span><span class="sxs-lookup"><span data-stu-id="909b1-124">(In Visual Studio 2015, there's also an option to add Application Insights in the New Project dialog.)</span></span>

<span data-ttu-id="909b1-125">Ir para a página de configuração do Application Insights:</span><span class="sxs-lookup"><span data-stu-id="909b1-125">Continue to the Application Insights configuration page:</span></span>

![Captura de tela de registrar seu aplicativo com o Application Insights](./media/app-insights-asp-net/visual-studio-register-dialog.png)

<span data-ttu-id="909b1-127">**a.**</span><span class="sxs-lookup"><span data-stu-id="909b1-127">**a.**</span></span> <span data-ttu-id="909b1-128">Selecione a conta e assinatura que você usa para acessar o Azure.</span><span class="sxs-lookup"><span data-stu-id="909b1-128">Select the account and subscription that you use to access Azure.</span></span>

<span data-ttu-id="909b1-129">**b.**</span><span class="sxs-lookup"><span data-stu-id="909b1-129">**b.**</span></span> <span data-ttu-id="909b1-130">Selecione o recurso no Azure onde você deseja ver os dados do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="909b1-130">Select the resource in Azure where you want to see the data from your app.</span></span> <span data-ttu-id="909b1-131">Normalmente:</span><span class="sxs-lookup"><span data-stu-id="909b1-131">Usually:</span></span>

* <span data-ttu-id="909b1-132">Use um [único recurso para diferentes componentes](app-insights-monitor-multi-role-apps.md) de um único aplicativo.</span><span class="sxs-lookup"><span data-stu-id="909b1-132">Use a [single resource for different components](app-insights-monitor-multi-role-apps.md) of a single application.</span></span> 
* <span data-ttu-id="909b1-133">Crie recursos separados para aplicativos não relacionados.</span><span class="sxs-lookup"><span data-stu-id="909b1-133">Create separate resources for unrelated applications.</span></span>
 
<span data-ttu-id="909b1-134">Se você deseja definir o grupo de recursos ou o local onde os dados estão armazenado, clique **configurações**.</span><span class="sxs-lookup"><span data-stu-id="909b1-134">If you want to set the resource group or the location where your data is stored, click **Configure settings**.</span></span> <span data-ttu-id="909b1-135">Grupos de recursos são usados para controlar o acesso aos dados.</span><span class="sxs-lookup"><span data-stu-id="909b1-135">Resource groups are used to control access to data.</span></span> <span data-ttu-id="909b1-136">Por exemplo, se você tiver vários aplicativos que fazem parte do mesmo sistema, você pode colocar seus dados do Application Insights no mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="909b1-136">For example, if you have several apps that form part of the same system, you might put their Application Insights data in the same resource group.</span></span>

<span data-ttu-id="909b1-137">**c.**</span><span class="sxs-lookup"><span data-stu-id="909b1-137">**c.**</span></span> <span data-ttu-id="909b1-138">Defina um limite no limite de volume de dados gratuito para evitar cobranças.</span><span class="sxs-lookup"><span data-stu-id="909b1-138">Set a cap at the free data volume limit, to avoid charges.</span></span> <span data-ttu-id="909b1-139">O Application Insights está gratuitos até um determinado volume de telemetria.</span><span class="sxs-lookup"><span data-stu-id="909b1-139">Application Insights is free up to a certain volume of telemetry.</span></span> <span data-ttu-id="909b1-140">Depois que o recurso for criado, você pode alterar sua seleção no portal abrindo **Recursos + preços** > **Gerenciamento do volume de dados** > **Limite diário de volume**.</span><span class="sxs-lookup"><span data-stu-id="909b1-140">After the resource is created, you can change your selection in the portal by opening  **Features + pricing** > **Data volume management** > **Daily volume cap**.</span></span>

<span data-ttu-id="909b1-141">**d.**</span><span class="sxs-lookup"><span data-stu-id="909b1-141">**d.**</span></span> <span data-ttu-id="909b1-142">Clique em **registrar** vá em frente e configurar o Application Insights para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="909b1-142">Click **Register** to go ahead and configure Application Insights for your web app.</span></span> <span data-ttu-id="909b1-143">Telemetria será enviada para o [portal do Azure](https://portal.azure.com), durante a depuração e depois de ter publicado seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="909b1-143">Telemetry will be sent to the [Azure portal](https://portal.azure.com), both during debugging and after you have published your app.</span></span>

<span data-ttu-id="909b1-144">**e.**</span><span class="sxs-lookup"><span data-stu-id="909b1-144">**e.**</span></span> <span data-ttu-id="909b1-145">Se você não quiser enviar telemetria para o portal durante a depuração, adicione o SDK do Application Insights ao seu aplicativo, mas não configure um recurso no portal.</span><span class="sxs-lookup"><span data-stu-id="909b1-145">If you don't want to send telemetry to the portal while you're debugging, just add the Application Insights SDK to your app but don't configure a resource in the portal.</span></span> <span data-ttu-id="909b1-146">Você poderá ver a telemetria no Visual Studio enquanto você está depurando.</span><span class="sxs-lookup"><span data-stu-id="909b1-146">You will be able to see telemetry in Visual Studio while you are debugging.</span></span> <span data-ttu-id="909b1-147">Posteriormente, você pode retornar a esta página de configuração, ou você poderia esperar até depois de implantar seu aplicativo e [ative telemetria em tempo de execução](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="909b1-147">Later, you can return to this configuration page, or you could wait until after you have deployed your app and [switch on telemetry at run time](app-insights-monitor-performance-live-website-now.md).</span></span>


## <span data-ttu-id="909b1-148"><a name="run"></a>Etapa 2: Executar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="909b1-148"><a name="run"></a> Step 2: Run your app</span></span>
<span data-ttu-id="909b1-149">Execute o aplicativo com F5.</span><span class="sxs-lookup"><span data-stu-id="909b1-149">Run your app with F5.</span></span> <span data-ttu-id="909b1-150">Abra páginas diferentes para gerar alguma telemetria.</span><span class="sxs-lookup"><span data-stu-id="909b1-150">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="909b1-151">No Visual Studio, você vê uma contagem dos eventos que foram registrados.</span><span class="sxs-lookup"><span data-stu-id="909b1-151">In Visual Studio, you see a count of the events that have been logged.</span></span>

![Captura de tela do Visual Studio.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a><span data-ttu-id="909b1-154">Etapa 3: conferir sua telemetria</span><span class="sxs-lookup"><span data-stu-id="909b1-154">Step 3: See your telemetry</span></span>
<span data-ttu-id="909b1-155">Você pode ver sua telemetria no Visual Studio ou no portal da web Application Insights.</span><span class="sxs-lookup"><span data-stu-id="909b1-155">You can see your telemetry either in Visual Studio or in the Application Insights web portal.</span></span> <span data-ttu-id="909b1-156">Pesquise a telemetria no Visual Studio para ajudá-lo a depurar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="909b1-156">Search telemetry in Visual Studio to help you debug your app.</span></span> <span data-ttu-id="909b1-157">Monitore o desempenho e o uso no portal da Web quando o sistema estiver ativo.</span><span class="sxs-lookup"><span data-stu-id="909b1-157">Monitor performance and usage in the web portal when your system is live.</span></span> 

### <a name="see-your-telemetry-in-visual-studio"></a><span data-ttu-id="909b1-158">Confira sua telemetria no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="909b1-158">See your telemetry in Visual Studio</span></span>

<span data-ttu-id="909b1-159">No Visual Studio, abra a janela do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="909b1-159">In Visual Studio, open the Application Insights window.</span></span> <span data-ttu-id="909b1-160">Clique no botão **Application Insights** ou clique com o botão direito do mouse em seu projeto no Gerenciador de Soluções, selecione **Application Insights** e clique em **Pesquisar Telemetria Dinâmica**.</span><span class="sxs-lookup"><span data-stu-id="909b1-160">Either click the **Application Insights** button, or right-click your project in Solution Explorer, select **Application Insights**, and then click **Search Live Telemetry**.</span></span>

<span data-ttu-id="909b1-161">Na janela de pesquisa do Application Insights do Visual Studio, consulte o **dados da sessão de depuração** exibição de telemetria gerada no lado do servidor de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="909b1-161">In the Visual Studio Application Insights Search window, see the **Data from Debug session** view for telemetry generated in the server side of your app.</span></span> <span data-ttu-id="909b1-162">Experimente os filtros e clique em qualquer evento para ver mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="909b1-162">Experiment with the filters, and click any event to see more detail.</span></span>

![Captura de tela dos dados da exibição da sessão de depuração na janela do Application Insights.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> <span data-ttu-id="909b1-164">Caso você não veja os dados, verifique se o intervalo de tempo está correto e clique no ícone Pesquisa.</span><span class="sxs-lookup"><span data-stu-id="909b1-164">If you don't see any data, make sure the time range is correct, and click the Search icon.</span></span>

<span data-ttu-id="909b1-165">[Saiba mais sobre as ferramentas do Application Insights no Visual Studio](app-insights-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="909b1-165">[Learn more about Application Insights tools in Visual Studio](app-insights-visual-studio.md).</span></span>

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a><span data-ttu-id="909b1-166">Conferir telemetria no portal da Web</span><span class="sxs-lookup"><span data-stu-id="909b1-166">See telemetry in web portal</span></span>

<span data-ttu-id="909b1-167">Você também pode ver a telemetria no portal da Web do Application Insights (a menos que você opte por instalar somente o SDK).</span><span class="sxs-lookup"><span data-stu-id="909b1-167">You can also see telemetry in the Application Insights web portal (unless you chose to install only the SDK).</span></span> <span data-ttu-id="909b1-168">O portal tem mais gráficos, ferramentas analíticas e modos de exibição entre componentes do que o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="909b1-168">The portal has more charts, analytic tools, and cross-component views than Visual Studio.</span></span> <span data-ttu-id="909b1-169">O portal também fornece alertas.</span><span class="sxs-lookup"><span data-stu-id="909b1-169">The portal also provides alerts.</span></span>

<span data-ttu-id="909b1-170">Abra seu recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="909b1-170">Open your Application Insights resource.</span></span> <span data-ttu-id="909b1-171">Entre no [portal do Azure](https://portal.azure.com/) e localize-o ou clique com o botão direito do mouse no projeto no Visual Studio e deixe que ele o leve até lá.</span><span class="sxs-lookup"><span data-stu-id="909b1-171">Either sign in to the [Azure portal](https://portal.azure.com/) and find it there, or right-click the project in Visual Studio, and let it take you there.</span></span>

![Captura de tela do Visual Studio, mostrando como abrir o portal do Application Insights](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> <span data-ttu-id="909b1-173">Se você receber um erro de acesso: você tem mais de um conjunto de credenciais da Microsoft e você está conectado com o conjunto errado?</span><span class="sxs-lookup"><span data-stu-id="909b1-173">If you get an access error: Do you have more than one set of Microsoft credentials, and are you signed in with the wrong set?</span></span> <span data-ttu-id="909b1-174">No portal, saia e entre novamente.</span><span class="sxs-lookup"><span data-stu-id="909b1-174">In the portal, sign out and sign in again.</span></span>

<span data-ttu-id="909b1-175">O portal é aberto em uma exibição da telemetria do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="909b1-175">The portal opens on a view of the telemetry from your app.</span></span>

![Captura de tela da página de visão geral do Application Insights](./media/app-insights-asp-net/66.png)

<span data-ttu-id="909b1-177">No portal, clique em qualquer bloco ou gráfico para ver mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="909b1-177">In the portal, click any tile or chart to see more detail.</span></span>

<span data-ttu-id="909b1-178">[Saiba mais sobre como usar o Application Insights no portal do Azure](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="909b1-178">[Learn more about using Application Insights in the Azure portal](app-insights-dashboards.md).</span></span>

## <a name="step-4-publish-your-app"></a><span data-ttu-id="909b1-179">Etapa 4: Publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="909b1-179">Step 4: Publish your app</span></span>
<span data-ttu-id="909b1-180">Publica seu aplicativo no servidor IIS ou no Azure.</span><span class="sxs-lookup"><span data-stu-id="909b1-180">Publish your app to your IIS server or to Azure.</span></span> <span data-ttu-id="909b1-181">Observe o [Fluxo de Métricas Ativo](app-insights-metrics-explorer.md#live-metrics-stream) para verificar se tudo está funcionando corretamente.</span><span class="sxs-lookup"><span data-stu-id="909b1-181">Watch [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) to make sure everything is running smoothly.</span></span>

<span data-ttu-id="909b1-182">A telemetria se acumula no portal do Application Insights, em que você pode monitorar as métricas, pesquisar a telemetria e configurar [painéis](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="909b1-182">Your telemetry builds up in the Application Insights portal, where you can monitor metrics, search your telemetry, and set up [dashboards](app-insights-dashboards.md).</span></span> <span data-ttu-id="909b1-183">Você também pode usar a poderosa [linguagem de consulta do Log Analytics](https://docs.loganalytics.io/) para analisar o uso e o desempenho ou para encontrar eventos específicos.</span><span class="sxs-lookup"><span data-stu-id="909b1-183">You can also use the powerful [Log Analytics query language](https://docs.loganalytics.io/) to analyze usage and performance, or to find specific events.</span></span>

<span data-ttu-id="909b1-184">Você também pode continuar a analisar a telemetria no [Visual Studio](app-insights-visual-studio.md) com ferramentas como pesquisa de diagnóstico e de [tendências](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="909b1-184">You can also continue to analyze your telemetry in [Visual Studio](app-insights-visual-studio.md), with tools such as diagnostic search and [trends](app-insights-visual-studio-trends.md).</span></span>

> [!NOTE]
> <span data-ttu-id="909b1-185">Se seu aplicativo enviar telemetria suficiente para se aproximar das [limitações](app-insights-pricing.md#limits-summary), a [amostragem](app-insights-sampling.md) automática será ativada.</span><span class="sxs-lookup"><span data-stu-id="909b1-185">If your app sends enough telemetry to approach the [throttling limits](app-insights-pricing.md#limits-summary), automatic [sampling](app-insights-sampling.md) switches on.</span></span> <span data-ttu-id="909b1-186">A amostragem reduz a quantidade de telemetria enviada do seu aplicativo, preservando dados correlacionados para fins de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="909b1-186">Sampling reduces the quantity of telemetry sent from your app, while preserving correlated data for diagnostic purposes.</span></span>
>
>

## <span data-ttu-id="909b1-187"><a name="land"></a> Você está pronto</span><span class="sxs-lookup"><span data-stu-id="909b1-187"><a name="land"></a> You're all set</span></span>

<span data-ttu-id="909b1-188">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="909b1-188">Congratulations!</span></span> <span data-ttu-id="909b1-189">Você instalou o pacote do Application Insights em seu aplicativo e o configurou para enviar telemetria para o serviço Application Insights no Azure.</span><span class="sxs-lookup"><span data-stu-id="909b1-189">You installed the Application Insights package in your app, and configured it to send telemetry to the Application Insights service on Azure.</span></span>

![Diagrama de movimentação de telemetria](./media/app-insights-asp-net/01-scheme.png)

<span data-ttu-id="909b1-191">O recurso do Azure que recebe a telemetria do seu aplicativo é identificado por uma *chave de instrumentação*.</span><span class="sxs-lookup"><span data-stu-id="909b1-191">The Azure resource that receives your app's telemetry is identified by an *instrumentation key*.</span></span> <span data-ttu-id="909b1-192">Você encontrará essa chave no arquivo applicationinsights.config.</span><span class="sxs-lookup"><span data-stu-id="909b1-192">You'll find this key in the ApplicationInsights.config file.</span></span>


## <a name="upgrade-to-future-sdk-versions"></a><span data-ttu-id="909b1-193">Atualizar para versões futuras do SDK</span><span class="sxs-lookup"><span data-stu-id="909b1-193">Upgrade to future SDK versions</span></span>
<span data-ttu-id="909b1-194">Para atualizar para uma [nova versão do SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), abra o **gerenciador de pacotes do NuGet** novamente e filtre os pacotes instalados.</span><span class="sxs-lookup"><span data-stu-id="909b1-194">To upgrade to a [new release of the SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), open the **NuGet package manager** again, and filter on installed packages.</span></span> <span data-ttu-id="909b1-195">Selecione **Microsoft.ApplicationInsights.Web** e escolha **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="909b1-195">Select **Microsoft.ApplicationInsights.Web**, and choose **Upgrade**.</span></span>

<span data-ttu-id="909b1-196">Se você fez todas as personalizações no ApplicationInsights.config, salve uma cópia dele antes de atualizar.</span><span class="sxs-lookup"><span data-stu-id="909b1-196">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade.</span></span> <span data-ttu-id="909b1-197">Em seguida, mescle suas alterações para a nova versão.</span><span class="sxs-lookup"><span data-stu-id="909b1-197">Then, merge your changes into the new version.</span></span>

## <a name="video"></a><span data-ttu-id="909b1-198">Vídeo</span><span class="sxs-lookup"><span data-stu-id="909b1-198">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="909b1-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="909b1-199">Next steps</span></span>

### <a name="more-telemetry"></a><span data-ttu-id="909b1-200">Mais telemetria</span><span class="sxs-lookup"><span data-stu-id="909b1-200">More telemetry</span></span>

* <span data-ttu-id="909b1-201">**[Navegador e página carregam dados](app-insights-javascript.md)**  -insira um trecho de código em suas páginas da Web.</span><span class="sxs-lookup"><span data-stu-id="909b1-201">**[Browser and page load data](app-insights-javascript.md)** - Insert a code snippet in your web pages.</span></span>
* <span data-ttu-id="909b1-202">**[Obtenha monitoramento de dependência e de exceção mais detalhado](app-insights-monitor-performance-live-website-now.md)**  -instale o Monitor de Status no seu servidor.</span><span class="sxs-lookup"><span data-stu-id="909b1-202">**[Get more detailed dependency and exception monitoring](app-insights-monitor-performance-live-website-now.md)** - Install Status Monitor on your server.</span></span>
* <span data-ttu-id="909b1-203">**[Eventos personalizados de código](app-insights-api-custom-events-metrics.md)** para contagem, tempo ou medição de ações do usuário.</span><span class="sxs-lookup"><span data-stu-id="909b1-203">**[Code custom events](app-insights-api-custom-events-metrics.md)** to count, time, or measure user actions.</span></span>
* <span data-ttu-id="909b1-204">**[Obter dados de log](app-insights-asp-net-trace-logs.md)**  - correlacionar dados de log com a telemetria.</span><span class="sxs-lookup"><span data-stu-id="909b1-204">**[Get log data](app-insights-asp-net-trace-logs.md)** - Correlate log data with your telemetry.</span></span>

### <a name="analysis"></a><span data-ttu-id="909b1-205">Análise</span><span class="sxs-lookup"><span data-stu-id="909b1-205">Analysis</span></span>

* <span data-ttu-id="909b1-206">**[Trabalhar com o Application Insights no Visual Studio](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="909b1-206">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="909b1-207">Inclui informações sobre a depuração de telemetria, pesquisa de diagnóstico e análise por meio de código.</span><span class="sxs-lookup"><span data-stu-id="909b1-207">Includes information about debugging with telemetry, diagnostic search, and drill through to code.</span></span>
* <span data-ttu-id="909b1-208">**[Trabalhando com o portal do Application Insights](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="909b1-208">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/> <span data-ttu-id="909b1-209">Inclui informações sobre painéis, poderosas ferramentas de diagnóstico e análise, alertas, um mapa de dependências em tempo real de seu aplicativo e a exportação de telemetria.</span><span class="sxs-lookup"><span data-stu-id="909b1-209">Includes information about dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span>
* <span data-ttu-id="909b1-210">**[Analytics](app-insights-analytics-tour.md)** - a linguagem de consulta poderosa.</span><span class="sxs-lookup"><span data-stu-id="909b1-210">**[Analytics](app-insights-analytics-tour.md)** - The powerful query language.</span></span>

### <a name="alerts"></a><span data-ttu-id="909b1-211">Alertas</span><span class="sxs-lookup"><span data-stu-id="909b1-211">Alerts</span></span>

* <span data-ttu-id="909b1-212">[Testes de disponibilidade](app-insights-monitor-web-app-availability.md): criar testes para verificar se seu site está visível na web.</span><span class="sxs-lookup"><span data-stu-id="909b1-212">[Availability tests](app-insights-monitor-web-app-availability.md): Create tests to make sure your site is visible on the web.</span></span>
* <span data-ttu-id="909b1-213">[Inteligente diagnóstico](app-insights-proactive-diagnostics.md): esses testes são executados automaticamente, portanto você não precisa fazer nada para configurá-los.</span><span class="sxs-lookup"><span data-stu-id="909b1-213">[Smart diagnostics](app-insights-proactive-diagnostics.md): These tests run automatically, so you don't have to do anything to set them up.</span></span> <span data-ttu-id="909b1-214">Eles informam se o aplicativo tem uma taxa incomum de solicitações com falha.</span><span class="sxs-lookup"><span data-stu-id="909b1-214">They tell you if your app has an unusual rate of failed requests.</span></span>
* <span data-ttu-id="909b1-215">[Alertas de métrica](app-insights-alerts.md): defina-os para avisar se uma métrica ultrapassar um limite.</span><span class="sxs-lookup"><span data-stu-id="909b1-215">[Metric alerts](app-insights-alerts.md): Set these to warn you if a metric crosses a threshold.</span></span> <span data-ttu-id="909b1-216">Você pode defini-los em métricas personalizadas que você codifica em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="909b1-216">You can set them on custom metrics that you code into your app.</span></span>

### <a name="automation"></a><span data-ttu-id="909b1-217">Automação</span><span class="sxs-lookup"><span data-stu-id="909b1-217">Automation</span></span>

* [<span data-ttu-id="909b1-218">Automatizar a criação de um recurso adicional do Application Insights</span><span class="sxs-lookup"><span data-stu-id="909b1-218">Automate creating an Application Insights resource</span></span>](app-insights-powershell.md)
