---
title: SDK do .NET de Gerenciamento para Stream Analytics do Azure | Microsoft Docs
description: "Comece com o SDK .NET do Azure Stream Analytics Management. Saiba como configurar e executar trabalhos de análise. Criar um projeto, entradas, saídas e transformações."
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
ms.openlocfilehash: f9aa812e6e82cc0f72d0cd1fe63058e53f794775
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-the-azure-stream-analytics-api-for-net"></a><span data-ttu-id="66fea-106">SDK .NET de gerenciamento: configurar e executar trabalhos de análise usando a API do Azure Stream Analytics para .NET</span><span class="sxs-lookup"><span data-stu-id="66fea-106">Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="66fea-107">Saiba como configurar e executar trabalhos de análise usando a API do Stream Analytics para .NET usando o SDK do .NET de Gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="66fea-107">Learn how to set up and run analytics jobs using the Stream Analytics API for .NET using the Management .NET SDK.</span></span> <span data-ttu-id="66fea-108">Configurar um projeto, criar fontes de entrada e saídas, transformações e iniciar e parar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="66fea-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="66fea-109">Seus trabalhos de análise, você pode transmitir dados de armazenamento de Blob ou de um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="66fea-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="66fea-110">Consulte a [Documentação de referência de gerenciamento da API do Stream Analytics para .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="66fea-110">See the [management reference documentation for the Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="66fea-111">O Azure Stream Analytics é um serviço completamente gerenciado que oferece baixa latência, alta disponibilidade e processamento escalonável de eventos complexos por streaming de dados na nuvem.</span><span class="sxs-lookup"><span data-stu-id="66fea-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="66fea-112">O Stream Analytics permite que os clientes configurem trabalhos de streaming para analisar fluxos de dados e realizem análise quase em tempo real.</span><span class="sxs-lookup"><span data-stu-id="66fea-112">Stream Analytics enables customers to set up streaming jobs to analyze data streams, and allows them to drive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="66fea-113">Atualizamos o código de exemplo neste artigo com a versão v2.x do SDK do .NET de Gerenciamento do Stream Analytics do Azure.</span><span class="sxs-lookup"><span data-stu-id="66fea-113">We have updated the sample code in this article with Azure Stream Analytics Management .NET SDK v2.x version.</span></span> <span data-ttu-id="66fea-114">Para código de exemplo usando a versão herdada (1.x) do SDK, consulte [Usar o SDK do .NET de Gerenciamento v1.x para Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span><span class="sxs-lookup"><span data-stu-id="66fea-114">For sample code using the uses lagecy (1.x) SDK version, please see [Use the Management .NET SDK v1.x for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66fea-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="66fea-115">Prerequisites</span></span>
<span data-ttu-id="66fea-116">Antes de começar este artigo, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="66fea-116">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="66fea-117">Instale o Visual Studio 2017 ou 2015.</span><span class="sxs-lookup"><span data-stu-id="66fea-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="66fea-118">Baixe e instale o [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="66fea-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="66fea-119">Crie um grupo de recursos do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="66fea-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="66fea-120">O seguinte é um exemplo de script do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="66fea-120">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="66fea-121">Para obter mais informações sobre o PowerShell do Azure, consulte [Instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="66fea-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered to the subscription, remove the remark symbol (#) to run the Register-AzureRMProvider cmdlet to register the provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="66fea-122">Configure uma origem de entrada e o destino de saída para usar.</span><span class="sxs-lookup"><span data-stu-id="66fea-122">Set up an input source and output target to use.</span></span> <span data-ttu-id="66fea-123">Para obter mais instruções, consulte [Adicionar Entradas](stream-analytics-add-inputs.md) para configurar uma entrada de exemplo e [Adicionar Saídas](stream-analytics-add-outputs.md) para configurar uma saída de exemplo.</span><span class="sxs-lookup"><span data-stu-id="66fea-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) to set up a sample input and [Add Outputs](stream-analytics-add-outputs.md) to set up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="66fea-124">Configurar um projeto</span><span class="sxs-lookup"><span data-stu-id="66fea-124">Set up a project</span></span>
<span data-ttu-id="66fea-125">Para criar um trabalho de análise, use a API do Stream Analytics para .NET. Primeiro, configure seu projeto.</span><span class="sxs-lookup"><span data-stu-id="66fea-125">To create an analytics job use the Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="66fea-126">Crie um aplicativo de console do Visual Studio C# .NET.</span><span class="sxs-lookup"><span data-stu-id="66fea-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="66fea-127">No Console do Gerenciador de pacotes, execute os seguintes comandos para instalar os pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="66fea-127">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="66fea-128">O primeiro é o SDK .NET do Azure Stream Analytics Management.</span><span class="sxs-lookup"><span data-stu-id="66fea-128">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="66fea-129">A segunda é para autenticação de cliente do Azure.</span><span class="sxs-lookup"><span data-stu-id="66fea-129">The second one is for Azure client authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. <span data-ttu-id="66fea-130">Adicione a seguinte seção **appSettings** ao arquivo App.config.</span><span class="sxs-lookup"><span data-stu-id="66fea-130">Add the following **appSettings** section to the App.config file:</span></span>
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    <span data-ttu-id="66fea-131">Substitua os valores por **SubscriptionId** e **ActiveDirectoryTenantId** por suas IDs de assinatura e locatário do Azure.</span><span class="sxs-lookup"><span data-stu-id="66fea-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="66fea-132">Você pode obter esses valores executando o seguinte cmdlet do PowerShell do Azure:</span><span class="sxs-lookup"><span data-stu-id="66fea-132">You can get these values by running the following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="66fea-133">Adicione a seguinte referência em seu arquivo .csproj:</span><span class="sxs-lookup"><span data-stu-id="66fea-133">Add the following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

5. <span data-ttu-id="66fea-134">Adicione as seguintes declarações **using** ao arquivo de origem (Program.cs) no projeto.</span><span class="sxs-lookup"><span data-stu-id="66fea-134">Add the following **using** statements to the source file (Program.cs) in the project:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. <span data-ttu-id="66fea-135">Adicione um método auxiliar de autenticação:</span><span class="sxs-lookup"><span data-stu-id="66fea-135">Add an authentication helper method:</span></span>

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="66fea-136">Crie um cliente de gerenciamento do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="66fea-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="66fea-137">Um objeto **StreamAnalyticsManagementClient** permite que você gerencie o trabalho e os componentes de trabalho, como entrada, saída e transformação.</span><span class="sxs-lookup"><span data-stu-id="66fea-137">A **StreamAnalyticsManagementClient** object allows you to manage the job and the job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="66fea-138">Adicione o seguinte código ao início do método **Main** :</span><span class="sxs-lookup"><span data-stu-id="66fea-138">Add the following code to the beginning of the **Main** method:</span></span>

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

<span data-ttu-id="66fea-139">O valor da variável **resourceGroupName** deve ser igual ao nome do grupo de recursos que você criou ou escolheu nas etapas de pré-requisito.</span><span class="sxs-lookup"><span data-stu-id="66fea-139">The **resourceGroupName** variable's value should be the same as the name of the resource group you created or picked in the prerequisite steps.</span></span>

<span data-ttu-id="66fea-140">Para automatizar o aspecto de apresentação de credencial da criação do trabalho, consulte [Autenticação de uma entidade de serviço com o Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="66fea-140">To automate the credential presentation aspect of job creation, refer to [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="66fea-141">As seções restantes deste artigo pressupõem que esse código esteja no início do método **Main** .</span><span class="sxs-lookup"><span data-stu-id="66fea-141">The remaining sections of this article assume that this code is at the beginning of the **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="66fea-142">Criar um trabalho de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="66fea-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="66fea-143">O código a seguir cria um trabalho do Stream Analytics sob o grupo de recursos que você definiu.</span><span class="sxs-lookup"><span data-stu-id="66fea-143">The following code creates a Stream Analytics job under the resource group that you have defined.</span></span> <span data-ttu-id="66fea-144">Você adicionará entrada, saída e transformação ao trabalho mais tarde.</span><span class="sxs-lookup"><span data-stu-id="66fea-144">You will add an input, output, and transformation to the job later.</span></span>

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

## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="66fea-145">Criar uma fonte de entrada do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="66fea-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="66fea-146">O código a seguir cria uma fonte de entrada do Stream Analytics com o tipo de fonte de entrada de blob e serialização de CSV.</span><span class="sxs-lookup"><span data-stu-id="66fea-146">The following code creates a Stream Analytics input source with the blob input source type and CSV serialization.</span></span> <span data-ttu-id="66fea-147">Para criar uma fonte de entrada de hub de eventos, use **EventHubStreamInputDataSource** em vez de **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="66fea-147">To create an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="66fea-148">Da mesma forma, você pode personalizar o tipo de serialização da fonte de entrada.</span><span class="sxs-lookup"><span data-stu-id="66fea-148">Similarly, you can customize the serialization type of the input source.</span></span>

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

<span data-ttu-id="66fea-149">As fontes de entrada de armazenamento de Blob ou de um hub de eventos estão ligadas a um trabalho específico.</span><span class="sxs-lookup"><span data-stu-id="66fea-149">Input sources, whether from Blob storage or an event hub, are tied to a specific job.</span></span> <span data-ttu-id="66fea-150">Para usar a mesma fonte de entrada para trabalhos diferentes, chame o método novamente e especifique um nome de trabalho diferente.</span><span class="sxs-lookup"><span data-stu-id="66fea-150">To use the same input source for different jobs, you must call the method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="66fea-151">Testar uma fonte de entrada do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="66fea-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="66fea-152">O método **TestConnection** testa se o trabalho do Stream Analytics é capaz de se conectar à fonte de entrada, bem como outros aspectos específicos para o tipo de fonte de entrada.</span><span class="sxs-lookup"><span data-stu-id="66fea-152">The **TestConnection** method tests whether the Stream Analytics job is able to connect to the input source as well as other aspects specific to the input source type.</span></span> <span data-ttu-id="66fea-153">Por exemplo, em que na fonte de entrada de blob criada em uma etapa anterior, o método verificará se o nome da conta de armazenamento e o par de chaves podem ser usados para conectar-se à conta de armazenamento, bem como verificará se o contêiner especificado existe.</span><span class="sxs-lookup"><span data-stu-id="66fea-153">For example, in the blob input source you created in an earlier step, the method will check that the Storage account name and key pair can be used to connect to the Storage account as well as check that the specified container exists.</span></span>

   ```
   // Test the connection to the input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="66fea-154">Criar um destino de saída do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="66fea-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="66fea-155">Criar um destino de saída é muito semelhante a criar uma fonte de entrada do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="66fea-155">Creating an output target is very similar to creating a Stream Analytics input source.</span></span> <span data-ttu-id="66fea-156">Como as fontes de entrada, os destinos de saída são vinculados a trabalho específico.</span><span class="sxs-lookup"><span data-stu-id="66fea-156">Like input sources, output targets are tied to a specific job.</span></span> <span data-ttu-id="66fea-157">Para usar o mesmo destino de saída para diferentes trabalhos, chame o método novamente e especifique um nome de trabalho diferente.</span><span class="sxs-lookup"><span data-stu-id="66fea-157">To use the same output target for different jobs, you must call the method again and specify a different job name.</span></span>

<span data-ttu-id="66fea-158">O código a seguir cria um destino de saída (Banco de Dados SQL do Azure).</span><span class="sxs-lookup"><span data-stu-id="66fea-158">The following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="66fea-159">Você pode personalizar o tipo de dados de destino de saída e/ou o tipo de serialização.</span><span class="sxs-lookup"><span data-stu-id="66fea-159">You can customize the output target's data type and/or serialization type.</span></span>

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

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="66fea-160">Testar um destino de saída do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="66fea-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="66fea-161">Um destino de saída do Stream Analytics também tem um método **TestConnection** para conexões de teste.</span><span class="sxs-lookup"><span data-stu-id="66fea-161">A Stream Analytics output target also has the **TestConnection** method for testing connections.</span></span>

   ```
   // Test the connection to the output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="66fea-162">Criar uma transformação do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="66fea-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="66fea-163">O código a seguir cria uma transformação do Stream Analytics com a consulta "selecionar * da entrada" e especifica para alocar uma unidade de streaming para o trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="66fea-163">The following code creates a Stream Analytics transformation with the query "select * from Input" and specifies to allocate one streaming unit for the Stream Analytics job.</span></span> <span data-ttu-id="66fea-164">Para obter mais informações sobre o ajuste de unidades de streaming, consulte Dimensionar trabalhos do [Escalonar trabalhos de Análise de fluxo do Azure](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="66fea-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with the value you put for the 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

<span data-ttu-id="66fea-165">Como entrada e saída, uma transformação também está vinculada ao trabalho de Stream Analytics específico sob o qual foi criada.</span><span class="sxs-lookup"><span data-stu-id="66fea-165">Like input and output, a transformation is also tied to the specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="66fea-166">Iniciar um trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="66fea-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="66fea-167">Depois de criar um trabalho do Stream Analytics e suas entradas, saídas e transformação, você pode iniciar o trabalho chamando o método **Iniciar** .</span><span class="sxs-lookup"><span data-stu-id="66fea-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start the job by calling the **Start** method.</span></span>

<span data-ttu-id="66fea-168">O código de exemplo a seguir inicia um trabalho do Stream Analytics com uma hora de início de saída personalizada definida para 12 de dezembro de 2012, 12h12min12 UTC:</span><span class="sxs-lookup"><span data-stu-id="66fea-168">The following sample code starts a Stream Analytics job with a custom output start time set to December 12, 2012, 12:12:12 UTC:</span></span>

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="66fea-169">Interromper um trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="66fea-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="66fea-170">Você pode interromper um trabalho do Stream Analytics em execução chamando o método **Parar** .</span><span class="sxs-lookup"><span data-stu-id="66fea-170">You can stop a running Stream Analytics job by calling the **Stop** method.</span></span>

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="66fea-171">Excluir um trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="66fea-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="66fea-172">O método **Excluir** excluirá o trabalho, bem como os sub-recursos subjacentes, incluindo entradas, saídas e transformação do trabalho.</span><span class="sxs-lookup"><span data-stu-id="66fea-172">The **Delete** method will delete the job as well as the underlying sub-resources, including input(s), output(s), and transformation of the job.</span></span>

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a><span data-ttu-id="66fea-173">Obtenha suporte</span><span class="sxs-lookup"><span data-stu-id="66fea-173">Get support</span></span>
<span data-ttu-id="66fea-174">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="66fea-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="66fea-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="66fea-175">Next steps</span></span>
<span data-ttu-id="66fea-176">Você aprendeu as noções básicas do uso de um SDK do .NET para criar e executar trabalhos de análise.</span><span class="sxs-lookup"><span data-stu-id="66fea-176">You've learned the basics of using a .NET SDK to create and run analytics jobs.</span></span> <span data-ttu-id="66fea-177">Para saber mais, consulte os seguintes:</span><span class="sxs-lookup"><span data-stu-id="66fea-177">To learn more, see the following:</span></span>

* [<span data-ttu-id="66fea-178">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="66fea-178">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="66fea-179">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="66fea-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="66fea-180">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="66fea-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="66fea-181">[SDK .NET do Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn889315.aspx)</span><span class="sxs-lookup"><span data-stu-id="66fea-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="66fea-182">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="66fea-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="66fea-183">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="66fea-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
