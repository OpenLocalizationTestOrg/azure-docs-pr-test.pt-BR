---
title: "exemplos de início rápido aaaAzure Monitor CLI 1.0. | Microsoft Docs"
description: "Comandos de exemplo da CLI 1.0 para recursos do Azure Monitor. Monitor do Azure é um serviço do Microsoft Azure que permite que as notificações de alerta de toosend, chamada web URLs com base nos valores de dados de telemetria configurado e os serviços de nuvem de dimensionamento automático, máquinas virtuais e aplicativos Web."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="8dd80-105">Exemplos de início rápido da CLI 1.0 de plataforma cruzada do Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="8dd80-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="8dd80-106">Este mostra artigo exemplo toohelp de comandos de interface de linha de comando (CLI) você acessar os recursos do Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="8dd80-106">This article shows you sample command-line interface (CLI) commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="8dd80-107">Monitor do Azure permite que notificações de alerta serviços de nuvem, máquinas virtuais e aplicativos Web e toosend tooAutoScale ou chamada web URLs com base nos valores de dados de telemetria configurado.</span><span class="sxs-lookup"><span data-stu-id="8dd80-107">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="8dd80-108">Monitor do Azure é Olá novo nome para o que era chamado de "Azure Insights" até 25 de setembro de 2016.</span><span class="sxs-lookup"><span data-stu-id="8dd80-108">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="8dd80-109">No entanto, Olá namespaces e, portanto, comandos de saudação abaixo ainda contêm insights"Olá".</span><span class="sxs-lookup"><span data-stu-id="8dd80-109">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="8dd80-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8dd80-110">Prerequisites</span></span>
<span data-ttu-id="8dd80-111">Se você ainda não instalou Olá CLI do Azure, consulte [instalação Olá CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8dd80-111">If you haven't already installed hello Azure CLI, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="8dd80-112">Se você estiver familiarizado com a CLI do Azure, você pode ler mais sobre ele no [Olá Use CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8dd80-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="8dd80-113">No Windows, instale o npm de saudação [site Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="8dd80-113">In Windows, install npm from hello [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="8dd80-114">Depois de concluir a instalação Olá, usando CMD.exe com privilégios de executar como administrador, execute o seguinte Olá da pasta Olá onde npm está instalado:</span><span class="sxs-lookup"><span data-stu-id="8dd80-114">After you complete hello installation, using CMD.exe with Run As Administrator privileges, execute hello following from hello folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="8dd80-115">Em seguida, navegue até os local da pasta tooany e digite a saudação de linha de comando:</span><span class="sxs-lookup"><span data-stu-id="8dd80-115">Next, navigate tooany folder/location you want and type at hello command-line:</span></span>

```console
azure help
```

## <a name="log-in-tooazure"></a><span data-ttu-id="8dd80-116">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="8dd80-116">Log in tooAzure</span></span>
<span data-ttu-id="8dd80-117">Olá primeira etapa é toologin tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="8dd80-117">hello first step is toologin tooyour Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="8dd80-118">Depois de executar esse comando, você tem toosign via instruções Olá na tela hello.</span><span class="sxs-lookup"><span data-stu-id="8dd80-118">After running this command, you have toosign in via hello instructions on hello screen.</span></span> <span data-ttu-id="8dd80-119">Posteriormente, você verá sua Conta, sua TenantId e sua ID da Assinatura padrão. Todos os comandos funcionam no contexto de saudação da sua assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="8dd80-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in hello context of your default subscription.</span></span>

<span data-ttu-id="8dd80-120">detalhes de saudação toolist de sua assinatura atual, use Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="8dd80-120">toolist hello details of your current subscription, use hello following command.</span></span>

```console
azure account show
```

<span data-ttu-id="8dd80-121">toochange trabalho contexto tooa assinatura diferente, use Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="8dd80-121">toochange working context tooa different subscription, use hello following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="8dd80-122">toouse Gerenciador de recursos do Azure e o Monitor do Azure os comandos, você precisa toobe no modo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8dd80-122">toouse Azure Resource Manager and Azure Monitor commands, you need toobe in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="8dd80-123">tooview uma lista de todos os comandos com suporte do Monitor do Azure, execute o seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="8dd80-123">tooview a list of all supported Azure Monitor commands, perform hello following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="8dd80-124">Exibir o log de atividade para uma assinatura</span><span class="sxs-lookup"><span data-stu-id="8dd80-124">View activity log for a subscription</span></span>
<span data-ttu-id="8dd80-125">tooview uma lista de eventos do log de atividade, execute o seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="8dd80-125">tooview a list of activity log events, perform hello following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="8dd80-126">Tente Olá tooview a seguir todas as opções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="8dd80-126">Try hello following tooview all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="8dd80-127">Aqui está um exemplo logs toolist por um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8dd80-127">Here is an example toolist logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="8dd80-128">Logs do exemplo toolist pelo chamador</span><span class="sxs-lookup"><span data-stu-id="8dd80-128">Example toolist logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="8dd80-129">Logs do exemplo toolist pelo chamador em um tipo de recurso, dentro de uma data de início e término</span><span class="sxs-lookup"><span data-stu-id="8dd80-129">Example toolist logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="8dd80-130">Trabalhar com alertas</span><span class="sxs-lookup"><span data-stu-id="8dd80-130">Work with alerts</span></span>
<span data-ttu-id="8dd80-131">Você pode usar informações de Olá Olá seção toowork com alertas.</span><span class="sxs-lookup"><span data-stu-id="8dd80-131">You can use hello information in hello section toowork with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="8dd80-132">Obter regras de alerta em um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8dd80-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="8dd80-133">Criar uma regra de alerta de métrica</span><span class="sxs-lookup"><span data-stu-id="8dd80-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="8dd80-134">Criar uma regra de alerta de teste na Web</span><span class="sxs-lookup"><span data-stu-id="8dd80-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="8dd80-135">Excluir uma regra de alerta</span><span class="sxs-lookup"><span data-stu-id="8dd80-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="8dd80-136">Perfis de log</span><span class="sxs-lookup"><span data-stu-id="8dd80-136">Log profiles</span></span>
<span data-ttu-id="8dd80-137">Use as informações de saudação toowork essa seção com perfis de log.</span><span class="sxs-lookup"><span data-stu-id="8dd80-137">Use hello information in this section toowork with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="8dd80-138">Obter um perfil de log</span><span class="sxs-lookup"><span data-stu-id="8dd80-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="8dd80-139">Adicionar um perfil de log sem retenção</span><span class="sxs-lookup"><span data-stu-id="8dd80-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="8dd80-140">Remover um perfil de log</span><span class="sxs-lookup"><span data-stu-id="8dd80-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="8dd80-141">Adicionar um perfil de log com retenção</span><span class="sxs-lookup"><span data-stu-id="8dd80-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="8dd80-142">Adicionar um perfil de log com retenção e Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="8dd80-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="8dd80-143">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="8dd80-143">Diagnostics</span></span>
<span data-ttu-id="8dd80-144">Use as informações de saudação toowork essa seção com as configurações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="8dd80-144">Use hello information in this section toowork with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="8dd80-145">Obter uma configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="8dd80-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="8dd80-146">Desabilitar uma configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="8dd80-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="8dd80-147">Habilitar uma configuração de diagnóstico sem retenção</span><span class="sxs-lookup"><span data-stu-id="8dd80-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="8dd80-148">Autoscale</span><span class="sxs-lookup"><span data-stu-id="8dd80-148">Autoscale</span></span>
<span data-ttu-id="8dd80-149">Use as informações de saudação toowork essa seção com configurações de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="8dd80-149">Use hello information in this section toowork with autoscale settings.</span></span> <span data-ttu-id="8dd80-150">É necessário toomodify esses exemplos.</span><span class="sxs-lookup"><span data-stu-id="8dd80-150">You need toomodify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="8dd80-151">Obter configurações de dimensionamento automático para um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8dd80-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="8dd80-152">Obter configurações de dimensionamento automático por nome em um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8dd80-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="8dd80-153">Definir as configurações de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="8dd80-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
