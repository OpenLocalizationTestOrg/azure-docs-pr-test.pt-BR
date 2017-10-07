---
title: aaaManagement .NET SDK para o Azure Stream Analytics | Microsoft Docs
description: "Comece com o SDK .NET do Azure Stream Analytics Management. Saiba como tooset up e executar trabalhos de análise. Criar um projeto, entradas, saídas e transformações."
keywords: ".NET SDK, API de análise"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5e93de87-0c6f-4f4b-be98-08d63f832897
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/06/2017
ms.author: jeffstok
ms.openlocfilehash: 507c11938bc5bf2249a2e41f6bcc076db8ead3f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a>Gerenciamento de SDK .NET: Configurar e executar trabalhos de análise usando Olá API de análise de fluxo do Azure para .NET
Saiba como tooset backup e trabalhos de análise de execução usando Olá API de análise de fluxo para .NET usando Olá SDK .NET de gerenciamento. Configurar um projeto, criar fontes de entrada e saídas, transformações e iniciar e parar trabalhos. Seus trabalhos de análise, você pode transmitir dados de armazenamento de Blob ou de um hub de eventos.

Consulte Olá [documentação de referência de gerenciamento para Olá API de análise de fluxo para .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).

Análise de fluxo do Azure é um serviço totalmente gerenciado fornecendo processamento de eventos de baixa latência, altamente disponível, escalonável e complexas ao longo do fluxo de dados na nuvem hello. Análise de fluxo permite que os clientes tooset o streaming de fluxos de dados de tooanalyze trabalhos e permite que toodrive próximo a análise em tempo real.  

