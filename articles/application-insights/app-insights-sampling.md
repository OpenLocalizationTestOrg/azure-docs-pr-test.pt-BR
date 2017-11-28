---
title: amostragem aaaTelemetry no Azure Application Insights | Microsoft Docs
description: "Como tookeep Olá volume de telemetria sob controle."
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="fb501-103">Amostragem no Application Insights</span><span class="sxs-lookup"><span data-stu-id="fb501-103">Sampling in Application Insights</span></span>


<span data-ttu-id="fb501-104">A amostragem é um recurso do [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fb501-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="fb501-105">É recomendado de saudação tráfego de telemetria do modo tooreduce e armazenamento, enquanto preserva uma análise estatística correta de dados de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fb501-105">It is hello recommended way tooreduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="fb501-106">filtro de saudação seleciona itens relacionados, para que você possa navegar entre os itens quando você estiver realizando investigações de diagnósticas.</span><span class="sxs-lookup"><span data-stu-id="fb501-106">hello filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="fb501-107">Quando as contagens de métrica são apresentadas tooyou no portal de hello, eles são renormalized tootake conta de saudação de amostragem toominimize qualquer efeito em estatísticas de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb501-107">When metric counts are presented tooyou in hello portal, they are renormalized tootake account of hello sampling, toominimize any effect on hello statistics.</span></span>

<span data-ttu-id="fb501-108">A amostragem reduz os custos de tráfego e de dados e ajuda a evitar a limitação.</span><span class="sxs-lookup"><span data-stu-id="fb501-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="fb501-109">Em resumo:</span><span class="sxs-lookup"><span data-stu-id="fb501-109">In brief:</span></span>
* <span data-ttu-id="fb501-110">Amostragem retém 1 em  *n*  registra e descarta o resto de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb501-110">Sampling retains 1 in *n* records and discards hello rest.</span></span> <span data-ttu-id="fb501-111">Por exemplo, ela pode reter 1 em 5 eventos, com uma taxa de amostragem de 20%.</span><span class="sxs-lookup"><span data-stu-id="fb501-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="fb501-112">A amostragem acontece automaticamente se o seu aplicativo enviar muita telemetria em aplicativos de servidor Web do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fb501-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="fb501-113">Você também pode definir a amostragem manualmente, a saudação na portal em Olá preços página; ou, no hello SDK de ASP.NET no arquivo. config de hello, tooalso reduzir o tráfego de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb501-113">You can also set sampling manually, either in hello portal on hello pricing page; or in hello ASP.NET SDK in hello .config file, tooalso reduce hello network traffic.</span></span>
* <span data-ttu-id="fb501-114">Se você registra eventos personalizados e você desejar toomake-se de que um conjunto de eventos é retido ou descartado juntos, certifique-se de que eles têm Olá mesmo valor de ID da operação.</span><span class="sxs-lookup"><span data-stu-id="fb501-114">If you log custom events and you want toomake sure that a set of events is either retained or discarded together, make sure that they have hello same OperationId value.</span></span>
* <span data-ttu-id="fb501-115">divisor de amostragem Olá  *n*  é informada em cada registro na propriedade Olá `itemCount`, que pesquisa aparece sob Olá nome amigável "contagem de solicitação" ou "contagem de eventos".</span><span class="sxs-lookup"><span data-stu-id="fb501-115">hello sampling divisor *n* is reported in each record in hello property `itemCount`, which in Search appears under hello friendly name "request count" or "event count".</span></span> <span data-ttu-id="fb501-116">Quando a amostragem não estiver em operação, `itemCount==1`.</span><span class="sxs-lookup"><span data-stu-id="fb501-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="fb501-117">Se você escrever consultas de Análise, deverá [levar em conta a amostragem](app-insights-analytics-tour.md#counting-sampled-data).</span><span class="sxs-lookup"><span data-stu-id="fb501-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="fb501-118">Em particular, em vez de simplesmente contar registros, você deve usar `summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="fb501-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="fb501-119">Tipos de amostragem</span><span class="sxs-lookup"><span data-stu-id="fb501-119">Types of sampling</span></span>
<span data-ttu-id="fb501-120">Há três módulos de amostragem alternativos:</span><span class="sxs-lookup"><span data-stu-id="fb501-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="fb501-121">**Amostragem adaptável** ajusta automaticamente o volume de saudação de telemetria enviada do hello SDK em seu aplicativo ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fb501-121">**Adaptive sampling** automatically adjusts hello volume of telemetry sent from hello SDK in your ASP.NET app.</span></span> <span data-ttu-id="fb501-122">Ela é padrão desde o SDK v 2.0.0-beta3.</span><span class="sxs-lookup"><span data-stu-id="fb501-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="fb501-123">Disponível atualmente somente para telemetria ASP.NET do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="fb501-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="fb501-124">**-Taxa amostragem** reduz o volume de saudação de telemetria enviada do seu servidor ASP.NET e navegadores dos usuários.</span><span class="sxs-lookup"><span data-stu-id="fb501-124">**Fixed-rate sampling** reduces hello volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="fb501-125">Você definir a taxa de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb501-125">You set hello rate.</span></span> <span data-ttu-id="fb501-126">saudação de cliente e servidor sincronizará seu amostragem de forma que, na pesquisa, você pode navegar entre os modos de exibição de página relacionada e solicitações.</span><span class="sxs-lookup"><span data-stu-id="fb501-126">hello client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="fb501-127">**Amostragem de inclusão** funciona em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb501-127">**Ingestion sampling** works in hello Azure portal.</span></span> <span data-ttu-id="fb501-128">Descarta algumas telemetria Olá que chega de seu aplicativo, a uma taxa que você definir.</span><span class="sxs-lookup"><span data-stu-id="fb501-128">It discards some of hello telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="fb501-129">Ela não reduz o tráfego de telemetria, mas ajuda você a se manter em sua cota mensal.</span><span class="sxs-lookup"><span data-stu-id="fb501-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="fb501-130">Olá grande vantagem de amostragem de inclusão é que você pode configurá-lo sem reimplantar o aplicativo e funciona uniformemente para todos os servidores e clientes.</span><span class="sxs-lookup"><span data-stu-id="fb501-130">hello big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="fb501-131">Se a amostragem de taxa Adaptável ou Fixa estiver em operação, a amostragem de Ingestão estará desabilitada.</span><span class="sxs-lookup"><span data-stu-id="fb501-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="fb501-132">amostragem de ingestão</span><span class="sxs-lookup"><span data-stu-id="fb501-132">Ingestion sampling</span></span>
<span data-ttu-id="fb501-133">Essa forma de amostragem opera no ponto de saudação onde telemetria de saudação do seu servidor web, navegadores e dispositivos atinge o ponto de extremidade do serviço Olá Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fb501-133">This form of sampling operates at hello point where hello telemetry from your web server, browsers, and devices reaches hello Application Insights service endpoint.</span></span> <span data-ttu-id="fb501-134">Embora ele não reduzir o tráfego de telemetria de saudação enviado do seu aplicativo, ele reduzir a quantidade de saudação processados e retidos (e cobrada por) pelo Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fb501-134">Although it doesn't reduce hello telemetry traffic sent from your app, it does reduce hello amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="fb501-135">Use este tipo de amostragem, se seu aplicativo geralmente vai exceder sua cota mensal e você não tem a opção hello usando um dos tipos de saudação com base no SDK de amostragem.</span><span class="sxs-lookup"><span data-stu-id="fb501-135">Use this type of sampling if your app often goes over its monthly quota and you don't have hello option of using either of hello SDK-based types of sampling.</span></span> 

<span data-ttu-id="fb501-136">Definir a taxa de amostragem de saudação em Olá cotas e folha de preços:</span><span class="sxs-lookup"><span data-stu-id="fb501-136">Set hello sampling rate in hello Quotas and Pricing blade:</span></span>

![Na folha de visão geral do aplicativo hello, clique em configurações de cota, exemplos, e em seguida, selecione uma taxa de amostragem e clique em Atualizar.](./media/app-insights-sampling/04.png)

<span data-ttu-id="fb501-138">Como outros tipos de amostragem, o algoritmo Olá retém itens de telemetria relacionados.</span><span class="sxs-lookup"><span data-stu-id="fb501-138">Like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="fb501-139">Por exemplo, quando você está verificando telemetria Olá na pesquisa, você poderá toofind solicitação de saudação relacionadas tooa exceção em particular.</span><span class="sxs-lookup"><span data-stu-id="fb501-139">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> <span data-ttu-id="fb501-140">As contagens de métrica como a taxa de solicitação e a taxa de exceções são mantidas corretamente.</span><span class="sxs-lookup"><span data-stu-id="fb501-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="fb501-141">Os pontos de dados que são descartados pela amostragem não estão disponíveis em nenhum recurso do Application Insights como [Exportação Contínua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="fb501-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="fb501-142">A amostragem de ingestão não funciona enquanto a amostragem adaptável ou de taxa fixa com base no SDK estiver em operação.</span><span class="sxs-lookup"><span data-stu-id="fb501-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="fb501-143">Se a taxa de amostragem de saudação em Olá SDK for inferior a 100%, em seguida, hello taxa de amostragem de inclusão definido é ignorada.</span><span class="sxs-lookup"><span data-stu-id="fb501-143">If hello sampling rate at hello SDK is less than 100%, then hello ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="fb501-144">valor Olá mostrado no bloco Olá indica o valor de saudação que você definiu para amostragem de inclusão.</span><span class="sxs-lookup"><span data-stu-id="fb501-144">hello value shown on hello tile indicates hello value that you set for ingestion sampling.</span></span> <span data-ttu-id="fb501-145">Ele não representa a taxa de amostragem real Olá se amostragem SDK está em operação.</span><span class="sxs-lookup"><span data-stu-id="fb501-145">It doesn't represent hello actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="fb501-146">Amostragem adaptável em seu servidor Web</span><span class="sxs-lookup"><span data-stu-id="fb501-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="fb501-147">Amostragem adaptável está disponível para Olá SDK do Application Insights para ASP.NET v 2.0.0-beta3 e posterior e é habilitada por padrão.</span><span class="sxs-lookup"><span data-stu-id="fb501-147">Adaptive sampling is available for hello Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="fb501-148">Amostragem adaptável afeta o volume de saudação de telemetria enviada do seu toohello de aplicativo do servidor web serviço do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fb501-148">Adaptive sampling affects hello volume of telemetry sent from your web server app toohello Application Insights service.</span></span> <span data-ttu-id="fb501-149">Olá volume é ajustado automaticamente tookeep dentro de uma taxa máxima especificada de tráfego.</span><span class="sxs-lookup"><span data-stu-id="fb501-149">hello volume is adjusted automatically tookeep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="fb501-150">Ela não funciona em volumes baixos de telemetria e, portanto, um aplicativo em depuração ou um site com baixo uso não serão afetados.</span><span class="sxs-lookup"><span data-stu-id="fb501-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="fb501-151">o volume de destino do tooachieve hello, alguns dos telemetria Olá gerada é descartado.</span><span class="sxs-lookup"><span data-stu-id="fb501-151">tooachieve hello target volume, some of hello telemetry generated is discarded.</span></span> <span data-ttu-id="fb501-152">Mas, como outros tipos de amostragem, o algoritmo Olá retém itens de telemetria relacionados.</span><span class="sxs-lookup"><span data-stu-id="fb501-152">But like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="fb501-153">Por exemplo, quando você está verificando telemetria Olá na pesquisa, você poderá toofind solicitação de saudação relacionadas tooa exceção em particular.</span><span class="sxs-lookup"><span data-stu-id="fb501-153">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> 

<span data-ttu-id="fb501-154">Métrica de conta, como taxa de solicitação e taxa de exceções são toocompensate ajustada para Olá taxa de amostragem para que elas mostram valores aproximadamente corretos no Explorer de métrica.</span><span class="sxs-lookup"><span data-stu-id="fb501-154">Metric counts such as request rate and exception rate are adjusted toocompensate for hello sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="fb501-155">**Atualização NuGet do projeto** pacotes toohello mais recente *pré-lançamento* versão do Application Insights: clique com botão direito Olá no Gerenciador de soluções, escolha gerenciar pacotes NuGet, verifique **Include pré-lançamento** e procure Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="fb501-155">**Update your project's NuGet** packages toohello latest *pre-release* version of Application Insights: Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="fb501-156">Em [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), você pode ajustar vários parâmetros no hello `AdaptiveSamplingTelemetryProcessor` nó.</span><span class="sxs-lookup"><span data-stu-id="fb501-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in hello `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="fb501-157">números Olá mostrados são valores padrão de saudação:</span><span class="sxs-lookup"><span data-stu-id="fb501-157">hello figures shown are hello default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="fb501-158">Olá taxa de destino que Olá algoritmo adaptável objetiva **em cada host de servidor**.</span><span class="sxs-lookup"><span data-stu-id="fb501-158">hello target rate that hello adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="fb501-159">Se seu aplicativo web é executado em vários hosts, reduza esse valor como tooremain dentro de sua taxa de destino do tráfego no portal do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="fb501-159">If your web app runs on many hosts, reduce this value so as tooremain within your target rate of traffic at hello Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="fb501-160">intervalo de saudação em qual Olá taxa atual de telemetria é avaliada novamente.</span><span class="sxs-lookup"><span data-stu-id="fb501-160">hello interval at which hello current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="fb501-161">Avaliação é executada como uma média móvel.</span><span class="sxs-lookup"><span data-stu-id="fb501-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="fb501-162">Talvez você queira tooshorten esse intervalo se a telemetria é intermitências toosudden responsável.</span><span class="sxs-lookup"><span data-stu-id="fb501-162">You might want tooshorten this interval if your telemetry is liable toosudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="fb501-163">Quando alterações de valor de porcentagem de amostragem, quanto tempo depois é permitido toolower amostragem percentual novamente toocapture menos dados.</span><span class="sxs-lookup"><span data-stu-id="fb501-163">When sampling percentage value changes, how soon after are we allowed toolower sampling percentage again toocapture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="fb501-164">Quando alterações de valor de porcentagem de amostragem, quanto tempo depois podemos tooincrease amostragem percentual novamente toocapture mais dados.</span><span class="sxs-lookup"><span data-stu-id="fb501-164">When sampling percentage value changes, how soon after are we allowed tooincrease sampling percentage again toocapture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="fb501-165">Como percentual de amostragem varia, o que é o valor mínimo de saudação tooset são permitidos.</span><span class="sxs-lookup"><span data-stu-id="fb501-165">As sampling percentage varies, what is hello minimum value we're allowed tooset.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="fb501-166">Como percentual de amostragem varia, o que é o valor máximo de saudação tooset são permitidos.</span><span class="sxs-lookup"><span data-stu-id="fb501-166">As sampling percentage varies, what is hello maximum value we're allowed tooset.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="fb501-167">No cálculo de saudação do hello média móvel, peso Olá atribuído valor mais recente toohello.</span><span class="sxs-lookup"><span data-stu-id="fb501-167">In hello calculation of hello moving average, hello weight assigned toohello most recent value.</span></span> <span data-ttu-id="fb501-168">Use um tooor igual do valor menor que 1.</span><span class="sxs-lookup"><span data-stu-id="fb501-168">Use a value equal tooor less than 1.</span></span> <span data-ttu-id="fb501-169">Valores menores alterar algoritmo Olá menos reativo toosudden.</span><span class="sxs-lookup"><span data-stu-id="fb501-169">Smaller values make hello algorithm less reactive toosudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="fb501-170">valor de Olá atribuído quando o aplicativo hello começou.</span><span class="sxs-lookup"><span data-stu-id="fb501-170">hello value assigned when hello app has just started.</span></span> <span data-ttu-id="fb501-171">Não o reduza enquanto estiver depurando.</span><span class="sxs-lookup"><span data-stu-id="fb501-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="fb501-172">Lista de tipos que não deseja toobe amostra delimitada por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="fb501-172">A semi-colon delimited list of types that you do not want toobe sampled.</span></span> <span data-ttu-id="fb501-173">Os tipos reconhecidos são: Dependência, Evento, Exceção, PageView, Solicitação, Rastreamento.</span><span class="sxs-lookup"><span data-stu-id="fb501-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="fb501-174">Todas as instâncias de saudação especificado tipos são transmitidos; tipos de saudação que não são especificados são amostrados.</span><span class="sxs-lookup"><span data-stu-id="fb501-174">All instances of hello specified types are transmitted; hello types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="fb501-175">Uma lista delimitada por ponto e vírgula de tipos que você deseja toobe de amostra.</span><span class="sxs-lookup"><span data-stu-id="fb501-175">A semi-colon delimited list of types that you want toobe sampled.</span></span> <span data-ttu-id="fb501-176">Os tipos reconhecidos são: Dependência, Evento, Exceção, PageView, Solicitação, Rastreamento.</span><span class="sxs-lookup"><span data-stu-id="fb501-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="fb501-177">Olá especificados tipos são amostrados; todas as instâncias de saudação os outros tipos sempre serão transmitidos.</span><span class="sxs-lookup"><span data-stu-id="fb501-177">hello specified types are sampled; all instances of hello other types will always be transmitted.</span></span>


<span data-ttu-id="fb501-178">**tooswitch desativar** amostragem adaptável, remover Olá AdaptiveSamplingTelemetryProcessor nó de configuração applicationinsights.</span><span class="sxs-lookup"><span data-stu-id="fb501-178">**tooswitch off** adaptive sampling, remove hello AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="fb501-179">Alternativa: configurar amostragem adaptável no código</span><span class="sxs-lookup"><span data-stu-id="fb501-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="fb501-180">Em vez de ajuste de amostragem no arquivo. config de saudação, você pode usar o código.</span><span class="sxs-lookup"><span data-stu-id="fb501-180">Instead of adjusting sampling in hello .config file, you can use code.</span></span> <span data-ttu-id="fb501-181">Isso permite que você toospecify uma função de retorno de chamada invocado sempre que a taxa de amostragem hello serão reavaliada.</span><span class="sxs-lookup"><span data-stu-id="fb501-181">This allows you toospecify a callback function that is invoked whenever hello sampling rate is re-evaluated.</span></span> <span data-ttu-id="fb501-182">Você pode usar isso, por exemplo, toofind limite de taxa de amostragem que está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="fb501-182">You could use this, for example, toofind out what sampling rate is being used.</span></span>

<span data-ttu-id="fb501-183">Remover Olá `AdaptiveSamplingTelemetryProcessor` nó do arquivo. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb501-183">Remove hello `AdaptiveSamplingTelemetryProcessor` node from hello .config file.</span></span>

<span data-ttu-id="fb501-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="fb501-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="fb501-185">([Saiba mais sobre os processadores de telemetria](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="fb501-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="fb501-186">Amostragem para áginas da Web com JavaScript</span><span class="sxs-lookup"><span data-stu-id="fb501-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="fb501-187">Você pode configurar as páginas da Web para amostragem de taxa fixa de qualquer servidor.</span><span class="sxs-lookup"><span data-stu-id="fb501-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="fb501-188">Quando você [configurar páginas de web Olá para o Application Insights](app-insights-javascript.md), modificar o trecho de saudação que você obteve no portal do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="fb501-188">When you [configure hello web pages for Application Insights](app-insights-javascript.md), modify hello snippet that you get from hello Application Insights portal.</span></span> <span data-ttu-id="fb501-189">(Em aplicativos ASP.NET, trecho Olá geralmente vai layout. cshtml.)  Inserir uma linha como `samplingPercentage: 10,` antes da chave de instrumentação hello:</span><span class="sxs-lookup"><span data-stu-id="fb501-189">(In ASP.NET apps, hello snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before hello instrumentation key:</span></span>

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

<span data-ttu-id="fb501-190">Para o percentual de amostragem hello, escolha uma porcentagem que é fechar too100/N onde N é um inteiro.</span><span class="sxs-lookup"><span data-stu-id="fb501-190">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="fb501-191">Atualmente, a amostragem não dá suporte a outros valores.</span><span class="sxs-lookup"><span data-stu-id="fb501-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="fb501-192">Se você habilitar também-taxa amostragem no servidor de saudação, servidor e clientes hello serão sincronizados para que, na pesquisa, você pode navegar entre os modos de exibição de página relacionada e solicitações.</span><span class="sxs-lookup"><span data-stu-id="fb501-192">If you also enable fixed-rate sampling at hello server, hello clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="fb501-193">Amostragem de taxa fixa para sites ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fb501-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="fb501-194">Taxa fixa amostragem reduz o tráfego de saudação enviado do seu servidor web e navegadores da web.</span><span class="sxs-lookup"><span data-stu-id="fb501-194">Fixed rate sampling reduces hello traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="fb501-195">Ao contrário da amostragem adaptável, ela reduz a telemetria a uma taxa fixa decidida por você.</span><span class="sxs-lookup"><span data-stu-id="fb501-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="fb501-196">Ele também sincronizará cliente hello e amostragem de servidor para que itens relacionados são mantidos - por exemplo, para que se você observar um modo de exibição de página na pesquisa, você pode encontrar sua solicitação relacionadas.</span><span class="sxs-lookup"><span data-stu-id="fb501-196">It also synchronizes hello client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="fb501-197">algoritmo de amostragem Olá retém itens relacionados.</span><span class="sxs-lookup"><span data-stu-id="fb501-197">hello sampling algorithm retains related items.</span></span> <span data-ttu-id="fb501-198">Para cada evento de solicitação HTTP, ele e os eventos relacionados são descartados ou transmitidos.</span><span class="sxs-lookup"><span data-stu-id="fb501-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="fb501-199">No Metrics Explorer taxas como contagens de solicitação e a exceção são multiplicadas por toocompensate um fator de taxa de amostragem de hello, para que eles sejam aproximadamente corretos.</span><span class="sxs-lookup"><span data-stu-id="fb501-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor toocompensate for hello sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="fb501-200">**Atualizar pacotes do NuGet do projeto** toohello mais recente *pré-lançamento* versão do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fb501-200">**Update your project's NuGet packages** toohello latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="fb501-201">Clique com botão direito Olá no Gerenciador de soluções, escolha gerenciar pacotes NuGet, verifique **incluir pré-lançamento** e procure Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="fb501-201">Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="fb501-202">**Desabilitar amostragem adaptável**: em [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), remova ou comente Olá `AdaptiveSamplingTelemetryProcessor` nó.</span><span class="sxs-lookup"><span data-stu-id="fb501-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out hello `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="fb501-203">**Habilita Olá-taxa de amostragem módulo.**</span><span class="sxs-lookup"><span data-stu-id="fb501-203">**Enable hello fixed-rate sampling module.**</span></span> <span data-ttu-id="fb501-204">Adicionar este trecho de código muito[Applicationinsights](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="fb501-204">Add this snippet too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="fb501-205">Para o percentual de amostragem hello, escolha uma porcentagem que é fechar too100/N onde N é um inteiro.</span><span class="sxs-lookup"><span data-stu-id="fb501-205">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="fb501-206">Atualmente, a amostragem não dá suporte a outros valores.</span><span class="sxs-lookup"><span data-stu-id="fb501-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="fb501-207">Alternativa: habilite a amostragem de taxa fixa no código do servidor</span><span class="sxs-lookup"><span data-stu-id="fb501-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="fb501-208">Em vez de definir o parâmetro de amostragem de saudação no arquivo. config de saudação, você pode usar o código.</span><span class="sxs-lookup"><span data-stu-id="fb501-208">Instead of setting hello sampling parameter in hello .config file, you can use code.</span></span> 

<span data-ttu-id="fb501-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="fb501-209">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="fb501-210">([Saiba mais sobre os processadores de telemetria](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="fb501-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-toouse-sampling"></a><span data-ttu-id="fb501-211">Quando toouse amostragem?</span><span class="sxs-lookup"><span data-stu-id="fb501-211">When toouse sampling?</span></span>
<span data-ttu-id="fb501-212">Amostragem adaptável é habilitada automaticamente se você usar o hello ASP.NET SDK versão 2.0.0-beta3 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="fb501-212">Adaptive sampling is automatically enabled if you use hello ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="fb501-213">Você pode usar a amostragem de ingestão (em nosso servidor) independente da versão do SDK utilizada.</span><span class="sxs-lookup"><span data-stu-id="fb501-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="fb501-214">A amostragem não é necessária para a maioria dos aplicativos de pequeno e médio porte.</span><span class="sxs-lookup"><span data-stu-id="fb501-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="fb501-215">informações de diagnóstico mais úteis Hello e estatísticas mais precisas são obtidas pela coleta de dados em todas as atividades do usuário.</span><span class="sxs-lookup"><span data-stu-id="fb501-215">hello most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="fb501-216">Olá principais vantagens de amostragem são:</span><span class="sxs-lookup"><span data-stu-id="fb501-216">hello main advantages of sampling are:</span></span>

* <span data-ttu-id="fb501-217">O serviço Application Insights remove (“limita”) os pontos de dados quando o aplicativo envia uma taxa muito alta de telemetria em um curto intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="fb501-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="fb501-218">tookeep em Olá [cota](app-insights-pricing.md) de pontos de dados para o tipo de preços.</span><span class="sxs-lookup"><span data-stu-id="fb501-218">tookeep within hello [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="fb501-219">tráfego de rede tooreduce da coleção de saudação de telemetria.</span><span class="sxs-lookup"><span data-stu-id="fb501-219">tooreduce network traffic from hello collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="fb501-220">Que tipo de amostragem eu devo usar?</span><span class="sxs-lookup"><span data-stu-id="fb501-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="fb501-221">**Use a amostragem de ingestão se:**</span><span class="sxs-lookup"><span data-stu-id="fb501-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="fb501-222">Você geralmente ultrapassa sua cota mensal de telemetria.</span><span class="sxs-lookup"><span data-stu-id="fb501-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="fb501-223">Você está usando uma versão do hello SDK que não dá suporte a amostragem - por exemplo, Olá Java SDK ou ASP.NET versões anteriores a 2.</span><span class="sxs-lookup"><span data-stu-id="fb501-223">You're using a version of hello SDK that doesn't support sampling - for example, hello Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="fb501-224">Você estiver recebendo muita telemetria dos navegadores dos usuários.</span><span class="sxs-lookup"><span data-stu-id="fb501-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="fb501-225">**Use a amostragem de taxa fixa se:**</span><span class="sxs-lookup"><span data-stu-id="fb501-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="fb501-226">Você está usando Olá SDK do Application Insights para a versão de serviços web do ASP.NET 2.0.0 ou posterior, e</span><span class="sxs-lookup"><span data-stu-id="fb501-226">You're using hello Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="fb501-227">Você deseja amostragem sincronizados entre cliente e servidor, para que, quando você estiver investigando eventos em [pesquisa](app-insights-diagnostic-search.md), você pode navegar entre os eventos relacionados no cliente hello e servidor, como exibições de página e solicitações http.</span><span class="sxs-lookup"><span data-stu-id="fb501-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on hello client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="fb501-228">Que esteja confiante de percentual de amostragem apropriado de saudação para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fb501-228">You are confident of hello appropriate sampling percentage for your app.</span></span> <span data-ttu-id="fb501-229">Ele deve ser uma métrica precisa tooget alta o suficiente, mas abaixo Olá taxa excede sua cota de preços e Olá limites de limitação.</span><span class="sxs-lookup"><span data-stu-id="fb501-229">It should be high enough tooget accurate metrics, but below hello rate that exceeds your pricing quota and hello throttling limits.</span></span> 

<span data-ttu-id="fb501-230">**Use a amostragem adaptável:**</span><span class="sxs-lookup"><span data-stu-id="fb501-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="fb501-231">Caso contrário, recomendamos a amostragem adaptável.</span><span class="sxs-lookup"><span data-stu-id="fb501-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="fb501-232">Isso é habilitado por padrão no servidor do ASP.NET Olá SDK, versão 2.0.0-beta3 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="fb501-232">This is enabled by default in hello ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="fb501-233">Ela não reduz o tráfego até uma determinada taxa mínima e, portanto, não afetará um site de baixa utilização.</span><span class="sxs-lookup"><span data-stu-id="fb501-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="fb501-234">Como saber se a amostragem está em operação?</span><span class="sxs-lookup"><span data-stu-id="fb501-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="fb501-235">toodiscover Olá real amostragem taxa, independentemente de onde ela foi aplicada, use um [consulta analítica](app-insights-analytics.md) como este:</span><span class="sxs-lookup"><span data-stu-id="fb501-235">toodiscover hello actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="fb501-236">Em cada retidos registro, `itemCount` indica número Olá de originais registros que ele representa, igual too1 + número de saudação de registros descartados anteriores.</span><span class="sxs-lookup"><span data-stu-id="fb501-236">In each retained record, `itemCount` indicates hello number of original records that it represents, equal too1 + hello number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="fb501-237">Como funciona a amostragem?</span><span class="sxs-lookup"><span data-stu-id="fb501-237">How does sampling work?</span></span>
<span data-ttu-id="fb501-238">Taxa fixa e amostragem adaptável são um recurso da saudação SDK em versões do ASP.NET de 2.0.0 em diante.</span><span class="sxs-lookup"><span data-stu-id="fb501-238">Fixed-rate and adaptive sampling are a feature of hello SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="fb501-239">Amostragem de inclusão é um recurso do hello serviço Application Insights e pode estar em operação se Olá SDK não está executando a amostragem.</span><span class="sxs-lookup"><span data-stu-id="fb501-239">Ingestion sampling is a feature of hello Application Insights service, and can be in operation if hello SDK is not performing sampling.</span></span> 

<span data-ttu-id="fb501-240">algoritmo de amostragem Olá decide qual toodrop de itens de telemetria e quais os tookeep (se está Olá SDK ou no serviço do Application Insights Olá).</span><span class="sxs-lookup"><span data-stu-id="fb501-240">hello sampling algorithm decides which telemetry items toodrop, and which ones tookeep (whether it's in hello SDK or in hello Application Insights service).</span></span> <span data-ttu-id="fb501-241">Olá amostragem decisão se baseia em várias regras que visam toopreserve todos os pontos de dados inter-relacionados intacto, manter uma experiência no Application Insights acionáveis e confiável até mesmo com um conjunto reduzido de dados de diagnóstica.</span><span class="sxs-lookup"><span data-stu-id="fb501-241">hello sampling decision is based on several rules that aim toopreserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="fb501-242">Por exemplo, se para uma solicitação com falha seu aplicativo enviar itens de telemetria adicionais (como exceção e rastreamentos registrados desta solicitação), a amostragem não dividirá essa solicitação e outra telemetria.</span><span class="sxs-lookup"><span data-stu-id="fb501-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="fb501-243">Ela mantém ou remove todos juntos.</span><span class="sxs-lookup"><span data-stu-id="fb501-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="fb501-244">Como resultado, quando examinar os detalhes de solicitação de saudação no Application Insights, você verá sempre solicitação Olá junto com seus itens de telemetria associada.</span><span class="sxs-lookup"><span data-stu-id="fb501-244">As a result, when you look at hello request details in Application Insights, you can always see hello request along with its associated telemetry items.</span></span> 

<span data-ttu-id="fb501-245">Para aplicativos que definem o "usuário" (ou seja, aplicativos de web mais comuns), Olá amostragem decisão se baseia no hash de saudação do id de usuário hello, o que significa que toda a telemetria para qualquer usuário específico é preservada ou descartada.</span><span class="sxs-lookup"><span data-stu-id="fb501-245">For applications that define "user" (that is, most typical web applications), hello sampling decision is based on hello hash of hello user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="fb501-246">Para tipos de saudação de aplicativos que não definem os usuários (como serviços web) Olá amostragem decisão se baseia na id de operação de saudação da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb501-246">For hello types of applications that don't define users (such as web services) hello sampling decision is based on hello operation id of hello request.</span></span> <span data-ttu-id="fb501-247">Por fim, para itens de telemetria Olá que não têm a id de usuário nem operação definida (por exemplo, itens telemetria relatados de threads assíncronas com nenhum contexto http) amostragem simplesmente captura uma porcentagem de itens de telemetria de cada tipo.</span><span class="sxs-lookup"><span data-stu-id="fb501-247">Finally, for hello telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="fb501-248">Ao apresentar tooyou back telemetria, Olá Application Insights serviço ajusta as métricas de saudação por Olá mesmo percentual de amostragem que foi usado no tempo de saudação da coleção, toocompensate para Olá pontos de dados.</span><span class="sxs-lookup"><span data-stu-id="fb501-248">When presenting telemetry back tooyou, hello Application Insights service adjusts hello metrics by hello same sampling percentage that was used at hello time of collection, toocompensate for hello missing data points.</span></span> <span data-ttu-id="fb501-249">Portanto, ao analisar a telemetria Olá no Application Insights, usuários hello estão vendo aproximações estatisticamente corretas que são muito próxima toohello em números reais.</span><span class="sxs-lookup"><span data-stu-id="fb501-249">Hence, when looking at hello telemetry in Application Insights, hello users are seeing statistically correct approximations that are very close toohello real numbers.</span></span>

<span data-ttu-id="fb501-250">precisão de saudação do aproximação Olá depende principalmente da porcentagem de amostragem de saudação configurada.</span><span class="sxs-lookup"><span data-stu-id="fb501-250">hello accuracy of hello approximation largely depends on hello configured sampling percentage.</span></span> <span data-ttu-id="fb501-251">Além disso, aumenta a precisão de saudação para aplicativos que lidam com um grande volume de solicitações geralmente semelhantes de vários usuários.</span><span class="sxs-lookup"><span data-stu-id="fb501-251">Also, hello accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="fb501-252">Em Olá outro lado, para aplicativos que não funcionam com uma carga significativa, a amostragem não é necessário como esses aplicativos normalmente podem enviar todos os seu telemetria mantendo dentro da cota de saudação sem causar perda de dados da limitação.</span><span class="sxs-lookup"><span data-stu-id="fb501-252">On hello other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within hello quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="fb501-253">Observe que o Application Insights não exemplos de tipos de telemetria de métricas e sessões, desde para esses tipos, redução na precisão Olá pode ser altamente indesejável.</span><span class="sxs-lookup"><span data-stu-id="fb501-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in hello precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="fb501-254">amostragem adaptável</span><span class="sxs-lookup"><span data-stu-id="fb501-254">Adaptive sampling</span></span>
<span data-ttu-id="fb501-255">Amostragem adaptável adiciona um componente que monitores Olá atual taxa de transmissão de Olá SDK e ajusta Olá amostragem percentual tootry toostay na taxa máxima de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb501-255">Adaptive sampling adds a component that monitors hello current rate of transmission from hello SDK, and adjusts hello sampling percentage tootry toostay within hello target maximum rate.</span></span> <span data-ttu-id="fb501-256">ajuste Olá é recalculado em intervalos regulares e baseia-se em uma média móvel de saudação taxa de transmissão de saída.</span><span class="sxs-lookup"><span data-stu-id="fb501-256">hello adjustment is recalculated at regular intervals, and is based on a moving average of hello outgoing transmission rate.</span></span>

## <a name="sampling-and-hello-javascript-sdk"></a><span data-ttu-id="fb501-257">Amostragem e hello SDK de JavaScript</span><span class="sxs-lookup"><span data-stu-id="fb501-257">Sampling and hello JavaScript SDK</span></span>
<span data-ttu-id="fb501-258">saudação do cliente (JavaScript) SDK participa-taxa amostragem em conjunto com saudação do servidor SDK.</span><span class="sxs-lookup"><span data-stu-id="fb501-258">hello client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with hello server-side SDK.</span></span> <span data-ttu-id="fb501-259">páginas Olá instrumentado somente enviará telemetria do lado do cliente da saudação mesmos usuários para qual saudação do servidor feita sua decisão muito "sample em."</span><span class="sxs-lookup"><span data-stu-id="fb501-259">hello instrumented pages will only send client-side telemetry from hello same users for which hello server-side made its decision too"sample in."</span></span> <span data-ttu-id="fb501-260">Essa lógica é projetado toomaintain integridade de sessão de usuário em lado cliente e servidor lados.</span><span class="sxs-lookup"><span data-stu-id="fb501-260">This logic is designed toomaintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="fb501-261">Como resultado, em qualquer item de telemetria específico no Application Insights é possível encontrar todos os outros itens de telemetria para esse usuário ou sessão.</span><span class="sxs-lookup"><span data-stu-id="fb501-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="fb501-262">*Minha telemetria do lado do cliente e do servidor não mostra exemplos coordenados como descrito acima.*</span><span class="sxs-lookup"><span data-stu-id="fb501-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="fb501-263">Verifique se você habilitou a amostragem de taxa fixa tanto no servidor quanto no cliente.</span><span class="sxs-lookup"><span data-stu-id="fb501-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="fb501-264">Certifique-se de que a versão SDK Olá é 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="fb501-264">Make sure that hello SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="fb501-265">Verifique se você definir Olá mesmo amostragem percentual no hello cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="fb501-265">Check that you set hello same sampling percentage in both hello client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="fb501-266">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="fb501-266">Frequently Asked Questions</span></span>
<span data-ttu-id="fb501-267">*Por que a amostragem não se trata apenas de “coletar X% de cada tipo de telemetria”?*</span><span class="sxs-lookup"><span data-stu-id="fb501-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="fb501-268">Enquanto essa abordagem de amostragem ofereceria com uma precisão muito alta em aproximações métricas, ele interrompe os dados de diagnóstico capacidade toocorrelate por usuário, sessão e solicitação, que é essencial para diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="fb501-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability toocorrelate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="fb501-269">Portanto, a amostragem funciona melhor com a lógica “coletar todos os itens de telemetria para X% de usuários do aplicativo” ou “coletar toda a telemetria para X% das solicitações do aplicativo”.</span><span class="sxs-lookup"><span data-stu-id="fb501-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="fb501-270">Para itens de telemetria Olá não associados a solicitações de saudação (como o processamento assíncrono em segundo plano), estão Olá será muito "coletar X por cento de todos os itens para cada tipo de telemetria."</span><span class="sxs-lookup"><span data-stu-id="fb501-270">For hello telemetry items not associated with hello requests (such as background asynchronous processing), hello fall back is too"collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="fb501-271">*Percentual de amostragem Olá pode mudar ao longo do tempo?*</span><span class="sxs-lookup"><span data-stu-id="fb501-271">*Can hello sampling percentage change over time?*</span></span>

* <span data-ttu-id="fb501-272">Sim, a amostragem adaptável gradualmente altera percentual de amostragem hello, com base em Olá observada no momento o volume de telemetria de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb501-272">Yes, adaptive sampling gradually changes hello sampling percentage, based on hello currently observed volume of hello telemetry.</span></span>

<span data-ttu-id="fb501-273">*Se usar-taxa amostragem, como saber quais amostragem percentual funcionará Olá melhor para meu aplicativo?*</span><span class="sxs-lookup"><span data-stu-id="fb501-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work hello best for my app?*</span></span>

* <span data-ttu-id="fb501-274">Uma maneira é toostart com a amostragem adaptável, descobrir o que classificar paga em (consulte Olá acima pergunta), e, em seguida, switch toofixed-taxa de amostragem usando essa taxa.</span><span class="sxs-lookup"><span data-stu-id="fb501-274">One way is toostart with adaptive sampling, find out what rate it settles on (see hello above question), and then switch toofixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="fb501-275">Caso contrário, você tem tooguess.</span><span class="sxs-lookup"><span data-stu-id="fb501-275">Otherwise, you have tooguess.</span></span> <span data-ttu-id="fb501-276">Analisar o uso atual de telemetria em AI, observe qualquer limitação ou seja ocorrendo e estimativa Olá volume de telemetria Olá coletado.</span><span class="sxs-lookup"><span data-stu-id="fb501-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate hello volume of hello collected telemetry.</span></span> <span data-ttu-id="fb501-277">Esses três entradas, junto com sua camada de preços selecionada, sugerem quanto desejar tooreduce volume de saudação de telemetria Olá coletado.</span><span class="sxs-lookup"><span data-stu-id="fb501-277">These three inputs, together with your selected pricing tier, suggest how much you might want tooreduce hello volume of hello collected telemetry.</span></span> <span data-ttu-id="fb501-278">No entanto, um aumento no número de saudação dos usuários ou alguns outros shift no volume de saudação de telemetria pode invalidar sua estimativa.</span><span class="sxs-lookup"><span data-stu-id="fb501-278">However, an increase in hello number of your users or some other shift in hello volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="fb501-279">*O que acontece se eu configurar o percentual de amostragem com um valor muito baixo?*</span><span class="sxs-lookup"><span data-stu-id="fb501-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="fb501-280">Percentual de amostragem excessivamente baixo (over-aggressive amostragem) reduz a precisão de saudação do aproximações Olá, ao Application Insights tentativas de visualização de saudação toocompensate dos dados Olá para redução de volume de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb501-280">Excessively low sampling percentage (over-aggressive sampling) reduces hello accuracy of hello approximations, when Application Insights attempts toocompensate hello visualization of hello data for hello data volume reduction.</span></span> <span data-ttu-id="fb501-281">Além disso, experiência de diagnóstica pode piorar, pois algumas Olá raramente falhando ou solicitações lenta podem servir como amostra.</span><span class="sxs-lookup"><span data-stu-id="fb501-281">Also, diagnostic experience might be negatively impacted, as some of hello infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="fb501-282">*O que acontece se eu configurar o percentual de amostragem com um valor muito alto?*</span><span class="sxs-lookup"><span data-stu-id="fb501-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="fb501-283">Configurando resultados de porcentagem (não agressiva suficiente) de amostragem muito alto em uma redução insuficiente no volume de saudação do hello coletados telemetria.</span><span class="sxs-lookup"><span data-stu-id="fb501-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in hello volume of hello collected telemetry.</span></span> <span data-ttu-id="fb501-284">Pode ocorrer perda de dados relacionados a toothrottling e o custo de saudação do usando o Application Insights podem ser maior do que você planejado devido toooverage encargos de telemetria.</span><span class="sxs-lookup"><span data-stu-id="fb501-284">You may still experience telemetry data loss related toothrottling, and hello cost of using Application Insights might be higher than you planned due toooverage charges.</span></span>

<span data-ttu-id="fb501-285">*Em quais plataformas posso usar a amostragem?*</span><span class="sxs-lookup"><span data-stu-id="fb501-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="fb501-286">Amostragem de ingestão poderá ocorrer automaticamente para qualquer telemetria acima de um determinado volume se Olá SDK não está executando a amostragem.</span><span class="sxs-lookup"><span data-stu-id="fb501-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if hello SDK is not performing sampling.</span></span> <span data-ttu-id="fb501-287">Isso funcionaria, por exemplo, se seu aplicativo usa um servidor Java, ou se você estiver usando uma versão mais antiga do hello SDK do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fb501-287">This would work, for example, if your app uses a Java server, or if you are using an older version of hello ASP.NET SDK.</span></span>
* <span data-ttu-id="fb501-288">Se você estiver usando versões do SDK de ASP.NET 2.0.0 e superior (hospedado no Azure ou em seu próprio servidor), você obtém adaptável amostragem por padrão, mas você pode alternar a taxa de toofixed conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="fb501-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch toofixed-rate as described above.</span></span> <span data-ttu-id="fb501-289">Com-taxa amostragem, o navegador Olá SDK sincroniza automaticamente toosample eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="fb501-289">With fixed-rate sampling, hello browser SDK automatically synchronizes toosample related events.</span></span> 

<span data-ttu-id="fb501-290">*Há certos eventos raros desejo sempre toosee. Como posso obtê-los após o módulo de amostragem Olá?*</span><span class="sxs-lookup"><span data-stu-id="fb501-290">*There are certain rare events I always want toosee. How can I get them past hello sampling module?*</span></span>

* <span data-ttu-id="fb501-291">Inicialize uma instância separada do TelemetryClient com um novo TelemetryConfiguration (não saudação padrão ativo).</span><span class="sxs-lookup"><span data-stu-id="fb501-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not hello default Active one).</span></span> <span data-ttu-id="fb501-292">Use esse toosend seus eventos raros.</span><span class="sxs-lookup"><span data-stu-id="fb501-292">Use that toosend your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb501-293">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fb501-293">Next steps</span></span>
* <span data-ttu-id="fb501-294">[filtragem](app-insights-api-filtering-sampling.md) pode fornecer um controle mais restrito do que o SDK envia.</span><span class="sxs-lookup"><span data-stu-id="fb501-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

