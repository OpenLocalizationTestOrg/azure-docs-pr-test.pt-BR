---
title: "aaaOverview dos Logs de diagnóstico do Azure | Microsoft Docs"
description: "Saiba quais são os logs de diagnósticos do Azure e como você pode usá-los toounderstand eventos que ocorrem dentro de um recurso do Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a>Coletar e consumir dados de log dos recursos do Azure

## <a name="what-are-azure-resource-diagnostic-logs"></a>O que são os logs de diagnóstico de recursos do Azure
**Logs de diagnóstico do Azure de nível de recurso** logs emitido por um recurso que fornecem dados ricos, frequentes sobre a operação de saudação do recurso. conteúdo de saudação desses logs varia por tipo de recurso. Por exemplo, os contadores de regra do Grupo de Segurança de Rede e as auditorias do Key Vault são duas categorias de logs de recursos.

Logs de diagnóstico do nível de recursos diferem das Olá [Log de atividades](monitoring-overview-activity-logs.md). Olá Log de atividades fornece informações sobre operações Olá que foram executadas em recursos em sua assinatura usando o Gerenciador de recursos, por exemplo, criar uma máquina virtual ou a exclusão de um aplicativo lógico. Hello atividade de Log é um log de nível de assinatura. Os logs de diagnóstico no nível do recurso fornecem informações sobre as operações executadas dentro do próprio recurso, por exemplo, obtenção de um segredo de um Key Vault.

Os logs de diagnóstico no nível do recurso também diferem dos logs de diagnóstico no nível do sistema operacional convidado. Os logs de diagnóstico do sistema operacional convidado são aqueles coletados por um agente em execução dentro de uma máquina virtual ou outro tipo de recurso com suporte. Logs de diagnóstico do nível de recursos exigem que os dados de recursos específicos sem agente e a captura de saudação plataforma Windows Azure, enquanto os logs de diagnóstico de nível de sistema operacional convidado capturam dados de sistema de operacional hello e aplicativos em execução em uma máquina virtual.

Nem todos os recursos oferecem suporte a saudação novo tipo de logs de diagnóstico recursos descritos aqui. Este artigo contém uma lista de seção quais tipos de recursos oferecer suporte a novos logs de diagnóstico nível do recurso hello.

