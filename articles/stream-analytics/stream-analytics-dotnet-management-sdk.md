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
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a><span data-ttu-id="94d4f-106">Gerenciamento de SDK .NET: Configurar e executar trabalhos de análise usando Olá API de análise de fluxo do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="94d4f-106">Management .NET SDK: Set up and run analytics jobs using hello Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="94d4f-107">Saiba como tooset backup e trabalhos de análise de execução usando Olá API de análise de fluxo para .NET usando Olá SDK .NET de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="94d4f-107">Learn how tooset up and run analytics jobs using hello Stream Analytics API for .NET using hello Management .NET SDK.</span></span> <span data-ttu-id="94d4f-108">Configurar um projeto, criar fontes de entrada e saídas, transformações e iniciar e parar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="94d4f-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="94d4f-109">Seus trabalhos de análise, você pode transmitir dados de armazenamento de Blob ou de um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="94d4f-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="94d4f-110">Consulte Olá [documentação de referência de gerenciamento para Olá API de análise de fluxo para .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="94d4f-110">See hello [management reference documentation for hello Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="94d4f-111">Análise de fluxo do Azure é um serviço totalmente gerenciado fornecendo processamento de eventos de baixa latência, altamente disponível, escalonável e complexas ao longo do fluxo de dados na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="94d4f-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="94d4f-112">Análise de fluxo permite que os clientes tooset o streaming de fluxos de dados de tooanalyze trabalhos e permite que toodrive próximo a análise em tempo real.</span><span class="sxs-lookup"><span data-stu-id="94d4f-112">Stream Analytics enables customers tooset up streaming jobs tooanalyze data streams, and allows them toodrive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="94d4f-113">Atualizamos o código de exemplo hello neste artigo com a versão do SDK do .NET do Azure Stream Analytics gerenciamento v2. x.</span><span class="sxs-lookup"><span data-stu-id="94d4f-113">We have updated hello sample code in this article with Azure Stream Analytics Management .NET SDK v2.x version.</span></span> <span data-ttu-id="94d4f-114">Para exemplo de código usando Olá usa a versão do SDK lagecy (1. x), consulte [usar v1. x do hello SDK .NET de gerenciamento de análise de fluxo](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span><span class="sxs-lookup"><span data-stu-id="94d4f-114">For sample code using hello uses lagecy (1.x) SDK version, please see [Use hello Management .NET SDK v1.x for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94d4f-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="94d4f-115">Prerequisites</span></span>
<span data-ttu-id="94d4f-116">Antes de começar este artigo, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="94d4f-116">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="94d4f-117">Instale o Visual Studio 2017 ou 2015.</span><span class="sxs-lookup"><span data-stu-id="94d4f-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="94d4f-118">Baixe e instale o [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="94d4f-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="94d4f-119">Crie um grupo de recursos do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="94d4f-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="94d4f-120">a seguir Olá é um exemplo de script do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="94d4f-120">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="94d4f-121">Para obter mais informações sobre o PowerShell do Azure, consulte [Instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="94d4f-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="94d4f-122">Configurar uma fonte de entrada e saída toouse de destino.</span><span class="sxs-lookup"><span data-stu-id="94d4f-122">Set up an input source and output target toouse.</span></span> <span data-ttu-id="94d4f-123">Para obter mais instruções, consulte [adicionar entradas](stream-analytics-add-inputs.md) tooset uma entrada de exemplo e [adicionar saídas](stream-analytics-add-outputs.md) tooset a uma saída de exemplo.</span><span class="sxs-lookup"><span data-stu-id="94d4f-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) tooset up a sample input and [Add Outputs](stream-analytics-add-outputs.md) tooset up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="94d4f-124">Configurar um projeto</span><span class="sxs-lookup"><span data-stu-id="94d4f-124">Set up a project</span></span>
<span data-ttu-id="94d4f-125">toocreate um trabalho de análise use Olá API de análise de fluxo para .NET, primeiro configure seu projeto.</span><span class="sxs-lookup"><span data-stu-id="94d4f-125">toocreate an analytics job use hello Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="94d4f-126">Crie um aplicativo de console do Visual Studio C# .NET.</span><span class="sxs-lookup"><span data-stu-id="94d4f-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="94d4f-127">Olá Package Manager Console, seguinte Olá execução comandos de pacotes do NuGet Olá tooinstall.</span><span class="sxs-lookup"><span data-stu-id="94d4f-127">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="94d4f-128">Olá primeiro um é hello gerenciamento .NET SDK do Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="94d4f-128">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="94d4f-129">Olá segundo é para autenticação de cliente do Azure.</span><span class="sxs-lookup"><span data-stu-id="94d4f-129">hello second one is for Azure client authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. <span data-ttu-id="94d4f-130">Adicione o seguinte Olá **appSettings** arquivo App. config da seção toohello:</span><span class="sxs-lookup"><span data-stu-id="94d4f-130">Add hello following **appSettings** section toohello App.config file:</span></span>
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    <span data-ttu-id="94d4f-131">Substitua os valores por **SubscriptionId** e **ActiveDirectoryTenantId** por suas IDs de assinatura e locatário do Azure.</span><span class="sxs-lookup"><span data-stu-id="94d4f-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="94d4f-132">Você pode obter esses valores executando hello Azure PowerShell cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="94d4f-132">You can get these values by running hello following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="94d4f-133">Adicione Olá referência em seu arquivo. csproj a seguir:</span><span class="sxs-lookup"><span data-stu-id="94d4f-133">Add hello following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

5. <span data-ttu-id="94d4f-134">Adicione o seguinte Olá **usando** arquivo de origem toohello instruções (Program.cs) no projeto de saudação:</span><span class="sxs-lookup"><span data-stu-id="94d4f-134">Add hello following **using** statements toohello source file (Program.cs) in hello project:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. <span data-ttu-id="94d4f-135">Adicione um método auxiliar de autenticação:</span><span class="sxs-lookup"><span data-stu-id="94d4f-135">Add an authentication helper method:</span></span>

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="94d4f-136">Crie um cliente de gerenciamento do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="94d4f-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="94d4f-137">Um **StreamAnalyticsManagementClient** objeto permite que você toomanage Olá trabalho e hello trabalho componentes, como entrada, saída e transformação.</span><span class="sxs-lookup"><span data-stu-id="94d4f-137">A **StreamAnalyticsManagementClient** object allows you toomanage hello job and hello job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="94d4f-138">Adicionar Olá após o início do código toohello de saudação **principal** método:</span><span class="sxs-lookup"><span data-stu-id="94d4f-138">Add hello following code toohello beginning of hello **Main** method:</span></span>

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

<span data-ttu-id="94d4f-139">Olá **resourceGroupName** valor da variável deve ser Olá igual ao nome de saudação do recurso de saudação de grupo é criado ou separados em etapas de pré-requisito hello.</span><span class="sxs-lookup"><span data-stu-id="94d4f-139">hello **resourceGroupName** variable's value should be hello same as hello name of hello resource group you created or picked in hello prerequisite steps.</span></span>

<span data-ttu-id="94d4f-140">proporção de apresentação de credencial tooautomate Olá da criação de trabalho, consulte muito[autenticar uma entidade de serviço com o Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="94d4f-140">tooautomate hello credential presentation aspect of job creation, refer too[Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="94d4f-141">Olá seções restantes deste artigo presumem que este código seja no início de saudação do hello **principal** método.</span><span class="sxs-lookup"><span data-stu-id="94d4f-141">hello remaining sections of this article assume that this code is at hello beginning of hello **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="94d4f-142">Criar um trabalho de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="94d4f-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="94d4f-143">Olá código a seguir cria um trabalho do Stream Analytics no grupo de recursos de saudação que você definiu.</span><span class="sxs-lookup"><span data-stu-id="94d4f-143">hello following code creates a Stream Analytics job under hello resource group that you have defined.</span></span> <span data-ttu-id="94d4f-144">Você adicionará um trabalho de entrada, saída e transformação toohello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="94d4f-144">You will add an input, output, and transformation toohello job later.</span></span>

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

## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="94d4f-145">Criar uma fonte de entrada do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="94d4f-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="94d4f-146">Olá código a seguir cria uma fonte de entrada de análise de fluxo com o tipo de fonte de entrada de blob hello e serialização de CSV.</span><span class="sxs-lookup"><span data-stu-id="94d4f-146">hello following code creates a Stream Analytics input source with hello blob input source type and CSV serialization.</span></span> <span data-ttu-id="94d4f-147">toocreate uma fonte de entrada de hub de evento, use **EventHubStreamInputDataSource** em vez de **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="94d4f-147">toocreate an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="94d4f-148">Da mesma forma, você pode personalizar o tipo de serialização Olá Olá da fonte de entrada.</span><span class="sxs-lookup"><span data-stu-id="94d4f-148">Similarly, you can customize hello serialization type of hello input source.</span></span>

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

<span data-ttu-id="94d4f-149">Fontes de entrada, do armazenamento de Blob ou de um hub de eventos são específicas de trabalho tooa associado.</span><span class="sxs-lookup"><span data-stu-id="94d4f-149">Input sources, whether from Blob storage or an event hub, are tied tooa specific job.</span></span> <span data-ttu-id="94d4f-150">toouse Olá a mesma fonte de entrada para tarefas diferentes, você deve chamar o método hello novamente e especifique um nome de trabalho diferente.</span><span class="sxs-lookup"><span data-stu-id="94d4f-150">toouse hello same input source for different jobs, you must call hello method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="94d4f-151">Testar uma fonte de entrada do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="94d4f-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="94d4f-152">Olá **TestConnection** se o trabalho de análise de fluxo de saudação é capaz de tooconnect toohello entrada origem, bem como outros toohello de aspectos específicos de testes de método de tipo de fonte de entrada.</span><span class="sxs-lookup"><span data-stu-id="94d4f-152">hello **TestConnection** method tests whether hello Stream Analytics job is able tooconnect toohello input source as well as other aspects specific toohello input source type.</span></span> <span data-ttu-id="94d4f-153">Por exemplo, na fonte de entrada de blob Olá criados em uma etapa anterior, método hello verificará que o nome de conta de armazenamento hello e par de chaves pode ser usado tooconnect toohello conta de armazenamento, bem como verificar que contêiner Olá especificado existe.</span><span class="sxs-lookup"><span data-stu-id="94d4f-153">For example, in hello blob input source you created in an earlier step, hello method will check that hello Storage account name and key pair can be used tooconnect toohello Storage account as well as check that hello specified container exists.</span></span>

   ```
   // Test hello connection toohello input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="94d4f-154">Criar um destino de saída do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="94d4f-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="94d4f-155">Criar um destino de saída é muito semelhante toocreating uma fonte de entrada de análise de fluxo.</span><span class="sxs-lookup"><span data-stu-id="94d4f-155">Creating an output target is very similar toocreating a Stream Analytics input source.</span></span> <span data-ttu-id="94d4f-156">Como fontes de entrada, os destinos de saída são trabalho específico tooa associado.</span><span class="sxs-lookup"><span data-stu-id="94d4f-156">Like input sources, output targets are tied tooa specific job.</span></span> <span data-ttu-id="94d4f-157">toouse Olá mesmo destino de saída para trabalhos de diferentes, você deve chamar o método hello novamente e especifique um nome de trabalho diferente.</span><span class="sxs-lookup"><span data-stu-id="94d4f-157">toouse hello same output target for different jobs, you must call hello method again and specify a different job name.</span></span>

<span data-ttu-id="94d4f-158">saudação de código a seguir cria um destino de saída (banco de dados do SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="94d4f-158">hello following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="94d4f-159">Você pode personalizar o tipo de dados de destino da saída de hello e/ou tipo de serialização.</span><span class="sxs-lookup"><span data-stu-id="94d4f-159">You can customize hello output target's data type and/or serialization type.</span></span>

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

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="94d4f-160">Testar um destino de saída do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="94d4f-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="94d4f-161">Um destino de análise de fluxo de saída também tem Olá **TestConnection** método para conexões de teste.</span><span class="sxs-lookup"><span data-stu-id="94d4f-161">A Stream Analytics output target also has hello **TestConnection** method for testing connections.</span></span>

   ```
   // Test hello connection toohello output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="94d4f-162">Criar uma transformação do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="94d4f-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="94d4f-163">Olá código a seguir cria uma transformação de análise de fluxo com consulta hello "Selecione * de entrada" e especifica tooallocate uma unidade de streaming para o trabalho de análise de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="94d4f-163">hello following code creates a Stream Analytics transformation with hello query "select * from Input" and specifies tooallocate one streaming unit for hello Stream Analytics job.</span></span> <span data-ttu-id="94d4f-164">Para obter mais informações sobre o ajuste de unidades de streaming, consulte Dimensionar trabalhos do [Escalonar trabalhos de Análise de fluxo do Azure](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="94d4f-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with hello value you put for hello 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

<span data-ttu-id="94d4f-165">Como entrada e saída, uma transformação é também trabalho do Stream Analytics específico toohello associado em que foi criado.</span><span class="sxs-lookup"><span data-stu-id="94d4f-165">Like input and output, a transformation is also tied toohello specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="94d4f-166">Iniciar um trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="94d4f-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="94d4f-167">Depois de criar um trabalho de análise de fluxo e suas entradas, saídas e transformação, você pode iniciar trabalho Olá Olá chamada **iniciar** método.</span><span class="sxs-lookup"><span data-stu-id="94d4f-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start hello job by calling hello **Start** method.</span></span>

<span data-ttu-id="94d4f-168">Olá, código de exemplo a seguir inicia um trabalho de análise de fluxo com uma saída personalizada start time conjunto tooDecember 12, 2012, 12:12:12 UTC:</span><span class="sxs-lookup"><span data-stu-id="94d4f-168">hello following sample code starts a Stream Analytics job with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC:</span></span>

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="94d4f-169">Interromper um trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="94d4f-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="94d4f-170">Você pode interromper um trabalho de análise de fluxo em execução, Olá chamada **parar** método.</span><span class="sxs-lookup"><span data-stu-id="94d4f-170">You can stop a running Stream Analytics job by calling hello **Stop** method.</span></span>

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="94d4f-171">Excluir um trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="94d4f-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="94d4f-172">Olá **excluir** método irá excluir trabalho hello, bem como Olá subjacente sub-recursos, inclusive entradas, saídas e transformação de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="94d4f-172">hello **Delete** method will delete hello job as well as hello underlying sub-resources, including input(s), output(s), and transformation of hello job.</span></span>

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a><span data-ttu-id="94d4f-173">Obtenha suporte</span><span class="sxs-lookup"><span data-stu-id="94d4f-173">Get support</span></span>
<span data-ttu-id="94d4f-174">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="94d4f-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="94d4f-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="94d4f-175">Next steps</span></span>
<span data-ttu-id="94d4f-176">Você aprendeu Noções básicas de saudação do uso de um SDK .NET toocreate e executar trabalhos de análise.</span><span class="sxs-lookup"><span data-stu-id="94d4f-176">You've learned hello basics of using a .NET SDK toocreate and run analytics jobs.</span></span> <span data-ttu-id="94d4f-177">toolearn mais, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="94d4f-177">toolearn more, see hello following:</span></span>

* [<span data-ttu-id="94d4f-178">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="94d4f-178">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="94d4f-179">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="94d4f-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="94d4f-180">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="94d4f-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="94d4f-181">[SDK .NET do Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn889315.aspx)</span><span class="sxs-lookup"><span data-stu-id="94d4f-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="94d4f-182">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="94d4f-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="94d4f-183">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="94d4f-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
