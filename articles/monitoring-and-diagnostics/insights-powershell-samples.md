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
# <a name="azure-monitor-powershell-quick-start-samples"></a>Exemplos de início rápido do PowerShell do Azure Monitor
Este mostra artigo exemplo toohelp de comandos do PowerShell acessar os recursos do Monitor do Azure. Monitor do Azure permite que notificações de alerta serviços de nuvem, máquinas virtuais e aplicativos Web e toosend tooAutoScale ou chamada web URLs com base nos valores de dados de telemetria configurado.

> [!NOTE]
> Monitor do Azure é Olá novo nome para o que era chamado de "Azure Insights" até 25 de setembro de 2016. No entanto, Olá namespaces e, portanto, Olá ainda os comandos a seguir contêm insights"Olá".
> 
> 

## <a name="set-up-powershell"></a>Configurar o PowerShell
Se você ainda não fez isso, configure toorun PowerShell em seu computador. Para obter mais informações, consulte [como tooInstall e configurar o PowerShell](/powershell/azure/overview).

## <a name="examples-in-this-article"></a>Exemplos neste artigo
Olá artigo Olá ilustram como você pode usar os cmdlets do Monitor do Azure. Você também pode analisar toda a lista de cmdlets do PowerShell do Azure Monitor no hello [Cmdlets do Monitor do Azure (Insights)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).

## <a name="sign-in-and-use-subscriptions"></a>Conectar-se e usar assinaturas
Primeiro, faça logon em tooyour assinatura do Azure.

```PowerShell
Login-AzureRmAccount
```

Isso exige que você toosign no. Quando fizer isso, você verá sua Conta, sua TenantID e ID da Assinatura padrão. Todos os Olá cmdlets do Azure funcionam no contexto de saudação da sua assinatura padrão. lista de saudação tooview de assinaturas que você tem acesso a, use Olá comando a seguir.

```PowerShell
Get-AzureRmSubscription
```

toochange seu trabalho contexto tooa assinatura diferente, use Olá comando a seguir.

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a>Recuperar o log de atividade para uma assinatura
Saudação de uso `Get-AzureRmLog` cmdlet.  Olá seguem alguns exemplos comuns.

Obter entradas de log do toopresent data/hora:

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

Obter entradas de log em um intervalo de data/hora:

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

Obter entradas de log de um grupo de recursos específico:

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

Obter entradas de log de um provedor de recursos específico um intervalo de data/hora:

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

Obter todas as entradas de log com um autor de chamadas específico:

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

Olá recupera Olá últimas 1000 eventos do log de atividades de saudação do comando a seguir:

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

`Get-AzureRmLog` dá suporte a muitos outros parâmetros. Consulte Olá `Get-AzureRmLog` referência para obter mais informações.

