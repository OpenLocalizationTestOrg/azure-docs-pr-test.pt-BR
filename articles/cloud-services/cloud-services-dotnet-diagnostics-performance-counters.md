---
title: "aaaUse contadores de desempenho no diagnóstico do Azure | Microsoft Docs"
description: "Use os contadores de desempenho em serviços de nuvem do Azure ou máquina virtual toofind afunilamentos e ajustar o desempenho."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a>Criar e usar contadores de desempenho em um aplicativo do Azure
Este artigo descreve os benefícios de saudação do e como os contadores de desempenho de tooput em seu aplicativo do Azure. Você pode usá-los toocollect dados, detectar gargalos de e ajustar o desempenho do sistema e do aplicativo.

Contadores de desempenho disponíveis para o Windows Server, IIS e ASP.NET também podem ser coletados e usados toodetermine integridade de saudação de suas funções web do Azure, funções de trabalho e máquinas virtuais. Você também pode criar e usar contadores de desempenho personalizados.  

É possível examinar os dados do contador de desempenho

1. Diretamente no host de aplicativo hello com a ferramenta de Monitor de desempenho Olá acessada usando a área de trabalho remota
2. Com o System Center Operations Manager usando Olá o pacote de gerenciamento do Azure
3. Com outras ferramentas de monitoramentos que acessam Olá dados de diagnóstico transferidos tooAzure armazenamento. Consulte [Armazenar e exibir dados de diagnóstico no armazenamento do Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) para saber mais.  

