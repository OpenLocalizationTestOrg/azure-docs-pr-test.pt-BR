---
title: trabalhos de monitor aaaProgrammatically no Stream Analytics | Microsoft Docs
description: Saiba como tooprogrammatically monitorar trabalhos do Stream Analytics criados por meio de APIs REST, o SDK do Azure ou o PowerShell.
keywords: monitor .net, monitor de trabalhos, aplicativo de monitoramento
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 2ec02cc9-4ca5-4a25-ae60-c44be9ad4835
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 44a9c29c2161ee81ea76ece4646a8691bf5d5b48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="272fd-104">Criar programaticamente um monitor de trabalhos do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="272fd-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="272fd-105">Este artigo demonstra como tooenable monitoramento para um trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="272fd-105">This article demonstrates how tooenable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="272fd-106">Os trabalhos de Stream Analytics criados por meio de APIs REST, do SDK do Azure ou do PowerShell não têm monitoramento habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="272fd-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="272fd-107">Você pode ativá-lo manualmente no portal do Azure de saudação acessando a página de Monitor toohello do trabalho e clicando em Olá Habilitar botão ou você pode automatizar esse processo, seguindo as etapas de saudação neste artigo.</span><span class="sxs-lookup"><span data-stu-id="272fd-107">You can manually enable it in hello Azure portal by going toohello job’s Monitor page and clicking hello Enable button or you can automate this process by following hello steps in this article.</span></span> <span data-ttu-id="272fd-108">dados de monitoramento de saudação aparecerá na área de métricas de saudação do hello portal do Azure para o trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="272fd-108">hello monitoring data will show up in hello Metrics area of hello Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="272fd-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="272fd-109">Prerequisites</span></span>

<span data-ttu-id="272fd-110">Antes de começar esse processo, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="272fd-110">Before you begin this process, you must have hello following:</span></span>

* <span data-ttu-id="272fd-111">Visual Studio 2017 ou 2015</span><span class="sxs-lookup"><span data-stu-id="272fd-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="272fd-112">[SDK do Azure .NET](https://azure.microsoft.com/downloads/) baixado e instalado</span><span class="sxs-lookup"><span data-stu-id="272fd-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="272fd-113">Um trabalho de análise de fluxo existente que precisa toohave monitoramento habilitado</span><span class="sxs-lookup"><span data-stu-id="272fd-113">An existing Stream Analytics job that needs toohave monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="272fd-114">Criar um projeto</span><span class="sxs-lookup"><span data-stu-id="272fd-114">Create a project</span></span>

1. <span data-ttu-id="272fd-115">Crie um aplicativo de console do Visual Studio C# .NET.</span><span class="sxs-lookup"><span data-stu-id="272fd-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="272fd-116">Olá Package Manager Console, seguinte Olá execução comandos de pacotes do NuGet Olá tooinstall.</span><span class="sxs-lookup"><span data-stu-id="272fd-116">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="272fd-117">Olá primeiro um é hello gerenciamento .NET SDK do Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="272fd-117">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="272fd-118">Olá segundo é Olá SDK do Monitor do Azure que será usada tooenable monitoramento.</span><span class="sxs-lookup"><span data-stu-id="272fd-118">hello second one is hello Azure Monitor SDK that will be used tooenable monitoring.</span></span> <span data-ttu-id="272fd-119">Hello última um é cliente do Active Directory do Azure Olá que será usado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="272fd-119">hello last one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="272fd-120">Adicione Olá arquivo App. config do appSettings seção toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="272fd-120">Add hello following appSettings section toohello App.config file.</span></span>
   
   ```
   <appSettings>
     <!--CSM Prod related values-->
     <add key="ResourceGroupName" value="RESOURCE GROUP NAME" />
     <add key="JobName" value="YOUR JOB NAME" />
     <add key="StorageAccountName" value="YOUR STORAGE ACCOUNT"/>
     <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
     <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
     <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
     <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
     <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
     <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION ID" />
     <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
   </appSettings>
   ```
   <span data-ttu-id="272fd-121">Substitua os valores por *SubscriptionId* e *ActiveDirectoryTenantId* por suas IDs de assinatura e locatário do Azure.</span><span class="sxs-lookup"><span data-stu-id="272fd-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="272fd-122">Você pode obter esses valores, executando Olá cmdlet do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="272fd-122">You can get these values by running hello following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="272fd-123">Adicione o seguinte Olá usando o arquivo de origem toohello instruções (Program.cs) no projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="272fd-123">Add hello following using statements toohello source file (Program.cs) in hello project.</span></span>
   
   ```
     using System;
     using System.Configuration;
     using System.Threading;
     using Microsoft.Azure;
     using Microsoft.Azure.Management.Insights;
     using Microsoft.Azure.Management.Insights.Models;
     using Microsoft.Azure.Management.StreamAnalytics;
     using Microsoft.Azure.Management.StreamAnalytics.Models;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
   ```
