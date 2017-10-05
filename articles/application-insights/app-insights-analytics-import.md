---
title: Importar seus dados para o Analytics no Azure Application Insights | Microsoft Docs
description: "Importe dados estáticos para unir a telemetria de aplicativo, ou importe um fluxo de dados separado para consultar com o Analytics."
services: application-insights
keywords: "abrir o esquema, importação de dados"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: aa855a9050ec4e5e7c5db88b7209b8bb48bdba51
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="d3bf9-104">Importar dados para o Analytics</span><span class="sxs-lookup"><span data-stu-id="d3bf9-104">Import data into Analytics</span></span>

<span data-ttu-id="d3bf9-105">Importe quaisquer dados tabulares para o [Analytics](app-insights-analytics.md), seja para associá-los com a telemetria do [Application Insights](app-insights-overview.md) do seu aplicativo ou para que você possa analisá-los como um fluxo separado.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-105">Import any tabular data into [Analytics](app-insights-analytics.md), either to join it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="d3bf9-106">O Analytics é uma poderosa linguagem de consulta ideal para analisar fluxos de telemetria de grande volume com carimbo de data e hora.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-106">Analytics is a powerful query language well-suited to analyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="d3bf9-107">Você pode importar dados para o Analytics usando seu próprio esquema.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="d3bf9-108">Ele não precisa usar os esquemas padrão do Application Insights, como solicitação ou rastreamento.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-108">It doesn't have to use the standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="d3bf9-109">Você pode importar arquivos JSON ou DSV (valores separados por delimitador - vírgula, ponto-e-vírgula ou tabulação).</span><span class="sxs-lookup"><span data-stu-id="d3bf9-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="d3bf9-110">Há três situações em que a importação para o Analytics é útil:</span><span class="sxs-lookup"><span data-stu-id="d3bf9-110">There are three situations where importing to Analytics is useful:</span></span>

* <span data-ttu-id="d3bf9-111">**Associar à telemetria de aplicativo.**</span><span class="sxs-lookup"><span data-stu-id="d3bf9-111">**Join with app telemetry.**</span></span> <span data-ttu-id="d3bf9-112">Por exemplo, você pode importar uma tabela que mapeia as URLs do seu site para títulos de página mais legíveis.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-112">For example, you could import a table that maps URLs from your website to more readable page titles.</span></span> <span data-ttu-id="d3bf9-113">No Analytics, é possível criar um relatório de gráfico de painel que mostra as dez páginas mais populares no seu site.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-113">In Analytics, you can create a dashboard chart report that shows the ten most popular pages in your website.</span></span> <span data-ttu-id="d3bf9-114">Agora ele pode mostrar os títulos das páginas ao invés das URLs.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-114">Now it can show the page titles instead of the URLs.</span></span>
* <span data-ttu-id="d3bf9-115">**Correlacione a telemetria de aplicativo** com outras fontes, como tráfego de rede, dados de servidor ou arquivos de log da CDN.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="d3bf9-116">**Aplique o Analytics a um fluxo de dados separado.**</span><span class="sxs-lookup"><span data-stu-id="d3bf9-116">**Apply Analytics to a separate data stream.**</span></span> <span data-ttu-id="d3bf9-117">O Analytics do Application Insights é uma ferramenta poderosa, que funciona bem com fluxos esparsos com carimbo de data e hora, muito melhor do que com o SQL em muitos casos.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="d3bf9-118">Se você tiver tal fluxo de outra origem, pode analisá-lo com o Analytics.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="d3bf9-119">É fácil enviar dados à fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-119">Sending data to your data source is easy.</span></span> 

1. <span data-ttu-id="d3bf9-120">(Uma vez) Defina o esquema dos dados em uma “fonte de dados”.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-120">(One time) Define the schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="d3bf9-121">(Periodicamente) Carregue os dados no armazenamento do Azure e chame a API REST para notificar que novos dados estão aguardando a ingestão.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-121">(Periodically) Upload your data to Azure storage, and call the REST API to notify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="d3bf9-122">Em poucos minutos, os dados estarão disponíveis para consulta no Analytics.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-122">Within a few minutes, the data is available for query in Analytics.</span></span>

