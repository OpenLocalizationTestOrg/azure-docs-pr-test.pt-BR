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
# <a name="azure-monitoring-rest-api-walkthrough"></a><span data-ttu-id="710da-103">Passo a passo da API REST de monitoramento do Azure</span><span class="sxs-lookup"><span data-stu-id="710da-103">Azure Monitoring REST API Walkthrough</span></span>
<span data-ttu-id="710da-104">Este artigo mostra como tooperform autenticação para o seu código pode usar Olá [referência de API REST do Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="710da-104">This article shows you how tooperform authentication so your code can use hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>         

<span data-ttu-id="710da-105">Olá API do Monitor do Azure torna possível tooprogrammatically recuperar saudação padrão disponíveis de definições de métricas (tipo de saudação da métrica, como tempo de CPU, solicitações, etc.), granularidade e valores da métrica.</span><span class="sxs-lookup"><span data-stu-id="710da-105">hello Azure Monitor API makes it possible tooprogrammatically retrieve hello available default metric definitions (hello type of metric such as CPU Time, Requests, etc.), granularity, and metric values.</span></span> <span data-ttu-id="710da-106">Depois de recuperados, dados saudação podem ser salvos em um repositório de dados separado, como o banco de dados do SQL Azure, o banco de dados do Azure Cosmos ou do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="710da-106">Once retrieved, hello data can be saved in a separate data store such as Azure SQL Database, Azure Cosmos DB, or Azure Data Lake.</span></span> <span data-ttu-id="710da-107">A partir daí análises adicionais podem ser executadas conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="710da-107">From there additional analysis can be performed as needed.</span></span>

<span data-ttu-id="710da-108">Além de trabalhar com vários pontos de dados da métrica, conforme este artigo demonstra, Olá Monitor API torna as regras de alerta toolist possíveis, exibir logs de atividade e muito mais.</span><span class="sxs-lookup"><span data-stu-id="710da-108">Besides working with various metric data points, as this article demonstrates, hello Monitor API makes it possible toolist alert rules, view activity logs, and much more.</span></span> <span data-ttu-id="710da-109">Para obter uma lista completa de operações disponíveis, consulte Olá [referência de API REST do Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="710da-109">For a full list of available operations, see hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

## <a name="authenticating-azure-monitor-requests"></a><span data-ttu-id="710da-110">Autenticação de solicitações do Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="710da-110">Authenticating Azure Monitor Requests</span></span>
<span data-ttu-id="710da-111">Olá primeira etapa é a solicitação de saudação tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="710da-111">hello first step is tooauthenticate hello request.</span></span>

<span data-ttu-id="710da-112">Todas as tarefas de saudação executadas em relação hello Azure Monitor API use hello Azure Resource Manager autenticação modelo.</span><span class="sxs-lookup"><span data-stu-id="710da-112">All hello tasks executed against hello Azure Monitor API use hello Azure Resource Manager authentication model.</span></span> <span data-ttu-id="710da-113">Portanto, todas as solicitações devem ser autenticadas com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="710da-113">Therefore, all requests must be authenticated with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="710da-114">Um aplicativo de cliente abordagem tooauthenticate hello é toocreate uma entidade de serviço do AD do Azure e recuperar o token de autenticação (JWT) hello.</span><span class="sxs-lookup"><span data-stu-id="710da-114">One approach tooauthenticate hello client application is toocreate an Azure AD service principal and retrieve hello authentication (JWT) token.</span></span> <span data-ttu-id="710da-115">Olá seguinte script de exemplo demonstra como criar um AD do Azure entidade de serviço por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="710da-115">hello following sample script demonstrates creating an Azure AD service principal via PowerShell.</span></span> <span data-ttu-id="710da-116">Para obter instruções mais detalhadas, consulte a documentação do toohello em [usando Azure PowerShell toocreate um recurso do serviço principal tooaccess](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span><span class="sxs-lookup"><span data-stu-id="710da-116">For a more detailed walk-through, refer toohello documentation on [using Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span></span> <span data-ttu-id="710da-117">Também é possível muito[criar uma entidade de serviço por meio do portal do Azure de saudação](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="710da-117">It is also possible too[create a service principal via hello Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

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

<span data-ttu-id="710da-118">Olá tooquery API do Monitor do Azure, aplicativo de cliente hello deve usar Olá criado anteriormente tooauthenticate principal do serviço.</span><span class="sxs-lookup"><span data-stu-id="710da-118">tooquery hello Azure Monitor API, hello client application should use hello previously created service principal tooauthenticate.</span></span> <span data-ttu-id="710da-119">saudação de script do PowerShell de exemplo a seguir mostra uma abordagem, usando Olá [biblioteca de autenticação do Active Directory](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp obter token de JWT de saudação autenticação.</span><span class="sxs-lookup"><span data-stu-id="710da-119">hello following example PowerShell script shows one approach, using hello [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp get hello JWT authentication token.</span></span> <span data-ttu-id="710da-120">token JWT de saudação é passada como parte de um parâmetro de autorização HTTP no solicitações toohello API de REST do Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="710da-120">hello JWT token is passed as part of an HTTP Authorization parameter in requests toohello Azure Monitor REST API.</span></span>

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

<span data-ttu-id="710da-121">Após a conclusão da etapa de configuração de autenticação hello, consultas, em seguida, podem ser executadas em relação a saudação API de REST do Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="710da-121">Once hello authentication setup step is complete, queries can then be executed against hello Azure Monitor REST API.</span></span> <span data-ttu-id="710da-122">Há duas consultas úteis:</span><span class="sxs-lookup"><span data-stu-id="710da-122">There are two helpful queries:</span></span>

1. <span data-ttu-id="710da-123">Lista de definições de métricas de saudação para um recurso</span><span class="sxs-lookup"><span data-stu-id="710da-123">List hello metric definitions for a resource</span></span>
2. <span data-ttu-id="710da-124">Recuperar os valores da métrica Olá</span><span class="sxs-lookup"><span data-stu-id="710da-124">Retrieve hello metric values</span></span>

## <a name="retrieve-metric-definitions"></a><span data-ttu-id="710da-125">Recuperar as definições de métrica</span><span class="sxs-lookup"><span data-stu-id="710da-125">Retrieve Metric Definitions</span></span>
> [!NOTE]
> <span data-ttu-id="710da-126">definições de métrica tooretrieve usando Olá API de REST do Monitor do Azure, use "2016-03-01" como Olá versão da API.</span><span class="sxs-lookup"><span data-stu-id="710da-126">tooretrieve metric definitions using hello Azure Monitor REST API, use "2016-03-01" as hello API version.</span></span>
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
<span data-ttu-id="710da-127">Um aplicativo do Azure lógica, definições de métrica Olá apareceria semelhante toohello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="710da-127">For an Azure Logic App, hello metric definitions would appear similar toohello following screenshot:</span></span>

![Alt "Visão JSON da resposta da definição da métrica."](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

<span data-ttu-id="710da-129">Para obter mais informações, consulte Olá [lista definições de métricas de saudação para um recurso na API de REST do Azure Monitor](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentação.</span><span class="sxs-lookup"><span data-stu-id="710da-129">For more information, see hello [List hello metric definitions for a resource in Azure Monitor REST API](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentation.</span></span>

## <a name="retrieve-metric-values"></a><span data-ttu-id="710da-130">Recuperar valores de métrica</span><span class="sxs-lookup"><span data-stu-id="710da-130">Retrieve Metric Values</span></span>
<span data-ttu-id="710da-131">Depois de definições de métricas disponíveis Olá são conhecidas, é então tooretrieve possíveis Olá valores relacionados de métrica.</span><span class="sxs-lookup"><span data-stu-id="710da-131">Once hello available metric definitions are known, it is then possible tooretrieve hello related metric values.</span></span> <span data-ttu-id="710da-132">Use nome 'value' da métrica Olá (não Olá 'localizedValue') para todas as solicitações filtragem (por exemplo, recuperar Olá 'CpuTime' e 'Solicitar' métrica pontos de dados).</span><span class="sxs-lookup"><span data-stu-id="710da-132">Use hello metric’s name ‘value’ (not hello ‘localizedValue’) for any filtering requests (for example, retrieve hello ‘CpuTime’ and ‘Requests’ metric data points).</span></span> <span data-ttu-id="710da-133">Se nenhum filtro for especificado, a métrica de padrão de saudação é retornada.</span><span class="sxs-lookup"><span data-stu-id="710da-133">If no filters are specified, hello default metric is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="710da-134">valores da métrica tooretrieve usando Olá API de REST do Monitor do Azure, use "2016-06-01" como Olá versão da API.</span><span class="sxs-lookup"><span data-stu-id="710da-134">tooretrieve metric values using hello Azure Monitor REST API, use "2016-06-01" as hello API version.</span></span>
>
>

<span data-ttu-id="710da-135">**Método**: GET</span><span class="sxs-lookup"><span data-stu-id="710da-135">**Method**: GET</span></span>

<span data-ttu-id="710da-136">**URI de solicitação**: https://management.azure.com/subscriptions/*{id-da-assinatura}*/resourceGroups/*{nome-do-grupo-de-recursos}*/providers/*{namespace-do-provedor-recursos}*/*{tipo-de-recurso}*/*{nome-do-recurso}*/providers/microsoft.insights/metrics?$filter=*{filtro}*&api-version=*{versão-da-api}*</span><span class="sxs-lookup"><span data-stu-id="710da-136">**Request URI**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span></span>

<span data-ttu-id="710da-137">Por exemplo, tooretrieve os pontos de dados de métrica Olá RunsSucceeded para Olá recebe o intervalo de tempo em um intervalo de tempo de 1 hora, solicitação Olá seria da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="710da-137">For example, tooretrieve hello RunsSucceeded metric data points for hello given time range and for a time grain of 1 hour, hello request would be as follows:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

<span data-ttu-id="710da-138">resultado de saudação apareceria exemplo toohello semelhante a captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="710da-138">hello result would appear similar toohello example following screenshot:</span></span>

![Alt "Resposta JSON mostrando o valor da métrica Tempo Médio de Resposta"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

<span data-ttu-id="710da-140">tooretrieve dados ou agregação de vários pontos, adicione nomes de definição de métrica hello e filtro de toohello de tipos de agregação, como visto no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="710da-140">tooretrieve multiple data or aggregation points, add hello metric definition names and aggregation types toohello filter, as seen in hello following example:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a><span data-ttu-id="710da-141">Use o ARMClient</span><span class="sxs-lookup"><span data-stu-id="710da-141">Use ARMClient</span></span>
<span data-ttu-id="710da-142">Uma alternativa toousing PowerShell (conforme mostrado acima), é toouse [ARMClient](https://github.com/projectkudu/ARMClient) em seu computador Windows.</span><span class="sxs-lookup"><span data-stu-id="710da-142">An alternative toousing PowerShell (as shown above), is toouse [ARMClient](https://github.com/projectkudu/ARMClient) on your Windows machine.</span></span> <span data-ttu-id="710da-143">ARMClient manipula automaticamente a autenticação de saudação do AD do Azure (e token JWT resultante).</span><span class="sxs-lookup"><span data-stu-id="710da-143">ARMClient handles hello Azure AD authentication (and resulting JWT token) automatically.</span></span> <span data-ttu-id="710da-144">Olá, etapas a seguir descrevem o uso do ARMClient para recuperar dados da métrica:</span><span class="sxs-lookup"><span data-stu-id="710da-144">hello following steps outline use of ARMClient for retrieving metric data:</span></span>

1. <span data-ttu-id="710da-145">Instalar [Chocolatey](https://chocolatey.org/) e [ARMClient](https://github.com/projectkudu/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="710da-145">Install [Chocolatey](https://chocolatey.org/) and [ARMClient](https://github.com/projectkudu/ARMClient).</span></span>
2. <span data-ttu-id="710da-146">Em uma janela de terminal, digite *armclient.exe login*.</span><span class="sxs-lookup"><span data-stu-id="710da-146">In a terminal window, type *armclient.exe login*.</span></span> <span data-ttu-id="710da-147">Isso solicitará que você toolog em tooAzure.</span><span class="sxs-lookup"><span data-stu-id="710da-147">This prompts you toolog in tooAzure.</span></span>
3. <span data-ttu-id="710da-148">Digite *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span><span class="sxs-lookup"><span data-stu-id="710da-148">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span></span>
4. <span data-ttu-id="710da-149">Digite *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span><span class="sxs-lookup"><span data-stu-id="710da-149">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span></span>

![ALT "Usando o ARMClient toowork com hello API de REST de monitoramento do Azure"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a><span data-ttu-id="710da-151">Recuperar Olá ID de recurso</span><span class="sxs-lookup"><span data-stu-id="710da-151">Retrieve hello Resource ID</span></span>
<span data-ttu-id="710da-152">Usando a API REST de saudação realmente pode ajudar definições de métricas disponíveis toounderstand hello, granularidade e valores relacionados.</span><span class="sxs-lookup"><span data-stu-id="710da-152">Using hello REST API can really help toounderstand hello available metric definitions, granularity, and related values.</span></span> <span data-ttu-id="710da-153">Essa informação é útil ao usar Olá [biblioteca de gerenciamento do Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="710da-153">That information is helpful when using hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>

<span data-ttu-id="710da-154">Olá precede o código, Olá toouse de ID de recurso é toohello de caminho completo de saudação desejado recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="710da-154">For hello preceding code, hello resource ID toouse is hello full path toohello desired Azure resource.</span></span> <span data-ttu-id="710da-155">Por exemplo, tooquery em relação a um aplicativo Web do Azure, ID de recurso Olá seria:</span><span class="sxs-lookup"><span data-stu-id="710da-155">For example, tooquery against an Azure Web App, hello resource ID would be:</span></span>

<span data-ttu-id="710da-156">*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span><span class="sxs-lookup"><span data-stu-id="710da-156">*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span></span>

<span data-ttu-id="710da-157">Olá lista a seguir contém alguns exemplos de formatos de ID de recurso para vários recursos do Azure:</span><span class="sxs-lookup"><span data-stu-id="710da-157">hello following list contains a few examples of resource ID formats for various Azure resources:</span></span>

* <span data-ttu-id="710da-158">**Hub IoT** - /subscriptions/*{id-da-assinatura}*/resourceGroups/*{nome-do-grupo-de-recursos}*/providers/Microsoft.Devices/IotHubs/*{nome-do-hub-iot}*</span><span class="sxs-lookup"><span data-stu-id="710da-158">**IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span></span>
* <span data-ttu-id="710da-159">**Pool SQL Elástico** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span><span class="sxs-lookup"><span data-stu-id="710da-159">**Elastic SQL Pool** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span></span>
* <span data-ttu-id="710da-160">**Banco de Dados SQL (v12)** - /subscriptions/*{id-da-assinatura}*/resourceGroups/*{nome-do-grupo-de-recursos}*/providers/Microsoft.Sql/servers/*{nome-do-servidor}*/databases/*{nome-do-banco-de-dados}*</span><span class="sxs-lookup"><span data-stu-id="710da-160">**SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span></span>
* <span data-ttu-id="710da-161">**Barramento de Serviço** - /subscriptions/*{id-da-assinatura}*/resourceGroups/*{nome-do-grupo-de-recursos}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span><span class="sxs-lookup"><span data-stu-id="710da-161">**Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span></span>
* <span data-ttu-id="710da-162">**Conjuntos de Dimensionamento da VM** - /subscriptions/*{id-da-assinatura}*/resourceGroups/*{nome-do-grupo-de-recursos}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span><span class="sxs-lookup"><span data-stu-id="710da-162">**VM Scale Sets** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span></span>
* <span data-ttu-id="710da-163">**VMs** - /subscriptions/*{id-da-assinatura}*/resourceGroups/*{nome-do-grupo-de-recursos}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span><span class="sxs-lookup"><span data-stu-id="710da-163">**VMs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span></span>
* <span data-ttu-id="710da-164">**Hubs de Eventos** - /subscriptions/*{id-da-assinatura}*/resourceGroups/*{nome-do-grupo-de-recursos}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span><span class="sxs-lookup"><span data-stu-id="710da-164">**Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span></span>

<span data-ttu-id="710da-165">Há abordagens alternativas tooretrieving Olá ID do recurso, incluindo o uso do Gerenciador de recursos do Azure, exibindo recursos Olá desejado na Olá portal do Azure e por meio do PowerShell ou hello CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="710da-165">There are alternative approaches tooretrieving hello resource ID, including using Azure Resource Explorer, viewing hello desired resource in hello Azure portal, and via PowerShell or hello Azure CLI.</span></span>

### <a name="azure-resource-explorer"></a><span data-ttu-id="710da-166">Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="710da-166">Azure Resource Explorer</span></span>
<span data-ttu-id="710da-167">toofind Olá ID de recurso para um recurso desejado, uma abordagem útil é Olá toouse [Gerenciador de recursos do Azure](https://resources.azure.com) ferramenta.</span><span class="sxs-lookup"><span data-stu-id="710da-167">toofind hello resource ID for a desired resource, one helpful approach is toouse hello [Azure Resource Explorer](https://resources.azure.com) tool.</span></span> <span data-ttu-id="710da-168">Navegue recurso toohello desejado e depois examinar ID Olá mostrado como Olá captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="710da-168">Navigate toohello desired resource and then look at hello ID shown, as in hello following screenshot:</span></span>

![Alt "Explorador de Recursos do Azure"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a><span data-ttu-id="710da-170">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="710da-170">Azure portal</span></span>
<span data-ttu-id="710da-171">ID do recurso Olá também pode ser obtido Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="710da-171">hello resource ID can also be obtained from hello Azure portal.</span></span> <span data-ttu-id="710da-172">toodo assim, navegue recurso toohello desejado e, em seguida, selecione Propriedades.</span><span class="sxs-lookup"><span data-stu-id="710da-172">toodo so, navigate toohello desired resource and then select Properties.</span></span> <span data-ttu-id="710da-173">Olá ID de recurso é exibida na folha de propriedades de hello, como visto no hello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="710da-173">hello Resource ID is displayed in hello Properties blade, as seen in hello following screenshot:</span></span>

![ALT "ID de recurso exibida na folha de propriedades de saudação em Olá portal do Azure"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a><span data-ttu-id="710da-175">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="710da-175">Azure PowerShell</span></span>
<span data-ttu-id="710da-176">ID do recurso Olá pode ser recuperado usando cmdlets do PowerShell do Azure também.</span><span class="sxs-lookup"><span data-stu-id="710da-176">hello resource ID can be retrieved using Azure PowerShell cmdlets as well.</span></span> <span data-ttu-id="710da-177">Por exemplo, ID de recurso Olá tooobtain para um aplicativo Web do Azure, execute Olá Get-AzureRmWebApp cmdlet, como Olá captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="710da-177">For example, tooobtain hello resource ID for an Azure Web App, execute hello Get-AzureRmWebApp cmdlet, as in hello following screenshot:</span></span>

![Alt "ID do recurso obtido por meio do PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a><span data-ttu-id="710da-179">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="710da-179">Azure CLI</span></span>
<span data-ttu-id="710da-180">tooretrieve Olá ID de recurso usando Olá CLI do Azure, execute o comando de 'webapp azure Mostrar' hello, especificando o hello ' – json' opção, conforme mostrado no hello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="710da-180">tooretrieve hello resource ID using hello Azure CLI, execute hello 'azure webapp show' command, specifying hello '--json' option, as shown in hello following screenshot:</span></span>

![Alt "ID do recurso obtido por meio do PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a><span data-ttu-id="710da-182">Recuperar dados de Log de atividade</span><span class="sxs-lookup"><span data-stu-id="710da-182">Retrieve Activity Log Data</span></span>
<span data-ttu-id="710da-183">Em adição tooworking com definições de métricas e valores relacionados, também é possível tooretrieve interessantes insights tooAzure relacionados obter recursos adicionais.</span><span class="sxs-lookup"><span data-stu-id="710da-183">In addition tooworking with metric definitions and related values, it is also possible tooretrieve additional interesting insights related tooAzure resources.</span></span> <span data-ttu-id="710da-184">Por exemplo, é possível tooquery [log de atividades](https://msdn.microsoft.com/library/azure/dn931934.aspx) dados.</span><span class="sxs-lookup"><span data-stu-id="710da-184">As an example, it is possible tooquery [activity log](https://msdn.microsoft.com/library/azure/dn931934.aspx) data.</span></span> <span data-ttu-id="710da-185">Olá exemplo a seguir demonstra o uso de dados de log de atividade Olá API REST do Azure Monitor tooquery dentro de um intervalo de datas específicas para uma assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="710da-185">hello following sample demonstrates using hello Azure Monitor REST API tooquery activity log data within a specific date range for an Azure subscription:</span></span>

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a><span data-ttu-id="710da-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="710da-186">Next steps</span></span>
* <span data-ttu-id="710da-187">Saudação de revisão [visão geral do monitoramento](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="710da-187">Review hello [Overview of Monitoring](monitoring-overview.md).</span></span>
* <span data-ttu-id="710da-188">Saudação de exibição [suporte para métricas com o Azure Monitor](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="710da-188">View hello [Supported metrics with Azure Monitor](monitoring-supported-metrics.md).</span></span>
* <span data-ttu-id="710da-189">Saudação de revisão [referência de API REST do Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="710da-189">Review hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>
* <span data-ttu-id="710da-190">Saudação de revisão [biblioteca de gerenciamento do Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="710da-190">Review hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>
