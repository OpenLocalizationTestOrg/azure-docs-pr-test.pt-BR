---
title: Monitorar trabalhos programaticamente no Stream Analytics | Microsoft Docs
description: Saiba como monitorar programaticamente os trabalhos do Stream Analytics criados por meio de APIs REST, do SDK do Azure ou do PowerShell.
keywords: monitor .net, monitor de trabalhos, aplicativo de monitoramento
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 2ec02cc9-4ca5-4a25-ae60-c44be9ad4835
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: samacha
ms.openlocfilehash: 7e9d2f6f03fd539c59b105108fb46697bcd60f1c
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a>Criar programaticamente um monitor de trabalhos do Stream Analytics

Este artigo demonstra como habilitar o monitoramento para um trabalho do Stream Analytics. Os trabalhos de Stream Analytics criados por meio de APIs REST, do SDK do Azure ou do PowerShell não têm monitoramento habilitado por padrão. Você pode habilitá-lo manualmente no Portal do Azure indo até a página de Monitor do trabalho e clicando no botão Habilitar ou então pode automatizar esse processo seguindo as etapas neste artigo. Os dados de monitoramento serão exibidos na guia Métricas no Portal do Azure para o trabalho do Stream Analytics.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar este processo, você deve ter o seguinte:

* Visual Studio 2017 ou 2015
* [SDK do Azure .NET](https://azure.microsoft.com/downloads/) baixado e instalado
* Um trabalho de Stream Analytics existente que precisa ter monitoramento habilitado

## <a name="create-a-project"></a>Criar um projeto

1. Crie um aplicativo de console do Visual Studio C# .NET.
2. No Console do Gerenciador de pacotes, execute os seguintes comandos para instalar os pacotes do NuGet. O primeiro é o SDK .NET do Azure Stream Analytics Management. O segundo é o SDK do Azure Monitor que será usado para habilitar o monitoramento. O último é o cliente do Active Directory do Azure que será usado para autenticação.
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. Adicione a seguinte seção appSettings ao arquivo App.config.
   
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
   Substitua os valores por *SubscriptionId* e *ActiveDirectoryTenantId* por suas IDs de assinatura e locatário do Azure. Você pode obter esses valores executando o seguinte cmdlet do PowerShell:
   
   ```
   Get-AzureAccount
   ```
4. Adicione as seguintes declarações usando o arquivo de origem (Program.cs) no projeto.
   
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
   
             throw new InvalidOperationException("Failed to acquire token");
     }

## <a name="create-management-clients"></a>Criar clientes de gerenciamento

O código a seguir configurará as variáveis necessárias e os clientes de gerenciamento.

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

O código a seguir habilita o monitoramento para um trabalho de Stream Analytics **existente**. A primeira parte do código realiza uma solicitação GET em relação ao serviço de Stream Analytics para recuperar informações sobre o trabalho específico do Stream Analytics. Ele usa a propriedade *Id* (recuperada da solicitação GET) como um parâmetro para o método Put na segunda metade do código que envia uma solicitação PUT ao serviço Insights para habilitar o monitoramento para o trabalho de Stream Analytics.

>[!WARNING]
>Se você habilitou o monitoramento de um trabalho diferente do Stream Analytics anteriormente, por meio do Portal do Azure ou programaticamente por meio do código abaixo, **recomendamos que você forneça o mesmo nome de conta de armazenamento que usou quando o habilitou.**
> 
> A conta de armazenamento está vinculada à região em que você criou o trabalho do Stream Analytics, não especificamente ao trabalho em si.
> 
> Todos os trabalhos do Stream Analytics (e todos os outros recursos do Azure) na mesma região compartilham essa conta de armazenamento para armazenar dados de monitoramento. Se você fornecer uma conta de armazenamento diferente, isso poderá causar efeitos colaterais indesejados no monitoramento de seus outros trabalhos do Stream Analytics ou outros recursos do Azure.
> 
> O nome da conta de armazenamento que você usa para substituir `<YOUR STORAGE ACCOUNT NAME>` no código a seguir deve ser uma conta de armazenamento que esteja na mesma assinatura que o trabalho do Stream Analytics para o qual você estiver habilitando o monitoramento.
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

* [Introdução ao Stream Analytics do Azure](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