<span data-ttu-id="d3bf9-123">Você define a frequência do carregamento e a rapidez com que deseja que os dados estejam disponíveis para consultas.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-123">The frequency of the upload is defined by you and how fast would you like your data to be available for queries.</span></span> <span data-ttu-id="d3bf9-124">É mais eficiente carregar dados em blocos maiores, mas não maiores que 1 GB.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-124">It is more efficient to upload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="d3bf9-125">*Você tem muitas fontes de dados para analisar?*</span><span class="sxs-lookup"><span data-stu-id="d3bf9-125">*Got lots of data sources to analyze?*</span></span> [<span data-ttu-id="d3bf9-126">*Considere usar* logstash *para enviar seus dados para o Application Insights.*</span><span class="sxs-lookup"><span data-stu-id="d3bf9-126">*Consider using* logstash *to ship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="d3bf9-127">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="d3bf9-127">Before you start</span></span>

<span data-ttu-id="d3bf9-128">Você precisa de:</span><span class="sxs-lookup"><span data-stu-id="d3bf9-128">You need:</span></span>

1. <span data-ttu-id="d3bf9-129">Um recurso do Application Insights no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="d3bf9-130">Se quiser analisar seus dados separadamente de qualquer outra telemetria, [crie um novo recurso do Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="d3bf9-130">If you want to analyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="d3bf9-131">Se você estiver unindo ou comparando os dados com a telemetria de um aplicativo que já está configurado com o Application Insights, pode usar o recurso desse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use the resource for that app.</span></span>
 * <span data-ttu-id="d3bf9-132">Acesso de colaborador ou proprietário para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-132">Contributor or owner access to that resource.</span></span>
 
2. <span data-ttu-id="d3bf9-133">Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-133">Azure storage.</span></span> <span data-ttu-id="d3bf9-134">Carregue no armazenamento do Azure e o Analytics recebe seus dados.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-134">You upload to Azure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="d3bf9-135">Recomendamos que você crie uma conta de armazenamento dedicada para seus blobs.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="d3bf9-136">Se seus blobs estiverem compartilhados com outros processos, pode demorar mais para que nossos processos leiam seus blobs.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-136">If your blobs are shared with other processes, it takes longer for our processes to read your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="d3bf9-137">Definir seu esquema</span><span class="sxs-lookup"><span data-stu-id="d3bf9-137">Define your schema</span></span>

<span data-ttu-id="d3bf9-138">Antes de importar dados, você deve definir uma *fonte de dados*, que especifica o esquema de seus dados.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-138">Before you can import data, you must define a *data source,* which specifies the schema of your data.</span></span>
<span data-ttu-id="d3bf9-139">É possível ter até 50 fontes de dados em um único recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="d3bf9-139">You can have up to 50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="d3bf9-140">Inicie o assistente de fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-140">Start the data source wizard.</span></span> <span data-ttu-id="d3bf9-141">Use o botão "Adicionar nova fonte de dados".</span><span class="sxs-lookup"><span data-stu-id="d3bf9-141">Use "Add new data source" button.</span></span> <span data-ttu-id="d3bf9-142">Como alternativa - clique no botão de configurações no canto superior direito e escolha "Fontes de Dados" no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![Adicionar uma nova fonte de dados](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="d3bf9-144">Forneça um nome para a nova fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="d3bf9-145">Defina o formato dos arquivos que serão carregados.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-145">Define format of the files that you will upload.</span></span>

    <span data-ttu-id="d3bf9-146">É possível definir o formato manualmente ou carregar um arquivo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-146">You can either define the format manually, or upload a sample file.</span></span>

    <span data-ttu-id="d3bf9-147">Se os dados estiverem no formato CSV, a primeira linha da amostra poderá ser cabeçalhos de coluna.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-147">If the data is in CSV format, the first row of the sample can be column headers.</span></span> <span data-ttu-id="d3bf9-148">É possível alterar os nomes dos campos na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-148">You can change the field names in the next step.</span></span>

    <span data-ttu-id="d3bf9-149">A amostra deve incluir, pelo menos, 10 linhas ou registros de dados.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-149">The sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="d3bf9-150">Os nomes de coluna ou de campo devem ter nomes alfanuméricos (sem espaços nem sinais de pontuação).</span><span class="sxs-lookup"><span data-stu-id="d3bf9-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![Carregar um arquivo de exemplo](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="d3bf9-152">Examine o esquema obtido pelo assistente.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-152">Review the schema that the wizard has got.</span></span> <span data-ttu-id="d3bf9-153">Se ele inferiu os tipos com base em uma amostra, provavelmente, será necessário ajustar os tipos inferidos das colunas.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-153">If it inferred the types from a sample, you might need to adjust the inferred types of the columns.</span></span>

    ![Examinar o esquema inferido](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="d3bf9-155">(Opcional). Carregue uma definição de esquema.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="d3bf9-156">Veja o formato a seguir.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-156">See the format below.</span></span>

 * <span data-ttu-id="d3bf9-157">Selecione um carimbo de data/hora.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-157">Select a Timestamp.</span></span> <span data-ttu-id="d3bf9-158">Todos os dados no Analytics devem ter um campo de carimbo de data/hora.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="d3bf9-159">Ele deve ter o tipo `datetime`, mas não precisa ser chamado de ‘carimbo de data/hora’.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-159">It must have type `datetime`, but it doesn't have to be named 'timestamp'.</span></span> <span data-ttu-id="d3bf9-160">Se os dados tiverem uma coluna com data e hora no formato ISO, escolha esta opção como a coluna de carimbo de data/hora.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-160">If your data has a column containing a date and time in ISO format, choose this as the timestamp column.</span></span> <span data-ttu-id="d3bf9-161">Caso contrário, escolha "conforme os dados chegarem", e o processo de importação adicionará um campo de carimbo de data/hora.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-161">Otherwise, choose "as data arrived", and the import process will add a timestamp field.</span></span>

5. <span data-ttu-id="d3bf9-162">Crie a fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-162">Create the data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="d3bf9-163">Formato de arquivo da definição de esquema</span><span class="sxs-lookup"><span data-stu-id="d3bf9-163">Schema definition file format</span></span>

<span data-ttu-id="d3bf9-164">Em vez de editar o esquema na interface do usuário, você pode carregar a definição de esquema a partir de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-164">Instead of editing the schema in UI, you can load the schema definition from a file.</span></span> <span data-ttu-id="d3bf9-165">O formato de definição de esquema é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d3bf9-165">The schema definition format is as follows:</span></span> 

<span data-ttu-id="d3bf9-166">Formato delimitado</span><span class="sxs-lookup"><span data-stu-id="d3bf9-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="d3bf9-167">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="d3bf9-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="d3bf9-168">Cada coluna é identificada pelo local, nome e tipo.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-168">Each column is identified by the location, name and type.</span></span> 

* <span data-ttu-id="d3bf9-169">Local - para o formato de arquivo delimitado, é a posição do valor mapeado.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-169">Location – For delimited file format it is the position of the mapped value.</span></span> <span data-ttu-id="d3bf9-170">Para o formato JSON, é o jpath da chave mapeada.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-170">For JSON format, it is the jpath of the mapped key.</span></span>
* <span data-ttu-id="d3bf9-171">Nome - o nome exibido da coluna.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-171">Name – the displayed name of the column.</span></span>
* <span data-ttu-id="d3bf9-172">Tipo - o tipo de dados dessa coluna.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-172">Type – the data type of that column.</span></span>
 
<span data-ttu-id="d3bf9-173">Caso alguns dados de exemplo tenham sido usados, e o formato de arquivo seja delimitado, a definição de esquema deverá mapear todas as colunas e adicionar novas colunas ao final.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-173">In case a sample data was used and file format is delimited, the schema definition must map all columns and add new columns at the end.</span></span> 

<span data-ttu-id="d3bf9-174">O JSON permite o mapeamento parcial dos dados, portanto, a definição de esquema do formato JSON não precisa mapear todas as chaves que estão localizadas nos dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-174">JSON allows partial mapping of the data, therefore the schema definition of JSON format doesn’t have to map every key which is found in a sample data.</span></span> <span data-ttu-id="d3bf9-175">Também é possível mapear colunas que não fazem parte dos dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-175">It can also map columns which are not part of the sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="d3bf9-176">Importar dados</span><span class="sxs-lookup"><span data-stu-id="d3bf9-176">Import data</span></span>

<span data-ttu-id="d3bf9-177">Para importar dados, carregue-os no armazenamento do Azure, crie uma chave de acesso e, em seguida, faça uma chamada para a API REST.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-177">To import data, you upload it to Azure storage, create an access key for it, and then make a REST API call.</span></span>

![Adicionar uma nova fonte de dados](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="d3bf9-179">Você pode realizar o seguinte processo manualmente ou configurar um sistema automatizado para fazê-lo em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-179">You can perform the following process manually, or set up an automated system to do it at regular intervals.</span></span> <span data-ttu-id="d3bf9-180">Você precisa seguir estas etapas para cada bloco de dados que quiser importar.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-180">You need to follow these steps for each block of data you want to import.</span></span>

1. <span data-ttu-id="d3bf9-181">Carregue os dados no [armazenamento de blobs do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="d3bf9-181">Upload the data to [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="d3bf9-182">Blobs podem ter um tamanho de até 1 GB descompactados.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-182">Blobs can be any size up to 1GB uncompressed.</span></span> <span data-ttu-id="d3bf9-183">Os blobs grandes, com centenas de MB, são ideais da perspectiva do desempenho.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="d3bf9-184">Você pode compactá-los com Gzip para melhorar o tempo de carregamento e a latência, para que os dados fiquem disponíveis para consulta.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-184">You can compress it with Gzip to improve upload time and latency for the data to be available for query.</span></span> <span data-ttu-id="d3bf9-185">Use a extensão de nome de arquivo `.gz`.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-185">Use the `.gz` filename extension.</span></span>
 * <span data-ttu-id="d3bf9-186">É melhor usar uma conta de armazenamento separada para essa finalidade, para evitar chamadas de serviços diferentes que reduzem o desempenho.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-186">It's best to use a separate storage account for this purpose, to avoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="d3bf9-187">Ao enviar dados em alta frequência, em intervalos de segundos, é recomendável usar mais de uma conta de armazenamento, por motivos de desempenho.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-187">When sending data in high frequency, every few seconds, it is recommended to use more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="d3bf9-188">[Crie uma Assinatura de Acesso Compartilhado para o blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="d3bf9-188">[Create a Shared Access Signature key for the blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="d3bf9-189">A chave deve ter um período de validade de um dia e fornecer acesso de leitura.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-189">The key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="d3bf9-190">Faça uma chamada REST para notificar o Application Insights que os dados estão em espera.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-190">Make a REST call to notify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="d3bf9-191">Ponto de extremidade: `https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="d3bf9-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="d3bf9-192">Método HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="d3bf9-192">HTTP method: POST</span></span>
 * <span data-ttu-id="d3bf9-193">Conteúdo:</span><span class="sxs-lookup"><span data-stu-id="d3bf9-193">Payload:</span></span>

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

<span data-ttu-id="d3bf9-194">Os espaços reservados são:</span><span class="sxs-lookup"><span data-stu-id="d3bf9-194">The placeholders are:</span></span>

* <span data-ttu-id="d3bf9-195">`Blob URI with Shared Access Key`: você obtém isso no procedimento para criar uma chave.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-195">`Blob URI with Shared Access Key`: You get this from the procedure for creating a key.</span></span> <span data-ttu-id="d3bf9-196">É específico do blob.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-196">It is specific to the blob.</span></span>
* <span data-ttu-id="d3bf9-197">`Schema ID`: a ID de esquema gerada para seu esquema definido.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-197">`Schema ID`: The schema ID generated for your defined schema.</span></span> <span data-ttu-id="d3bf9-198">Os dados desse blob devem obedecer o esquema.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-198">The data in this blob should conform to the schema.</span></span>
* <span data-ttu-id="d3bf9-199">`DateTime`: a hora em que a solicitação foi enviada, em UTC.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-199">`DateTime`: The time at which the request is submitted, UTC.</span></span> <span data-ttu-id="d3bf9-200">Aceitamos os seguintes formatos: ISO8601 (como "2016-01-01 13:45:01"); RFC822 ("Qua, 14 dez 16 14:57:01 +0000"); RFC850 ("Quarta-feira, 14-dez-16 14:57:00 UTC"); RFC1123 ("Qua, 14 dez 2016 14:57:00 +0000").</span><span class="sxs-lookup"><span data-stu-id="d3bf9-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="d3bf9-201">`Instrumentation key` de seu recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="d3bf9-202">Os dados ficam disponíveis no Analytics depois de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-202">The data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="d3bf9-203">Respostas de erro</span><span class="sxs-lookup"><span data-stu-id="d3bf9-203">Error responses</span></span>

* <span data-ttu-id="d3bf9-204">**400 Solicitação incorreta**: indica que o conteúdo de solicitação é inválido.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-204">**400 bad request**: indicates that the request payload is invalid.</span></span> <span data-ttu-id="d3bf9-205">Verificação:</span><span class="sxs-lookup"><span data-stu-id="d3bf9-205">Check:</span></span>
 * <span data-ttu-id="d3bf9-206">chave de instrumentação correta.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="d3bf9-207">Valor de tempo válido.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-207">Valid time value.</span></span> <span data-ttu-id="d3bf9-208">Deve ser a hora atual em UTC.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-208">It should be the time now in UTC.</span></span>
 * <span data-ttu-id="d3bf9-209">O JSON do evento está em conformidade com o esquema.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-209">JSON of the event conforms to the schema.</span></span>
* <span data-ttu-id="d3bf9-210">**403 Proibido**: o blob que você enviou não está acessível.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-210">**403 Forbidden**: The blob you've sent is not accessible.</span></span> <span data-ttu-id="d3bf9-211">Certifique-se de que a chave de acesso compartilhado é válida e não expirou.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-211">Make sure that the shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="d3bf9-212">**404 Não Encontrado**:</span><span class="sxs-lookup"><span data-stu-id="d3bf9-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="d3bf9-213">o blob não existe.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-213">The blob doesn't exist.</span></span>
 * <span data-ttu-id="d3bf9-214">O sourceId está errado.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-214">The sourceId is wrong.</span></span>

<span data-ttu-id="d3bf9-215">Informações mais detalhadas estão disponíveis na mensagem de erro de resposta.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-215">More detailed information is available in the response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="d3bf9-216">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="d3bf9-216">Sample code</span></span>

<span data-ttu-id="d3bf9-217">Esse código usa o pacote [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) do NuGet.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-217">This code uses the [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="d3bf9-218">Classes</span><span class="sxs-lookup"><span data-stu-id="d3bf9-218">Classes</span></span>

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a><span data-ttu-id="d3bf9-219">Ingestão de dados</span><span class="sxs-lookup"><span data-stu-id="d3bf9-219">Ingest data</span></span>

<span data-ttu-id="d3bf9-220">Use este código para cada blob.</span><span class="sxs-lookup"><span data-stu-id="d3bf9-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="d3bf9-221">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d3bf9-221">Next steps</span></span>

* [<span data-ttu-id="d3bf9-222">Tour sobre a linguagem de consulta do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d3bf9-222">Tour of the Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="d3bf9-223">Usar *Logstash* para enviar dados ao Application Insights</span><span class="sxs-lookup"><span data-stu-id="d3bf9-223">Use *Logstash* to send data to Application Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