![Logs de diagnóstico do recurso versus outros tipos de logs ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a>O que você pode fazer com os logs de diagnóstico no nível do recurso
Aqui estão algumas das coisas Olá que você pode fazer com os logs de diagnóstico de recursos:

![Posicionamento lógico dos Logs de Diagnóstico de recurso](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* Salvá-las tooa [ **conta de armazenamento** ](monitoring-archive-diagnostic-logs.md) para inspeção de auditoria ou manual. Você pode especificar Olá retenção tempo (em dias) usando **configurações de diagnóstico de recurso**.
* [Transmiti-los muito**Hubs de eventos** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) para ingestão por um serviço de terceiros ou a solução de análise personalizado, como o Power BI.
* Analise-os com o [Log Analytics do OMS](../log-analytics/log-analytics-azure-storage.md)

Você pode usar uma conta de armazenamento ou o namespace de Hubs de eventos que não está em Olá mesma assinatura conforme Olá um emissor logs. usuário de saudação que configura a configuração de saudação deve ter assinaturas do hello apropriadas RBAC acesso tooboth.

## <a name="resource-diagnostic-settings"></a>Configurações do Diagnóstico do recurso
Os logs de diagnóstico do recurso para os recursos que não são de computação são configurados usando as configurações de diagnóstico do recurso. **Configurações de Diagnóstico do Recurso** para um controle de recursos:

* Para onde os logs de diagnóstico e as métricas do recurso são enviados (Conta de Armazenamento, Hubs de Eventos e/ou Log Analytics do OMS).
* Quais categorias de log são enviadas e se os dados de métrica também são enviados.
* Quanto tempo cada categoria de log deve ser mantida em uma conta de armazenamento
    - Uma retenção de zero dias significa que os registros serão mantidos indefinidamente. Caso contrário, o valor de saudação pode ser qualquer número de dias entre 1 e 2147483647.
    - Se as políticas de retenção são definidas, mas o armazenamento de logs em uma conta de armazenamento está desabilitado (por exemplo, se apenas as opções de Hubs de eventos ou do OMS são selecionadas), políticas de retenção de saudação não têm efeito.
    - Políticas de retenção são aplicadas por dia, para em Olá final de um dia (UTC), logs de dia de saudação que agora está além da política de retenção de saudação são excluídos. Por exemplo, se você tiver uma política de retenção de um dia, no início de saudação do dia Olá hoje hello logs de anteontem Olá seriam excluídas.

Essas configurações são definidas facilmente por meio de configurações de diagnóstico Olá para um recurso em Olá portal do Azure, por meio de comandos do PowerShell do Azure e a CLI ou Olá [API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).

> [!WARNING]
> Logs de diagnóstico e métricas da camada de sistema operacional convidado Olá de uso de recursos (por exemplo, máquinas virtuais ou malha do serviço) de computação [um mecanismo separado para configuração e seleção de saídas](../azure-diagnostics.md).
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a>Como coleção tooenable dos logs de diagnóstico de recurso
Coleta de logs de diagnóstico de recursos podem ser habilitadas [como parte da criação de um recurso em um modelo do Gerenciador de recursos](./monitoring-enable-diagnostic-logs-using-template.md) ou depois que um recurso é criado na página desse recurso no portal de saudação. Você também pode habilitar a coleção a qualquer momento usando comandos do Azure PowerShell ou CLI ou Olá API de REST do Monitor do Azure.

> [!TIP]
> Essas instruções podem não se aplicam diretamente tooevery recursos. Consulte Olá esquema links na parte inferior de saudação dessa página toounderstand especiais as etapas que podem ser aplicadas a tipos de recurso toocertain.
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a>Habilitar a coleta de logs de diagnóstico de recursos no portal de saudação
Você pode habilitar a coleta de logs de diagnóstico de recurso no hello Azure portal depois que um recurso foi criado pelo recurso específico tooa vai ou navegando tooAzure Monitor. tooenable isso por meio do Monitor do Azure:

1. Em Olá [portal do Azure](http://portal.azure.com), navegar tooAzure Monitor e clique em **configurações de diagnóstico**

    ![Seção de monitoramento do Azure Monitor](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. Se desejar filtrar lista Olá por tipo de recurso ou grupo de recursos, clique no recurso Olá para o qual você gostaria que tooset uma configuração de diagnóstica.

3. Se nenhuma configuração existir no recurso de saudação selecionado, você está toocreate solicitada uma configuração. Clique em “Ativar diagnóstico”.

   ![Adicionar configuração de diagnóstico - nenhuma configuração existente](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   Se houver configurações existentes no recurso hello, você verá uma lista de configurações já configurado nesse recurso. Clique em "Adicionar configuração de diagnóstico".

   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. Dê sua configuração para um nome, caixas de saudação de seleção para cada toowhich de destino que você deseja toosend dados e configurar o recurso que será usado para cada destino. Opcionalmente, defina um número de dias tooretain esses logs usando Olá **retenção (dias)** controles deslizantes (somente aplicável toohello conta destino de armazenamento). Uma retenção de zero dias armazena logs Olá indefinidamente.
   
   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. Clique em **Salvar**.

Após alguns instantes, Olá nova configuração é exibida na sua lista de configurações para esse recurso e logs de diagnóstico são enviados toohello especificado destinos assim que novos dados de evento são gerados.

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a>Habilitar a coleção de logs de diagnóstico de recurso via PowerShell
coleção de tooenable dos logs de diagnóstico de recursos por meio do PowerShell do Azure, use Olá comandos a seguir:

armazenamento de tooenable dos logs de diagnóstico em uma conta de armazenamento, use este comando:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

armazenamento Olá ID da conta é Olá ID de recurso para toowhich de conta de armazenamento Olá deseja toosend Olá logs.

tooenable streaming de hub de eventos de tooan de logs de diagnóstico, use este comando:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

Olá ID da regra de barramento de serviço é uma cadeia de caracteres com este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.

Enviar tooenable do espaço de trabalho de análise de Log de tooa logs de diagnóstico, use este comando:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

Você pode obter a ID de recurso de saudação do seu espaço de trabalho de análise de Log usando o comando a seguir de saudação:

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

Você pode combinar várias opções de saída para tooenable esses parâmetros.

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a>Habilitar a coleção de logs de diagnóstico do recurso via CLI
coleção de tooenable dos logs de diagnóstico de recursos por meio de saudação CLI do Azure, use Olá comandos a seguir:

armazenamento de tooenable dos logs de diagnóstico em uma conta de armazenamento, use este comando:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

armazenamento Olá ID da conta é Olá ID de recurso para toowhich de conta de armazenamento Olá deseja toosend Olá logs.

tooenable streaming de hub de eventos de tooan de logs de diagnóstico, use este comando:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

Olá ID da regra de barramento de serviço é uma cadeia de caracteres com este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.

Enviar tooenable do espaço de trabalho de análise de Log de tooa logs de diagnóstico, use este comando:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

Você pode combinar várias opções de saída para tooenable esses parâmetros.

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a>Habilitar a coleção de logs de diagnóstico do recurso via API REST
configurações de diagnóstico toochange usando Olá API de REST do Monitor do Azure, consulte [neste documento](https://msdn.microsoft.com/library/azure/dn931931.aspx).

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a>Gerenciar configurações de diagnóstico de recursos no portal de saudação
Verifique se todos os seus recursos estão definidos com as configurações de diagnóstico. Navegue muito**Monitor** em Olá portal e abra **configurações de diagnóstico**.

![Folha de Logs de diagnóstico no portal de saudação](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

Você pode ter tooclick seção de Monitor "Mais serviços" toofind hello.

Aqui você pode visualizar e filtrar todos os recursos que oferecem suporte a configurações de diagnóstico toosee se eles tiverem diagnóstico habilitado. Você também pode fazer drill down toosee se várias configurações são definidas em um recurso e verificar qual conta de armazenamento, o namespace de Hubs de eventos e/ou espaço de trabalho de análise de Log que os dados estão fluindo para.

![Resultados da folha Logs de Diagnóstico no portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

Adicionar que uma configuração de diagnóstica exibe Olá modo de exibição de configurações de diagnóstico, onde você pode habilitar, desabilitar ou modificar as configurações de diagnósticas para Olá selecionado recursos.

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a>Serviços, categorias e esquemas com suporte para os logs de diagnóstico de recurso
[Consulte este artigo](monitoring-diagnostic-logs-schema.md) para obter uma lista de serviços com suporte e categorias de log hello e esquemas usados por esses serviços.

## <a name="next-steps"></a>Próximas etapas

* [Logs de diagnóstico do recurso de fluxo muito**Hubs de eventos**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Alterar configurações de diagnóstico de recursos usando Olá API de REST do Monitor do Azure](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Analisar logs do Armazenamento do Azure com o Log Analytics](../log-analytics/log-analytics-azure-storage.md)
