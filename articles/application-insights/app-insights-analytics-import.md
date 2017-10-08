---
title: aaaImport tooAnalytics seus dados no Azure Application Insights | Microsoft Docs
description: "Importar dados estáticos toojoin com a telemetria de aplicativo ou importar um tooquery de fluxo de dados separado com a análise."
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
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="d18cb-104">Importar dados para o Analytics</span><span class="sxs-lookup"><span data-stu-id="d18cb-104">Import data into Analytics</span></span>

<span data-ttu-id="d18cb-105">Importar dados de tabela em [análise](app-insights-analytics.md), ou toojoin com [Application Insights](app-insights-overview.md) telemetria do seu aplicativo, ou para que você possa analisá-lo como um fluxo separado.</span><span class="sxs-lookup"><span data-stu-id="d18cb-105">Import any tabular data into [Analytics](app-insights-analytics.md), either toojoin it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="d18cb-106">Análise é um fluxos de marca de alto volume de tooanalyzing adequada de idioma consulta avançada de telemetria.</span><span class="sxs-lookup"><span data-stu-id="d18cb-106">Analytics is a powerful query language well-suited tooanalyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="d18cb-107">Você pode importar dados para o Analytics usando seu próprio esquema.</span><span class="sxs-lookup"><span data-stu-id="d18cb-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="d18cb-108">Ele não tem toouse saudação padrão do Application Insights esquemas como solicitação ou rastrear.</span><span class="sxs-lookup"><span data-stu-id="d18cb-108">It doesn't have toouse hello standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="d18cb-109">Você pode importar arquivos JSON ou DSV (valores separados por delimitador - vírgula, ponto-e-vírgula ou tabulação).</span><span class="sxs-lookup"><span data-stu-id="d18cb-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="d18cb-110">Existem três situações em que a importação tooAnalytics é útil:</span><span class="sxs-lookup"><span data-stu-id="d18cb-110">There are three situations where importing tooAnalytics is useful:</span></span>

* <span data-ttu-id="d18cb-111">**Associar à telemetria de aplicativo.**</span><span class="sxs-lookup"><span data-stu-id="d18cb-111">**Join with app telemetry.**</span></span> <span data-ttu-id="d18cb-112">Por exemplo, você pode importar uma tabela que mapeia as URLs de títulos de página legível de toomore seu site.</span><span class="sxs-lookup"><span data-stu-id="d18cb-112">For example, you could import a table that maps URLs from your website toomore readable page titles.</span></span> <span data-ttu-id="d18cb-113">Na análise, você pode criar um relatório de gráfico de painel que mostra Olá dez páginas mais populares em seu site.</span><span class="sxs-lookup"><span data-stu-id="d18cb-113">In Analytics, you can create a dashboard chart report that shows hello ten most popular pages in your website.</span></span> <span data-ttu-id="d18cb-114">Agora ele pode mostrar Olá títulos de página em vez de URLs de saudação.</span><span class="sxs-lookup"><span data-stu-id="d18cb-114">Now it can show hello page titles instead of hello URLs.</span></span>
* <span data-ttu-id="d18cb-115">**Correlacione a telemetria de aplicativo** com outras fontes, como tráfego de rede, dados de servidor ou arquivos de log da CDN.</span><span class="sxs-lookup"><span data-stu-id="d18cb-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="d18cb-116">**Aplica o fluxo de dados separado de tooa de análise.**</span><span class="sxs-lookup"><span data-stu-id="d18cb-116">**Apply Analytics tooa separate data stream.**</span></span> <span data-ttu-id="d18cb-117">O Analytics do Application Insights é uma ferramenta poderosa, que funciona bem com fluxos esparsos com carimbo de data e hora, muito melhor do que com o SQL em muitos casos.</span><span class="sxs-lookup"><span data-stu-id="d18cb-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="d18cb-118">Se você tiver tal fluxo de outra origem, pode analisá-lo com o Analytics.</span><span class="sxs-lookup"><span data-stu-id="d18cb-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="d18cb-119">Enviar dados de fonte de dados de tooyour é fácil.</span><span class="sxs-lookup"><span data-stu-id="d18cb-119">Sending data tooyour data source is easy.</span></span> 

