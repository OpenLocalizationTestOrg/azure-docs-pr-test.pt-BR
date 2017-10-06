---
title: "aaaExport usando a análise de fluxo do Azure Application Insights | Microsoft Docs"
description: "Análise de fluxo contínuo pode transformar, filtrar e rota Olá você de exportação de dados do Application Insights."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a><span data-ttu-id="0bfb8-103">Use Stream Analytics tooprocess dados exportados do Application Insights</span><span class="sxs-lookup"><span data-stu-id="0bfb8-103">Use Stream Analytics tooprocess exported data from Application Insights</span></span>
<span data-ttu-id="0bfb8-104">[O Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) é Olá a ferramenta ideal para o processamento de dados [exportados do Application Insights](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="0bfb8-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is hello ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="0bfb8-105">O Stream Analytics pode extrair dados de várias fontes.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="0bfb8-106">Ele pode transformar e filtrar dados de saudação e, em seguida, encaminhá-lo tooa vários coletores.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-106">It can transform and filter hello data, and then route it tooa variety of sinks.</span></span>

<span data-ttu-id="0bfb8-107">Neste exemplo, vamos criar um adaptador que usa dados do Application Insights, renomeia e processa alguns dos campos de saudação e direcioná-lo no Power BI.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of hello fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="0bfb8-108">Há muito melhor e mais fácil [maneiras recomendadas dados do Application Insights toodisplay no Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="0bfb8-108">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="0bfb8-109">Olá, caminho ilustrado aqui é apenas um tooillustrate de exemplo como tooprocess de dados exportados.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-109">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

![Diagrama de bloco para exportação por meio de SA tooPBI](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="0bfb8-111">Criar armazenamento no Azure</span><span class="sxs-lookup"><span data-stu-id="0bfb8-111">Create storage in Azure</span></span>
<span data-ttu-id="0bfb8-112">A exportação contínua sempre gera conta de armazenamento do Azure tooan dados, portanto você precisa de armazenamento de saudação toocreate primeiro.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-112">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="0bfb8-113">Criar uma conta de armazenamento "clássico" em sua assinatura no hello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0bfb8-113">Create a "classic" storage account in your subscription in hello [Azure portal](https://portal.azure.com).</span></span>
   
   ![No portal do Azure, escolha Novo, Dados e Armazenamento](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="0bfb8-115">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="0bfb8-115">Create a container</span></span>
   
    ![No novo armazenamento de hello, selecionar contêineres, clique em bloco de contêineres hello e, em seguida, adicionar](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="0bfb8-117">Copie a chave de acesso de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="0bfb8-117">Copy hello storage access key</span></span>
   
    <span data-ttu-id="0bfb8-118">Você precisará dele em breve tooset o serviço de análise de fluxo de entrada toohello hello.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-118">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![No armazenamento Olá, abra configurações, chaves e faça uma cópia da saudação chave de acesso primária](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="0bfb8-120">Iniciar a exportação contínua tooAzure armazenamento</span><span class="sxs-lookup"><span data-stu-id="0bfb8-120">Start continuous export tooAzure storage</span></span>
<span data-ttu-id="0bfb8-121">[exportação contínua](app-insights-export-telemetry.md) move os dados do Application Insights para o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="0bfb8-122">Na Olá portal do Azure, procure o recurso do Application Insights toohello criado para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-122">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Selecione Navegar, Application Insights e o nome do seu projeto.](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="0bfb8-124">Crie uma exportação contínua.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-124">Create a continuous export.</span></span>
   
    ![Escolha as Configurações, Exportação Contínua e Adicionar](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="0bfb8-126">Selecione a conta de armazenamento de saudação criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="0bfb8-126">Select hello storage account you created earlier:</span></span>

    ![Definir o destino de exportação de saudação](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="0bfb8-128">Defina tipos de evento de saudação desejado toosee:</span><span class="sxs-lookup"><span data-stu-id="0bfb8-128">Set hello event types you want toosee:</span></span>

    ![Escolher os tipos de evento](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="0bfb8-130">Deixe que alguns dados sejam acumulados.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-130">Let some data accumulate.</span></span> <span data-ttu-id="0bfb8-131">Agora relaxe e deixe as pessoas usarem seu aplicativo por um tempo.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="0bfb8-132">A telemetria chegará e você verá os gráficos estatísticos no [gerenciador de métricas](app-insights-metrics-explorer.md) e eventos individuais na [pesquisa de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="0bfb8-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="0bfb8-133">E, além disso, dados de saudação exportará tooyour armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-133">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="0bfb8-134">Inspecione dados hello exportada.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-134">Inspect hello exported data.</span></span> <span data-ttu-id="0bfb8-135">No Visual Studio, escolha **Exibir/Cloud Explorer**e abra Azure/Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="0bfb8-136">(Se você não tiver essa opção de menu, você precisa tooinstall Olá SDK do Azure: Abrir caixa de diálogo de novo projeto hello e abra o Visual C# / nuvem / obter o Microsoft Azure SDK para .NET.)</span><span class="sxs-lookup"><span data-stu-id="0bfb8-136">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="0bfb8-137">Anote a parte comum Olá Olá do nome do caminho, que é derivada da chave de nome e a instrumentação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-137">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="0bfb8-138">eventos de saudação são gravados tooblob arquivos no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-138">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="0bfb8-139">Cada arquivo pode conter um ou mais eventos.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-139">Each file may contain one or more events.</span></span> <span data-ttu-id="0bfb8-140">Portanto, gostaríamos de dados de evento de saudação tooread e filtrar campos Olá que desejamos.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-140">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="0bfb8-141">Todos os tipos de coisas que podemos fazer com dados hello, mas nosso plano de hoje é toouse do Stream Analytics toopipe Olá dados tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-141">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toopipe hello data tooPower BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="0bfb8-142">Criar uma instância do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0bfb8-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="0bfb8-143">De saudação [Portal clássico do Azure](https://manage.windowsazure.com/), selecione o serviço do Azure Stream Analytics hello e criar um novo trabalho de análise de fluxo:</span><span class="sxs-lookup"><span data-stu-id="0bfb8-143">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="0bfb8-144">Quando o novo trabalho de saudação é criado, expanda os detalhes:</span><span class="sxs-lookup"><span data-stu-id="0bfb8-144">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="0bfb8-145">Definir local de blob</span><span class="sxs-lookup"><span data-stu-id="0bfb8-145">Set blob location</span></span>
<span data-ttu-id="0bfb8-146">Defina-a entrada tootake do seu blob de exportação contínua:</span><span class="sxs-lookup"><span data-stu-id="0bfb8-146">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="0bfb8-147">Agora, você precisará Olá chave de acesso primário da conta de armazenamento, que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-147">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="0bfb8-148">Defina como Olá chave da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-148">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="0bfb8-149">Definir padrão de prefixo de caminho</span><span class="sxs-lookup"><span data-stu-id="0bfb8-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="0bfb8-150">**Ser se tooset Olá formato de data tooYYYY-MM-DD (com traços).**</span><span class="sxs-lookup"><span data-stu-id="0bfb8-150">**Be sure tooset hello Date Format tooYYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="0bfb8-151">saudação padrão de prefixo de caminho Especifica onde o Stream Analytics localiza os arquivos de entrada hello no armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-151">hello Path Prefix Pattern specifies where Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="0bfb8-152">Você precisa tooset-toohow toocorrespond exportação contínua armazena dados saudação.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-152">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="0bfb8-153">Defina-o assim:</span><span class="sxs-lookup"><span data-stu-id="0bfb8-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="0bfb8-154">Neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="0bfb8-154">In this example:</span></span>

* <span data-ttu-id="0bfb8-155">`webapplication27`é o nome de saudação de saudação recurso do Application Insights **todas as letras minúsculas**.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-155">`webapplication27` is hello name of hello Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="0bfb8-156">`1234...`é a chave de instrumentação de saudação de saudação recurso do Application Insights, **omitindo traços**.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-156">`1234...` is hello instrumentation key of hello Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="0bfb8-157">`PageViews`Olá tipo de dados que você deseja tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-157">`PageViews` is hello type of data you want tooanalyze.</span></span> <span data-ttu-id="0bfb8-158">tipos disponíveis de saudação dependem de filtro Olá definido na exportação contínua.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-158">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="0bfb8-159">Examinar outros tipos disponíveis de Olá Olá de toosee dados exportados e consulte Olá [exportar modelo de dados](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="0bfb8-159">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="0bfb8-160">`/{date}/{time}` um padrão escrito literalmente.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="0bfb8-161">Inspecione Olá armazenamento toomake-se de que obter o caminho de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-161">Inspect hello storage toomake sure you get hello path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="0bfb8-162">Concluir a configuração inicial</span><span class="sxs-lookup"><span data-stu-id="0bfb8-162">Finish initial setup</span></span>
<span data-ttu-id="0bfb8-163">Confirme o formato de serialização hello:</span><span class="sxs-lookup"><span data-stu-id="0bfb8-163">Confirm hello serialization format:</span></span>

![Confirme e feche o assistente](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="0bfb8-165">Fechar o Assistente de saudação e aguarde Olá toocomplete de instalação.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-165">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="0bfb8-166">Use toodownload de comando de exemplo hello alguns dados.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-166">Use hello Sample command toodownload some data.</span></span> <span data-ttu-id="0bfb8-167">Mantê-lo como um toodebug de exemplo de teste de sua consulta.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-167">Keep it as a test sample toodebug your query.</span></span>
> 
> 

## <a name="set-hello-output"></a><span data-ttu-id="0bfb8-168">Saída de saudação do conjunto</span><span class="sxs-lookup"><span data-stu-id="0bfb8-168">Set hello output</span></span>
<span data-ttu-id="0bfb8-169">Agora selecione o seu trabalho e definir a saída de hello.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-169">Now select your job and set hello output.</span></span>

![Selecione o novo canal de saudação, clique em saídas, adicionar, Power BI](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="0bfb8-171">Forneça seu **ou de estudante conta** tooauthorize tooaccess do Stream Analytics o recurso do Power BI.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-171">Provide your **work or school account** tooauthorize Stream Analytics tooaccess your Power BI resource.</span></span> <span data-ttu-id="0bfb8-172">Em seguida, crie um nome para a saída de hello e de tabela e conjunto de dados do hello destino Power BI.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-172">Then invent a name for hello output, and for hello target Power BI dataset and table.</span></span>

![Crie três nomes](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a><span data-ttu-id="0bfb8-174">Consulta de saudação do conjunto</span><span class="sxs-lookup"><span data-stu-id="0bfb8-174">Set hello query</span></span>
<span data-ttu-id="0bfb8-175">consulta Olá rege tradução de saudação do toooutput de entrada.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-175">hello query governs hello translation from input toooutput.</span></span>

![Selecione hello e clique em consulta.](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="0bfb8-178">Use Olá toocheck de função de teste que você receberá uma saída de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-178">Use hello Test function toocheck that you get hello right output.</span></span> <span data-ttu-id="0bfb8-179">Dê a ele dados de exemplo hello que você fez na página de entradas de saudação.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-179">Give it hello sample data that you took from hello inputs page.</span></span> 

### <a name="query-toodisplay-counts-of-events"></a><span data-ttu-id="0bfb8-180">Consulta toodisplay contagens de eventos</span><span class="sxs-lookup"><span data-stu-id="0bfb8-180">Query toodisplay counts of events</span></span>
<span data-ttu-id="0bfb8-181">Cole esta consulta:</span><span class="sxs-lookup"><span data-stu-id="0bfb8-181">Paste this query:</span></span>

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* <span data-ttu-id="0bfb8-182">entrada de exportação é alias Olá apresentamos a entrada de fluxo de toohello</span><span class="sxs-lookup"><span data-stu-id="0bfb8-182">export-input is hello alias we gave toohello stream input</span></span>
* <span data-ttu-id="0bfb8-183">saída de pbi é Olá alias de saída foi definido</span><span class="sxs-lookup"><span data-stu-id="0bfb8-183">pbi-output is hello output alias we defined</span></span>
* <span data-ttu-id="0bfb8-184">Usamos [GetElements externa aplicar](https://msdn.microsoft.com/library/azure/dn706229.aspx) porque o nome do evento hello está em um arrray aninhada de JSON.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because hello event name is in a nested JSON arrray.</span></span> <span data-ttu-id="0bfb8-185">Em seguida, escolhe selecione Olá Olá nome do evento, juntamente com uma contagem do número de saudação de instâncias com esse nome no período de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-185">Then hello Select picks hello event name, together with a count of hello number of instances with that name in hello time period.</span></span> <span data-ttu-id="0bfb8-186">Olá [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) cláusula agrupa elementos Olá em períodos de tempo de 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-186">hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups hello elements into time periods of 1 minute.</span></span>

### <a name="query-toodisplay-metric-values"></a><span data-ttu-id="0bfb8-187">Consulta toodisplay valores da métrica</span><span class="sxs-lookup"><span data-stu-id="0bfb8-187">Query toodisplay metric values</span></span>
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* <span data-ttu-id="0bfb8-188">Essa consulta detalhada na hora do evento Olá métricas da telemetria tooget hello e valor de métrica de saudação.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-188">This query drills into hello metrics telemetry tooget hello event time and hello metric value.</span></span> <span data-ttu-id="0bfb8-189">valores da métrica Olá estão dentro de uma matriz, para que possamos usar linhas de Olá Olá externa GetElements aplicar padrão tooextract.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-189">hello metric values are inside an array, so we use hello OUTER APPLY GetElements pattern tooextract hello rows.</span></span> <span data-ttu-id="0bfb8-190">"myMetric" é o nome de saudação da métrica Olá nesse caso.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-190">"myMetric" is hello name of hello metric in this case.</span></span> 

### <a name="query-tooinclude-values-of-dimension-properties"></a><span data-ttu-id="0bfb8-191">Consulta tooinclude valores de propriedades de dimensão</span><span class="sxs-lookup"><span data-stu-id="0bfb8-191">Query tooinclude values of dimension properties</span></span>
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* <span data-ttu-id="0bfb8-192">Essa consulta inclui valores de propriedades de dimensão Olá sem dependendo de uma dimensão específica que está sendo em um índice fixado na matriz de dimensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-192">This query includes values of hello dimension properties without depending on a particular dimension being at a fixed index in hello dimension array.</span></span>

## <a name="run-hello-job"></a><span data-ttu-id="0bfb8-193">Executar trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="0bfb8-193">Run hello job</span></span>
<span data-ttu-id="0bfb8-194">Você pode selecionar uma data no hello após toostart Olá trabalho do.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-194">You can select a date in hello past toostart hello job from.</span></span> 

![Selecione hello e clique em consulta.](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="0bfb8-197">Aguarde até que o trabalho hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-197">Wait until hello job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="0bfb8-198">Ver os resultados no Power BI</span><span class="sxs-lookup"><span data-stu-id="0bfb8-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="0bfb8-199">Há muito melhor e mais fácil [maneiras recomendadas dados do Application Insights toodisplay no Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="0bfb8-199">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="0bfb8-200">Olá, caminho ilustrado aqui é apenas um tooillustrate de exemplo como tooprocess de dados exportados.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-200">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

<span data-ttu-id="0bfb8-201">Abra o Power BI com seu trabalho ou conta de estudante, Olá selecione conjunto de dados e tabela definida como saída de saudação do trabalho de análise de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-201">Open Power BI with your work or school account, and select hello dataset and table that you defined as hello output of hello Stream Analytics job.</span></span>

![No Power BI, selecione o conjunto de dados e os campos.](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="0bfb8-203">Agora você pode usar esse conjunto de dados em relatórios e painéis no [Power BI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="0bfb8-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![No Power BI, selecione o conjunto de dados e os campos.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="0bfb8-205">Não há dados?</span><span class="sxs-lookup"><span data-stu-id="0bfb8-205">No data?</span></span>
* <span data-ttu-id="0bfb8-206">Verifique que você [formato de data do conjunto Olá](#set-path-prefix-pattern) corretamente tooYYYY-MM-DD (com traços).</span><span class="sxs-lookup"><span data-stu-id="0bfb8-206">Check that you [set hello date format](#set-path-prefix-pattern) correctly tooYYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="0bfb8-207">Vídeo</span><span class="sxs-lookup"><span data-stu-id="0bfb8-207">Video</span></span>
<span data-ttu-id="0bfb8-208">Noam Ben Zeev mostra como tooprocess exportado usando a análise de fluxo de dados.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-208">Noam Ben Zeev shows how tooprocess exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0bfb8-209">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0bfb8-209">Next steps</span></span>
* [<span data-ttu-id="0bfb8-210">Exportação contínua</span><span class="sxs-lookup"><span data-stu-id="0bfb8-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="0bfb8-211">Referência de tipos de propriedade hello e valores do modelo de dados detalhados.</span><span class="sxs-lookup"><span data-stu-id="0bfb8-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="0bfb8-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="0bfb8-212">Application Insights</span></span>](app-insights-overview.md)

