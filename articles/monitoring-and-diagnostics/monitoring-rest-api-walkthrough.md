---
title: aaaAzure passo a passo do monitoramento API REST | Microsoft Docs
description: "Como tooauthenticate solicita tooand use Olá API de REST de monitoramento do Azure."
author: mcollier
manager: 
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 565e6a88-3131-4a48-8b82-3effc9a3d5c6
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: mcollier
ms.openlocfilehash: b8ae3a03fd21af872f1dc5fed40a101a24ca1652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitoring-rest-api-walkthrough"></a>Passo a passo da API REST de monitoramento do Azure
Este artigo mostra como tooperform autenticação para o seu código pode usar Olá [referência de API REST do Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).         

Olá API do Monitor do Azure torna possível tooprogrammatically recuperar saudação padrão disponíveis de definições de métricas (tipo de saudação da métrica, como tempo de CPU, solicitações, etc.), granularidade e valores da métrica. Depois de recuperados, dados saudação podem ser salvos em um repositório de dados separado, como o banco de dados do SQL Azure, o banco de dados do Azure Cosmos ou do Azure Data Lake. A partir daí análises adicionais podem ser executadas conforme necessário.

Além de trabalhar com vários pontos de dados da métrica, conforme este artigo demonstra, Olá Monitor API torna as regras de alerta toolist possíveis, exibir logs de atividade e muito mais. Para obter uma lista completa de operações disponíveis, consulte Olá [referência de API REST do Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).

## <a name="authenticating-azure-monitor-requests"></a>Autenticação de solicitações do Azure Monitor
Olá primeira etapa é a solicitação de saudação tooauthenticate.

Todas as tarefas de saudação executadas em relação hello Azure Monitor API use hello Azure Resource Manager autenticação modelo. Portanto, todas as solicitações devem ser autenticadas com o Azure Active Directory (Azure AD). Um aplicativo de cliente abordagem tooauthenticate hello é toocreate uma entidade de serviço do AD do Azure e recuperar o token de autenticação (JWT) hello. Olá seguinte script de exemplo demonstra como criar um AD do Azure entidade de serviço por meio do PowerShell. Para obter instruções mais detalhadas, consulte a documentação do toohello em [usando Azure PowerShell toocreate um recurso do serviço principal tooaccess](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password). Também é possível muito[criar uma entidade de serviço por meio do portal do Azure de saudação](../azure-resource-manager/resource-group-create-service-principal-portal.md).

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"
$location = "centralus"

# Authenticate tooa specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for hello service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with hello designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role toohello newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

