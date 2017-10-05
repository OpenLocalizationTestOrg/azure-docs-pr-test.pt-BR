---
title: Exportar usando o Stream Analytics no Azure Application Insights | Microsoft Docs
description: O Stream Analytics pode transformar, filtrar e rotear continuamente os dados exportados do Application Insights.
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
ms.openlocfilehash: 6a84d8ff67c420ce712de905ab1172632502a863
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="use-stream-analytics-to-process-exported-data-from-application-insights"></a><span data-ttu-id="2aac8-103">Usar o Stream Analytics para processar os dados exportados do Application Insights</span><span class="sxs-lookup"><span data-stu-id="2aac8-103">Use Stream Analytics to process exported data from Application Insights</span></span>
<span data-ttu-id="2aac8-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) é a ferramenta ideal para processar dados [exportados do Application Insights](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="2aac8-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is the ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="2aac8-105">O Stream Analytics pode extrair dados de várias fontes.</span><span class="sxs-lookup"><span data-stu-id="2aac8-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="2aac8-106">Ele pode transformar e filtrar os dados e depois roteá-los a uma variedade de coletores.</span><span class="sxs-lookup"><span data-stu-id="2aac8-106">It can transform and filter the data, and then route it to a variety of sinks.</span></span>

<span data-ttu-id="2aac8-107">Neste exemplo, vamos criar um adaptador que usa dados do Application Insights, renomeia e processa alguns dos campos e os direciona ao Power BI.</span><span class="sxs-lookup"><span data-stu-id="2aac8-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of the fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="2aac8-108">Há [maneiras recomendadas para exibir os dados do Application Insights no Power BI](app-insights-export-power-bi.md) muito mais fáceis e eficientes.</span><span class="sxs-lookup"><span data-stu-id="2aac8-108">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="2aac8-109">O caminho ilustrado aqui é apenas um exemplo para mostrar como processar os dados exportados.</span><span class="sxs-lookup"><span data-stu-id="2aac8-109">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

