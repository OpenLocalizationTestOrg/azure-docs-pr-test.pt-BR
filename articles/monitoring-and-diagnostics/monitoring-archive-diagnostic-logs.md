---
title: "aaaArchive Logs de diagnóstico do Azure | Microsoft Docs"
description: "Saiba como tooarchive o diagnóstico do Azure registra para retenção de longo prazo em uma conta de armazenamento."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 3a55c73f-2ef3-45f3-8956-bcf9c0cb7e05
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: bc9edbd3a649023a728b7fe77130dba2b6e6370d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="archive-azure-diagnostic-logs"></a>Arquivar Logs de Diagnóstico do Azure
Neste artigo, mostramos como você pode usar o hello portal do Azure, Cmdlets do PowerShell, CLI ou REST API tooarchive seu [logs de diagnósticos do Azure](monitoring-overview-of-diagnostic-logs.md) em uma conta de armazenamento. Essa opção será útil se você gostaria que tooretain o diagnóstico registra em log com uma política de retenção opcional para auditoria, análise estática ou backup. conta de armazenamento Olá não tem toobe Olá mesma assinatura que o recurso Olá emitindo logs como usuário Olá que configura a configuração de saudação tem assinaturas de tooboth de acesso RBAC apropriadas.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, é preciso muito[criar uma conta de armazenamento](../storage/storage-create-storage-account.md) toowhich poderá arquivar os logs de diagnóstico. É altamente recomendável que você não use uma conta de armazenamento existente que tenha outros monitoramento não dados armazenados nela, para que você pode controlar melhor acesso toomonitoring dados. No entanto, se você estiver arquivando também o Log de atividades e a conta de armazenamento de tooa de métricas de diagnóstico, talvez faça sentido toouse essa conta de armazenamento para seu logs de diagnóstico também tookeep todos os dados de monitoramento em um local central. conta de armazenamento Olá usada deve ser uma conta de armazenamento de propósito geral, não uma conta de armazenamento de blob.

## <a name="diagnostic-settings"></a>Configurações de Diagnóstico
tooarchive o diagnóstico logs usando qualquer um dos métodos de saudação abaixo, defina um **configuração de diagnóstico** para um recurso específico. Uma configuração de diagnóstico para um recurso define as categorias de saudação de logs e dados de métrica enviados destino tooa (conta de armazenamento, o namespace de Hubs de eventos ou análise de Log). Ele também define a política de retenção de saudação (número de dias tooretain) para eventos de cada categoria de log e métricos dados armazenados em uma conta de armazenamento. Se uma política de retenção é definida toozero, eventos para essa categoria de log são armazenados indefinidamente (que é toosay, indefinidamente). Uma política de retenção pode ser qualquer quantidade de dias, entre 1 e 2147483647. [Leia mais sobre configurações de diagnóstico aqui](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings). Políticas de retenção são aplicadas por dia, para em Olá final de um dia (UTC), logs do dia Olá que agora está além da política de retenção hello serão excluídas. Por exemplo, se você tiver uma política de retenção de um dia, no início de saudação do dia Olá hoje hello logs de anteontem Olá seriam excluídos

