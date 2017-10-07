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
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a>Criar programaticamente um monitor de trabalhos do Stream Analytics

Este artigo demonstra como tooenable monitoramento para um trabalho do Stream Analytics. Os trabalhos de Stream Analytics criados por meio de APIs REST, do SDK do Azure ou do PowerShell não têm monitoramento habilitado por padrão. Você pode ativá-lo manualmente no portal do Azure de saudação acessando a página de Monitor toohello do trabalho e clicando em Olá Habilitar botão ou você pode automatizar esse processo, seguindo as etapas de saudação neste artigo. dados de monitoramento de saudação aparecerá na área de métricas de saudação do hello portal do Azure para o trabalho do Stream Analytics.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar esse processo, você deve ter o seguinte hello:

* Visual Studio 2017 ou 2015
* [SDK do Azure .NET](https://azure.microsoft.com/downloads/) baixado e instalado
* Um trabalho de análise de fluxo existente que precisa toohave monitoramento habilitado

## <a name="create-a-project"></a>Criar um projeto

1. Crie um aplicativo de console do Visual Studio C# .NET.
2. Olá Package Manager Console, seguinte Olá execução comandos de pacotes do NuGet Olá tooinstall. Olá primeiro um é hello gerenciamento .NET SDK do Azure Stream Analytics. Olá segundo é Olá SDK do Monitor do Azure que será usada tooenable monitoramento. Hello última um é cliente do Active Directory do Azure Olá que será usado para autenticação.
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. Adicione Olá arquivo App. config do appSettings seção toohello a seguir.
   
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
   Substitua os valores por *SubscriptionId* e *ActiveDirectoryTenantId* por suas IDs de assinatura e locatário do Azure. Você pode obter esses valores, executando Olá cmdlet do PowerShell a seguir:
   
   ```
   Get-AzureAccount
   ```
4. Adicione o seguinte Olá usando o arquivo de origem toohello instruções (Program.cs) no projeto de saudação.
   
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
5. Adicione um método auxiliar de autenticação.
   
     public static string GetAuthorizationHeader()
   
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
     }

## <a name="create-management-clients"></a>Criar clientes de gerenciamento

Olá código a seguir irá configurar variáveis necessárias hello e clientes de gerenciamento.

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a>Habilitar o monitoramento para um trabalho de Stream Analytics existente

Habilita o monitoramento para o código a seguir de saudação um **existente** trabalho do Stream Analytics. a primeira parte saudação do código Olá realiza uma solicitação GET com informações de tooretrieve de serviço Olá Stream Analytics sobre o trabalho de análise de fluxo específico de saudação. Ele usa Olá *Id* propriedade (recuperado da solicitação de obtenção de saudação) como um parâmetro para Olá método Put no hello segunda metade do código de saudação, que envia uma solicitação PUT Insights toohello monitoramento de serviço tooenable de saudação do Stream Analytics trabalho.

>[!WARNING]
>Se você tiver habilitado anteriormente monitoramento para um trabalho do Stream Analytics diferente, por meio de Olá portal do Azure ou programaticamente por meio de saudação abaixo do código, **é recomendável que você forneça Olá mesmo nome de conta de armazenamento que você usou quando você habilitado anteriormente monitoramento.**
> 
> conta de armazenamento Olá é vinculado toohello região que você criou o trabalho do Stream Analytics em não especificamente toohello próprio trabalho.
> 
> Análise de fluxo de todos os trabalhos (e todos os outros recursos do Azure) na mesma região compartilham esse toostore de conta de armazenamento que os dados de monitoramento. Se você fornecer uma conta de armazenamento diferentes, pode causar efeitos colaterais não intencionais na Olá monitoramento de seus outros trabalhos do Stream Analytics ou outros recursos do Azure.
> 
> nome de conta de armazenamento Olá que você use tooreplace `<YOUR STORAGE ACCOUNT NAME>` em Olá código a seguir deve ser uma conta de armazenamento que está em Olá mesma assinatura que o trabalho do Stream Analytics Olá que você está habilitando o monitoramento para.
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



## <a name="get-support"></a>Obtenha suporte

Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas

* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