![Diagrama de bloco para exportação por meio do SA para PBI](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="2aac8-111">Criar armazenamento no Azure</span><span class="sxs-lookup"><span data-stu-id="2aac8-111">Create storage in Azure</span></span>
<span data-ttu-id="2aac8-112">Exportação contínua sempre gera dados para uma conta de armazenamento do Azure, por isso você precisa primeiro criar o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2aac8-112">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="2aac8-113">Crie uma conta de armazenamento “clássica” na sua assinatura do [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2aac8-113">Create a "classic" storage account in your subscription in the [Azure portal](https://portal.azure.com).</span></span>
   
   ![No portal do Azure, escolha Novo, Dados e Armazenamento](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="2aac8-115">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="2aac8-115">Create a container</span></span>
   
    ![No novo armazenamento, selecione Contêineres, clique no bloco Contêineres e, em seguida, Adicionar](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="2aac8-117">Copie a chave de acesso de armazenamento</span><span class="sxs-lookup"><span data-stu-id="2aac8-117">Copy the storage access key</span></span>
   
    <span data-ttu-id="2aac8-118">Você precisará dela em breve para configurar a entrada para o serviço do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="2aac8-118">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![No armazenamento, abra Configurações, Chaves e faça uma cópia da Chave de Acesso Primária](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="2aac8-120">Iniciar exportação contínua no armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2aac8-120">Start continuous export to Azure storage</span></span>
<span data-ttu-id="2aac8-121">[exportação contínua](app-insights-export-telemetry.md) move os dados do Application Insights para o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2aac8-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="2aac8-122">No portal do Azure, navegue até o recurso do Application Insights que você criou para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2aac8-122">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![Selecione Navegar, Application Insights e o nome do seu projeto.](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="2aac8-124">Crie uma exportação contínua.</span><span class="sxs-lookup"><span data-stu-id="2aac8-124">Create a continuous export.</span></span>
   
    ![Escolha as Configurações, Exportação Contínua e Adicionar](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="2aac8-126">Selecione a conta de armazenamento criada anteriormente:</span><span class="sxs-lookup"><span data-stu-id="2aac8-126">Select the storage account you created earlier:</span></span>

    ![Definir o destino de exportação](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="2aac8-128">Defina os tipos de eventos que você deseja ver:</span><span class="sxs-lookup"><span data-stu-id="2aac8-128">Set the event types you want to see:</span></span>

    ![Escolher os tipos de evento](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="2aac8-130">Deixe que alguns dados sejam acumulados.</span><span class="sxs-lookup"><span data-stu-id="2aac8-130">Let some data accumulate.</span></span> <span data-ttu-id="2aac8-131">Agora relaxe e deixe as pessoas usarem seu aplicativo por um tempo.</span><span class="sxs-lookup"><span data-stu-id="2aac8-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="2aac8-132">A telemetria chegará e você verá os gráficos estatísticos no [gerenciador de métricas](app-insights-metrics-explorer.md) e eventos individuais na [pesquisa de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="2aac8-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="2aac8-133">E, além disso, os dados serão exportados para seu armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2aac8-133">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="2aac8-134">Inspecione os dados exportados.</span><span class="sxs-lookup"><span data-stu-id="2aac8-134">Inspect the exported data.</span></span> <span data-ttu-id="2aac8-135">No Visual Studio, escolha **Exibir/Cloud Explorer**e abra Azure/Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2aac8-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="2aac8-136">(Se você não tiver essa opção de menu, precisará instalar o Azure SDK: abra o diálogo Novo Projeto e abra Visual C#/Nuvem/Obter Microsoft Azure SDK para .NET.)</span><span class="sxs-lookup"><span data-stu-id="2aac8-136">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="2aac8-137">Anote a parte comum do nome do caminho, que deriva do nome do aplicativo e da chave de instrumentação.</span><span class="sxs-lookup"><span data-stu-id="2aac8-137">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="2aac8-138">Os eventos são gravados em arquivos blob formato JSON.</span><span class="sxs-lookup"><span data-stu-id="2aac8-138">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="2aac8-139">Cada arquivo pode conter um ou mais eventos.</span><span class="sxs-lookup"><span data-stu-id="2aac8-139">Each file may contain one or more events.</span></span> <span data-ttu-id="2aac8-140">Portanto, gostaríamos de escrever um código para ler os dados de evento e filtrar os campos desejados.</span><span class="sxs-lookup"><span data-stu-id="2aac8-140">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="2aac8-141">Podemos fazer todos os tipos de coisas com os dados, mas nosso plano para hoje é usar o Stream Analytics para redirecionar os dados ao Power BI.</span><span class="sxs-lookup"><span data-stu-id="2aac8-141">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to pipe the data to Power BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="2aac8-142">Criar uma instância do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2aac8-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="2aac8-143">No [Portal do Azure Clássico](https://manage.windowsazure.com/), selecione o serviço do Azure Stream Analytics e crie um novo trabalho do Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="2aac8-143">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="2aac8-144">Quando o novo trabalho for criado, expanda seus detalhes:</span><span class="sxs-lookup"><span data-stu-id="2aac8-144">When the new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="2aac8-145">Definir local de blob</span><span class="sxs-lookup"><span data-stu-id="2aac8-145">Set blob location</span></span>
<span data-ttu-id="2aac8-146">Defina a entrada do seu blob de Exportação Contínua:</span><span class="sxs-lookup"><span data-stu-id="2aac8-146">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="2aac8-147">Agora, você precisará da Chave de Acesso Primária da sua Conta de Armazenamento, previamente anotada.</span><span class="sxs-lookup"><span data-stu-id="2aac8-147">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="2aac8-148">Defina isso como a chave da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2aac8-148">Set this as the Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="2aac8-149">Definir padrão de prefixo de caminho</span><span class="sxs-lookup"><span data-stu-id="2aac8-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="2aac8-150">**Defina o Formato de Data como AAAA-MM-DD (com traços).**</span><span class="sxs-lookup"><span data-stu-id="2aac8-150">**Be sure to set the Date Format to YYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="2aac8-151">O Padrão de Prefixo de Caminho especifica como o Stream Analytics encontra os arquivos de entrada no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2aac8-151">The Path Prefix Pattern specifies where Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="2aac8-152">Você precisa configurá-lo para corresponder à maneira como a Exportação Contínua armazena os dados.</span><span class="sxs-lookup"><span data-stu-id="2aac8-152">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="2aac8-153">Defina-o assim:</span><span class="sxs-lookup"><span data-stu-id="2aac8-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="2aac8-154">Neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="2aac8-154">In this example:</span></span>

* <span data-ttu-id="2aac8-155">`webapplication27` é o nome do recurso do Application Insights **todo em minúsculas**.</span><span class="sxs-lookup"><span data-stu-id="2aac8-155">`webapplication27` is the name of the Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="2aac8-156">`1234...` é a chave de instrumentação do recurso do Application Insights **sem traços**.</span><span class="sxs-lookup"><span data-stu-id="2aac8-156">`1234...` is the instrumentation key of the Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="2aac8-157">`PageViews` é o tipo de dados que você deseja analisar.</span><span class="sxs-lookup"><span data-stu-id="2aac8-157">`PageViews` is the type of data you want to analyze.</span></span> <span data-ttu-id="2aac8-158">Os tipos disponíveis dependem do filtro definido na Exportação Contínua.</span><span class="sxs-lookup"><span data-stu-id="2aac8-158">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="2aac8-159">Examine os dados exportados para ver os outros tipos disponíveis e veja o [modelo de exportação de dados](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="2aac8-159">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="2aac8-160">`/{date}/{time}` um padrão escrito literalmente.</span><span class="sxs-lookup"><span data-stu-id="2aac8-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="2aac8-161">Inspecione o armazenamento para garantir que o caminho está certo.</span><span class="sxs-lookup"><span data-stu-id="2aac8-161">Inspect the storage to make sure you get the path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="2aac8-162">Concluir a configuração inicial</span><span class="sxs-lookup"><span data-stu-id="2aac8-162">Finish initial setup</span></span>
<span data-ttu-id="2aac8-163">Confirme o formato de serialização:</span><span class="sxs-lookup"><span data-stu-id="2aac8-163">Confirm the serialization format:</span></span>

![Confirme e feche o assistente](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="2aac8-165">Feche o assistente e aguarde até que a instalação seja concluída.</span><span class="sxs-lookup"><span data-stu-id="2aac8-165">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="2aac8-166">Use o comando Sample para baixar alguns dados.</span><span class="sxs-lookup"><span data-stu-id="2aac8-166">Use the Sample command to download some data.</span></span> <span data-ttu-id="2aac8-167">Mantenha-os como exemplo de teste para depurar sua consulta.</span><span class="sxs-lookup"><span data-stu-id="2aac8-167">Keep it as a test sample to debug your query.</span></span>
> 
> 

## <a name="set-the-output"></a><span data-ttu-id="2aac8-168">Definir a saída</span><span class="sxs-lookup"><span data-stu-id="2aac8-168">Set the output</span></span>
<span data-ttu-id="2aac8-169">Agora, selecione seu trabalho e defina a saída.</span><span class="sxs-lookup"><span data-stu-id="2aac8-169">Now select your job and set the output.</span></span>

![Selecione o novo canal, clique em Saídas, Adicionar, Power BI](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="2aac8-171">Forneça sua **conta corporativa ou de estudante** para autorizar o Stream Analytics a acessar seu recurso do Power BI.</span><span class="sxs-lookup"><span data-stu-id="2aac8-171">Provide your **work or school account** to authorize Stream Analytics to access your Power BI resource.</span></span> <span data-ttu-id="2aac8-172">Em seguida, crie um nome para a saída, bem como para a tabela e o conjunto de dados do Power BI de destino.</span><span class="sxs-lookup"><span data-stu-id="2aac8-172">Then invent a name for the output, and for the target Power BI dataset and table.</span></span>

![Crie três nomes](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-the-query"></a><span data-ttu-id="2aac8-174">Definir a consulta</span><span class="sxs-lookup"><span data-stu-id="2aac8-174">Set the query</span></span>
<span data-ttu-id="2aac8-175">A consulta controla a conversão de entrada para a saída.</span><span class="sxs-lookup"><span data-stu-id="2aac8-175">The query governs the translation from input to output.</span></span>

![Selecione o trabalho e clique em Consulta.](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="2aac8-178">Use a função Test para verificar se você obteve a saída certa.</span><span class="sxs-lookup"><span data-stu-id="2aac8-178">Use the Test function to check that you get the right output.</span></span> <span data-ttu-id="2aac8-179">Atribua a ela os exemplos de dados que você obteve da página de entradas.</span><span class="sxs-lookup"><span data-stu-id="2aac8-179">Give it the sample data that you took from the inputs page.</span></span> 

### <a name="query-to-display-counts-of-events"></a><span data-ttu-id="2aac8-180">Consulta para exibir contagens de eventos</span><span class="sxs-lookup"><span data-stu-id="2aac8-180">Query to display counts of events</span></span>
<span data-ttu-id="2aac8-181">Cole esta consulta:</span><span class="sxs-lookup"><span data-stu-id="2aac8-181">Paste this query:</span></span>

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

* <span data-ttu-id="2aac8-182">export-input é o alias que atribuímos à entrada do fluxo</span><span class="sxs-lookup"><span data-stu-id="2aac8-182">export-input is the alias we gave to the stream input</span></span>
* <span data-ttu-id="2aac8-183">pbi-output é o alias de saída que definimos</span><span class="sxs-lookup"><span data-stu-id="2aac8-183">pbi-output is the output alias we defined</span></span>
* <span data-ttu-id="2aac8-184">Usamos [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) porque o nome do evento está em uma matriz JSON aninhada.</span><span class="sxs-lookup"><span data-stu-id="2aac8-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because the event name is in a nested JSON arrray.</span></span> <span data-ttu-id="2aac8-185">Em seguida, o Select seleciona o nome do evento, juntamente com uma contagem do número de instâncias com esse nome no período de tempo.</span><span class="sxs-lookup"><span data-stu-id="2aac8-185">Then the Select picks the event name, together with a count of the number of instances with that name in the time period.</span></span> <span data-ttu-id="2aac8-186">A cláusula [Agrupar Por](https://msdn.microsoft.com/library/azure/dn835023.aspx) agrupa os elementos em períodos de tempo de 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="2aac8-186">The [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups the elements into time periods of 1 minute.</span></span>

### <a name="query-to-display-metric-values"></a><span data-ttu-id="2aac8-187">Consulta para exibir valores de métricas</span><span class="sxs-lookup"><span data-stu-id="2aac8-187">Query to display metric values</span></span>
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

* <span data-ttu-id="2aac8-188">Essa consulta detalha a telemetria de métricas para obter a hora do evento e o valor da métrica.</span><span class="sxs-lookup"><span data-stu-id="2aac8-188">This query drills into the metrics telemetry to get the event time and the metric value.</span></span> <span data-ttu-id="2aac8-189">Os valores de métrica estão dentro de uma matriz, por isso usamos o padrão OUTER APPLY GetElements para extrair as linhas.</span><span class="sxs-lookup"><span data-stu-id="2aac8-189">The metric values are inside an array, so we use the OUTER APPLY GetElements pattern to extract the rows.</span></span> <span data-ttu-id="2aac8-190">"myMetric" é o nome da métrica nesse caso.</span><span class="sxs-lookup"><span data-stu-id="2aac8-190">"myMetric" is the name of the metric in this case.</span></span> 

### <a name="query-to-include-values-of-dimension-properties"></a><span data-ttu-id="2aac8-191">Consulta para incluir valores das propriedades de dimensão</span><span class="sxs-lookup"><span data-stu-id="2aac8-191">Query to include values of dimension properties</span></span>
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

* <span data-ttu-id="2aac8-192">Essa consulta inclui os valores das propriedades de dimensão sem a necessidade de ter uma determinada dimensão em um índice fixo na matriz de dimensão.</span><span class="sxs-lookup"><span data-stu-id="2aac8-192">This query includes values of the dimension properties without depending on a particular dimension being at a fixed index in the dimension array.</span></span>

## <a name="run-the-job"></a><span data-ttu-id="2aac8-193">Executar o trabalho</span><span class="sxs-lookup"><span data-stu-id="2aac8-193">Run the job</span></span>
<span data-ttu-id="2aac8-194">Você pode selecionar uma data no passado a partir da qual iniciar o trabalho.</span><span class="sxs-lookup"><span data-stu-id="2aac8-194">You can select a date in the past to start the job from.</span></span> 

![Selecione o trabalho e clique em Consulta.](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="2aac8-197">Aguarde até o trabalho estar Em execução.</span><span class="sxs-lookup"><span data-stu-id="2aac8-197">Wait until the job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="2aac8-198">Ver os resultados no Power BI</span><span class="sxs-lookup"><span data-stu-id="2aac8-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="2aac8-199">Há [maneiras recomendadas para exibir os dados do Application Insights no Power BI](app-insights-export-power-bi.md) muito mais fáceis e eficientes.</span><span class="sxs-lookup"><span data-stu-id="2aac8-199">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="2aac8-200">O caminho ilustrado aqui é apenas um exemplo para mostrar como processar os dados exportados.</span><span class="sxs-lookup"><span data-stu-id="2aac8-200">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

<span data-ttu-id="2aac8-201">Abra o Power BI com sua conta corporativa ou de estudante e selecione o conjunto de dados e a tabela que você definiu como a saída do trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="2aac8-201">Open Power BI with your work or school account, and select the dataset and table that you defined as the output of the Stream Analytics job.</span></span>

![No Power BI, selecione o conjunto de dados e os campos.](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="2aac8-203">Agora você pode usar esse conjunto de dados em relatórios e painéis no [Power BI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="2aac8-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![No Power BI, selecione o conjunto de dados e os campos.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="2aac8-205">Não há dados?</span><span class="sxs-lookup"><span data-stu-id="2aac8-205">No data?</span></span>
* <span data-ttu-id="2aac8-206">Verifique se você [definiu o formato de data](#set-path-prefix-pattern) corretamente para AAAA-MM-DD (com traços).</span><span class="sxs-lookup"><span data-stu-id="2aac8-206">Check that you [set the date format](#set-path-prefix-pattern) correctly to YYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="2aac8-207">Vídeo</span><span class="sxs-lookup"><span data-stu-id="2aac8-207">Video</span></span>
<span data-ttu-id="2aac8-208">Noam Ben Zeev mostra como processar dados exportados usando o Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="2aac8-208">Noam Ben Zeev shows how to process exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2aac8-209">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2aac8-209">Next steps</span></span>
* [<span data-ttu-id="2aac8-210">Exportação contínua</span><span class="sxs-lookup"><span data-stu-id="2aac8-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="2aac8-211">Referência de modelo de dados detalhados para os tipos de propriedades e valores.</span><span class="sxs-lookup"><span data-stu-id="2aac8-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="2aac8-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="2aac8-212">Application Insights</span></span>](app-insights-overview.md)