## <a name="archive-diagnostic-logs-using-hello-portal"></a>Logs de diagnóstico de arquivamento usando o portal de saudação
1. No portal de hello, navegar tooAzure Monitor e clique em **configurações de diagnóstico**

    ![Seção de monitoramento do Azure Monitor](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. Se desejar filtrar lista Olá por tipo de recurso ou grupo de recursos, clique no recurso Olá para o qual você gostaria que tooset uma configuração de diagnóstica.

3. Se nenhuma configuração existir no recurso de saudação selecionado, você está toocreate solicitada uma configuração. Clique em “Ativar diagnóstico”.

   ![Adicionar configuração de diagnóstico - nenhuma configuração existente](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   Se houver configurações existentes no recurso hello, você verá uma lista de configurações já configurado nesse recurso. Clique em "Adicionar configuração de diagnóstico".

   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. Dê sua configuração para um nome e marque a caixa de saudação para **exportar tooStorage conta**, em seguida, selecione uma conta de armazenamento. Opcionalmente, defina um número de dias tooretain esses logs usando Olá **retenção (dias)** controles deslizantes. Uma retenção de zero dias armazena logs Olá indefinidamente.
   
   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. Clique em **Salvar**.

Após alguns instantes, nova configuração de saudação aparece na lista de configurações para esse recurso e logs de diagnóstico são arquivados toothat armazenamento conta assim que novos dados de evento são gerados.

## <a name="archive-diagnostic-logs-via-azure-powershell"></a>Arquivar logs de diagnóstico por meio do Azure PowerShell
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| Propriedade | Obrigatório | Descrição |
| --- | --- | --- |
| ResourceId |Sim |ID de recurso do recurso Olá no qual você deseja tooset uma configuração de diagnóstica. |
| StorageAccountId |Não |ID do recurso da conta de armazenamento de saudação toowhich Logs de diagnóstico deve ser salvo. |
| Categorias |Não |Lista separada por vírgulas de tooenable de categorias de log. |
| habilitado |Sim |Booliano indicando se os diagnósticos estão habilitados ou desabilitados nesse recurso. |
| RetentionEnabled |Não |Booliano indicando se há uma política de retenção habilitada nesse recurso. |
| RetentionInDays |Não |Número de dias durante os quais os eventos devem ser mantidos, entre 1 e 2147483647. Um valor de zero armazena logs Olá indefinidamente. |

## <a name="archive-diagnostic-logs-via-hello-cross-platform-cli"></a>Logs de diagnóstico de arquivamento via Olá CLI de plataforma cruzada
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| Propriedade | Obrigatório | Descrição |
| --- | --- | --- |
| ResourceId |Sim |ID de recurso do recurso Olá no qual você deseja tooset uma configuração de diagnóstica. |
| storageId |Não |ID do recurso dos logs de diagnóstico Olá conta de armazenamento toowhich deve ser salvos. |
| Categorias |Não |Lista separada por vírgulas de tooenable de categorias de log. |
| Habilitado |Sim |Booliano indicando se os diagnósticos estão habilitados ou desabilitados nesse recurso. |

## <a name="archive-diagnostic-logs-via-hello-rest-api"></a>Logs de diagnóstico de arquivamento via Olá API REST
[Consulte este documento](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) para obter informações sobre como você pode definir uma configuração de diagnóstico usando Olá API de REST do Monitor do Azure.

## <a name="schema-of-diagnostic-logs-in-hello-storage-account"></a>Esquema dos logs de diagnósticos na conta de armazenamento Olá
Depois que você configurar arquivamento, um contêiner de armazenamento é criado na conta de armazenamento Olá assim que um evento ocorre em uma das categorias de log Olá que você habilitou. blobs Hello dentro do contêiner de saudação siga Olá mesmo formato em Logs de diagnóstico e Log de atividades de hello. estrutura Olá esses blobs é:

> insights-logs-{nome da categoria de log}/resourceId=/SUBSCRIPTIONS/{ID da assinatura}/RESOURCEGROUPS/{nome do grupo de recursos}/PROVIDERS/{nome do provedor de recursos}/{tipo de recurso}/{nome do recurso}/y={ano com quatro dígitos numéricos}/m={mês com dois dígitos numéricos}/d={dia com dois dígitos numéricos}/h={horário com dois dígitos no formato 24 horas}/m=00/PT1H.json
> 
> 

Ou, mais simplesmente,

> insights-logs-{nome da categoria de log}/resourceId=/{ID do recurso}/y={ano com quatro dígitos numéricos}/m={mês com dois dígitos numéricos}/d={dia com dois dígitos numéricos}/h={horário com dois dígitos no formato 24 horas}/m=00/PT1H.json
> 
> 

Por exemplo, um nome de blob poderia ser:

> insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

Cada blob PT1H.json contém um blob JSON de eventos que ocorreram na hora de saudação especificada na URL de blob de saudação (por exemplo, h = 12). Durante a saudação hora presente, os eventos são acrescentadas toohello PT1H.json arquivo conforme elas ocorrem. Olá valor de minuto (m = 00) é sempre 00, desde que os eventos de log de diagnóstico são divididos em blobs individuais por hora.

No arquivo de PT1H.json hello, cada evento é armazenado na matriz de registros"hello", neste formato a seguir:

```
{
    "records": [
        {
            "time": "2016-07-01T00:00:37.2040000Z",
            "systemId": "46cdbb41-cb9c-4f3d-a5b4-1d458d827ff1",
            "category": "NetworkSecurityGroupRuleCounter",
            "resourceId": "/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/TESTNSG",
            "operationName": "NetworkSecurityGroupCounters",
            "properties": {
                "vnetResourceGuid": "{12345678-9012-3456-7890-123456789012}",
                "subnetPrefix": "10.3.0.0/24",
                "macAddress": "000123456789",
                "ruleName": "/subscriptions/ s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg/securityRules/default-allow-rdp",
                "direction": "In",
                "type": "allow",
                "matchedConnections": 1988
            }
        }
    ]
}
```

| Nome do elemento | Descrição |
| --- | --- |
| tempo real |Evento Olá correspondente de solicitação de carimbo de hora do evento Olá foi gerado pelo Olá Olá de processamento de serviço do Azure. |
| resourceId |ID do recurso da saudação afetados recursos. |
| operationName |Nome da operação de saudação. |
| categoria |Categoria de log de evento de saudação. |
| propriedades |Conjunto de `<Key, Value>` pares (ou seja, o dicionário) que descreve os detalhes de saudação do evento hello. |

> [!NOTE]
> Propriedades de saudação e o uso dessas propriedades podem variar dependendo de recurso hello.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* [Baixar blobs para análise](../storage/storage-dotnet-how-to-use-blobs.md)
* [Namespace de Hubs de eventos tooan logs de diagnóstico de fluxo](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Leia mais sobre logs de diagnóstico](monitoring-overview-of-diagnostic-logs.md)
