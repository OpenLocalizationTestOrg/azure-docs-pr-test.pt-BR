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
# <a name="import-data-into-analytics"></a>Importar dados para o Analytics

Importar dados de tabela em [análise](app-insights-analytics.md), ou toojoin com [Application Insights](app-insights-overview.md) telemetria do seu aplicativo, ou para que você possa analisá-lo como um fluxo separado. Análise é um fluxos de marca de alto volume de tooanalyzing adequada de idioma consulta avançada de telemetria.

Você pode importar dados para o Analytics usando seu próprio esquema. Ele não tem toouse saudação padrão do Application Insights esquemas como solicitação ou rastrear.

Você pode importar arquivos JSON ou DSV (valores separados por delimitador - vírgula, ponto-e-vírgula ou tabulação).

Existem três situações em que a importação tooAnalytics é útil:

* **Associar à telemetria de aplicativo.** Por exemplo, você pode importar uma tabela que mapeia as URLs de títulos de página legível de toomore seu site. Na análise, você pode criar um relatório de gráfico de painel que mostra Olá dez páginas mais populares em seu site. Agora ele pode mostrar Olá títulos de página em vez de URLs de saudação.
* **Correlacione a telemetria de aplicativo** com outras fontes, como tráfego de rede, dados de servidor ou arquivos de log da CDN.
* **Aplica o fluxo de dados separado de tooa de análise.** O Analytics do Application Insights é uma ferramenta poderosa, que funciona bem com fluxos esparsos com carimbo de data e hora, muito melhor do que com o SQL em muitos casos. Se você tiver tal fluxo de outra origem, pode analisá-lo com o Analytics.

Enviar dados de fonte de dados de tooyour é fácil. 

1. (Uma vez) Defina o esquema de saudação de seus dados em uma fonte de dados' '.
2. (Periodicamente) Carregar seu armazenamento de dados tooAzure e ligue Olá API REST toonotify que novos dados está aguardando para inclusão. Em alguns minutos, dados saudação estão disponíveis para consulta em análise.

Olá frequência de carregamento de saudação é definida por você e rapidez você gostaria que seu toobe de dados disponível para consultas. É mais eficientes dados tooupload em partes maiores, mas não é maior que 1GB.