> [!NOTE]
> Atualizamos o código de exemplo hello neste artigo com a versão do SDK do .NET do Azure Stream Analytics gerenciamento v2. x. Para exemplo de código usando Olá usa a versão do SDK lagecy (1. x), consulte [usar v1. x do hello SDK .NET de gerenciamento de análise de fluxo](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este artigo, você deve ter o seguinte hello:

* Instale o Visual Studio 2017 ou 2015.
* Baixe e instale o [Azure .NET SDK](https://azure.microsoft.com/downloads/).
* Crie um grupo de recursos do Azure em sua assinatura. a seguir Olá é um exemplo de script do PowerShell do Azure. Para obter mais informações sobre o PowerShell do Azure, consulte [Instalar e configurar o PowerShell do Azure](/powershell/azure/overview).  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* Configurar uma fonte de entrada e saída toouse de destino. Para obter mais instruções, consulte [adicionar entradas](stream-analytics-add-inputs.md) tooset uma entrada de exemplo e [adicionar saídas](stream-analytics-add-outputs.md) tooset a uma saída de exemplo.

## <a name="set-up-a-project"></a>Configurar um projeto
toocreate um trabalho de análise use Olá API de análise de fluxo para .NET, primeiro configure seu projeto.

1. Crie um aplicativo de console do Visual Studio C# .NET.
2. Olá Package Manager Console, seguinte Olá execução comandos de pacotes do NuGet Olá tooinstall. Olá primeiro um é hello gerenciamento .NET SDK do Azure Stream Analytics. Olá segundo é para autenticação de cliente do Azure.
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. Adicione o seguinte Olá **appSettings** arquivo App. config da seção toohello:
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    Substitua os valores por **SubscriptionId** e **ActiveDirectoryTenantId** por suas IDs de assinatura e locatário do Azure. Você pode obter esses valores executando hello Azure PowerShell cmdlet a seguir:

        Get-AzureAccount

4. Adicione Olá referência em seu arquivo. csproj a seguir:

        <Reference Include="System.Configuration" />

5. Adicione o seguinte Olá **usando** arquivo de origem toohello instruções (Program.cs) no projeto de saudação:
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. Adicione um método auxiliar de autenticação:

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a>Crie um cliente de gerenciamento do Stream Analytics
Um **StreamAnalyticsManagementClient** objeto permite que você toomanage Olá trabalho e hello trabalho componentes, como entrada, saída e transformação.

Adicionar Olá após o início do código toohello de saudação **principal** método:

   ```
    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamingJobName = "<YOUR STREAMING JOB NAME>";
    string inputName = "<YOUR JOB INPUT NAME>";
    string transformationName = "<YOUR JOB TRANSFORMATION NAME>";
    string outputName = "<YOUR JOB OUTPUT NAME>";
    
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    
    // Get credentials
    ServiceClientCredentials credentials = GetCredentials().Result;
    
    // Create Stream Analytics management client
    StreamAnalyticsManagementClient streamAnalyticsManagementClient = new StreamAnalyticsManagementClient(credentials)
    {
        SubscriptionId = ConfigurationManager.AppSettings["SubscriptionId"]
    };
   ```

Olá **resourceGroupName** valor da variável deve ser Olá igual ao nome de saudação do recurso de saudação de grupo é criado ou separados em etapas de pré-requisito hello.

proporção de apresentação de credencial tooautomate Olá da criação de trabalho, consulte muito[autenticar uma entidade de serviço com o Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Olá seções restantes deste artigo presumem que este código seja no início de saudação do hello **principal** método.

## <a name="create-a-stream-analytics-job"></a>Criar um trabalho de Stream Analytics
Olá código a seguir cria um trabalho do Stream Analytics no grupo de recursos de saudação que você definiu. Você adicionará um trabalho de entrada, saída e transformação toohello mais tarde.

   ```
   // Create a streaming job
   StreamingJob streamingJob = new StreamingJob()
   {
       Tags = new Dictionary<string, string>()
       {
           { "Origin", ".NET SDK" },
           { "ReasonCreated", "Getting started tutorial" }
       },
       Location = "West US",
       EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Drop,
       EventsOutOfOrderMaxDelayInSeconds = 5,
       EventsLateArrivalMaxDelayInSeconds = 16,
       OutputErrorPolicy = OutputErrorPolicy.Drop,
       DataLocale = "en-US",
       CompatibilityLevel = CompatibilityLevel.OneFullStopZero,
       Sku = new Sku()
       {
           Name = SkuName.Standard
       }
   };
   StreamingJob createStreamingJobResult = streamAnalyticsManagementClient.StreamingJobs.CreateOrReplace(streamingJob, resourceGroupName, streamingJobName);
   ```

## <a name="create-a-stream-analytics-input-source"></a>Criar uma fonte de entrada do Stream Analytics
Olá código a seguir cria uma fonte de entrada de análise de fluxo com o tipo de fonte de entrada de blob hello e serialização de CSV. toocreate uma fonte de entrada de hub de evento, use **EventHubStreamInputDataSource** em vez de **BlobStreamInputDataSource**. Da mesma forma, você pode personalizar o tipo de serialização Olá Olá da fonte de entrada.

   ```
   // Create an input
   StorageAccount storageAccount = new StorageAccount()
   {
       AccountName = "<YOUR STORAGE ACCOUNT NAME>",
       AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
   };
   Input input = new Input()
   {
       Properties = new StreamInputProperties()
       {
           Serialization = new CsvSerialization()
           {
               FieldDelimiter = ",",
               Encoding = Encoding.UTF8
           },
           Datasource = new BlobStreamInputDataSource()
           {
               StorageAccounts = new[] { storageAccount },
               Container = "<YOUR STORAGE BLOB CONTAINER>",
               PathPattern = "{date}/{time}",
               DateFormat = "yyyy/MM/dd",
               TimeFormat = "HH",
               SourcePartitionCount = 16
           }
       }
   };
   Input createInputResult = streamAnalyticsManagementClient.Inputs.CreateOrReplace(input, resourceGroupName, streamingJobName, inputName);
   ```

Fontes de entrada, do armazenamento de Blob ou de um hub de eventos são específicas de trabalho tooa associado. toouse Olá a mesma fonte de entrada para tarefas diferentes, você deve chamar o método hello novamente e especifique um nome de trabalho diferente.

## <a name="test-a-stream-analytics-input-source"></a>Testar uma fonte de entrada do Stream Analytics
Olá **TestConnection** se o trabalho de análise de fluxo de saudação é capaz de tooconnect toohello entrada origem, bem como outros toohello de aspectos específicos de testes de método de tipo de fonte de entrada. Por exemplo, na fonte de entrada de blob Olá criados em uma etapa anterior, método hello verificará que o nome de conta de armazenamento hello e par de chaves pode ser usado tooconnect toohello conta de armazenamento, bem como verificar que contêiner Olá especificado existe.

   ```
   // Test hello connection toohello input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a>Criar um destino de saída do Stream Analytics
Criar um destino de saída é muito semelhante toocreating uma fonte de entrada de análise de fluxo. Como fontes de entrada, os destinos de saída são trabalho específico tooa associado. toouse Olá mesmo destino de saída para trabalhos de diferentes, você deve chamar o método hello novamente e especifique um nome de trabalho diferente.

saudação de código a seguir cria um destino de saída (banco de dados do SQL Azure). Você pode personalizar o tipo de dados de destino da saída de hello e/ou tipo de serialização.

   ```
   // Create an output
   Output output = new Output()
   {
       Datasource = new AzureSqlDatabaseOutputDataSource()
       {
           Server = "<YOUR DATABASE SERVER NAME>",
           Database = "<YOUR DATABASE NAME>",
           User = "<YOUR DATABASE LOGIN>",
           Password = "<YOUR DATABASE LOGIN PASSWORD>",
           Table = "<YOUR DATABASE TABLE NAME>"
       }
   };
   Output createOutputResult = streamAnalyticsManagementClient.Outputs.CreateOrReplace(output, resourceGroupName, streamingJobName, outputName);
   ```

## <a name="test-a-stream-analytics-output-target"></a>Testar um destino de saída do Stream Analytics
Um destino de análise de fluxo de saída também tem Olá **TestConnection** método para conexões de teste.

   ```
   // Test hello connection toohello output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a>Criar uma transformação do Stream Analytics
Olá código a seguir cria uma transformação de análise de fluxo com consulta hello "Selecione * de entrada" e especifica tooallocate uma unidade de streaming para o trabalho de análise de fluxo de saudação. Para obter mais informações sobre o ajuste de unidades de streaming, consulte Dimensionar trabalhos do [Escalonar trabalhos de Análise de fluxo do Azure](stream-analytics-scale-jobs.md).

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with hello value you put for hello 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

Como entrada e saída, uma transformação é também trabalho do Stream Analytics específico toohello associado em que foi criado.

## <a name="start-a-stream-analytics-job"></a>Iniciar um trabalho do Stream Analytics
Depois de criar um trabalho de análise de fluxo e suas entradas, saídas e transformação, você pode iniciar trabalho Olá Olá chamada **iniciar** método.

Olá, código de exemplo a seguir inicia um trabalho de análise de fluxo com uma saída personalizada start time conjunto tooDecember 12, 2012, 12:12:12 UTC:

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a>Interromper um trabalho do Stream Analytics
Você pode interromper um trabalho de análise de fluxo em execução, Olá chamada **parar** método.

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a>Excluir um trabalho do Stream Analytics
Olá **excluir** método irá excluir trabalho hello, bem como Olá subjacente sub-recursos, inclusive entradas, saídas e transformação de trabalho hello.

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a>Obtenha suporte
Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
Você aprendeu Noções básicas de saudação do uso de um SDK .NET toocreate e executar trabalhos de análise. toolearn mais, consulte o seguinte hello:

* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [SDK .NET do Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn889315.aspx)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->
[5]: ./media/markdown-template-for-new-articles/octocats.png
[6]: ./media/markdown-template-for-new-articles/pretty49.png
[7]: ./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[azure.blob.storage]: http://azure.microsoft.com/documentation/services/storage/
[azure.blob.storage.use]: http://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/

[azure.event.hubs]: http://azure.microsoft.com/services/event-hubs/
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.forum]: http://go.microsoft.com/fwlink/?LinkId=512151

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
