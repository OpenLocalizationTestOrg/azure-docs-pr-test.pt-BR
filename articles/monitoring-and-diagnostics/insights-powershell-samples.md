---
title: "Exemplos de início rápido do PowerShell do Azure Monitor. | Microsoft Docs"
description: "Use o PowerShell para acessar os recursos do Azure Monitor, como o dimensionamento automático, alertas, webhooks e pesquisa de logs de atividade."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 48f064884c2a6d0a55cc58a44169ed03c62de46d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="71b87-104">Exemplos de início rápido do PowerShell do Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="71b87-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="71b87-105">Este artigo mostra exemplos de comandos do PowerShell que ajudarão você a acessar os recursos do Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="71b87-105">This article shows you sample PowerShell commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="71b87-106">O Azure Monitor permite que você dimensione automaticamente Serviços de Nuvem, Máquinas Virtuais e Aplicativos Web e envie notificações de alerta ou chame URLs da Web com base em valores de dados de telemetria configurados.</span><span class="sxs-lookup"><span data-stu-id="71b87-106">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="71b87-107">O Azure Monitor é o novo nome do que era chamado "Azure Insights" até 25 de setembro de 2016.</span><span class="sxs-lookup"><span data-stu-id="71b87-107">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="71b87-108">No entanto, os namespaces e, portanto, os comandos a seguir, ainda contêm os “insights”.</span><span class="sxs-lookup"><span data-stu-id="71b87-108">However, the namespaces and thus the following commands still contain the "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="71b87-109">Configurar o PowerShell</span><span class="sxs-lookup"><span data-stu-id="71b87-109">Set up PowerShell</span></span>
<span data-ttu-id="71b87-110">Se ainda não tiver feito isso, configure o PowerShell para ser executado no seu computador.</span><span class="sxs-lookup"><span data-stu-id="71b87-110">If you haven't already, set up PowerShell to run on your computer.</span></span> <span data-ttu-id="71b87-111">Para saber mais, consulte [Como instalar e configurar o PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="71b87-111">For more information, see [How to Install and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="71b87-112">Exemplos neste artigo</span><span class="sxs-lookup"><span data-stu-id="71b87-112">Examples in this article</span></span>
<span data-ttu-id="71b87-113">Os exemplos neste artigo ilustram como você pode usar os cmdlets do Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="71b87-113">The examples in the article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="71b87-114">Você também pode ver a lista completa de cmdlets do PowerShell do Azure Monitor em [Cmdlets do Azure Monitor (Insights)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="71b87-114">You can also review the entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="71b87-115">Conectar-se e usar assinaturas</span><span class="sxs-lookup"><span data-stu-id="71b87-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="71b87-116">Primeiro, entre em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="71b87-116">First, log in to your Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="71b87-117">Isso exige que você se conecte.</span><span class="sxs-lookup"><span data-stu-id="71b87-117">This requires you to sign in.</span></span> <span data-ttu-id="71b87-118">Quando fizer isso, você verá sua Conta, sua TenantID e ID da Assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="71b87-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="71b87-119">Todos os cmdlets do Azure funcionam no contexto de sua assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="71b87-119">All the Azure cmdlets work in the context of your default subscription.</span></span> <span data-ttu-id="71b87-120">Para ver a lista de assinaturas a que você tem acesso, use o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="71b87-120">To view the list of subscriptions you have access to, use the following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="71b87-121">Para alterar o contexto de trabalho para uma assinatura diferente, use o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="71b87-121">To change your working context to a different subscription, use the following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="71b87-122">Recuperar o log de atividade para uma assinatura</span><span class="sxs-lookup"><span data-stu-id="71b87-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="71b87-123">Use o cmdlet `Get-AzureRmLog` .</span><span class="sxs-lookup"><span data-stu-id="71b87-123">Use the `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="71b87-124">A seguir, temos alguns exemplos comuns.</span><span class="sxs-lookup"><span data-stu-id="71b87-124">The following are some common examples.</span></span>

<span data-ttu-id="71b87-125">Obter entradas de log dessa data/hora até o momento presente:</span><span class="sxs-lookup"><span data-stu-id="71b87-125">Get log entries from this time/date to present:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="71b87-126">Obter entradas de log em um intervalo de data/hora:</span><span class="sxs-lookup"><span data-stu-id="71b87-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="71b87-127">Obter entradas de log de um grupo de recursos específico:</span><span class="sxs-lookup"><span data-stu-id="71b87-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="71b87-128">Obter entradas de log de um provedor de recursos específico um intervalo de data/hora:</span><span class="sxs-lookup"><span data-stu-id="71b87-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="71b87-129">Obter todas as entradas de log com um autor de chamadas específico:</span><span class="sxs-lookup"><span data-stu-id="71b87-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="71b87-130">O comando a seguir recupera os últimos 1000 eventos do log de atividade:</span><span class="sxs-lookup"><span data-stu-id="71b87-130">The following command retrieves the last 1000 events from the activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="71b87-131">`Get-AzureRmLog` dá suporte a muitos outros parâmetros.</span><span class="sxs-lookup"><span data-stu-id="71b87-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="71b87-132">Para saber mais, consulte a referência `Get-AzureRmLog` .</span><span class="sxs-lookup"><span data-stu-id="71b87-132">See the `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="71b87-133">`Get-AzureRmLog` fornece apenas 15 dias de histórico.</span><span class="sxs-lookup"><span data-stu-id="71b87-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="71b87-134">Usar o parâmetro **-MaxEvents** permite consultar os últimos N eventos, além de 15 dias.</span><span class="sxs-lookup"><span data-stu-id="71b87-134">Using the **-MaxEvents** parameter allows you to query the last N events, beyond 15 days.</span></span> <span data-ttu-id="71b87-135">Para eventos de acesso que ocorreram há mais 15 dias, use a API REST ou o SDK (exemplo em C# usando o SDK).</span><span class="sxs-lookup"><span data-stu-id="71b87-135">To access events older than 15 days, use the REST API or SDK (C# sample using the SDK).</span></span> <span data-ttu-id="71b87-136">Se você não incluir **StartTime**, o valor padrão será **EndTime** menos uma hora.</span><span class="sxs-lookup"><span data-stu-id="71b87-136">If you do not include **StartTime**, then the default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="71b87-137">Se você não incluir **EndTime**, o valor padrão será a hora atual.</span><span class="sxs-lookup"><span data-stu-id="71b87-137">If you do not include **EndTime**, then the default value is current time.</span></span> <span data-ttu-id="71b87-138">Todas as horas estão no padrão UTC.</span><span class="sxs-lookup"><span data-stu-id="71b87-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="71b87-139">Recuperar o histórico de alertas</span><span class="sxs-lookup"><span data-stu-id="71b87-139">Retrieve alerts history</span></span>
<span data-ttu-id="71b87-140">Para ver todos os eventos de alerta, você pode consultar os logs do Azure Resource Manager usando os exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="71b87-140">To view all alert events, you can query the Azure Resource Manager logs using the following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="71b87-141">Para ver o histórico de uma regra de alerta específica, você pode usar o cmdlet `Get-AzureRmAlertHistory` , passando a ID de recurso da regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="71b87-141">To view the history for a specific alert rule, you can use the `Get-AzureRmAlertHistory` cmdlet, passing in the resource ID of the alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="71b87-142">O cmdlet `Get-AzureRmAlertHistory` dá suporte a vários parâmetros.</span><span class="sxs-lookup"><span data-stu-id="71b87-142">The `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="71b87-143">Para saber mais, consulte [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="71b87-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="71b87-144">Recuperar informações sobre regras de alerta</span><span class="sxs-lookup"><span data-stu-id="71b87-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="71b87-145">Todos os comandos a seguir atuam em um grupo de recursos denominado "montest".</span><span class="sxs-lookup"><span data-stu-id="71b87-145">All of the following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="71b87-146">Exibir todas as propriedades da regra de alerta:</span><span class="sxs-lookup"><span data-stu-id="71b87-146">View all the properties of the alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="71b87-147">Recuperar todos os alertas de um grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="71b87-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="71b87-148">Recuperar todas as regras de alerta definidas para um recurso de destino.</span><span class="sxs-lookup"><span data-stu-id="71b87-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="71b87-149">Por exemplo, todas as regras de alerta definidas em uma VM.</span><span class="sxs-lookup"><span data-stu-id="71b87-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="71b87-150">`Get-AzureRmAlertRule` dá suporte a outros parâmetros.</span><span class="sxs-lookup"><span data-stu-id="71b87-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="71b87-151">Consulte [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="71b87-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="71b87-152">Criar alertas de métricas</span><span class="sxs-lookup"><span data-stu-id="71b87-152">Create metric alerts</span></span>
<span data-ttu-id="71b87-153">Você pode usar o cmdlet `Add-AlertRule` para criar, atualizar ou desabilitar uma regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="71b87-153">You can use the `Add-AlertRule` cmdlet to create, update or disable an alert rule.</span></span>

<span data-ttu-id="71b87-154">Você pode criar propriedades de email e webhook usando `New-AzureRmAlertRuleEmail` e `New-AzureRmAlertRuleWebhook`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="71b87-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="71b87-155">No cmdlet da regra de alerta, atribua como ações para a propriedade **Actions** da regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="71b87-155">In the Alert rule cmdlet, assign these as actions to the **Actions** property of the Alert Rule.</span></span>

<span data-ttu-id="71b87-156">A tabela a seguir descreve os parâmetros e valores usados para criar um alerta usando uma métrica.</span><span class="sxs-lookup"><span data-stu-id="71b87-156">The following table describes the parameters and values used to create an alert using a metric.</span></span>

| <span data-ttu-id="71b87-157">parâmetro</span><span class="sxs-lookup"><span data-stu-id="71b87-157">parameter</span></span> | <span data-ttu-id="71b87-158">value</span><span class="sxs-lookup"><span data-stu-id="71b87-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="71b87-159">Nome</span><span class="sxs-lookup"><span data-stu-id="71b87-159">Name</span></span> |<span data-ttu-id="71b87-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="71b87-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="71b87-161">Local desta regra de alerta</span><span class="sxs-lookup"><span data-stu-id="71b87-161">Location of this alert rule</span></span> |<span data-ttu-id="71b87-162">Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="71b87-162">East US</span></span> |
| <span data-ttu-id="71b87-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="71b87-163">ResourceGroup</span></span> |<span data-ttu-id="71b87-164">montest</span><span class="sxs-lookup"><span data-stu-id="71b87-164">montest</span></span> |
| <span data-ttu-id="71b87-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="71b87-165">TargetResourceId</span></span> |<span data-ttu-id="71b87-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="71b87-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="71b87-167">MetricName do alerta que é criado</span><span class="sxs-lookup"><span data-stu-id="71b87-167">MetricName of the alert that is created</span></span> |<span data-ttu-id="71b87-168">\PhysicalDisk ( total) \Disk gravações/s. Consulte o `Get-MetricDefinitions` sobre como recuperar os nomes de métrica exatos do cmdlet</span><span class="sxs-lookup"><span data-stu-id="71b87-168">\PhysicalDisk(_Total)\Disk Writes/sec. See the `Get-MetricDefinitions` cmdlet about how to retrieve the exact metric names</span></span> |
| <span data-ttu-id="71b87-169">operator</span><span class="sxs-lookup"><span data-stu-id="71b87-169">operator</span></span> |<span data-ttu-id="71b87-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="71b87-170">GreaterThan</span></span> |
| <span data-ttu-id="71b87-171">Valor de limite (contagem/s para esta métrica)</span><span class="sxs-lookup"><span data-stu-id="71b87-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="71b87-172">1</span><span class="sxs-lookup"><span data-stu-id="71b87-172">1</span></span> |
| <span data-ttu-id="71b87-173">WindowSize (formato hh:mm:ss)</span><span class="sxs-lookup"><span data-stu-id="71b87-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="71b87-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="71b87-174">00:05:00</span></span> |
| <span data-ttu-id="71b87-175">agregador (estatística da métrica, que usa a contagem Média, nesse caso)</span><span class="sxs-lookup"><span data-stu-id="71b87-175">aggregator (statistic of the metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="71b87-176">Média</span><span class="sxs-lookup"><span data-stu-id="71b87-176">Average</span></span> |
| <span data-ttu-id="71b87-177">emails personalizados (matriz de cadeia de caracteres)</span><span class="sxs-lookup"><span data-stu-id="71b87-177">custom emails (string array)</span></span> |<span data-ttu-id="71b87-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="71b87-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="71b87-179">enviar email a proprietários, colaboradores e leitores</span><span class="sxs-lookup"><span data-stu-id="71b87-179">send email to owners, contributors and readers</span></span> |<span data-ttu-id="71b87-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="71b87-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="71b87-181">Ação Criar um email</span><span class="sxs-lookup"><span data-stu-id="71b87-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="71b87-182">Ação Criar um webhook</span><span class="sxs-lookup"><span data-stu-id="71b87-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="71b87-183">Criar a regra de alerta na métrica de % de CPU em uma VM clássica</span><span class="sxs-lookup"><span data-stu-id="71b87-183">Create the alert rule on the CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="71b87-184">Recuperar a regra de alerta</span><span class="sxs-lookup"><span data-stu-id="71b87-184">Retrieve the alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="71b87-185">O cmdlet de alerta Add também atualizará a regra se já existir uma regra de alerta para as propriedades determinadas.</span><span class="sxs-lookup"><span data-stu-id="71b87-185">The Add alert cmdlet also updates the rule if an alert rule already exists for the given properties.</span></span> <span data-ttu-id="71b87-186">Para desabilitar uma regra de alerta, inclua o parâmetro **- DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="71b87-186">To disable an alert rule, include the parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="71b87-187">Obter uma lista das métricas disponíveis para alertas</span><span class="sxs-lookup"><span data-stu-id="71b87-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="71b87-188">Você pode usar o cmdlet `Get-AzureRmMetricDefinition` para exibir a lista de todas as métricas para um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="71b87-188">You can use the `Get-AzureRmMetricDefinition` cmdlet to view the list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="71b87-189">O exemplo a seguir gera uma tabela com o nome de métrica e sua unidade.</span><span class="sxs-lookup"><span data-stu-id="71b87-189">The following example generates a table with the metric Name and the Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="71b87-190">Uma lista completa das opções disponíveis para `Get-AzureRmMetricDefinition` está disponível em [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="71b87-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="71b87-191">Criar e gerenciar configurações de Autoescala</span><span class="sxs-lookup"><span data-stu-id="71b87-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="71b87-192">Um recurso, assim como um aplicativo Web, VM, serviço de nuvem ou conjunto de dimensionamento de máquinas virtuais, pode ter apenas uma configuração de autoescala definida para ele.</span><span class="sxs-lookup"><span data-stu-id="71b87-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="71b87-193">No entanto, cada configuração de autoescala pode ter vários perfis.</span><span class="sxs-lookup"><span data-stu-id="71b87-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="71b87-194">Por exemplo, um para um perfil de escala baseada em desempenho e outro para um perfil baseado em agendamento.</span><span class="sxs-lookup"><span data-stu-id="71b87-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="71b87-195">Cada perfil pode ter várias regras configuradas nele.</span><span class="sxs-lookup"><span data-stu-id="71b87-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="71b87-196">Para obter mais informações sobre Dimensionamento Automático, confira [Como fazer o dimensionamento automático de um aplicativo](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="71b87-196">For more information about Autoscale, see [How to Autoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="71b87-197">Estas são as etapas que usaremos:</span><span class="sxs-lookup"><span data-stu-id="71b87-197">Here are the steps we will use:</span></span>

1. <span data-ttu-id="71b87-198">Criar regra(s).</span><span class="sxs-lookup"><span data-stu-id="71b87-198">Create rule(s).</span></span>
2. <span data-ttu-id="71b87-199">Crie perfis mapeando as regras que você criou anteriormente para os perfis.</span><span class="sxs-lookup"><span data-stu-id="71b87-199">Create profile(s) mapping the rules that you created previously to the profiles.</span></span>
3. <span data-ttu-id="71b87-200">Opcional: criar notificações de autoescala configurando propriedades de webhook e email.</span><span class="sxs-lookup"><span data-stu-id="71b87-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="71b87-201">Crie uma configuração de autoescala com um nome do recurso de destino mapeando os perfis e notificações que você criou nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="71b87-201">Create an autoscale setting with a name on the target resource by mapping the profiles and notifications that you created in the previous steps.</span></span>

<span data-ttu-id="71b87-202">Os exemplos a seguir mostram como você pode criar uma configuração de autoescala para um conjunto de dimensionamento de máquinas virtuais definido para um sistema operacional Windows usando a métrica de uso da CPU.</span><span class="sxs-lookup"><span data-stu-id="71b87-202">The following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using the CPU utilization metric.</span></span>

<span data-ttu-id="71b87-203">Primeiro, crie uma regra para expansão, com um aumento de contagem de instâncias.</span><span class="sxs-lookup"><span data-stu-id="71b87-203">First, create a rule to scale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="71b87-204">Em seguida, crie uma regra para expansão, com uma redução da contagem de instâncias.</span><span class="sxs-lookup"><span data-stu-id="71b87-204">Next, create a rule to scale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="71b87-205">Depois, crie um perfil para as regras.</span><span class="sxs-lookup"><span data-stu-id="71b87-205">Then, create a profile for the rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="71b87-206">Crie uma propriedade de webhook.</span><span class="sxs-lookup"><span data-stu-id="71b87-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="71b87-207">Crie a propriedade de notificação para a configuração de autoescala, incluindo o email e o webhook que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="71b87-207">Create the notification property for the autoscale setting, including email and the webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="71b87-208">Por fim, crie a configuração de autoescala para adicionar o perfil que você criou acima.</span><span class="sxs-lookup"><span data-stu-id="71b87-208">Finally, create the autoscale setting to add the profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="71b87-209">Para obter mais informações sobre como gerenciar configurações de Dimensionamento Automático, confira [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="71b87-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="71b87-210">Histórico de Autoescala</span><span class="sxs-lookup"><span data-stu-id="71b87-210">Autoscale history</span></span>
<span data-ttu-id="71b87-211">O exemplo a seguir mostra como você pode exibir eventos recentes de autoescala e alertas.</span><span class="sxs-lookup"><span data-stu-id="71b87-211">The following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="71b87-212">Use a pesquisa do log de atividades para exibir o histórico de autoescala.</span><span class="sxs-lookup"><span data-stu-id="71b87-212">Use the activity log search to view the autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="71b87-213">Você pode usar o cmdlet `Get-AzureRmAutoScaleHistory` para recuperar o histórico de Dimensionamento Automático.</span><span class="sxs-lookup"><span data-stu-id="71b87-213">You can use the `Get-AzureRmAutoScaleHistory` cmdlet to retrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="71b87-214">Para obter mais informações, confira [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="71b87-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="71b87-215">Exibir os detalhes de uma configuração de autoescala</span><span class="sxs-lookup"><span data-stu-id="71b87-215">View details for an autoscale setting</span></span>
<span data-ttu-id="71b87-216">Você pode usar o cmdlet `Get-Autoscalesetting` para recuperar mais informações sobre a configuração de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="71b87-216">You can use the `Get-Autoscalesetting` cmdlet to retrieve more information about the autoscale setting.</span></span>

<span data-ttu-id="71b87-217">O exemplo a seguir mostra detalhes de todas as configurações de autoescala no grupo de recursos "myrg1".</span><span class="sxs-lookup"><span data-stu-id="71b87-217">The following example shows details about all autoscale settings in the resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="71b87-218">O exemplo a seguir mostra detalhes sobre todas as configurações de autoescala do grupo de recursos "myrg1" e, especificamente, a configuração de autoescala chamada "MyScaleVMSSSetting".</span><span class="sxs-lookup"><span data-stu-id="71b87-218">The following example shows details about all autoscale settings in the resource group 'myrg1' and specifically the autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="71b87-219">Remover uma configuração de autoescala</span><span class="sxs-lookup"><span data-stu-id="71b87-219">Remove an autoscale setting</span></span>
<span data-ttu-id="71b87-220">Você pode usar o cmdlet `Remove-Autoscalesetting` para excluir uma configuração de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="71b87-220">You can use the `Remove-Autoscalesetting` cmdlet to delete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="71b87-221">Gerenciar perfis de log para logs de atividade</span><span class="sxs-lookup"><span data-stu-id="71b87-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="71b87-222">Você pode criar um *perfil de log* e exportar dados de logs de atividade para uma conta de armazenamento e pode configurar retenção de dados para ele.</span><span class="sxs-lookup"><span data-stu-id="71b87-222">You can create a *log profile* and export data from your activity log to a storage account and you can configure data retention for it.</span></span> <span data-ttu-id="71b87-223">Você também pode transmitir os dados para seu Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="71b87-223">Optionally, you can also stream the data to your Event Hub.</span></span> <span data-ttu-id="71b87-224">Observe que no momento esse recurso está em Preview e você só pode criar um perfil de log por assinatura.</span><span class="sxs-lookup"><span data-stu-id="71b87-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="71b87-225">Você pode usar os cmdlets a seguir com sua assinatura atual para criar e gerenciar perfis de log.</span><span class="sxs-lookup"><span data-stu-id="71b87-225">You can use the following cmdlets with your current subscription to create and manage log profiles.</span></span> <span data-ttu-id="71b87-226">Você também pode escolher uma assinatura específica.</span><span class="sxs-lookup"><span data-stu-id="71b87-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="71b87-227">Embora o PowerShell selecione a assinatura atual por padrão, você pode alterar isso usando `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="71b87-227">Although PowerShell defaults to the current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="71b87-228">Você pode configurar logs de atividade para encaminhar dados para qualquer conta de armazenamento ou Hub de eventos dentro dessa assinatura.</span><span class="sxs-lookup"><span data-stu-id="71b87-228">You can configure activity log to route data to any storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="71b87-229">Os dados são gravados como arquivos de blob no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="71b87-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="71b87-230">Obter um perfil de log</span><span class="sxs-lookup"><span data-stu-id="71b87-230">Get a log profile</span></span>
<span data-ttu-id="71b87-231">Para buscar os perfis de log existentes, use o cmdlet `Get-AzureRmLogProfile` .</span><span class="sxs-lookup"><span data-stu-id="71b87-231">To fetch your existing log profiles, use the `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="71b87-232">Adicionar um perfil de log sem retenção de dados</span><span class="sxs-lookup"><span data-stu-id="71b87-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="71b87-233">Remover um perfil de log</span><span class="sxs-lookup"><span data-stu-id="71b87-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="71b87-234">Adicionar um perfil de log com retenção de dados</span><span class="sxs-lookup"><span data-stu-id="71b87-234">Add a log profile with data retention</span></span>
<span data-ttu-id="71b87-235">Você pode especificar a propriedade **-RetentionInDays** com o número de dias, como um inteiro positivo, em que os dados são mantidos.</span><span class="sxs-lookup"><span data-stu-id="71b87-235">You can specify the **-RetentionInDays** property with the number of days, as a positive integer, where the data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="71b87-236">Adicionar perfil de log com retenção e Hub de eventos</span><span class="sxs-lookup"><span data-stu-id="71b87-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="71b87-237">Além de encaminhar seus dados para a conta de armazenamento, você também pode transmiti-los para um Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="71b87-237">In addition to routing your data to storage account, you can also stream it to an Event Hub.</span></span> <span data-ttu-id="71b87-238">Observe que nessa versão de teste a configuração da conta de armazenamento é obrigatória, mas a configuração do Hub de eventos é opcional.</span><span class="sxs-lookup"><span data-stu-id="71b87-238">Note that in this preview release and the storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="71b87-239">Configurar logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="71b87-239">Configure diagnostics logs</span></span>
<span data-ttu-id="71b87-240">Muitos serviços do Azure fornecem logs e telemetria adicionais que podem ser configurados para salvar dados em sua conta de Armazenamento do Azure, enviar para Hubs de Eventos e/ou enviar para um espaço de trabalho de Log Analytics do OMS.</span><span class="sxs-lookup"><span data-stu-id="71b87-240">Many Azure services provide additional logs and telemetry that can be configured to save data in your Azure Storage account, send to Event Hubs, and/or sent to an OMS Log Analytics workspace.</span></span> <span data-ttu-id="71b87-241">Essa operação só pode ser executada no nível dos recursos e a conta de armazenamento ou hub de eventos deve estar na mesma região que o recurso de destino em que a configuração de diagnóstico está definida.</span><span class="sxs-lookup"><span data-stu-id="71b87-241">That operation can only be performed at a resource level and the storage account or event hub should be present in the same region as the target resource where the diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="71b87-242">Obter configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="71b87-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="71b87-243">Desabilitar configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="71b87-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="71b87-244">Habilitar configuração de diagnóstico sem retenção</span><span class="sxs-lookup"><span data-stu-id="71b87-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="71b87-245">Habilitar configuração de diagnóstico com retenção</span><span class="sxs-lookup"><span data-stu-id="71b87-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="71b87-246">Habilitar configuração de diagnóstico com retenção para uma categoria de log específica</span><span class="sxs-lookup"><span data-stu-id="71b87-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="71b87-247">Habilitar configuração de diagnóstico para Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="71b87-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="71b87-248">Habilitar configuração de diagnóstico para OMS</span><span class="sxs-lookup"><span data-stu-id="71b87-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
