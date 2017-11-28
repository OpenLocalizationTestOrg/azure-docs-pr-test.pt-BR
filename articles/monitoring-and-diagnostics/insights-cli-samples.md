---
title: "Exemplos de início rápido da CLI 1.0 do Azure Monitor. | Microsoft Docs"
description: "Comandos de exemplo da CLI 1.0 para recursos do Azure Monitor. O Azure Monitor é um serviço do Microsoft Azure que permite enviar notificações de alerta ou chamar URLs da Web baseadas em valores dos dados de telemetria configurados, bem como dimensionar automaticamente Serviços de Nuvem, Máquinas Virtuais e Aplicativos Web."
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
ms.openlocfilehash: ec4512500dc3c77a40d2ebd1e6b460d5bb005811
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="9e0b6-105">Exemplos de início rápido da CLI 1.0 de plataforma cruzada do Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="9e0b6-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="9e0b6-106">Este artigo mostra um exemplo de CLI (interface de linha de comando) que ajudará você a acessar os recursos do Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-106">This article shows you sample command-line interface (CLI) commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="9e0b6-107">O Azure Monitor permite que você dimensione automaticamente Serviços de Nuvem, Máquinas Virtuais e Aplicativos Web e envie notificações de alerta ou chame URLs da Web com base em valores de dados de telemetria configurados.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-107">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="9e0b6-108">O Azure Monitor é o novo nome do que era chamado "Azure Insights" até 25 de setembro de 2016.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-108">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="9e0b6-109">No entanto, os namespaces e, portanto, os comandos a seguir ainda contêm os “insights”.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-109">However, the namespaces and thus the commands below still contain the "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="9e0b6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9e0b6-110">Prerequisites</span></span>
<span data-ttu-id="9e0b6-111">Se você ainda não tiver instalado a CLI do Azure, confira [Instalar a CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9e0b6-111">If you haven't already installed the Azure CLI, see [Install the Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="9e0b6-112">Se não estiver familiarizado com a CLI do Azure, você poderá ler mais sobre ela em [Usar a CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9e0b6-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="9e0b6-113">No Windows, instale o npm do [site do Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="9e0b6-113">In Windows, install npm from the [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="9e0b6-114">Após concluir a instalação, usando o CMD.exe com os privilégios de Executar como Administrador, execute o seguinte na pasta em que o npm está instalado:</span><span class="sxs-lookup"><span data-stu-id="9e0b6-114">After you complete the installation, using CMD.exe with Run As Administrator privileges, execute the following from the folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="9e0b6-115">Em seguida, navegue até qualquer pasta/local desejado e digite na linha de comando:</span><span class="sxs-lookup"><span data-stu-id="9e0b6-115">Next, navigate to any folder/location you want and type at the command-line:</span></span>

```console
azure help
```

## <a name="log-in-to-azure"></a><span data-ttu-id="9e0b6-116">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="9e0b6-116">Log in to Azure</span></span>
<span data-ttu-id="9e0b6-117">A primeira etapa é fazer logon na conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-117">The first step is to login to your Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="9e0b6-118">Depois de executar esse comando, será necessário entrar usando as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-118">After running this command, you have to sign in via the instructions on the screen.</span></span> <span data-ttu-id="9e0b6-119">Posteriormente, você verá sua Conta, sua TenantId e sua ID da Assinatura padrão. Todos os comandos funcionam no contexto de sua assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in the context of your default subscription.</span></span>

<span data-ttu-id="9e0b6-120">Para listar os detalhes da sua assinatura atual, use o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-120">To list the details of your current subscription, use the following command.</span></span>

```console
azure account show
```

<span data-ttu-id="9e0b6-121">Para alterar o contexto de trabalho para uma assinatura diferente, use o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-121">To change working context to a different subscription, use the following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="9e0b6-122">Para usar comandos do Azure Resource Manager e do Azure Monitor, você precisa estar no modo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-122">To use Azure Resource Manager and Azure Monitor commands, you need to be in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="9e0b6-123">Para exibir uma lista de todos os comandos permitidos do Azure Monitor, execute o seguinte.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-123">To view a list of all supported Azure Monitor commands, perform the following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="9e0b6-124">Exibir o log de atividade para uma assinatura</span><span class="sxs-lookup"><span data-stu-id="9e0b6-124">View activity log for a subscription</span></span>
<span data-ttu-id="9e0b6-125">Para exibir uma lista de eventos de log de atividade, execute o seguinte.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-125">To view a list of activity log events, perform the following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="9e0b6-126">Tente o seguinte para exibir todas as opções disponíveis:</span><span class="sxs-lookup"><span data-stu-id="9e0b6-126">Try the following to view all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="9e0b6-127">Veja um exemplo para listar logs por resourceGroup</span><span class="sxs-lookup"><span data-stu-id="9e0b6-127">Here is an example to list logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="9e0b6-128">Exemplo para listar logs por chamador</span><span class="sxs-lookup"><span data-stu-id="9e0b6-128">Example to list logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="9e0b6-129">Exemplo para listar logs por chamador em um tipo de recurso, entre datas de início e de término</span><span class="sxs-lookup"><span data-stu-id="9e0b6-129">Example to list logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="9e0b6-130">Trabalhar com alertas</span><span class="sxs-lookup"><span data-stu-id="9e0b6-130">Work with alerts</span></span>
<span data-ttu-id="9e0b6-131">Você pode usar as informações na seção para trabalhar com alertas.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-131">You can use the information in the section to work with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="9e0b6-132">Obter regras de alerta em um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9e0b6-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="9e0b6-133">Criar uma regra de alerta de métrica</span><span class="sxs-lookup"><span data-stu-id="9e0b6-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="9e0b6-134">Criar uma regra de alerta de teste na Web</span><span class="sxs-lookup"><span data-stu-id="9e0b6-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="9e0b6-135">Excluir uma regra de alerta</span><span class="sxs-lookup"><span data-stu-id="9e0b6-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="9e0b6-136">Perfis de log</span><span class="sxs-lookup"><span data-stu-id="9e0b6-136">Log profiles</span></span>
<span data-ttu-id="9e0b6-137">Use as informações desta seção para trabalhar com perfis de log.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-137">Use the information in this section to work with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="9e0b6-138">Obter um perfil de log</span><span class="sxs-lookup"><span data-stu-id="9e0b6-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="9e0b6-139">Adicionar um perfil de log sem retenção</span><span class="sxs-lookup"><span data-stu-id="9e0b6-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="9e0b6-140">Remover um perfil de log</span><span class="sxs-lookup"><span data-stu-id="9e0b6-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="9e0b6-141">Adicionar um perfil de log com retenção</span><span class="sxs-lookup"><span data-stu-id="9e0b6-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="9e0b6-142">Adicionar um perfil de log com retenção e Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="9e0b6-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="9e0b6-143">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="9e0b6-143">Diagnostics</span></span>
<span data-ttu-id="9e0b6-144">Use as informações desta seção para trabalhar com configurações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-144">Use the information in this section to work with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="9e0b6-145">Obter uma configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="9e0b6-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="9e0b6-146">Desabilitar uma configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="9e0b6-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="9e0b6-147">Habilitar uma configuração de diagnóstico sem retenção</span><span class="sxs-lookup"><span data-stu-id="9e0b6-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="9e0b6-148">Autoscale</span><span class="sxs-lookup"><span data-stu-id="9e0b6-148">Autoscale</span></span>
<span data-ttu-id="9e0b6-149">Use as informações desta seção para trabalhar com configurações de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-149">Use the information in this section to work with autoscale settings.</span></span> <span data-ttu-id="9e0b6-150">Você precisa modificar estes exemplos.</span><span class="sxs-lookup"><span data-stu-id="9e0b6-150">You need to modify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="9e0b6-151">Obter configurações de dimensionamento automático para um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9e0b6-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="9e0b6-152">Obter configurações de dimensionamento automático por nome em um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9e0b6-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="9e0b6-153">Definir as configurações de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="9e0b6-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