Para obter mais informações sobre como monitorar o desempenho de saudação do seu aplicativo em Olá [portal do Azure](http://portal.azure.com/), consulte [como serviços em nuvem tooMonitor](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).

Para obter orientação detalhada adicional sobre como criar um registro em log e rastreamento estratégia e uso de diagnóstico e outros problemas de tootroubleshoot técnicas e otimizar aplicativos do Azure, consulte [práticas recomendadas de solução de problemas para desenvolver o Azure Aplicativos](https://msdn.microsoft.com/library/azure/hh771389.aspx).

## <a name="enable-performance-counter-monitoring"></a>Habilitar o monitoramento do contador de desempenho
Os contadores de desempenho não estão habilitados por padrão. O aplicativo ou uma tarefa de inicialização deve modificar o diagnóstico de padrão de saudação contadores de desempenho de específicos de saudação do agente configuração tooinclude que você deseja toomonitor para cada instância de função.

### <a name="performance-counters-available-for-microsoft-azure"></a>Contadores de desempenho disponíveis para o Microsoft Azure
Azure fornece um subconjunto de contadores de desempenho de saudação disponíveis para Windows Server, IIS e Olá pilha do ASP.NET. Olá tabela a seguir lista alguns dos contadores de desempenho de saudação de interesse específico para aplicativos do Azure.

| Categoria do contador: Objeto (instância) | Nome do contador | Referência |
| --- | --- | --- |
| Exceções CLR do .NET (*Globais*) |Nº de Exceções Geradas/s |Contadores de Desempenho de Exceção |
| Memória CLR do .NET (*Global*) |% de Tempo na GC |Contadores de Desempenho de Memória |
| ASP.NET |Reinicializações de Aplicativo |Contadores de Desempenho do ASP.NET |
| ASP.NET |Tempo de Execução de Solicitação |Contadores de Desempenho do ASP.NET |
| ASP.NET |Solicitações Desconectadas |Contadores de Desempenho do ASP.NET |
| ASP.NET |Reinicializações do processo de trabalho |Contadores de Desempenho do ASP.NET |
| Aplicativos ASP.NET (**Total**) |Total de Solicitações |Contadores de Desempenho do ASP.NET |
| Aplicativos ASP.NET (**Total**) |Solicitações/s |Contadores de Desempenho do ASP.NET |
| ASP.NET v4.0.30319 |Tempo de Execução de Solicitação |Contadores de Desempenho do ASP.NET |
| ASP.NET v4.0.30319 |Tempo de Espera da Solicitação |Contadores de Desempenho do ASP.NET |
| ASP.NET v4.0.30319 |Solicitações Atuais |Contadores de Desempenho do ASP.NET |
| ASP.NET v4.0.30319 |Solicitações Enfileiradas |Contadores de Desempenho do ASP.NET |
| ASP.NET v4.0.30319 |Solicitações Rejeitadas |Contadores de Desempenho do ASP.NET |
| Memória |MBytes Disponíveis |Contadores de Desempenho de Memória |
| Memória |Bytes Confirmados |Contadores de Desempenho de Memória |
| Processador(_Total) |% Tempo do Processador |Contadores de Desempenho do ASP.NET |
| TCPv4 |Falhas de Conexão |Objeto TCP |
| TCPv4 |Conexões Estabelecidas |Objeto TCP |
| TCPv4 |Conexões Redefinidas |Objeto TCP |
| TCPv4 |Segmentos Enviados/s |Objeto TCP |
| Interface de Rede(*) |Bytes Recebidos/s |Objeto da Interface de Rede |
| Interface de Rede(*) |Bytes Enviados/s |Objeto da Interface de Rede |
| Interface de Rede (Adaptador de Rede do Barramento da Máquina Virtual da Microsoft _2) |Bytes Recebidos/s |Objeto da Interface de Rede |
| Interface de Rede (Adaptador de Rede do Barramento da Máquina Virtual da Microsoft _2) |Bytes Enviados/s |Objeto da Interface de Rede |
| Interface de Rede (Adaptador de Rede do Barramento da Máquina Virtual da Microsoft _2) |Bytes Totais/s |Objeto da Interface de Rede |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a>Criar e adicionar o aplicativo de tooyour de contadores de desempenho personalizados
O Azure tem suporte toocreate e modificar os contadores de desempenho personalizados para funções web e funções de trabalho. contadores de saudação podem ser usado comportamento de específicas do aplicativo de tootrack e monitor. Você pode criar e excluir categorias de contador de desempenho personalizados e especificadores de uma tarefa de inicialização, função Web ou função de trabalho com permissões elevadas.

> [!NOTE]
> Código que faz alterações toocustom contadores de desempenho deve ter elevado toorun de permissões. Se código Olá estiver em uma função web ou função de trabalho, função hello deve incluir a marca Olá <Runtime executionContext="elevated" /> em Olá servicedefinition. Csdef de arquivos para Olá função tooinitialize corretamente.
>
>

Você pode enviar o armazenamento de desempenho personalizado contador dados tooAzure usando o agente de diagnóstico de saudação.

dados do contador de desempenho padrão Olá são gerados pelo hello que Azure processa. Os dados personalizados de contador de desempenho devem ser criados pela sua função de trabalho ou aplicativo Web de função de trabalho. Consulte [tipos de contador de desempenho](https://msdn.microsoft.com/library/z573042h.aspx) para obter informações sobre tipos de saudação de dados que podem ser armazenados em contadores de desempenho personalizados. Consulte [Exemplo de PerformanceCounters](http://code.msdn.microsoft.com/azure/) para ver um exemplo que cria e define os dados do contador de desempenho personalizados em uma função Web.

## <a name="store-and-view-performance-counter-data"></a>Armazenar e exibir dados do contador de desempenho
O Azure armazena em cache os dados do contador de desempenho com outras informações de diagnóstico. Esses dados estão disponíveis para monitoramento remoto enquanto a instância de função hello está em execução usando as ferramentas de tooview de acesso de área de trabalho remota como o Monitor de desempenho. toopersist Olá fora da instância de função hello, agente de diagnóstico Olá deve transferência de dados de armazenamento de tooAzure Olá dados. limite de tamanho de saudação de saudação em cache dados do contador de desempenho pode ser configurada no agente de diagnóstico hello, ou pode ser configurado toobe parte de um limite compartilhado para todos os dados de diagnóstico de hello. Para obter mais informações sobre como definir o tamanho do buffer hello, consulte [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) e [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx). Consulte [armazenar e exibir dados de diagnóstico no armazenamento do Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) para obter uma visão geral de configuração de conta de armazenamento Olá diagnóstico agente tootransfer dados tooa.

Cada instância do contador de desempenho configurado é registrada em uma taxa de amostragem especificada e dados de amostra de saudação for transferidos toohello conta de armazenamento por uma solicitação de transferência agendada ou uma solicitação de transferência sob demanda. As transferências automáticas podem ser agendadas com uma frequência de até uma vez por minuto. Dados de contador de desempenho transferidos pelo agente de diagnóstico de saudação é armazenados em uma tabela, WADPerformanceCountersTable, na conta de armazenamento hello. Essa tabela pode ser acessada e consultada com métodos padrão da API do armazenamento do Azure. Consulte [exemplo de PerformanceCounters do Microsoft Azure](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) para obter um exemplo de como consultar e exibir dados de contador de desempenho da tabela de WADPerformanceCountersTable hello.

> [!NOTE]
> Dependendo da frequência de transferência de agente de diagnóstico hello e latência de fila, hello dados mais recentes do contador de desempenho na conta de armazenamento Olá podem estar vários minutos desatualizados.
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a>Habilitar os contadores de desempenho usando o arquivo de configuração de diagnóstico
Use Olá seguintes contadores de desempenho do procedimento tooenable em seu aplicativo do Azure.

## <a name="prerequisites"></a>Pré-requisitos
Esta seção pressupõe que você tiver importado o monitor de diagnóstico de saudação para seu aplicativo e adicionado Olá diagnóstico configuração arquivo tooyour Visual Studio solução (wadcfg no SDK 2.4 e abaixo ou wadcfgx no SDK 2.5 e superior). Consulte as etapas 1 e 2 em [Habilitando o Diagnóstico nos Serviços de Nuvem do Azure e Máquinas Virtuais](cloud-services-dotnet-diagnostics.md) para obter mais informações.

## <a name="step-1-collect-and-store-data-from-performance-counters"></a>Etapa 1: Coletar e armazenar dados de contadores de desempenho
Depois que você adicionou Olá diagnóstico arquivo tooyour solução do Visual Studio, você pode configurar coleta de saudação e o armazenamento de dados do contador de desempenho em um aplicativo do Azure. Isso é feito adicionando o arquivo de diagnóstico de toohello de contadores de desempenho. Dados de diagnóstico, incluindo contadores de desempenho são coletados primeiro na instância de saudação. dados de saudação forem persistente toohello WADPerformanceCountersTable tabela Olá serviço tabela do Azure, para que você também precisa toospecify Olá conta de armazenamento em seu aplicativo. Se você estiver testando seu aplicativo localmente no emulador de computação do hello, você também pode armazenar dados de diagnóstico localmente no emulador de armazenamento de saudação. Antes de armazenar dados de diagnóstico, você deverá primeiro ir toohello [portal do Azure](http://portal.azure.com/) e crie uma conta de armazenamento clássicos. Uma prática recomendada é toolocate sua conta de armazenamento Olá mesma localização geográfica que seu aplicativo do Azure. Por manter Olá conta de armazenamento e de aplicativo do Azure estão em Olá mesma localização geográfica, evitar pagar custos externos de largura de banda e reduzir a latência.

### <a name="add-performance-counters-toohello-diagnostics-file"></a>Adicionar arquivo de diagnóstico de toohello de contadores de desempenho
Há muitos contadores que você pode usar. Olá, exemplo a seguir mostra vários contadores de desempenho que são recomendados para web e monitoramento de função de trabalho.

Abra o arquivo de diagnóstico hello (wadcfg no SDK 2.4 e anterior ou wadcfgx no SDK 2.5 e superior) e adicione Olá toohello DiagnosticMonitorConfiguration elemento a seguir:

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

atributo de bufferQuotaInMB Hello, que especifica a quantidade máxima de saudação do armazenamento do sistema de arquivos que está disponível para o tipo de coleção de dados de saudação (logs do Azure, logs do IIS, etc.). saudação padrão é 0. Quando Olá cota for atingida, dados mais antigos Olá são excluídos como novos dados são adicionados. soma de saudação de todas as propriedades de bufferQuotaInMB Olá deve ser maior que o valor do atributo de OverallQuotaInMB Olá Olá. Para obter uma discussão mais detalhada de determinar a quantidade de armazenamento será necessária para a saudação de coleta de dados de diagnóstico, consulte Olá seção Configurar WAD de [práticas recomendadas de solução de problemas para desenvolver aplicativos do Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).

atributo de scheduledTransferPeriod Hello, que especifica o intervalo de saudação entre transferências agendadas de dados, arredondado toohello mais próximo minuto. Olá exemplos a seguir, ele é definido tooPT30M (30 minutos). Configuração Olá transferência tooa período valor pequeno, como 1 minuto, afetará negativamente o desempenho do seu aplicativo em produção, mas pode ser útil para ver o diagnóstico funcionando rapidamente quando você está testando. o período de transferência programado Olá deve ser pequeno o suficiente tooensure que os dados de diagnóstico não são substituídos na instância de hello, mas grande o suficiente para que ele não afetará o desempenho de saudação do seu aplicativo.

atributo de counterSpecifier Olá Especifica Olá toocollect de contador de desempenho. atributo de sampleRate Olá Especifica a taxa de saudação em que o contador de desempenho Olá deve ser testado, nesse caso 30 segundos.

Depois de adicionar contadores de desempenho de saudação que você deseja toocollect, salve o arquivo de diagnóstico de toohello de alterações. Em seguida, você precisa de conta de armazenamento de Olá toospecify que os dados de diagnóstico hello serão persistidos.

### <a name="specify-hello-storage-account"></a>Especifique a conta de armazenamento Olá
toopersist conta sua informações de diagnóstico tooyour armazenamento do Azure, você deve especificar uma cadeia de caracteres de conexão no arquivo de configuração (ServiceConfiguration. cscfg) do serviço.

2.5 do SDK do Azure, Olá conta de armazenamento pode ser especificado no arquivo de wadcfgx hello.

> [!NOTE]
> Essas instruções se aplicam somente a tooAzure SDK 2.4 e anterior. 2.5 do SDK do Azure, Olá conta de armazenamento pode ser especificado no arquivo de wadcfgx hello.
>
>

cadeias de conexão de saudação tooset:

1. Abra o arquivo de ServiceConfiguration hello usando seu editor de texto favorito e a cadeia de caracteres de conexão do conjunto Olá para seu armazenamento. Olá *AccountName* e *AccountKey* valores são encontrados na Olá portal do Azure no painel de conta de armazenamento hello, em chaves de acesso.

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. Salve o arquivo de ServiceConfiguration hello.
3. Abrir o arquivo de ServiceConfiguration Olá e verificar se UseDevelopmentStorage está definida tootrue.

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   Agora que as cadeias de caracteres de conexão Olá forem definidas, o aplicativo persistirá conta de armazenamento do tooyour de dados de diagnóstico quando seu aplicativo é implantado.
4. Salve e compile seu projeto e implante seu aplicativo.

## <a name="step-2-optional-create-custom-performance-counters"></a>Etapa 2: (Opcional) Criar contadores de desempenho personalizados
Além disso toohello predefinidas contadores de desempenho, você pode adicionar que sua próprias de desempenho personalizados contadores toomonitor funções de web ou de trabalho. Contadores de desempenho personalizados podem ser comportamento usado tootrack e monitor de específicas do aplicativo e pode ser criados ou excluídos em uma tarefa de inicialização, a função web ou a função de trabalho com permissões elevadas.

Agente de diagnóstico do Azure Olá atualiza Olá desempenho configuração do contador do arquivo. wadcfg de saudação um minuto após a inicialização.  Se você criar contadores de desempenho personalizados no método OnStart da saudação e suas tarefas de inicialização demorar mais do que um minuto tooexecute, seus contadores de desempenho personalizados não terá sido criadas quando o agente de diagnóstico do Azure Olá tenta tooload-los.  Nesse cenário, você verá que o diagnóstico do Azure captura corretamente todos os dados de diagnóstico exceto os seus contadores de desempenho personalizados.  tooresolve esse problema, crie Olá contadores de desempenho em uma tarefa de inicialização ou mover alguns dos sua tarefa de inicialização funcionam toohello OnStart método depois de criar hello contadores de desempenho.

Execute Olá etapas toocreate um contador denominado "\MyCustomCounterCategory\MyButton1Counter" de desempenho personalizado simples a seguir:

1. Abra o arquivo de definição de serviço hello (CSDEF) para o seu aplicativo.
2. Adicione Olá Runtime elemento toohello WebRole ou WorkerRole elemento tooallow execução com privilégios elevados:

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. Salve o arquivo hello.
4. Abra o arquivo de diagnóstico hello (wadcfg no SDK 2.4 e anterior ou wadcfgx no SDK 2.5 e superior) e adicione Olá toohello DiagnosticMonitorConfiguration a seguir

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. Salve o arquivo hello.
6. Crie categoria do contador de desempenho personalizados Olá no método OnStart de saudação de sua função, antes de chamar base. OnStart. Olá c# exemplo a seguir cria uma categoria personalizada, se ele ainda não existir:

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. Atualize contadores hello dentro de seu aplicativo. saudação de exemplo a seguir atualiza um contador de desempenho personalizados em eventos Button1_Click:

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. Salve o arquivo hello.  

Dados do contador de desempenho personalizados agora serão coletados pelo monitor de diagnóstico do Azure hello.

## <a name="step-3-query-performance-counter-data"></a>Etapa 3: Consultar dados do contador de desempenho
Depois que seu aplicativo é implantado e em execução, o monitor de diagnóstico Olá começarão a coletar contadores de desempenho e persistentes que tooAzure de armazenamento de dados. Use ferramentas como o Gerenciador de servidores no Visual Studio, [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), ou [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) por Cerebrata dados Olá de contadores de desempenho de saudação do tooview Tabela WADPerformanceCountersTable. Você pode consultar também programaticamente usando o serviço tabela Olá [c#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), ou [PHP](../cosmos-db/table-storage-how-to-use-php.md).

Olá c# de exemplo seguinte mostra uma consulta básica em relação à tabela WADPerformanceCountersTable hello e salva o arquivo CSV do hello diagnóstico dados tooa. Depois que os contadores de desempenho de saudação são salvos tooa arquivo CSV, você pode usar Olá graficamente recursos no Microsoft Excel ou outros ferramenta toovisualize Olá dados. Ser tooadd se tooMicrosoft.WindowsAzure.Storage.dll uma referência, que está incluído no hello Azure SDK para .NET de outubro de 2012 e posterior. assembly Hello é instalado toohello % programa Files%\Microsoft SDKs\Microsoft Azure.NET sdk\version-num\ref\. directory.

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

Entidades são mapeadas tooC # objetos usando uma classe personalizada derivada de **TableEntity**. Olá, código a seguir define uma classe de entidade que representa um contador de desempenho no hello **WADPerformanceCountersTable** tabela.

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a>Próximas etapas
[Exibir artigos adicionais sobre o Diagnóstico do Azure](../azure-diagnostics.md)