> [!NOTE]
> `Get-AzureRmLog` fornece apenas 15 dias de histórico. Usando Olá **- MaxEvents** parâmetro permite que você tooquery Olá últimos N eventos, além de 15 dias. tooaccess eventos com mais de 15 dias, use Olá API REST ou o SDK (exemplo em c# usando Olá SDK). Se você não incluir **StartTime**, e em seguida, o valor padrão de saudação é **EndTime** menos uma hora. Se você não incluir **EndTime**, e em seguida, o valor padrão de saudação é a hora atual. Todas as horas estão no padrão UTC.
> 
> 

## <a name="retrieve-alerts-history"></a>Recuperar o histórico de alertas
tooview todos os eventos de alerta, você pode consultar Olá logs do Azure Resource Manager usando Olá exemplos a seguir.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

histórico de saudação tooview para um alerta específico de regra, você pode usar o hello `Get-AzureRmAlertHistory` cmdlet, passando Olá recurso ID da regra de alerta de saudação.

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

Olá `Get-AzureRmAlertHistory` cmdlet oferece suporte a vários parâmetros. Para saber mais, consulte [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).

## <a name="retrieve-information-on-alert-rules"></a>Recuperar informações sobre regras de alerta
Todos os comandos a seguir de saudação agir em um grupo de recursos denominado "montest".

Exiba todas as propriedades de saudação da regra de alerta de saudação:

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

Recuperar todos os alertas de um grupo de recursos:

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

Recuperar todas as regras de alerta definidas para um recurso de destino. Por exemplo, todas as regras de alerta definidas em uma VM.

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

`Get-AzureRmAlertRule` dá suporte a outros parâmetros. Consulte [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) para obter mais informações.

## <a name="create-metric-alerts"></a>Criar alertas de métricas
Você pode usar o hello `Add-AlertRule` toocreate cmdlet, atualizar ou desabilitar uma regra de alerta.

Você pode criar propriedades de email e webhook usando `New-AzureRmAlertRuleEmail` e `New-AzureRmAlertRuleWebhook`, respectivamente. No cmdlet de regra de alerta hello, atribuí-las como ações toohello **ações** propriedade de regra de alerta de saudação.

Olá, a tabela a seguir descreve os parâmetros de saudação e valores toocreate usado um alerta usando uma métrica.

| parâmetro | value |
| --- | --- |
| Nome |simpletestdiskwrite |
| Local desta regra de alerta |Leste dos EUA |
| ResourceGroup |montest |
| TargetResourceId |/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig |
| MetricName de alerta de saudação que é criada |\PhysicalDisk ( total) \Disk gravações/s. Consulte Olá `Get-MetricDefinitions` sobre como tooretrieve Olá nomes de métrica exatos do cmdlet |
| operator |GreaterThan |
| Valor de limite (contagem/s para esta métrica) |1 |
| WindowSize (formato hh:mm:ss) |00:05:00 |
| agregador (estatística da métrica hello, que usa a média de contagem, nesse caso) |Média |
| emails personalizados (matriz de cadeia de caracteres) |'foo@example.com','bar@example.com' |
| Enviar email tooowners, colaboradores e leitores |-SendToServiceOwners |

Ação Criar um email

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

Ação Criar um webhook

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

Criar regra de alerta de saudação na métrica de % de CPU de saudação em uma VM clássica

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

Recuperar a regra de alerta de saudação

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

Olá adicionar alerta cmdlet também atualiza a regra Olá se já existe uma regra de alerta para Olá fornecido propriedades. toodisable uma regra de alerta, inclua o parâmetro hello **- DisableRule**.

## <a name="get-a-list-of-available-metrics-for-alerts"></a>Obter uma lista das métricas disponíveis para alertas
Você pode usar o hello `Get-AzureRmMetricDefinition` lista de saudação do cmdlet tooview de todas as métricas para um recurso específico.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

Olá exemplo a seguir gera uma tabela com o nome de métrica de saudação e Olá unidade para ele.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Uma lista completa das opções disponíveis para `Get-AzureRmMetricDefinition` está disponível em [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).

## <a name="create-and-manage-autoscale-settings"></a>Criar e gerenciar configurações de Autoescala
Um recurso, assim como um aplicativo Web, VM, serviço de nuvem ou conjunto de dimensionamento de máquinas virtuais, pode ter apenas uma configuração de autoescala definida para ele.
No entanto, cada configuração de autoescala pode ter vários perfis. Por exemplo, um para um perfil de escala baseada em desempenho e outro para um perfil baseado em agendamento. Cada perfil pode ter várias regras configuradas nele. Para obter mais informações sobre o dimensionamento automático, consulte [como um aplicativo de tooAutoscale](../cloud-services/cloud-services-how-to-scale.md).

Aqui estão as etapas Olá que usaremos:

1. Criar regra(s).
2. Criar perfis de saudação do mapeamento de regras que você criou anteriormente toohello perfis.
3. Opcional: criar notificações de autoescala configurando propriedades de webhook e email.
4. Crie uma configuração de AutoEscala com um nome de recurso de destino Olá mapeando perfis hello e notificações que você criou nas etapas anteriores hello.

Olá exemplos a seguir mostram como você pode criar uma configuração de AutoEscala para um conjunto de escala de máquina Virtual para um sistema operacional do Windows com base usando a métrica de utilização de CPU de saudação.

Primeiro, crie uma regra tooscale horizontal, com um aumento da contagem de instância.

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

Em seguida, crie uma regra tooscale-in com uma redução de contagem de instância.

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

Em seguida, crie um perfil para regras de saudação.

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

Crie uma propriedade de webhook.

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

Criar a propriedade de notificação de saudação para configuração de dimensionamento automático hello, incluindo email e Olá webhook que você criou anteriormente.

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

Finalmente, crie Olá AutoEscala configuração tooadd Olá perfil criado acima.

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

Para obter mais informações sobre como gerenciar configurações de Dimensionamento Automático, confira [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).

## <a name="autoscale-history"></a>Histórico de Autoescala
Olá exemplo a seguir mostra como você pode exibir eventos recentes de dimensionamento automático e o alerta. Use o hello atividade log pesquisa tooview Olá AutoEscala histórico.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

Você pode usar o hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve histórico de AutoEscala.

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

Para obter mais informações, confira [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).

### <a name="view-details-for-an-autoscale-setting"></a>Exibir os detalhes de uma configuração de autoescala
Você pode usar o hello `Get-Autoscalesetting` tooretrieve cmdlet para obter mais informações sobre a configuração de AutoEscala hello.

Olá exemplo a seguir mostra detalhes sobre todas as configurações de dimensionamento automático no grupo de recursos de saudação 'myrg1'.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

Olá exemplo a seguir mostra detalhes sobre todas as configurações de dimensionamento automático no grupo de recursos de saudação 'myrg1' e Olá especificamente a configuração de dimensionamento automático denominada 'MyScaleVMSSSetting'.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a>Remover uma configuração de autoescala
Você pode usar o hello `Remove-Autoscalesetting` cmdlet toodelete uma configuração de AutoEscala.

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a>Gerenciar perfis de log para logs de atividade
Você pode criar um *log perfil* e exportar dados de sua conta de armazenamento de tooa de log de atividade e você podem configurar a retenção de dados para ele. Opcionalmente, você também pode transmitir Olá dados tooyour Hub de eventos. Observe que no momento esse recurso está em Preview e você só pode criar um perfil de log por assinatura. Você pode usar o hello seguintes cmdlets com o toocreate da assinatura atual e gerenciar perfis de log. Você também pode escolher uma assinatura específica. Embora PowerShell padrão é a assinatura atual toohello, você pode alterar sempre que usar `Set-AzureRmContext`. Você pode configurar a conta de armazenamento atividade log tooroute dados tooany ou Hub de eventos dentro dessa assinatura. Os dados são gravados como arquivos de blob no formato JSON.

### <a name="get-a-log-profile"></a>Obter um perfil de log
toofetch seus perfis de log existentes, use Olá `Get-AzureRmLogProfile` cmdlet.

### <a name="add-a-log-profile-without-data-retention"></a>Adicionar um perfil de log sem retenção de dados
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Remover um perfil de log
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a>Adicionar um perfil de log com retenção de dados
Você pode especificar Olá **- RetentionInDays** propriedade com hello número de dias, como um inteiro positivo, onde os dados de saudação são retidos.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a>Adicionar perfil de log com retenção e Hub de eventos
Em adição toorouting sua conta de toostorage de dados, você também pode transmitir-tooan Hub de eventos. Observe que, nesta visualização configuração de conta de armazenamento de versão e hello é obrigatória, mas a configuração do Hub de eventos é opcional.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a>Configurar logs de diagnóstico
Muitos serviços do Azure fornecem tooEvent Hubs de envio de logs adicionais e telemetria que pode ser dados toosave configurado em sua conta de armazenamento do Azure, e/ou enviados tooan espaço de trabalho de análise de logs do OMS. Essa operação só pode ser executada em um nível de recurso e hub de evento ou a conta de armazenamento Olá deve estar presente no hello mesma região que o recurso de destino Olá onde a configuração de diagnóstico de saudação está configurada.

### <a name="get-diagnostic-setting"></a>Obter configuração de diagnóstico
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

Desabilitar configuração de diagnóstico

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

Habilitar configuração de diagnóstico sem retenção

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

Habilitar configuração de diagnóstico com retenção

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

Habilitar configuração de diagnóstico com retenção para uma categoria de log específica

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

Habilitar configuração de diagnóstico para Hubs de Eventos

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

Habilitar configuração de diagnóstico para OMS

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
