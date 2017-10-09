---
title: "as métricas de armazenamento aaaEnabling em Olá portal do Azure | Microsoft Docs"
description: "Como as métricas de armazenamento tooenable para Olá serviços Blob, fila, tabela e arquivo"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 2fb5b229-f099-4334-92be-4e0e7dd257d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 4c990371e08a6586d935b0535149eabd4960cfaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a>Habilitando métricas de armazenamento e exibição de dados de métricas
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a>Visão geral
As Métricas de Armazenamento são habilitadas por padrão quando você cria uma nova conta de armazenamento. Você pode configurar o monitoramento usando qualquer Olá [Portal clássico do Azure](https://manage.windowsazure.com), Windows PowerShell, ou programaticamente por meio de uma API de armazenamento.

Quando você habilita as métricas de armazenamento, você deve escolher um período de retenção de dados de saudação: esse período determina para armazenamento de saudação quanto tempo o serviço mantém métricas hello e encargos por Olá espaço necessário toostore-los. Normalmente, você deve usar um período de retenção mais curto para métricas de minuto de hora devido a espaço adicional significativo Olá necessário para métricas de minuto. Você deve escolher um período de retenção, de modo que você tem dados suficientes de saudação de tooanalyze tempo e baixar as métricas que você deseja tookeep para análise offline ou para fins de relatório. Lembre-se de que você também será cobrado para baixar dados de métrica de sua conta de armazenamento.

## <a name="how-tooenable-storage-metrics-using-hello-azure-classic-portal"></a>Como as métricas de armazenamento tooenable usando Olá Portal clássico do Azure
Em Olá [Portal clássico do Azure](https://manage.windowsazure.com), você usar a página Configurar de saudação para uma conta de armazenamento toocontrol as métricas de armazenamento. Para monitoramento, você pode definir um nível e um período de retenção em dias para cada um dos blobs, tabelas e filas. Em cada caso, o nível de saudação é um dos seguintes hello:

* Desativado — nenhuma métrica será coletada.
* Mínimo — As métricas de armazenamento coleta um conjunto básico de métricas como ingresso/egresso, disponibilidade, latência e porcentagens de êxito, que são agregadas para os serviços de Blob, tabela e fila hello.
* Detalhado, Coleta de métricas de armazenamento, um conjunto completo de métricas que inclui Olá mesmas métricas para cada operação da API de armazenamento, além de toohello nível de serviço métricas. As métricas no modo detalhado permitem uma análise mais próxima dos problemas que ocorrem durante operações de aplicativo.

Observe que Olá Portal clássico do Azure atualmente permite que você tooconfigure métricas de minutos em sua conta de armazenamento; Você deve habilitar métricas de minuto usando o PowerShell ou programaticamente.

## <a name="how-tooenable-storage-metrics-using-powershell"></a>Como as métricas de armazenamento tooenable usando o PowerShell
Você pode usar o PowerShell em tooconfigure seu computador local as métricas de armazenamento em sua conta de armazenamento usando hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve Olá configurações atuais e Olá cmdlet Set-AzureStorageServiceMetricsProperty toochange Olá as configurações atuais.

Olá que controlam as métricas de armazenamento usam Olá parâmetros a seguir:

* Os valorespossíveis de MetricsType são hora e minuto.
* Os possíveis valores de ServiceType são Blob, Fila e Tabela.
* MetricsLevel os valores possíveis são: None (tooOff equivalente no hello Portal clássico do Azure), o serviço (tooMinimal equivalente no hello Portal clássico do Azure) e ServiceAndApi (tooVerbose equivalente no hello Portal clássico do Azure).

Por exemplo, hello seguinte comando ativa em minuto métricas para serviço de blob de saudação em sua conta de armazenamento padrão com o período de retenção Olá definir toofive dias:

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
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
Quando você tiver configurado as métricas de armazenamento toomonitor sua conta de armazenamento, ele registra as métricas de saudação em um conjunto de tabelas bem conhecidas em sua conta de armazenamento. Você pode usar a página de Monitor de saudação para sua conta de armazenamento Olá métricas de hora do Portal clássico do Azure tooview Olá assim que estiverem disponíveis em um gráfico. Nessa página na Olá Portal clássico do Azure, você pode:

* Selecione quais tooplot métricas no gráfico de hello (Olá escolha de métricas disponíveis dependerá se você escolheu o monitoramento detalhado ou mínimo para o serviço de saudação na página Configurar de saudação).
* Selecione o intervalo de tempo de saudação para métricas de saudação exibidas no gráfico de saudação.
* Escolha toouse uma métrica de saudação tooplot escala absoluta ou relativa.
* Configurar toonotify de alertas de email quando uma métrica específica atinge determinado valor.

Se quiser que as métricas de saudação toodownload para armazenamento de longo prazo ou tooanalyze-las localmente, você precisa toouse uma ferramenta ou escrever um código tooread tabelas de saudação. Você deve baixar as métricas de minutos de saudação para análise. Olá tabelas não aparecem se você listar todas as tabelas de saudação em sua conta de armazenamento, mas você pode acessá-los diretamente por nome. Muitas ferramentas de navegação de armazenamento de terceiros reconhecem essas tabelas e permitem que você tooview-los diretamente (consulte a postagem de blog Olá [gerenciadores de armazenamento do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) para obter uma lista de ferramentas disponíveis).

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

Considere configurar alertas em Olá Portal clássico do Azure na página do Monitor de saudação para que as métricas de armazenamento pode notificá-lo automaticamente de alterações importantes no comportamento de saudação de seus serviços de armazenamento. Se você usar esses dados de métricas de um toodownload de ferramenta do Gerenciador de armazenamento em um formato delimitado, você pode usar dados do Microsoft Excel tooanalyze saudação. Consulte a postagem de blog Olá [gerenciadores de armazenamento do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) para obter uma lista de ferramentas do Gerenciador de armazenamento disponível.

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

## <a name="next-steps"></a>Próximas etapas:
[Habilitando o armazenamento de análise de log e acessando os dados de log](https://msdn.microsoft.com/library/dn782840.aspx)