1. <span data-ttu-id="d18cb-120">(Uma vez) Defina o esquema de saudação de seus dados em uma fonte de dados' '.</span><span class="sxs-lookup"><span data-stu-id="d18cb-120">(One time) Define hello schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="d18cb-121">(Periodicamente) Carregar seu armazenamento de dados tooAzure e ligue Olá API REST toonotify que novos dados está aguardando para inclusão.</span><span class="sxs-lookup"><span data-stu-id="d18cb-121">(Periodically) Upload your data tooAzure storage, and call hello REST API toonotify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="d18cb-122">Em alguns minutos, dados saudação estão disponíveis para consulta em análise.</span><span class="sxs-lookup"><span data-stu-id="d18cb-122">Within a few minutes, hello data is available for query in Analytics.</span></span>

<span data-ttu-id="d18cb-123">Olá frequência de carregamento de saudação é definida por você e rapidez você gostaria que seu toobe de dados disponível para consultas.</span><span class="sxs-lookup"><span data-stu-id="d18cb-123">hello frequency of hello upload is defined by you and how fast would you like your data toobe available for queries.</span></span> <span data-ttu-id="d18cb-124">É mais eficientes dados tooupload em partes maiores, mas não é maior que 1GB.</span><span class="sxs-lookup"><span data-stu-id="d18cb-124">It is more efficient tooupload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="d18cb-125">*Você tem muita tooanalyze de fontes de dados?*</span><span class="sxs-lookup"><span data-stu-id="d18cb-125">*Got lots of data sources tooanalyze?*</span></span> [<span data-ttu-id="d18cb-126">*Considere o uso de* logstash *tooship seus dados do Application Insights.*</span><span class="sxs-lookup"><span data-stu-id="d18cb-126">*Consider using* logstash *tooship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="d18cb-127">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="d18cb-127">Before you start</span></span>

<span data-ttu-id="d18cb-128">Você precisa de:</span><span class="sxs-lookup"><span data-stu-id="d18cb-128">You need:</span></span>

1. <span data-ttu-id="d18cb-129">Um recurso do Application Insights no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d18cb-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="d18cb-130">Se você quiser tooanalyze seus dados separadamente de outros telemetria [criar um novo recurso do Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="d18cb-130">If you want tooanalyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="d18cb-131">Se você estiver unindo ou comparar os dados com a telemetria de um aplicativo que já está configurado com o Application Insights, você pode usar o recurso de saudação para esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d18cb-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use hello resource for that app.</span></span>
 * <span data-ttu-id="d18cb-132">Recurso de toothat de acesso Colaborador ou proprietário.</span><span class="sxs-lookup"><span data-stu-id="d18cb-132">Contributor or owner access toothat resource.</span></span>
 
2. <span data-ttu-id="d18cb-133">Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d18cb-133">Azure storage.</span></span> <span data-ttu-id="d18cb-134">Carregar tooAzure armazenamento e análise obtém seus dados a partir daí.</span><span class="sxs-lookup"><span data-stu-id="d18cb-134">You upload tooAzure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="d18cb-135">Recomendamos que você crie uma conta de armazenamento dedicada para seus blobs.</span><span class="sxs-lookup"><span data-stu-id="d18cb-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="d18cb-136">Se seus blobs são compartilhados com outros processos, leva mais tempo para nossos processos tooread seus blobs.</span><span class="sxs-lookup"><span data-stu-id="d18cb-136">If your blobs are shared with other processes, it takes longer for our processes tooread your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="d18cb-137">Definir seu esquema</span><span class="sxs-lookup"><span data-stu-id="d18cb-137">Define your schema</span></span>

<span data-ttu-id="d18cb-138">Antes de importar dados, você deve definir um *fonte de dados,* que especifica o esquema de saudação de seus dados.</span><span class="sxs-lookup"><span data-stu-id="d18cb-138">Before you can import data, you must define a *data source,* which specifies hello schema of your data.</span></span>
<span data-ttu-id="d18cb-139">Você pode ter até too50 fontes de dados em um único recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="d18cb-139">You can have up too50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="d18cb-140">Inicie o Assistente de fonte de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d18cb-140">Start hello data source wizard.</span></span> <span data-ttu-id="d18cb-141">Use o botão "Adicionar nova fonte de dados".</span><span class="sxs-lookup"><span data-stu-id="d18cb-141">Use "Add new data source" button.</span></span> <span data-ttu-id="d18cb-142">Como alternativa - clique no botão de configurações no canto superior direito e escolha "Fontes de Dados" no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="d18cb-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![Adicionar uma nova fonte de dados](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="d18cb-144">Forneça um nome para a nova fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="d18cb-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="d18cb-145">Defina o formato dos arquivos de saudação que você fará o upload.</span><span class="sxs-lookup"><span data-stu-id="d18cb-145">Define format of hello files that you will upload.</span></span>

    <span data-ttu-id="d18cb-146">Você pode definir o formato de saudação manualmente ou carregar um arquivo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d18cb-146">You can either define hello format manually, or upload a sample file.</span></span>

    <span data-ttu-id="d18cb-147">Se dados saudação estão em formato CSV, a primeira linha de saudação do exemplo hello pode ser cabeçalhos de coluna.</span><span class="sxs-lookup"><span data-stu-id="d18cb-147">If hello data is in CSV format, hello first row of hello sample can be column headers.</span></span> <span data-ttu-id="d18cb-148">Você pode alterar os nomes de campo Olá na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="d18cb-148">You can change hello field names in hello next step.</span></span>

    <span data-ttu-id="d18cb-149">exemplo Hello deve incluir pelo menos 10 linhas ou registros de dados.</span><span class="sxs-lookup"><span data-stu-id="d18cb-149">hello sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="d18cb-150">Os nomes de coluna ou de campo devem ter nomes alfanuméricos (sem espaços nem sinais de pontuação).</span><span class="sxs-lookup"><span data-stu-id="d18cb-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![Carregar um arquivo de exemplo](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="d18cb-152">Esquema de saudação de revisão que Olá assistente tem.</span><span class="sxs-lookup"><span data-stu-id="d18cb-152">Review hello schema that hello wizard has got.</span></span> <span data-ttu-id="d18cb-153">Se ele inferir tipos de saudação de uma amostra, talvez seja necessário tooadjust tipos de saudação inferido de colunas de saudação.</span><span class="sxs-lookup"><span data-stu-id="d18cb-153">If it inferred hello types from a sample, you might need tooadjust hello inferred types of hello columns.</span></span>

    ![Esquema de saudação inferida de revisão](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="d18cb-155">(Opcional). Carregue uma definição de esquema.</span><span class="sxs-lookup"><span data-stu-id="d18cb-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="d18cb-156">Consulte o formato de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="d18cb-156">See hello format below.</span></span>

 * <span data-ttu-id="d18cb-157">Selecione um carimbo de data/hora.</span><span class="sxs-lookup"><span data-stu-id="d18cb-157">Select a Timestamp.</span></span> <span data-ttu-id="d18cb-158">Todos os dados no Analytics devem ter um campo de carimbo de data/hora.</span><span class="sxs-lookup"><span data-stu-id="d18cb-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="d18cb-159">Ele deve ter tipo `datetime`, mas ele não tem toobe denominado 'timestamp'.</span><span class="sxs-lookup"><span data-stu-id="d18cb-159">It must have type `datetime`, but it doesn't have toobe named 'timestamp'.</span></span> <span data-ttu-id="d18cb-160">Se os dados tiverem uma coluna que contém uma data e hora no formato ISO, escolha esta opção como coluna de carimbo de hora hello.</span><span class="sxs-lookup"><span data-stu-id="d18cb-160">If your data has a column containing a date and time in ISO format, choose this as hello timestamp column.</span></span> <span data-ttu-id="d18cb-161">Caso contrário, escolha "como dados chegaram" e o processo de importação Olá adicionará um campo de carimbo de hora.</span><span class="sxs-lookup"><span data-stu-id="d18cb-161">Otherwise, choose "as data arrived", and hello import process will add a timestamp field.</span></span>

5. <span data-ttu-id="d18cb-162">Crie fonte de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d18cb-162">Create hello data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="d18cb-163">Formato de arquivo da definição de esquema</span><span class="sxs-lookup"><span data-stu-id="d18cb-163">Schema definition file format</span></span>

<span data-ttu-id="d18cb-164">Em vez de editar o esquema de saudação na interface do usuário, você pode carregar a definição de esquema de saudação de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="d18cb-164">Instead of editing hello schema in UI, you can load hello schema definition from a file.</span></span> <span data-ttu-id="d18cb-165">formato de definição de esquema de saudação é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d18cb-165">hello schema definition format is as follows:</span></span> 

<span data-ttu-id="d18cb-166">Formato delimitado</span><span class="sxs-lookup"><span data-stu-id="d18cb-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="d18cb-167">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="d18cb-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="d18cb-168">Cada coluna é identificada por tipo, nome e local de saudação.</span><span class="sxs-lookup"><span data-stu-id="d18cb-168">Each column is identified by hello location, name and type.</span></span> 

* <span data-ttu-id="d18cb-169">Local – para formato de arquivo delimitado por ele é a posição de saudação do valor Olá mapeado.</span><span class="sxs-lookup"><span data-stu-id="d18cb-169">Location – For delimited file format it is hello position of hello mapped value.</span></span> <span data-ttu-id="d18cb-170">Para o formato JSON, é jpath Olá da chave Olá mapeado.</span><span class="sxs-lookup"><span data-stu-id="d18cb-170">For JSON format, it is hello jpath of hello mapped key.</span></span>
* <span data-ttu-id="d18cb-171">Nome – Olá exibidos o nome da coluna de saudação.</span><span class="sxs-lookup"><span data-stu-id="d18cb-171">Name – hello displayed name of hello column.</span></span>
* <span data-ttu-id="d18cb-172">Tipo – tipo de dados Olá dessa coluna.</span><span class="sxs-lookup"><span data-stu-id="d18cb-172">Type – hello data type of that column.</span></span>
 
<span data-ttu-id="d18cb-173">No caso de dados de exemplo foi usados e o formato de arquivo é delimitado, definição de esquema Olá deve mapear todas as colunas e adicionar novas colunas ao final de saudação.</span><span class="sxs-lookup"><span data-stu-id="d18cb-173">In case a sample data was used and file format is delimited, hello schema definition must map all columns and add new columns at hello end.</span></span> 

<span data-ttu-id="d18cb-174">JSON permite que um mapeamento parcial de dados hello, portanto hello definição de esquema do formato JSON não tem toomap cada chave encontrada em dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d18cb-174">JSON allows partial mapping of hello data, therefore hello schema definition of JSON format doesn’t have toomap every key which is found in a sample data.</span></span> <span data-ttu-id="d18cb-175">Ele também pode mapear as colunas que não fazem parte dos dados de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="d18cb-175">It can also map columns which are not part of hello sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="d18cb-176">Importar dados</span><span class="sxs-lookup"><span data-stu-id="d18cb-176">Import data</span></span>

<span data-ttu-id="d18cb-177">dados de tooimport, carregá-lo tooAzure armazenamento, criar uma chave de acesso para ele e, em seguida, fazer uma chamada de API REST.</span><span class="sxs-lookup"><span data-stu-id="d18cb-177">tooimport data, you upload it tooAzure storage, create an access key for it, and then make a REST API call.</span></span>

![Adicionar uma nova fonte de dados](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="d18cb-179">Você pode executar Olá seguindo o processo manualmente ou configurar um sistema automatizado toodo-lo em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="d18cb-179">You can perform hello following process manually, or set up an automated system toodo it at regular intervals.</span></span> <span data-ttu-id="d18cb-180">É necessário toofollow estas etapas para cada bloco de dados que você deseja tooimport.</span><span class="sxs-lookup"><span data-stu-id="d18cb-180">You need toofollow these steps for each block of data you want tooimport.</span></span>

1. <span data-ttu-id="d18cb-181">Carregar dados de saudação muito[armazenamento de BLOBs do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="d18cb-181">Upload hello data too[Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="d18cb-182">BLOBs podem ser de qualquer tamanho até too1GB descompactados.</span><span class="sxs-lookup"><span data-stu-id="d18cb-182">Blobs can be any size up too1GB uncompressed.</span></span> <span data-ttu-id="d18cb-183">Os blobs grandes, com centenas de MB, são ideais da perspectiva do desempenho.</span><span class="sxs-lookup"><span data-stu-id="d18cb-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="d18cb-184">Você pode compactá-los com o tempo de carregamento de tooimprove Gzip e latência de saudação toobe de dados disponível para consulta.</span><span class="sxs-lookup"><span data-stu-id="d18cb-184">You can compress it with Gzip tooimprove upload time and latency for hello data toobe available for query.</span></span> <span data-ttu-id="d18cb-185">Saudação de uso `.gz` extensão de nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="d18cb-185">Use hello `.gz` filename extension.</span></span>
 * <span data-ttu-id="d18cb-186">É melhor toouse uma conta de armazenamento separado para essa finalidade, tooavoid chamadas de serviços diferentes, diminuindo o desempenho.</span><span class="sxs-lookup"><span data-stu-id="d18cb-186">It's best toouse a separate storage account for this purpose, tooavoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="d18cb-187">Ao enviar dados em alta frequência, em alguns segundos, é recomendável toouse mais de uma conta de armazenamento, por motivos de desempenho.</span><span class="sxs-lookup"><span data-stu-id="d18cb-187">When sending data in high frequency, every few seconds, it is recommended toouse more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="d18cb-188">[Criar uma chave de assinatura de acesso compartilhado para blob Olá](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="d18cb-188">[Create a Shared Access Signature key for hello blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="d18cb-189">chave de saudação deve ter um período de expiração de um dia e fornecer acesso de leitura.</span><span class="sxs-lookup"><span data-stu-id="d18cb-189">hello key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="d18cb-190">Fazer uma chamada REST toonotify Application Insights está aguardando dados.</span><span class="sxs-lookup"><span data-stu-id="d18cb-190">Make a REST call toonotify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="d18cb-191">Ponto de extremidade: `https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="d18cb-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="d18cb-192">Método HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="d18cb-192">HTTP method: POST</span></span>
 * <span data-ttu-id="d18cb-193">Conteúdo:</span><span class="sxs-lookup"><span data-stu-id="d18cb-193">Payload:</span></span>

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

<span data-ttu-id="d18cb-194">espaços reservados de saudação são:</span><span class="sxs-lookup"><span data-stu-id="d18cb-194">hello placeholders are:</span></span>

* <span data-ttu-id="d18cb-195">`Blob URI with Shared Access Key`: Você obtidas pelo procedimento Olá para a criação de uma chave.</span><span class="sxs-lookup"><span data-stu-id="d18cb-195">`Blob URI with Shared Access Key`: You get this from hello procedure for creating a key.</span></span> <span data-ttu-id="d18cb-196">É blob toohello específico.</span><span class="sxs-lookup"><span data-stu-id="d18cb-196">It is specific toohello blob.</span></span>
* <span data-ttu-id="d18cb-197">`Schema ID`: Olá ID do esquema gerado para a esquema definido.</span><span class="sxs-lookup"><span data-stu-id="d18cb-197">`Schema ID`: hello schema ID generated for your defined schema.</span></span> <span data-ttu-id="d18cb-198">dados Olá esse blob devem estar de acordo com esquema toohello.</span><span class="sxs-lookup"><span data-stu-id="d18cb-198">hello data in this blob should conform toohello schema.</span></span>
* <span data-ttu-id="d18cb-199">`DateTime`: o tempo de saudação no qual Olá solicitação for enviada, UTC.</span><span class="sxs-lookup"><span data-stu-id="d18cb-199">`DateTime`: hello time at which hello request is submitted, UTC.</span></span> <span data-ttu-id="d18cb-200">Aceitamos os seguintes formatos: ISO8601 (como "2016-01-01 13:45:01"); RFC822 ("Qua, 14 dez 16 14:57:01 +0000"); RFC850 ("Quarta-feira, 14-dez-16 14:57:00 UTC"); RFC1123 ("Qua, 14 dez 2016 14:57:00 +0000").</span><span class="sxs-lookup"><span data-stu-id="d18cb-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="d18cb-201">`Instrumentation key` de seu recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d18cb-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="d18cb-202">dados de saudação estão disponíveis na análise após alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="d18cb-202">hello data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="d18cb-203">Respostas de erro</span><span class="sxs-lookup"><span data-stu-id="d18cb-203">Error responses</span></span>

* <span data-ttu-id="d18cb-204">**400 Solicitação incorreta**: indica que essa carga de solicitação de saudação é inválida.</span><span class="sxs-lookup"><span data-stu-id="d18cb-204">**400 bad request**: indicates that hello request payload is invalid.</span></span> <span data-ttu-id="d18cb-205">Verificação:</span><span class="sxs-lookup"><span data-stu-id="d18cb-205">Check:</span></span>
 * <span data-ttu-id="d18cb-206">chave de instrumentação correta.</span><span class="sxs-lookup"><span data-stu-id="d18cb-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="d18cb-207">Valor de tempo válido.</span><span class="sxs-lookup"><span data-stu-id="d18cb-207">Valid time value.</span></span> <span data-ttu-id="d18cb-208">Ele deve ser o tempo de saudação agora em UTC.</span><span class="sxs-lookup"><span data-stu-id="d18cb-208">It should be hello time now in UTC.</span></span>
 * <span data-ttu-id="d18cb-209">JSON de evento hello está de acordo com esquema toohello.</span><span class="sxs-lookup"><span data-stu-id="d18cb-209">JSON of hello event conforms toohello schema.</span></span>
* <span data-ttu-id="d18cb-210">**403 Proibido**: blob Olá você enviou não está acessível.</span><span class="sxs-lookup"><span data-stu-id="d18cb-210">**403 Forbidden**: hello blob you've sent is not accessible.</span></span> <span data-ttu-id="d18cb-211">Verifique se essa chave de acesso compartilhado Olá é válido e não expirou.</span><span class="sxs-lookup"><span data-stu-id="d18cb-211">Make sure that hello shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="d18cb-212">**404 Não Encontrado**:</span><span class="sxs-lookup"><span data-stu-id="d18cb-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="d18cb-213">Olá blob não existir.</span><span class="sxs-lookup"><span data-stu-id="d18cb-213">hello blob doesn't exist.</span></span>
 * <span data-ttu-id="d18cb-214">Olá sourceId é incorreto.</span><span class="sxs-lookup"><span data-stu-id="d18cb-214">hello sourceId is wrong.</span></span>

<span data-ttu-id="d18cb-215">Informações mais detalhadas estão disponíveis na mensagem de erro de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="d18cb-215">More detailed information is available in hello response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="d18cb-216">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="d18cb-216">Sample code</span></span>

<span data-ttu-id="d18cb-217">Esse código usa Olá [newtonsoft](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="d18cb-217">This code uses hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="d18cb-218">Classes</span><span class="sxs-lookup"><span data-stu-id="d18cb-218">Classes</span></span>

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

### <a name="ingest-data"></a><span data-ttu-id="d18cb-219">Ingestão de dados</span><span class="sxs-lookup"><span data-stu-id="d18cb-219">Ingest data</span></span>

<span data-ttu-id="d18cb-220">Use este código para cada blob.</span><span class="sxs-lookup"><span data-stu-id="d18cb-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="d18cb-221">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d18cb-221">Next steps</span></span>

* [<span data-ttu-id="d18cb-222">Tour do hello linguagem de consulta de análise de Log</span><span class="sxs-lookup"><span data-stu-id="d18cb-222">Tour of hello Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="d18cb-223">Use *Logstash* toosend dados tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="d18cb-223">Use *Logstash* toosend data tooApplication Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
