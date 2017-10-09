---
title: "as métricas de armazenamento aaaEnabling em Olá portal do Azure | Microsoft Docs"
description: "Como as métricas de armazenamento tooenable para Olá serviços Blob, fila, tabela e arquivo"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0407adfc-2a41-4126-922d-b76e90b74563
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/14/2017
ms.author: robinsh
ms.openlocfilehash: 4e705ecbdd083c77f8ceff87214d7221495d2d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a>Habilitando métricas do Armazenamento do Azure e exibição de dados de métricas
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a>Visão geral
As Métricas de Armazenamento são habilitadas por padrão quando você cria uma nova conta de armazenamento. Você pode configurar o monitoramento por meio de saudação [portal do Azure](https://portal.azure.com) ou o Windows PowerShell, ou programaticamente por meio de bibliotecas de saudação do cliente de armazenamento.

Você pode configurar um período de retenção de dados de métricas de saudação: esse período determina para armazenamento de saudação quanto tempo o serviço mantém métricas hello e encargos por Olá espaço necessário toostore-los. Normalmente, você deve usar um período de retenção mais curto para métricas de minuto de hora devido a espaço adicional significativo Olá necessário para métricas de minuto. Você deve escolher um período de retenção, de modo que você tem dados suficientes de saudação de tooanalyze tempo e baixar as métricas que você deseja tookeep para análise offline ou para fins de relatório. Lembre-se de que você também será cobrado para baixar dados de métrica de sua conta de armazenamento.

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a>Como as métricas de tooenable usando Olá portal do Azure
Siga essas métricas de tooenable etapas no hello [portal do Azure](https://portal.azure.com):

1. Navegue tooyour conta de armazenamento.
1. Selecione **diagnóstico** em Olá **Menu** folha
1. Certifique-se de que **Status** está definido muito**em**.
1. Métricas de saudação Select para serviços de saudação desejar toomonitor.
1. Especifique um tooindicate de política de retenção quanto tempo dados de log e métricas de tooretain.
1. Selecione **Salvar**.

Observe que Olá [portal do Azure](https://portal.azure.com) atualmente permite que você tooconfigure métricas de minutos em sua conta de armazenamento; você deve habilitar métricas de minuto usando o PowerShell ou programaticamente.

## <a name="how-tooenable-metrics-using-powershell"></a>Como as métricas de tooenable usando o PowerShell
Você pode usar o PowerShell em tooconfigure seu computador local as métricas de armazenamento em sua conta de armazenamento usando hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve Olá configurações atuais e Olá cmdlet Set-AzureStorageServiceMetricsProperty toochange Olá as configurações atuais.

Olá que controlam as métricas de armazenamento usam Olá parâmetros a seguir:

* Os valorespossíveis de MetricsType são hora e minuto.
* ServiceType: os possíveis valores são Blob, Fila e Tabela.
* MetricsLevel: os valores possíveis são None, Serviço e ServiceAndApi.

Por exemplo, hello seguinte comando ativa em minuto métricas para serviço de Blob de saudação em sua conta de armazenamento padrão com o período de retenção Olá definir toofive dias:

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

Olá seguinte comando recupera Olá atual por hora métricas nível e retenção de dias para o serviço de blob de saudação em sua conta de armazenamento padrão:

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

Para obter informações sobre como tooconfigure hello Azure PowerShell cmdlets toowork com sua assinatura do Azure e como tooselect Olá armazenamento padrão da conta toouse, consulte: [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

## <a name="how-tooenable-storage-metrics-programmatically"></a>Como tooenable as métricas de armazenamento programaticamente
saudação de trecho de código c# a seguir mostra como tooenable métricas e registro em log para usar o serviço Blob Olá Olá biblioteca de cliente de armazenamento para .NET:

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days.
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a>Exibindo as métricas de armazenamento
Depois de configurar a análise de armazenamento métricas toomonitor sua conta de armazenamento, o Storage Analytics registra métricas Olá em um conjunto de tabelas bem conhecidas em sua conta de armazenamento. Você pode configurar métricas de hora gráficos tooview Olá [portal do Azure](https://portal.azure.com):

1. Navegue de conta de armazenamento tooyour Olá [portal do Azure](https://portal.azure.com).
1. Selecione **métricas** em Olá **Menu** folha para Olá cujas métricas de serviço você deseja tooview.
1. Selecione **editar** no gráfico de saudação desejado tooconfigure.
1. Em Olá **Editar gráfico** folha, selecione Olá **intervalo de tempo**, **tipo de gráfico**e você deseja exibir no gráfico de saudação de métricas de saudação.
1. Selecione **OK**

Se você quiser que as métricas de saudação toodownload para armazenamento de longo prazo ou tooanalyze-las localmente, você precisará:

* Use uma ferramenta que está ciente dessas tabelas e permitem que você tooview e baixá-los.
* Gravar um tooread de aplicativo ou script personalizado e armazenar tabelas hello.

Muitas ferramentas de navegação de armazenamento de terceiros reconhecem essas tabelas e permitem que você tooview-los diretamente.
Confira [Ferramentas de Cliente do Armazenamento do Azure](storage-explorers.md) para obter uma lista de ferramentas disponíveis.

> [!NOTE]
> Começando com a versão 0.8.0 de saudação [Microsoft Azure Storage Explorer](http://storageexplorer.com/), você pode exibir e baixar as tabelas de métricas de análise de saudação.
> 
> 

Na análise de saudação do pedido tooaccess tabelas programaticamente, observe que tabelas de análise de saudação não aparecerá se você listar todas as tabelas de saudação em sua conta de armazenamento. Você pode acessá-los diretamente por nome ou usar Olá [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) em nomes de tabela Olá de tooquery biblioteca de cliente .NET de saudação.

### <a name="hourly-metrics"></a>Métricas por hora
* $MetricsHourPrimaryTransactionsBlob
* $MetricsHourPrimaryTransactionsTable
* $MetricsHourPrimaryTransactionsQueue

### <a name="minute-metrics"></a>Métricas por minuto
* $MetricsMinutePrimaryTransactionsBlob
* $MetricsMinutePrimaryTransactionsTable
* $MetricsMinutePrimaryTransactionsQueue

### <a name="capacity"></a>Capacidade
* $MetricsCapacityBlob

Você pode encontrar detalhes completos de esquemas Olá para essas tabelas em [esquema de tabela de métricas de análise de armazenamento](https://msdn.microsoft.com/library/azure/hh343264.aspx). linhas de exemplo Hello abaixo mostram apenas um subconjunto de colunas de saudação disponíveis, mas ilustram alguns recursos importantes da maneira Olá que métricas de armazenamento salvam essas métricas:

| PartitionKey | RowKey | Timestamp | TotalRequests | TotalBillableRequests | TotalIngress | TotalEgress | Disponibilidade | AverageE2ELatency | AverageServerLatency | PercentSuccess |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| 20140522T1100 |user;All |2014-05-22T11:01:16.7650250Z |7 |7 |4003 |46801 |100 |104.4286 |6.857143 |100 |
| 20140522T1100 |usuário;QueryEntities |2014-05-22T11:01:16.7640250Z |5 |5 |2694 |45951 |100 |143.8 |7.8 |100 |
| 20140522T1100 |user;QueryEntity |2014-05-22T11:01:16.7650250Z |1 |1 |538 |633 |100 |3 |3 |100 |
| 20140522T1100 |user;UpdateEntity |2014-05-22T11:01:16.7650250Z |1 |1 |771 |217 |100 |9 |6 |100 |

Este exemplo de dados de métricas de minutos, chave de partição Olá usa tempo de saudação na resolução de minutos. chave de linha de saudação identifica o tipo de saudação de informações armazenadas em linha hello e isso é composto de duas partes de informações, o tipo de acesso hello e tipo de solicitação de saudação:

* tipo de acesso de saudação é o usuário ou sistema, em que o usuário refere-se o serviço de armazenamento do tooall usuário solicitações toohello e refere-se toorequests feitas pela análise de armazenamento.
* tipo de solicitação de saudação é todos os caso em que é uma linha de resumo, ou ele identifica a API específica hello como QueryEntity ou UpdateEntity.

dados de exemplo Hello acima mostra que todos os Olá registra para um único minuto (começando às 11:00 AM), portanto número de saudação de solicitações de QueryEntities mais hello número de solicitações de QueryEntity mais o número de saudação de solicitações de UpdateEntity somar tooseven, que é Olá total mostrado em linha do usuário: All Hello. Da mesma forma, você pode derivar Olá latência média de ponta a ponta 104,4286 na linha de user: All Olá Calculando ((143.8 * 5) + 3 + 9) / 7.

## <a name="metrics-alerts"></a>Alertas de métricas
Você deve considerar a configuração de alertas no hello [portal do Azure](https://portal.azure.com) para métricas de armazenamento pode notificá-lo automaticamente de alterações importantes no comportamento de saudação de seus serviços de armazenamento. Se você usar esses dados de métricas de um toodownload de ferramenta do Gerenciador de armazenamento em um formato delimitado, você pode usar dados do Microsoft Excel tooanalyze saudação. Confira [Ferramentas de Cliente do Armazenamento do Azure](storage-explorers.md) para obter uma lista de ferramentas do gerenciador de armazenamento disponíveis. Você pode configurar alertas em Olá **regras de alerta** folha, acessível em **monitoramento** na folha de menu de conta de armazenamento hello.

> [!IMPORTANT]
> Pode haver um atraso entre um evento de armazenamento e quando Olá correspondente de dados de métricas de horas ou minutos é registrado. No caso de saudação de métricas de minutos, vários minutos de dados podem ser gravados uma vez. Isso pode levar tootransactions de minutos anteriores que está sendo agregados em transação Olá para Olá minuto atual. Quando isso acontece, o alerta Olá serviço pode não ter todos os dados de métricas disponíveis para hello configurado intervalo do alerta, que pode levar tooalerts acionamento inesperadamente.
>

## <a name="accessing-metrics-data-programmatically"></a>Acessando dados de métrica programaticamente
Olá lista a seguir mostra exemplo código c# que acessa as métricas de minutos de saudação para um intervalo de minutos e exibe os resultados de saudação em uma janela do console. Ele usa Olá biblioteca de armazenamento do Azure versão 4, que inclui Olá CloudAnalyticsClient classe que simplifica ao acessar tabelas de métricas de saudação no armazenamento.

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
      string.Format("Time: {0}, ", entity.Time) +
      string.Format("AccessType: {0}, ", entity.AccessType) +
      string.Format("TransactionType: {0}, ", entity.TransactionType) +
      string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a>Quais taxas você provoca quando habilita a métrica de armazenamento?
Grave solicitações toocreate de entidades de tabela para métricas são cobradas a operações de armazenamento do Azure Olá taxas padrão tooall aplicável.

Solicitações de leitura e exclusão por um toometrics de dados do cliente também são faturáveis com taxas padrão. Se você configurou uma política de retenção de dados, que não seja cobrado quando o armazenamento do Azure excluir dados de métricas antigos. No entanto, se você excluir dados de análise, sua conta é cobrada Olá para operações de exclusão.

capacidade de saudação usada por tabelas de métricas de saudação também é cobrável: você pode usar o hello tooestimate quantidade de saudação do usado para armazenar dados de métricas de capacidade a seguir:

* Se a cada hora um serviço utilizar cada API em cada serviço, cerca de 148KB de dados é armazenado nas tabelas de transações de métricas de saudação a cada hora se você tiver ativado o serviço e o resumo de nível de API.
* Se a cada hora um serviço utilizar cada API em cada serviço, cerca de 12KB de dados é armazenado nas tabelas de transações de métricas de saudação a cada hora se você tiver habilitado o nível de serviço apenas resumo.
* Olá, tabela de capacidade para blobs tem duas linhas adicionadas por dia (fornecida pelo usuário tenha optado pelos logs): isso implica que cada dia Olá tamanho dessa tabela aumenta conforme o tooapproximately 300 bytes.

## <a name="next-steps"></a>Próximas etapas
[Habilitando o armazenamento de log e acessando os dados de log](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
