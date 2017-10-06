---
title: "aaaStream Olá Log de atividades do Azure tooEvent Hubs | Microsoft Docs"
description: "Saiba como toostream Olá tooEvent do Log de atividades do Azure Hubs."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 336f92771b9d4379ad9dbcadc6997dfae7fae7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a>Fluxo de tooEvent de Log de atividades do Azure Olá Hubs
Olá [ **o Log de atividades do Azure** ](monitoring-overview-activity-logs.md) pode ser transmitida em quase em tempo real tooany aplicativo usando a opção Olá interna "Exportar" no portal de hello, ou habilitando Olá Id de regra de barramento de serviço em um perfil de registro por meio de saudação Cmdlets do PowerShell do Azure ou Azure CLI.

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a>O que você pode fazer com hello Log de atividades e Hubs de eventos
Aqui estão algumas maneiras que você pode usar o hello streaming funcionalidade para Olá Log de atividades:

* **Fluxo de sistemas de registro em log e telemetria toothird terceiros** – ao longo do tempo, streaming de Hubs de eventos se tornará Olá mecanismo toopipe o Log de atividades em SIEMs de terceiros e soluções de análise de log.
* **Criar uma plataforma de registro em log e telemetria personalizada** – se você já tem uma plataforma de telemetria personalizada ou estão pensando sobre como criar um, Olá altamente escalonável de publicação / assinatura natureza dos Hubs de eventos permite que você tooflexibly ingestão Olá log de atividades. [Consulte toousing de guia de Dan Rosanova Hubs de eventos em uma plataforma de telemetria de escala global aqui.](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a>Habilitar o streaming de saudação Log de atividades
Você pode habilitar o streaming de hello atividade de Log programaticamente ou por meio do portal de saudação. De qualquer forma, você escolhe um Namespace de barramento de serviço e uma política de acesso compartilhado para que o namespace e um Hub de eventos é criado no namespace quando ocorre Olá primeiro novo evento de Log de atividades. Se você não tem um Namespace de barramento de serviço, é necessário primeiro toocreate um. Se você tiver anteriormente transmitido toothis de eventos do Log de atividades Namespace de barramento de serviço, Olá Hub de eventos que foi criado anteriormente será reutilizada. política de acesso compartilhada de saudação define permissões de saudação com mecanismo de fluxo de saudação. Atualmente, o streaming de Hubs de eventos tooan exige **gerenciar**, **enviar**, e **escutar** permissões. Você pode criar ou modificar políticas de acesso do Namespace de barramento de serviço compartilhado no portal clássico do hello na guia de "Configurar" Olá para o Namespace de barramento de serviço. tooupdate Olá fluxo contínuo tooinclude de perfil do log de Log de atividades, usuário Olá Olá alteração deve ter permissão de ListKey Olá nessa regra de autorização do barramento de serviço.

Olá namespace de hub de evento ou de barramento de serviço não tem toobe em Olá mesma assinatura que Olá emitindo logs como usuário Olá que configura a configuração de saudação tem assinaturas de tooboth de acesso RBAC apropriadas.

### <a name="via-azure-portal"></a>Via Portal do Azure
1. Navegue toohello **Log de atividades** folha usando o menu de saudação em Olá esquerda do portal de saudação.
   
    ![Navegue tooActivity Log no portal](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Clique em Olá **exportar** botão na parte superior de saudação da folha de saudação.
   
    ![Botão Exportar no portal](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. Na folha de saudação que aparece, você pode selecionar regiões Olá para o qual você gostaria que os eventos toostream e Olá Namespace de barramento de serviço em que você gostaria que um toobe de Hub de eventos criado para esses eventos de fluxo contínuo.
   
    ![Folha Exportar Log de Atividades](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Clique em **salvar** toosave essas configurações. configurações de saudação imediatamente são ser aplicada tooyour assinatura.

### <a name="via-powershell-cmdlets"></a>Via Cmdlets do PowerShell
Se já existir um perfil de registro, é necessário primeiro tooremove esse perfil.

1. Use `Get-AzureRmLogProfile` tooidentify se existe um perfil de registro
2. Nesse caso, use `Remove-AzureRmLogProfile` tooremove-lo.
3. Use `Set-AzureRmLogProfile` toocreate um perfil:

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

Olá ID de regra de barramento de serviço é uma cadeia de caracteres com este formato: {ID de recurso do barramento de serviço} /authorizationrules/ {nome da chave}, por exemplo 

### <a name="via-azure-cli"></a>Via CLI do Azure
Se já existir um perfil de registro, é necessário primeiro tooremove esse perfil.

1. Use `azure insights logprofile list` tooidentify se existe um perfil de registro
2. Nesse caso, use `azure insights logprofile delete` tooremove-lo.
3. Use `azure insights logprofile add` toocreate um perfil:

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

Olá ID de regra de barramento de serviço é uma cadeia de caracteres com este formato: `{service bus resource ID}/authorizationrules/{key name}`.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>Como consomem a dados de log de saudação dos Hubs de eventos?
[esquema Olá Olá Log de atividade está disponível aqui](monitoring-overview-activity-logs.md). Cada evento é uma matriz de blobs JSON chamada "registros".

## <a name="next-steps"></a>Próximas etapas
* [Saudação de arquivamento conta de armazenamento do Log de atividades tooa](monitoring-archive-activity-log.md)
* [Ler visão geral de saudação do hello Log de atividades do Azure](monitoring-overview-activity-logs.md)
* [Configurar um alerta com base em um evento do Log de Atividades](insights-auditlog-to-webhook-email.md)

