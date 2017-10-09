---
title: "exemplos de início rápido do PowerShell do Monitor aaaAzure. | Microsoft Docs"
description: "Use o PowerShell tooaccess recursos de Monitor do Azure, como o dimensionamento automático, alertas, webhooks e pesquisa de logs de atividade."
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
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="c7131-104">Exemplos de início rápido do PowerShell do Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="c7131-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="c7131-105">Este mostra artigo exemplo toohelp de comandos do PowerShell acessar os recursos do Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7131-105">This article shows you sample PowerShell commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="c7131-106">Monitor do Azure permite que notificações de alerta serviços de nuvem, máquinas virtuais e aplicativos Web e toosend tooAutoScale ou chamada web URLs com base nos valores de dados de telemetria configurado.</span><span class="sxs-lookup"><span data-stu-id="c7131-106">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="c7131-107">Monitor do Azure é Olá novo nome para o que era chamado de "Azure Insights" até 25 de setembro de 2016.</span><span class="sxs-lookup"><span data-stu-id="c7131-107">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="c7131-108">No entanto, Olá namespaces e, portanto, Olá ainda os comandos a seguir contêm insights"Olá".</span><span class="sxs-lookup"><span data-stu-id="c7131-108">However, hello namespaces and thus hello following commands still contain hello "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="c7131-109">Configurar o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7131-109">Set up PowerShell</span></span>
<span data-ttu-id="c7131-110">Se você ainda não fez isso, configure toorun PowerShell em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c7131-110">If you haven't already, set up PowerShell toorun on your computer.</span></span> <span data-ttu-id="c7131-111">Para obter mais informações, consulte [como tooInstall e configurar o PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c7131-111">For more information, see [How tooInstall and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="c7131-112">Exemplos neste artigo</span><span class="sxs-lookup"><span data-stu-id="c7131-112">Examples in this article</span></span>
<span data-ttu-id="c7131-113">Olá artigo Olá ilustram como você pode usar os cmdlets do Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7131-113">hello examples in hello article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="c7131-114">Você também pode analisar toda a lista de cmdlets do PowerShell do Azure Monitor no hello [Cmdlets do Monitor do Azure (Insights)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7131-114">You can also review hello entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="c7131-115">Conectar-se e usar assinaturas</span><span class="sxs-lookup"><span data-stu-id="c7131-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="c7131-116">Primeiro, faça logon em tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7131-116">First, log in tooyour Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="c7131-117">Isso exige que você toosign no.</span><span class="sxs-lookup"><span data-stu-id="c7131-117">This requires you toosign in.</span></span> <span data-ttu-id="c7131-118">Quando fizer isso, você verá sua Conta, sua TenantID e ID da Assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="c7131-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="c7131-119">Todos os Olá cmdlets do Azure funcionam no contexto de saudação da sua assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="c7131-119">All hello Azure cmdlets work in hello context of your default subscription.</span></span> <span data-ttu-id="c7131-120">lista de saudação tooview de assinaturas que você tem acesso a, use Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="c7131-120">tooview hello list of subscriptions you have access to, use hello following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="c7131-121">toochange seu trabalho contexto tooa assinatura diferente, use Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="c7131-121">toochange your working context tooa different subscription, use hello following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="c7131-122">Recuperar o log de atividade para uma assinatura</span><span class="sxs-lookup"><span data-stu-id="c7131-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="c7131-123">Saudação de uso `Get-AzureRmLog` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c7131-123">Use hello `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="c7131-124">Olá seguem alguns exemplos comuns.</span><span class="sxs-lookup"><span data-stu-id="c7131-124">hello following are some common examples.</span></span>

<span data-ttu-id="c7131-125">Obter entradas de log do toopresent data/hora:</span><span class="sxs-lookup"><span data-stu-id="c7131-125">Get log entries from this time/date toopresent:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="c7131-126">Obter entradas de log em um intervalo de data/hora:</span><span class="sxs-lookup"><span data-stu-id="c7131-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="c7131-127">Obter entradas de log de um grupo de recursos específico:</span><span class="sxs-lookup"><span data-stu-id="c7131-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="c7131-128">Obter entradas de log de um provedor de recursos específico um intervalo de data/hora:</span><span class="sxs-lookup"><span data-stu-id="c7131-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="c7131-129">Obter todas as entradas de log com um autor de chamadas específico:</span><span class="sxs-lookup"><span data-stu-id="c7131-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="c7131-130">Olá recupera Olá últimas 1000 eventos do log de atividades de saudação do comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7131-130">hello following command retrieves hello last 1000 events from hello activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="c7131-131">`Get-AzureRmLog` dá suporte a muitos outros parâmetros.</span><span class="sxs-lookup"><span data-stu-id="c7131-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="c7131-132">Consulte Olá `Get-AzureRmLog` referência para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="c7131-132">See hello `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="c7131-133">`Get-AzureRmLog` fornece apenas 15 dias de histórico.</span><span class="sxs-lookup"><span data-stu-id="c7131-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="c7131-134">Usando Olá **- MaxEvents** parâmetro permite que você tooquery Olá últimos N eventos, além de 15 dias.</span><span class="sxs-lookup"><span data-stu-id="c7131-134">Using hello **-MaxEvents** parameter allows you tooquery hello last N events, beyond 15 days.</span></span> <span data-ttu-id="c7131-135">tooaccess eventos com mais de 15 dias, use Olá API REST ou o SDK (exemplo em c# usando Olá SDK).</span><span class="sxs-lookup"><span data-stu-id="c7131-135">tooaccess events older than 15 days, use hello REST API or SDK (C# sample using hello SDK).</span></span> <span data-ttu-id="c7131-136">Se você não incluir **StartTime**, e em seguida, o valor padrão de saudação é **EndTime** menos uma hora.</span><span class="sxs-lookup"><span data-stu-id="c7131-136">If you do not include **StartTime**, then hello default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="c7131-137">Se você não incluir **EndTime**, e em seguida, o valor padrão de saudação é a hora atual.</span><span class="sxs-lookup"><span data-stu-id="c7131-137">If you do not include **EndTime**, then hello default value is current time.</span></span> <span data-ttu-id="c7131-138">Todas as horas estão no padrão UTC.</span><span class="sxs-lookup"><span data-stu-id="c7131-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="c7131-139">Recuperar o histórico de alertas</span><span class="sxs-lookup"><span data-stu-id="c7131-139">Retrieve alerts history</span></span>
<span data-ttu-id="c7131-140">tooview todos os eventos de alerta, você pode consultar Olá logs do Azure Resource Manager usando Olá exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="c7131-140">tooview all alert events, you can query hello Azure Resource Manager logs using hello following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="c7131-141">histórico de saudação tooview para um alerta específico de regra, você pode usar o hello `Get-AzureRmAlertHistory` cmdlet, passando Olá recurso ID da regra de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7131-141">tooview hello history for a specific alert rule, you can use hello `Get-AzureRmAlertHistory` cmdlet, passing in hello resource ID of hello alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="c7131-142">Olá `Get-AzureRmAlertHistory` cmdlet oferece suporte a vários parâmetros.</span><span class="sxs-lookup"><span data-stu-id="c7131-142">hello `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="c7131-143">Para saber mais, consulte [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7131-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="c7131-144">Recuperar informações sobre regras de alerta</span><span class="sxs-lookup"><span data-stu-id="c7131-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="c7131-145">Todos os comandos a seguir de saudação agir em um grupo de recursos denominado "montest".</span><span class="sxs-lookup"><span data-stu-id="c7131-145">All of hello following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="c7131-146">Exiba todas as propriedades de saudação da regra de alerta de saudação:</span><span class="sxs-lookup"><span data-stu-id="c7131-146">View all hello properties of hello alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="c7131-147">Recuperar todos os alertas de um grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="c7131-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="c7131-148">Recuperar todas as regras de alerta definidas para um recurso de destino.</span><span class="sxs-lookup"><span data-stu-id="c7131-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="c7131-149">Por exemplo, todas as regras de alerta definidas em uma VM.</span><span class="sxs-lookup"><span data-stu-id="c7131-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="c7131-150">`Get-AzureRmAlertRule` dá suporte a outros parâmetros.</span><span class="sxs-lookup"><span data-stu-id="c7131-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="c7131-151">Consulte [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="c7131-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="c7131-152">Criar alertas de métricas</span><span class="sxs-lookup"><span data-stu-id="c7131-152">Create metric alerts</span></span>
<span data-ttu-id="c7131-153">Você pode usar o hello `Add-AlertRule` toocreate cmdlet, atualizar ou desabilitar uma regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="c7131-153">You can use hello `Add-AlertRule` cmdlet toocreate, update or disable an alert rule.</span></span>

<span data-ttu-id="c7131-154">Você pode criar propriedades de email e webhook usando `New-AzureRmAlertRuleEmail` e `New-AzureRmAlertRuleWebhook`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="c7131-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="c7131-155">No cmdlet de regra de alerta hello, atribuí-las como ações toohello **ações** propriedade de regra de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7131-155">In hello Alert rule cmdlet, assign these as actions toohello **Actions** property of hello Alert Rule.</span></span>

<span data-ttu-id="c7131-156">Olá, a tabela a seguir descreve os parâmetros de saudação e valores toocreate usado um alerta usando uma métrica.</span><span class="sxs-lookup"><span data-stu-id="c7131-156">hello following table describes hello parameters and values used toocreate an alert using a metric.</span></span>

| <span data-ttu-id="c7131-157">parâmetro</span><span class="sxs-lookup"><span data-stu-id="c7131-157">parameter</span></span> | <span data-ttu-id="c7131-158">value</span><span class="sxs-lookup"><span data-stu-id="c7131-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="c7131-159">Nome</span><span class="sxs-lookup"><span data-stu-id="c7131-159">Name</span></span> |<span data-ttu-id="c7131-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="c7131-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="c7131-161">Local desta regra de alerta</span><span class="sxs-lookup"><span data-stu-id="c7131-161">Location of this alert rule</span></span> |<span data-ttu-id="c7131-162">Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="c7131-162">East US</span></span> |
| <span data-ttu-id="c7131-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c7131-163">ResourceGroup</span></span> |<span data-ttu-id="c7131-164">montest</span><span class="sxs-lookup"><span data-stu-id="c7131-164">montest</span></span> |
| <span data-ttu-id="c7131-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="c7131-165">TargetResourceId</span></span> |<span data-ttu-id="c7131-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="c7131-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="c7131-167">MetricName de alerta de saudação que é criada</span><span class="sxs-lookup"><span data-stu-id="c7131-167">MetricName of hello alert that is created</span></span> |<span data-ttu-id="c7131-168">\PhysicalDisk ( total) \Disk gravações/s. Consulte Olá `Get-MetricDefinitions` sobre como tooretrieve Olá nomes de métrica exatos do cmdlet</span><span class="sxs-lookup"><span data-stu-id="c7131-168">\PhysicalDisk(_Total)\Disk Writes/sec. See hello `Get-MetricDefinitions` cmdlet about how tooretrieve hello exact metric names</span></span> |
| <span data-ttu-id="c7131-169">operator</span><span class="sxs-lookup"><span data-stu-id="c7131-169">operator</span></span> |<span data-ttu-id="c7131-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="c7131-170">GreaterThan</span></span> |
| <span data-ttu-id="c7131-171">Valor de limite (contagem/s para esta métrica)</span><span class="sxs-lookup"><span data-stu-id="c7131-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="c7131-172">1</span><span class="sxs-lookup"><span data-stu-id="c7131-172">1</span></span> |
| <span data-ttu-id="c7131-173">WindowSize (formato hh:mm:ss)</span><span class="sxs-lookup"><span data-stu-id="c7131-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="c7131-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="c7131-174">00:05:00</span></span> |
| <span data-ttu-id="c7131-175">agregador (estatística da métrica hello, que usa a média de contagem, nesse caso)</span><span class="sxs-lookup"><span data-stu-id="c7131-175">aggregator (statistic of hello metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="c7131-176">Média</span><span class="sxs-lookup"><span data-stu-id="c7131-176">Average</span></span> |
| <span data-ttu-id="c7131-177">emails personalizados (matriz de cadeia de caracteres)</span><span class="sxs-lookup"><span data-stu-id="c7131-177">custom emails (string array)</span></span> |<span data-ttu-id="c7131-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="c7131-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="c7131-179">Enviar email tooowners, colaboradores e leitores</span><span class="sxs-lookup"><span data-stu-id="c7131-179">send email tooowners, contributors and readers</span></span> |<span data-ttu-id="c7131-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="c7131-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="c7131-181">Ação Criar um email</span><span class="sxs-lookup"><span data-stu-id="c7131-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="c7131-182">Ação Criar um webhook</span><span class="sxs-lookup"><span data-stu-id="c7131-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="c7131-183">Criar regra de alerta de saudação na métrica de % de CPU de saudação em uma VM clássica</span><span class="sxs-lookup"><span data-stu-id="c7131-183">Create hello alert rule on hello CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="c7131-184">Recuperar a regra de alerta de saudação</span><span class="sxs-lookup"><span data-stu-id="c7131-184">Retrieve hello alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="c7131-185">Olá adicionar alerta cmdlet também atualiza a regra Olá se já existe uma regra de alerta para Olá fornecido propriedades.</span><span class="sxs-lookup"><span data-stu-id="c7131-185">hello Add alert cmdlet also updates hello rule if an alert rule already exists for hello given properties.</span></span> <span data-ttu-id="c7131-186">toodisable uma regra de alerta, inclua o parâmetro hello **- DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="c7131-186">toodisable an alert rule, include hello parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="c7131-187">Obter uma lista das métricas disponíveis para alertas</span><span class="sxs-lookup"><span data-stu-id="c7131-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="c7131-188">Você pode usar o hello `Get-AzureRmMetricDefinition` lista de saudação do cmdlet tooview de todas as métricas para um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="c7131-188">You can use hello `Get-AzureRmMetricDefinition` cmdlet tooview hello list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="c7131-189">Olá exemplo a seguir gera uma tabela com o nome de métrica de saudação e Olá unidade para ele.</span><span class="sxs-lookup"><span data-stu-id="c7131-189">hello following example generates a table with hello metric Name and hello Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="c7131-190">Uma lista completa das opções disponíveis para `Get-AzureRmMetricDefinition` está disponível em [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7131-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="c7131-191">Criar e gerenciar configurações de Autoescala</span><span class="sxs-lookup"><span data-stu-id="c7131-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="c7131-192">Um recurso, assim como um aplicativo Web, VM, serviço de nuvem ou conjunto de dimensionamento de máquinas virtuais, pode ter apenas uma configuração de autoescala definida para ele.</span><span class="sxs-lookup"><span data-stu-id="c7131-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="c7131-193">No entanto, cada configuração de autoescala pode ter vários perfis.</span><span class="sxs-lookup"><span data-stu-id="c7131-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="c7131-194">Por exemplo, um para um perfil de escala baseada em desempenho e outro para um perfil baseado em agendamento.</span><span class="sxs-lookup"><span data-stu-id="c7131-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="c7131-195">Cada perfil pode ter várias regras configuradas nele.</span><span class="sxs-lookup"><span data-stu-id="c7131-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="c7131-196">Para obter mais informações sobre o dimensionamento automático, consulte [como um aplicativo de tooAutoscale](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="c7131-196">For more information about Autoscale, see [How tooAutoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="c7131-197">Aqui estão as etapas Olá que usaremos:</span><span class="sxs-lookup"><span data-stu-id="c7131-197">Here are hello steps we will use:</span></span>

1. <span data-ttu-id="c7131-198">Criar regra(s).</span><span class="sxs-lookup"><span data-stu-id="c7131-198">Create rule(s).</span></span>
2. <span data-ttu-id="c7131-199">Criar perfis de saudação do mapeamento de regras que você criou anteriormente toohello perfis.</span><span class="sxs-lookup"><span data-stu-id="c7131-199">Create profile(s) mapping hello rules that you created previously toohello profiles.</span></span>
3. <span data-ttu-id="c7131-200">Opcional: criar notificações de autoescala configurando propriedades de webhook e email.</span><span class="sxs-lookup"><span data-stu-id="c7131-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="c7131-201">Crie uma configuração de AutoEscala com um nome de recurso de destino Olá mapeando perfis hello e notificações que você criou nas etapas anteriores hello.</span><span class="sxs-lookup"><span data-stu-id="c7131-201">Create an autoscale setting with a name on hello target resource by mapping hello profiles and notifications that you created in hello previous steps.</span></span>

<span data-ttu-id="c7131-202">Olá exemplos a seguir mostram como você pode criar uma configuração de AutoEscala para um conjunto de escala de máquina Virtual para um sistema operacional do Windows com base usando a métrica de utilização de CPU de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7131-202">hello following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using hello CPU utilization metric.</span></span>

<span data-ttu-id="c7131-203">Primeiro, crie uma regra tooscale horizontal, com um aumento da contagem de instância.</span><span class="sxs-lookup"><span data-stu-id="c7131-203">First, create a rule tooscale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="c7131-204">Em seguida, crie uma regra tooscale-in com uma redução de contagem de instância.</span><span class="sxs-lookup"><span data-stu-id="c7131-204">Next, create a rule tooscale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="c7131-205">Em seguida, crie um perfil para regras de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7131-205">Then, create a profile for hello rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="c7131-206">Crie uma propriedade de webhook.</span><span class="sxs-lookup"><span data-stu-id="c7131-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="c7131-207">Criar a propriedade de notificação de saudação para configuração de dimensionamento automático hello, incluindo email e Olá webhook que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c7131-207">Create hello notification property for hello autoscale setting, including email and hello webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="c7131-208">Finalmente, crie Olá AutoEscala configuração tooadd Olá perfil criado acima.</span><span class="sxs-lookup"><span data-stu-id="c7131-208">Finally, create hello autoscale setting tooadd hello profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="c7131-209">Para obter mais informações sobre como gerenciar configurações de Dimensionamento Automático, confira [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7131-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="c7131-210">Histórico de Autoescala</span><span class="sxs-lookup"><span data-stu-id="c7131-210">Autoscale history</span></span>
<span data-ttu-id="c7131-211">Olá exemplo a seguir mostra como você pode exibir eventos recentes de dimensionamento automático e o alerta.</span><span class="sxs-lookup"><span data-stu-id="c7131-211">hello following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="c7131-212">Use o hello atividade log pesquisa tooview Olá AutoEscala histórico.</span><span class="sxs-lookup"><span data-stu-id="c7131-212">Use hello activity log search tooview hello autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="c7131-213">Você pode usar o hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve histórico de AutoEscala.</span><span class="sxs-lookup"><span data-stu-id="c7131-213">You can use hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="c7131-214">Para obter mais informações, confira [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7131-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="c7131-215">Exibir os detalhes de uma configuração de autoescala</span><span class="sxs-lookup"><span data-stu-id="c7131-215">View details for an autoscale setting</span></span>
<span data-ttu-id="c7131-216">Você pode usar o hello `Get-Autoscalesetting` tooretrieve cmdlet para obter mais informações sobre a configuração de AutoEscala hello.</span><span class="sxs-lookup"><span data-stu-id="c7131-216">You can use hello `Get-Autoscalesetting` cmdlet tooretrieve more information about hello autoscale setting.</span></span>

<span data-ttu-id="c7131-217">Olá exemplo a seguir mostra detalhes sobre todas as configurações de dimensionamento automático no grupo de recursos de saudação 'myrg1'.</span><span class="sxs-lookup"><span data-stu-id="c7131-217">hello following example shows details about all autoscale settings in hello resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="c7131-218">Olá exemplo a seguir mostra detalhes sobre todas as configurações de dimensionamento automático no grupo de recursos de saudação 'myrg1' e Olá especificamente a configuração de dimensionamento automático denominada 'MyScaleVMSSSetting'.</span><span class="sxs-lookup"><span data-stu-id="c7131-218">hello following example shows details about all autoscale settings in hello resource group 'myrg1' and specifically hello autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="c7131-219">Remover uma configuração de autoescala</span><span class="sxs-lookup"><span data-stu-id="c7131-219">Remove an autoscale setting</span></span>
<span data-ttu-id="c7131-220">Você pode usar o hello `Remove-Autoscalesetting` cmdlet toodelete uma configuração de AutoEscala.</span><span class="sxs-lookup"><span data-stu-id="c7131-220">You can use hello `Remove-Autoscalesetting` cmdlet toodelete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="c7131-221">Gerenciar perfis de log para logs de atividade</span><span class="sxs-lookup"><span data-stu-id="c7131-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="c7131-222">Você pode criar um *log perfil* e exportar dados de sua conta de armazenamento de tooa de log de atividade e você podem configurar a retenção de dados para ele.</span><span class="sxs-lookup"><span data-stu-id="c7131-222">You can create a *log profile* and export data from your activity log tooa storage account and you can configure data retention for it.</span></span> <span data-ttu-id="c7131-223">Opcionalmente, você também pode transmitir Olá dados tooyour Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="c7131-223">Optionally, you can also stream hello data tooyour Event Hub.</span></span> <span data-ttu-id="c7131-224">Observe que no momento esse recurso está em Preview e você só pode criar um perfil de log por assinatura.</span><span class="sxs-lookup"><span data-stu-id="c7131-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="c7131-225">Você pode usar o hello seguintes cmdlets com o toocreate da assinatura atual e gerenciar perfis de log.</span><span class="sxs-lookup"><span data-stu-id="c7131-225">You can use hello following cmdlets with your current subscription toocreate and manage log profiles.</span></span> <span data-ttu-id="c7131-226">Você também pode escolher uma assinatura específica.</span><span class="sxs-lookup"><span data-stu-id="c7131-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="c7131-227">Embora PowerShell padrão é a assinatura atual toohello, você pode alterar sempre que usar `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="c7131-227">Although PowerShell defaults toohello current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="c7131-228">Você pode configurar a conta de armazenamento atividade log tooroute dados tooany ou Hub de eventos dentro dessa assinatura.</span><span class="sxs-lookup"><span data-stu-id="c7131-228">You can configure activity log tooroute data tooany storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="c7131-229">Os dados são gravados como arquivos de blob no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="c7131-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="c7131-230">Obter um perfil de log</span><span class="sxs-lookup"><span data-stu-id="c7131-230">Get a log profile</span></span>
<span data-ttu-id="c7131-231">toofetch seus perfis de log existentes, use Olá `Get-AzureRmLogProfile` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c7131-231">toofetch your existing log profiles, use hello `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="c7131-232">Adicionar um perfil de log sem retenção de dados</span><span class="sxs-lookup"><span data-stu-id="c7131-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="c7131-233">Remover um perfil de log</span><span class="sxs-lookup"><span data-stu-id="c7131-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="c7131-234">Adicionar um perfil de log com retenção de dados</span><span class="sxs-lookup"><span data-stu-id="c7131-234">Add a log profile with data retention</span></span>
<span data-ttu-id="c7131-235">Você pode especificar Olá **- RetentionInDays** propriedade com hello número de dias, como um inteiro positivo, onde os dados de saudação são retidos.</span><span class="sxs-lookup"><span data-stu-id="c7131-235">You can specify hello **-RetentionInDays** property with hello number of days, as a positive integer, where hello data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="c7131-236">Adicionar perfil de log com retenção e Hub de eventos</span><span class="sxs-lookup"><span data-stu-id="c7131-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="c7131-237">Em adição toorouting sua conta de toostorage de dados, você também pode transmitir-tooan Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="c7131-237">In addition toorouting your data toostorage account, you can also stream it tooan Event Hub.</span></span> <span data-ttu-id="c7131-238">Observe que, nesta visualização configuração de conta de armazenamento de versão e hello é obrigatória, mas a configuração do Hub de eventos é opcional.</span><span class="sxs-lookup"><span data-stu-id="c7131-238">Note that in this preview release and hello storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="c7131-239">Configurar logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="c7131-239">Configure diagnostics logs</span></span>
<span data-ttu-id="c7131-240">Muitos serviços do Azure fornecem tooEvent Hubs de envio de logs adicionais e telemetria que pode ser dados toosave configurado em sua conta de armazenamento do Azure, e/ou enviados tooan espaço de trabalho de análise de logs do OMS.</span><span class="sxs-lookup"><span data-stu-id="c7131-240">Many Azure services provide additional logs and telemetry that can be configured toosave data in your Azure Storage account, send tooEvent Hubs, and/or sent tooan OMS Log Analytics workspace.</span></span> <span data-ttu-id="c7131-241">Essa operação só pode ser executada em um nível de recurso e hub de evento ou a conta de armazenamento Olá deve estar presente no hello mesma região que o recurso de destino Olá onde a configuração de diagnóstico de saudação está configurada.</span><span class="sxs-lookup"><span data-stu-id="c7131-241">That operation can only be performed at a resource level and hello storage account or event hub should be present in hello same region as hello target resource where hello diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="c7131-242">Obter configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="c7131-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="c7131-243">Desabilitar configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="c7131-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="c7131-244">Habilitar configuração de diagnóstico sem retenção</span><span class="sxs-lookup"><span data-stu-id="c7131-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="c7131-245">Habilitar configuração de diagnóstico com retenção</span><span class="sxs-lookup"><span data-stu-id="c7131-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="c7131-246">Habilitar configuração de diagnóstico com retenção para uma categoria de log específica</span><span class="sxs-lookup"><span data-stu-id="c7131-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="c7131-247">Habilitar configuração de diagnóstico para Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="c7131-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="c7131-248">Habilitar configuração de diagnóstico para OMS</span><span class="sxs-lookup"><span data-stu-id="c7131-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