5. <span data-ttu-id="272fd-124">Adicione um método auxiliar de autenticação.</span><span class="sxs-lookup"><span data-stu-id="272fd-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="272fd-125">public static string GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="272fd-125">public static string GetAuthorizationHeader()</span></span>
   
         {
             AuthenticationResult result = null;
             var thread = new Thread(() =>
             {
                 try
                 {
                     var context = new AuthenticationContext(
                         ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
                         ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
   
                     result = context.AcquireToken(
                         resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                         clientId: ConfigurationManager.AppSettings["AsaClientId"],
                         redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
                         promptBehavior: PromptBehavior.Always);
                 }
                 catch (Exception threadEx)
                 {
                     Console.WriteLine(threadEx.Message);
                 }
             });
   
             thread.SetApartmentState(ApartmentState.STA);
             thread.Name = "AcquireTokenThread";
             thread.Start();
             thread.Join();
   
             if (result != null)
             {
                 return result.AccessToken;
             }
   
             throw new InvalidOperationException("Failed tooacquire token");
     <span data-ttu-id="272fd-126">}</span><span class="sxs-lookup"><span data-stu-id="272fd-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="272fd-127">Criar clientes de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="272fd-127">Create management clients</span></span>

<span data-ttu-id="272fd-128">Olá código a seguir irá configurar variáveis necessárias hello e clientes de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="272fd-128">hello following code will set up hello necessary variables and management clients.</span></span>

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials =
        new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader());

    Uri resourceManagerUri = new
    Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    // Create Stream Analytics and Insights management client
    StreamAnalyticsManagementClient streamAnalyticsClient = new
    StreamAnalyticsManagementClient(aadTokenCredentials, resourceManagerUri);
    InsightsManagementClient insightsClient = new
    InsightsManagementClient(aadTokenCredentials, resourceManagerUri);

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="272fd-129">Habilitar o monitoramento para um trabalho de Stream Analytics existente</span><span class="sxs-lookup"><span data-stu-id="272fd-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="272fd-130">Habilita o monitoramento para o código a seguir de saudação um **existente** trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="272fd-130">hello following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="272fd-131">a primeira parte saudação do código Olá realiza uma solicitação GET com informações de tooretrieve de serviço Olá Stream Analytics sobre o trabalho de análise de fluxo específico de saudação.</span><span class="sxs-lookup"><span data-stu-id="272fd-131">hello first part of hello code performs a GET request against hello Stream Analytics service tooretrieve information about hello particular Stream Analytics job.</span></span> <span data-ttu-id="272fd-132">Ele usa Olá *Id* propriedade (recuperado da solicitação de obtenção de saudação) como um parâmetro para Olá método Put no hello segunda metade do código de saudação, que envia uma solicitação PUT Insights toohello monitoramento de serviço tooenable de saudação do Stream Analytics trabalho.</span><span class="sxs-lookup"><span data-stu-id="272fd-132">It uses hello *Id* property (retrieved from hello GET request) as a parameter for hello Put method in hello second half of hello code, which sends a PUT request toohello Insights service tooenable monitoring for hello Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="272fd-133">Se você tiver habilitado anteriormente monitoramento para um trabalho do Stream Analytics diferente, por meio de Olá portal do Azure ou programaticamente por meio de saudação abaixo do código, **é recomendável que você forneça Olá mesmo nome de conta de armazenamento que você usou quando você habilitado anteriormente monitoramento.**</span><span class="sxs-lookup"><span data-stu-id="272fd-133">If you have previously enabled monitoring for a different Stream Analytics job, either through hello Azure portal or programmatically via hello below code, **we recommend that you provide hello same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="272fd-134">conta de armazenamento Olá é vinculado toohello região que você criou o trabalho do Stream Analytics em não especificamente toohello próprio trabalho.</span><span class="sxs-lookup"><span data-stu-id="272fd-134">hello storage account is linked toohello region that you created your Stream Analytics job in, not specifically toohello job itself.</span></span>
> 
> <span data-ttu-id="272fd-135">Análise de fluxo de todos os trabalhos (e todos os outros recursos do Azure) na mesma região compartilham esse toostore de conta de armazenamento que os dados de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="272fd-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account toostore monitoring data.</span></span> <span data-ttu-id="272fd-136">Se você fornecer uma conta de armazenamento diferentes, pode causar efeitos colaterais não intencionais na Olá monitoramento de seus outros trabalhos do Stream Analytics ou outros recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="272fd-136">If you provide a different storage account, it might cause unintended side effects in hello monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="272fd-137">nome de conta de armazenamento Olá que você use tooreplace `<YOUR STORAGE ACCOUNT NAME>` em Olá código a seguir deve ser uma conta de armazenamento que está em Olá mesma assinatura que o trabalho do Stream Analytics Olá que você está habilitando o monitoramento para.</span><span class="sxs-lookup"><span data-stu-id="272fd-137">hello storage account name that you use tooreplace `<YOUR STORAGE ACCOUNT NAME>` in hello following code should be a storage account that is in hello same subscription as hello Stream Analytics job that you are enabling monitoring for.</span></span>
> 
> 

    // Get an existing Stream Analytics job
    JobGetParameters jobGetParameters = new JobGetParameters()
    {
        PropertiesToExpand = "inputs,transformation,outputs"
    };
    JobGetResponse jobGetResponse = streamAnalyticsClient.StreamingJobs.Get(resourceGroupName, streamAnalyticsJobName, jobGetParameters);

    // Enable monitoring
    ServiceDiagnosticSettingsPutParameters insightPutParameters = new ServiceDiagnosticSettingsPutParameters()
    {
            Properties = new ServiceDiagnosticSettings()
            {
                StorageAccountName = "<YOUR STORAGE ACCOUNT NAME>"
            }
    };
    insightsClient.ServiceDiagnosticSettingsOperations.Put(jobGetResponse.Job.Id, insightPutParameters);



## <a name="get-support"></a><span data-ttu-id="272fd-138">Obtenha suporte</span><span class="sxs-lookup"><span data-stu-id="272fd-138">Get support</span></span>

<span data-ttu-id="272fd-139">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="272fd-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="272fd-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="272fd-140">Next steps</span></span>

* [<span data-ttu-id="272fd-141">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="272fd-141">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="272fd-142">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="272fd-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="272fd-143">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="272fd-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="272fd-144">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="272fd-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="272fd-145">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="272fd-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