Olá tooquery API do Monitor do Azure, aplicativo de cliente hello deve usar Olá criado anteriormente tooauthenticate principal do serviço. saudação de script do PowerShell de exemplo a seguir mostra uma abordagem, usando Olá [biblioteca de autenticação do Active Directory](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp obter token de JWT de saudação autenticação. token JWT de saudação é passada como parte de um parâmetro de autorização HTTP no solicitações toohello API de REST do Monitor do Azure.

```PowerShell
$azureAdApplication = Get-AzureRmADApplication -IdentifierUri "https://localhost/azure-monitor"

$subscription = Get-AzureRmSubscription -SubscriptionId $subscriptionId

$clientId = $azureAdApplication.ApplicationId.Guid
$tenantId = $subscription.TenantId
$authUrl = "https://login.microsoftonline.com/${tenantId}"

$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl
$cred = New-Object -TypeName Microsoft.IdentityModel.Clients.ActiveDirectory.ClientCredential -ArgumentList ($clientId, $pwd)

$result = $AuthContext.AcquireToken("https://management.core.windows.net/", $cred)

# Build an array of HTTP header values
$authHeader = @{
'Content-Type'='application/json'
'Accept'='application/json'
'Authorization'=$result.CreateAuthorizationHeader()
}
```

Após a conclusão da etapa de configuração de autenticação hello, consultas, em seguida, podem ser executadas em relação a saudação API de REST do Monitor do Azure. Há duas consultas úteis:

1. Lista de definições de métricas de saudação para um recurso
2. Recuperar os valores da métrica Olá

## <a name="retrieve-metric-definitions"></a>Recuperar as definições de métrica
> [!NOTE]
> definições de métrica tooretrieve usando Olá API de REST do Monitor do Azure, use "2016-03-01" como Olá versão da API.
>
>

```PowerShell
$apiVersion = "2016-03-01"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metricDefinitions?api-version=${apiVersion}"

Invoke-RestMethod -Uri $request `
                  -Headers $authHeader `
                  -Method Get `
                  -Verbose
```
Um aplicativo do Azure lógica, definições de métrica Olá apareceria semelhante toohello captura de tela a seguir:

![Alt "Visão JSON da resposta da definição da métrica."](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

Para obter mais informações, consulte Olá [lista definições de métricas de saudação para um recurso na API de REST do Azure Monitor](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentação.

## <a name="retrieve-metric-values"></a>Recuperar valores de métrica
Depois de definições de métricas disponíveis Olá são conhecidas, é então tooretrieve possíveis Olá valores relacionados de métrica. Use nome 'value' da métrica Olá (não Olá 'localizedValue') para todas as solicitações filtragem (por exemplo, recuperar Olá 'CpuTime' e 'Solicitar' métrica pontos de dados). Se nenhum filtro for especificado, a métrica de padrão de saudação é retornada.

> [!NOTE]
> valores da métrica tooretrieve usando Olá API de REST do Monitor do Azure, use "2016-06-01" como Olá versão da API.
>
>

**Método**: GET

**URI de solicitação**: https://management.azure.com/subscriptions/*{id-da-assinatura}*/resourceGroups/*{nome-do-grupo-de-recursos}*/providers/*{namespace-do-provedor-recursos}*/*{tipo-de-recurso}*/*{nome-do-recurso}*/providers/microsoft.insights/metrics?$filter=*{filtro}*&api-version=*{versão-da-api}*

Por exemplo, tooretrieve os pontos de dados de métrica Olá RunsSucceeded para Olá recebe o intervalo de tempo em um intervalo de tempo de 1 hora, solicitação Olá seria da seguinte maneira:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

resultado de saudação apareceria exemplo toohello semelhante a captura de tela a seguir:

![Alt "Resposta JSON mostrando o valor da métrica Tempo Médio de Resposta"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

tooretrieve dados ou agregação de vários pontos, adicione nomes de definição de métrica hello e filtro de toohello de tipos de agregação, como visto no exemplo a seguir de saudação:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a>Use o ARMClient
Uma alternativa toousing PowerShell (conforme mostrado acima), é toouse [ARMClient](https://github.com/projectkudu/ARMClient) em seu computador Windows. ARMClient manipula automaticamente a autenticação de saudação do AD do Azure (e token JWT resultante). Olá, etapas a seguir descrevem o uso do ARMClient para recuperar dados da métrica:

1. Instalar [Chocolatey](https://chocolatey.org/) e [ARMClient](https://github.com/projectkudu/ARMClient).
2. Em uma janela de terminal, digite *armclient.exe login*. Isso solicitará que você toolog em tooAzure.
3. Digite *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*
4. Digite *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*

![ALT "Usando o ARMClient toowork com hello API de REST de monitoramento do Azure"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a>Recuperar Olá ID de recurso
Usando a API REST de saudação realmente pode ajudar definições de métricas disponíveis toounderstand hello, granularidade e valores relacionados. Essa informação é útil ao usar Olá [biblioteca de gerenciamento do Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).

Olá precede o código, Olá toouse de ID de recurso é toohello de caminho completo de saudação desejado recursos do Azure. Por exemplo, tooquery em relação a um aplicativo Web do Azure, ID de recurso Olá seria:

*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*

Olá lista a seguir contém alguns exemplos de formatos de ID de recurso para vários recursos do Azure:

* **Hub IoT** - /subscriptions/*{id-da-assinatura}*/resourceGroups/*{nome-do-grupo-de-recursos}*/providers/Microsoft.Devices/IotHubs/*{nome-do-hub-iot}*
* **Pool SQL Elástico** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*
* **Banco de Dados SQL (v12)** - /subscriptions/*{id-da-assinatura}*/resourceGroups/*{nome-do-grupo-de-recursos}*/providers/Microsoft.Sql/servers/*{nome-do-servidor}*/databases/*{nome-do-banco-de-dados}*
* **Barramento de Serviço** - /subscriptions/*{id-da-assinatura}*/resourceGroups/*{nome-do-grupo-de-recursos}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*
* **Conjuntos de Dimensionamento da VM** - /subscriptions/*{id-da-assinatura}*/resourceGroups/*{nome-do-grupo-de-recursos}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*
* **VMs** - /subscriptions/*{id-da-assinatura}*/resourceGroups/*{nome-do-grupo-de-recursos}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*
* **Hubs de Eventos** - /subscriptions/*{id-da-assinatura}*/resourceGroups/*{nome-do-grupo-de-recursos}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*

Há abordagens alternativas tooretrieving Olá ID do recurso, incluindo o uso do Gerenciador de recursos do Azure, exibindo recursos Olá desejado na Olá portal do Azure e por meio do PowerShell ou hello CLI do Azure.

### <a name="azure-resource-explorer"></a>Gerenciador de Recursos do Azure
toofind Olá ID de recurso para um recurso desejado, uma abordagem útil é Olá toouse [Gerenciador de recursos do Azure](https://resources.azure.com) ferramenta. Navegue recurso toohello desejado e depois examinar ID Olá mostrado como Olá captura de tela a seguir:

![Alt "Explorador de Recursos do Azure"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a>Portal do Azure
ID do recurso Olá também pode ser obtido Olá portal do Azure. toodo assim, navegue recurso toohello desejado e, em seguida, selecione Propriedades. Olá ID de recurso é exibida na folha de propriedades de hello, como visto no hello captura de tela a seguir:

![ALT "ID de recurso exibida na folha de propriedades de saudação em Olá portal do Azure"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a>Azure PowerShell
ID do recurso Olá pode ser recuperado usando cmdlets do PowerShell do Azure também. Por exemplo, ID de recurso Olá tooobtain para um aplicativo Web do Azure, execute Olá Get-AzureRmWebApp cmdlet, como Olá captura de tela a seguir:

![Alt "ID do recurso obtido por meio do PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a>CLI do Azure
tooretrieve Olá ID de recurso usando Olá CLI do Azure, execute o comando de 'webapp azure Mostrar' hello, especificando o hello ' – json' opção, conforme mostrado no hello captura de tela a seguir:

![Alt "ID do recurso obtido por meio do PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a>Recuperar dados de Log de atividade
Em adição tooworking com definições de métricas e valores relacionados, também é possível tooretrieve interessantes insights tooAzure relacionados obter recursos adicionais. Por exemplo, é possível tooquery [log de atividades](https://msdn.microsoft.com/library/azure/dn931934.aspx) dados. Olá exemplo a seguir demonstra o uso de dados de log de atividade Olá API REST do Azure Monitor tooquery dentro de um intervalo de datas específicas para uma assinatura do Azure:

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a>Próximas etapas
* Saudação de revisão [visão geral do monitoramento](monitoring-overview.md).
* Saudação de exibição [suporte para métricas com o Azure Monitor](monitoring-supported-metrics.md).
* Saudação de revisão [referência de API REST do Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).
* Saudação de revisão [biblioteca de gerenciamento do Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).