> [!NOTE]
> *Você tem muita tooanalyze de fontes de dados?* [*Considere o uso de* logstash *tooship seus dados do Application Insights.*](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a>Antes de começar

Você precisa de:

1. Um recurso do Application Insights no Microsoft Azure.

 * Se você quiser tooanalyze seus dados separadamente de outros telemetria [criar um novo recurso do Application Insights](app-insights-create-new-resource.md).
 * Se você estiver unindo ou comparar os dados com a telemetria de um aplicativo que já está configurado com o Application Insights, você pode usar o recurso de saudação para esse aplicativo.
 * Recurso de toothat de acesso Colaborador ou proprietário.
 
2. Armazenamento do Azure. Carregar tooAzure armazenamento e análise obtém seus dados a partir daí. 

 * Recomendamos que você crie uma conta de armazenamento dedicada para seus blobs. Se seus blobs são compartilhados com outros processos, leva mais tempo para nossos processos tooread seus blobs.


## <a name="define-your-schema"></a>Definir seu esquema

Antes de importar dados, você deve definir um *fonte de dados,* que especifica o esquema de saudação de seus dados.
Você pode ter até too50 fontes de dados em um único recurso do Application Insights

1. Inicie o Assistente de fonte de dados de saudação. Use o botão "Adicionar nova fonte de dados". Como alternativa - clique no botão de configurações no canto superior direito e escolha "Fontes de Dados" no menu suspenso.

    ![Adicionar uma nova fonte de dados](./media/app-insights-analytics-import/add-new-data-source.png)

    Forneça um nome para a nova fonte de dados.

2. Defina o formato dos arquivos de saudação que você fará o upload.

    Você pode definir o formato de saudação manualmente ou carregar um arquivo de exemplo.

    Se dados saudação estão em formato CSV, a primeira linha de saudação do exemplo hello pode ser cabeçalhos de coluna. Você pode alterar os nomes de campo Olá na próxima etapa do hello.

    exemplo Hello deve incluir pelo menos 10 linhas ou registros de dados.

    Os nomes de coluna ou de campo devem ter nomes alfanuméricos (sem espaços nem sinais de pontuação).

    ![Carregar um arquivo de exemplo](./media/app-insights-analytics-import/sample-data-file.png)


3. Esquema de saudação de revisão que Olá assistente tem. Se ele inferir tipos de saudação de uma amostra, talvez seja necessário tooadjust tipos de saudação inferido de colunas de saudação.

    ![Esquema de saudação inferida de revisão](./media/app-insights-analytics-import/data-source-review-schema.png)

 * (Opcional). Carregue uma definição de esquema. Consulte o formato de saudação abaixo.

 * Selecione um carimbo de data/hora. Todos os dados no Analytics devem ter um campo de carimbo de data/hora. Ele deve ter tipo `datetime`, mas ele não tem toobe denominado 'timestamp'. Se os dados tiverem uma coluna que contém uma data e hora no formato ISO, escolha esta opção como coluna de carimbo de hora hello. Caso contrário, escolha "como dados chegaram" e o processo de importação Olá adicionará um campo de carimbo de hora.

5. Crie fonte de dados de saudação.

### <a name="schema-definition-file-format"></a>Formato de arquivo da definição de esquema

Em vez de editar o esquema de saudação na interface do usuário, você pode carregar a definição de esquema de saudação de um arquivo. formato de definição de esquema de saudação é o seguinte: 

Formato delimitado 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

Formato JSON 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
Cada coluna é identificada por tipo, nome e local de saudação. 

* Local – para formato de arquivo delimitado por ele é a posição de saudação do valor Olá mapeado. Para o formato JSON, é jpath Olá da chave Olá mapeado.
* Nome – Olá exibidos o nome da coluna de saudação.
* Tipo – tipo de dados Olá dessa coluna.
 
No caso de dados de exemplo foi usados e o formato de arquivo é delimitado, definição de esquema Olá deve mapear todas as colunas e adicionar novas colunas ao final de saudação. 

JSON permite que um mapeamento parcial de dados hello, portanto hello definição de esquema do formato JSON não tem toomap cada chave encontrada em dados de exemplo. Ele também pode mapear as colunas que não fazem parte dos dados de exemplo hello. 

## <a name="import-data"></a>Importar dados

dados de tooimport, carregá-lo tooAzure armazenamento, criar uma chave de acesso para ele e, em seguida, fazer uma chamada de API REST.

![Adicionar uma nova fonte de dados](./media/app-insights-analytics-import/analytics-upload-process.png)

Você pode executar Olá seguindo o processo manualmente ou configurar um sistema automatizado toodo-lo em intervalos regulares. É necessário toofollow estas etapas para cada bloco de dados que você deseja tooimport.

1. Carregar dados de saudação muito[armazenamento de BLOBs do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md). 

 * BLOBs podem ser de qualquer tamanho até too1GB descompactados. Os blobs grandes, com centenas de MB, são ideais da perspectiva do desempenho.
 * Você pode compactá-los com o tempo de carregamento de tooimprove Gzip e latência de saudação toobe de dados disponível para consulta. Saudação de uso `.gz` extensão de nome de arquivo.
 * É melhor toouse uma conta de armazenamento separado para essa finalidade, tooavoid chamadas de serviços diferentes, diminuindo o desempenho.
 * Ao enviar dados em alta frequência, em alguns segundos, é recomendável toouse mais de uma conta de armazenamento, por motivos de desempenho.

 
2. [Criar uma chave de assinatura de acesso compartilhado para blob Olá](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md). chave de saudação deve ter um período de expiração de um dia e fornecer acesso de leitura.
3. Fazer uma chamada REST toonotify Application Insights está aguardando dados.

 * Ponto de extremidade: `https://dc.services.visualstudio.com/v2/track`
 * Método HTTP: POST
 * Conteúdo:

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

espaços reservados de saudação são:

* `Blob URI with Shared Access Key`: Você obtidas pelo procedimento Olá para a criação de uma chave. É blob toohello específico.
* `Schema ID`: Olá ID do esquema gerado para a esquema definido. dados Olá esse blob devem estar de acordo com esquema toohello.
* `DateTime`: o tempo de saudação no qual Olá solicitação for enviada, UTC. Aceitamos os seguintes formatos: ISO8601 (como "2016-01-01 13:45:01"); RFC822 ("Qua, 14 dez 16 14:57:01 +0000"); RFC850 ("Quarta-feira, 14-dez-16 14:57:00 UTC"); RFC1123 ("Qua, 14 dez 2016 14:57:00 +0000").
* `Instrumentation key` de seu recurso do Application Insights.

dados de saudação estão disponíveis na análise após alguns minutos.

## <a name="error-responses"></a>Respostas de erro

* **400 Solicitação incorreta**: indica que essa carga de solicitação de saudação é inválida. Verificação:
 * chave de instrumentação correta.
 * Valor de tempo válido. Ele deve ser o tempo de saudação agora em UTC.
 * JSON de evento hello está de acordo com esquema toohello.
* **403 Proibido**: blob Olá você enviou não está acessível. Verifique se essa chave de acesso compartilhado Olá é válido e não expirou.
* **404 Não Encontrado**:
 * Olá blob não existir.
 * Olá sourceId é incorreto.

Informações mais detalhadas estão disponíveis na mensagem de erro de resposta de saudação.


## <a name="sample-code"></a>Exemplo de código

Esse código usa Olá [newtonsoft](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) pacote NuGet.

### <a name="classes"></a>Classes

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

### <a name="ingest-data"></a>Ingestão de dados

Use este código para cada blob. 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a>Próximas etapas

* [Tour do hello linguagem de consulta de análise de Log](app-insights-analytics-tour.md)
* [Use *Logstash* toosend dados tooApplication Insights](https://github.com/Microsoft/logstash-output-application-insights)
