---
title: aaaUsing API REST para alertas do OMS Log Analytics
description: "Olá API de REST de alerta da análise de Log permite que você toocreate e gerencie alertas na análise de Log que é parte do Operations Management Suite (OMS).  Este artigo fornece detalhes de saudação API e vários exemplos para executar operações diferentes."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a>Criar e gerenciar regras de alerta no Log Analytics com a API REST
Olá API de REST de alerta da análise de Log permite toocreate e gerenciar alertas no OMS Operations Management Suite ().  Este artigo fornece detalhes de saudação API e vários exemplos para executar operações diferentes.

Olá API de REST de pesquisa de análise de Log é RESTful e pode ser acessado via Olá API de REST do Gerenciador de recursos do Azure. Neste documento você encontrará exemplos em que o hello API é acessada de uma linha de comando do PowerShell usando [ARMClient](https://github.com/projectkudu/ARMClient), uma ferramenta de linha de comando de software livre que simplifica a invocação Olá API do Gerenciador de recursos do Azure. uso de saudação do ARMClient e do PowerShell é uma saudação de tooaccess muitas opções API de pesquisa de análise de Log. Com essas ferramentas, você pode utilizar Olá API RESTful do Gerenciador de recursos do Azure toomake chamadas tooOMS espaços de trabalho e executar comandos de pesquisa dentro deles. Olá API produzirá tooyou de resultados de pesquisa no formato JSON, permitindo que você resultados da pesquisa Olá toouse de diferentes maneiras por meio de programação.

## <a name="prerequisites"></a>Pré-requisitos
Atualmente, os alertas somente podem ser criados com uma pesquisa salva no Log Analytics.  Você pode consultar toohello [API de REST de pesquisa de Log](log-analytics-log-search-api.md) para obter mais informações.

## <a name="schedules"></a>Agendas
Uma pesquisa salva pode ter um ou mais agendamentos. Olá agenda define quantas vezes hello pesquisa é executada e intervalo de tempo de saudação sobre os critérios de saudação é identificado.
Agendas têm propriedades de saudação no Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| Intervalo |Frequência hello pesquisa é executada. Medida em minutos. |
| QueryTimeSpan |intervalo de tempo de saudação em qual Olá critérios é avaliada. Deve ser maior que o intervalo tooor igual. Medida em minutos. |
| Versão |Olá versão de API que está sendo usada.  Atualmente, isso deve sempre ser definido too1. |

Por exemplo, considere uma consulta de evento com um Interval (Intervalo) de 15 minutos e Timespan (Período) de 30 minutos. Nesse caso, Olá consulta será executada a cada 15 minutos, e um alerta será disparado se critérios Olá continuação tooresolve tootrue em um intervalo de 30 minutos.

### <a name="retrieving-schedules"></a>Recuperando agendamentos
Olá Use obter método tooretrieve todas as agendas de uma pesquisa salva.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

Olá Use obter método com um tooretrieve de ID de agenda uma agenda específica de uma pesquisa salva.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

A seguir está um exemplo de resposta para um agendamento.

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a>Criando uma agenda
Use o método de Put de saudação com uma ID de agenda exclusiva toocreate uma nova agenda.  Observe que duas agendas não podem ter Olá a mesma ID mesmo se eles estão associados com diferentes pesquisas salvas.  Quando você cria uma agenda no console do OMS hello, um GUID é criado para ID de agenda hello.

> [!NOTE]
> nome de saudação para pesquisas salvas todas as agendas e ações criadas com hello API de análise de Log deve ser em letras minúsculas.

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a>Editando um agendamento
Use o método de Put de saudação com uma agenda existente ID para Olá mesmo salvo pesquisar toomodify agendar.  corpo de saudação da solicitação Olá deve incluir Olá etag da agenda de saudação.

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a>Excluindo agendamentos
Use o método de exclusão de saudação com uma ID de agenda toodelete uma agenda.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a>Ações
Um agendamento pode ter várias ações. Uma ação pode definir um ou mais tooperform de processos, como enviar um email ou iniciar um runbook, ou ele pode definir um limite que determina quando os resultados de saudação de uma pesquisa correspondem a alguns critérios.  Algumas ações definirá ambos para que os processos de saudação são executados quando Olá limite é atingido.

Todas as ações têm propriedades de saudação no Olá a tabela a seguir.  Diferentes tipos de alertas têm diferentes propriedades adicionais que são descritas abaixo.

| Propriedade | Descrição |
|:--- |:--- |
| Tipo |Tipo de ação de saudação.  No momento Olá possíveis valores são alerta e Webhook. |
| Nome |Nome de exibição de alerta de saudação. |
| Versão |Olá versão de API que está sendo usada.  Atualmente, isso deve sempre ser definido too1. |

### <a name="retrieving-actions"></a>Recuperando ações
Olá Use obter método tooretrieve todas as ações de uma agenda.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

Olá Use obter método com hello tooretrieve de ID de ação uma ação específica para um agendamento.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a>Criar ou editar ações
Use o método de Put de saudação com uma ID de ação que é exclusivo toohello agenda toocreate uma nova ação.  Quando você cria uma ação no console do OMS hello, um GUID é para ID de ação de saudação.

> [!NOTE]
> nome de saudação para pesquisas salvas todas as agendas e ações criadas com hello API de análise de Log deve ser em letras minúsculas.

Use o método de Put de saudação com uma ação de ID para Olá mesmo salvo pesquisar toomodify agendar.  corpo de saudação da solicitação Olá deve incluir Olá etag da agenda de saudação.

formato da solicitação Olá para criar uma nova ação varia de acordo com o tipo de ação para que esses exemplos são fornecidos nas seções de saudação abaixo.

### <a name="deleting-actions"></a>Excluindo ações
Use o método de exclusão de Olá com hello ação ID toodelete uma ação.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a>Ações de Alerta
Um Agendamento deve ter somente uma ação de Alerta.  Ações de alerta tem uma ou mais das seções Olá Olá a tabela a seguir.  Elas são descritas em mais detalhes abaixo.

| Seção | Descrição |
|:--- |:--- |
| Limite |Critérios para quando a ação de saudação é executada. |
| EmailNotification |Envie email de destinatários toomultiple. |
| Correção |Iniciar um runbook na automação do Azure tooattempt toocorrect identificado o problema. |

#### <a name="thresholds"></a>Limites
Uma ação de Alerta deve ter somente um limite.  Quando os resultados de saudação de uma pesquisa salva correspondem limite de saudação em uma ação associada que a pesquisa, outros processos na ação são executados.  Uma ação também pode conter apenas um limite para ser usado com ações de outros tipos que não contêm os limites.

Limites têm as propriedades de saudação no Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| operador |Operador de comparação de limite de saudação. <br> gt = Maior Que <br> lt = Menor Que |
| Valor |Valor de limite de saudação. |

Por exemplo, considere uma consulta de evento com um Interval (Intervalo) de 15 minutos, Timespan (Período) de 30 minutos e Threshold (Limite) maior que 10. Nesse caso, Olá consulta será executada a cada 15 minutos, e um alerta será disparado quando retornado 10 eventos que foram criados em um intervalo de 30 minutos.

Veja a seguir um exemplo de resposta para uma ação com apenas um limite.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

Use o método de Put de saudação com uma ID de ação exclusivo toocreate uma nova ação de limite para um agendamento.  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

Use o método de Put de saudação com um toomodify de ID de ação uma ação de limite existente para um agendamento.  corpo de saudação da solicitação de saudação deve incluir Olá etag da ação de saudação.

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a>Notificação por email
Notificações por email enviam email tooone ou mais destinatários.  Elas incluem propriedades Olá em Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| Destinatários |Lista de endereços de email. |
| Assunto |assunto Olá mail hello. |
| Anexo |Atualmente, não há suporte para nexos, por isso este item sempre terá um valor de "None" (Nenhum). |

Veja a seguir uma resposta de exemplo para uma ação de notificação por email com um limite.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

Use o método de Put de saudação com uma ID de ação exclusivo toocreate uma nova ação de email para um agendamento.  Olá exemplo a seguir cria uma notificação por email com um limite para que mensagens de saudação é enviada quando resultados Olá Olá pesquisa salva excederem o limite de saudação.

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

Use o método de Put de saudação com um toomodify de ID de ação uma ação de email existente para um agendamento.  corpo de saudação da solicitação de saudação deve incluir Olá etag da ação de saudação.

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a>Ações de correção
Correções de iniciar um runbook na automação do Azure que tentativas de problema de saudação toocorrect identificado pelo alerta hello.  Você deve criar um webhook de runbook Olá usada em uma ação de correção e especifique Olá URI Olá WebhookUri propriedade.  Quando você cria esta ação usando o console do OMS hello, um webhook novo é criado automaticamente para Olá runbook.

Correções incluem propriedades de saudação em Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| RunbookName |Nome do runbook hello. Isso deve corresponder a um runbook publicado na conta de automação de saudação configurado no hello solução de automação em seu espaço de trabalho do OMS. |
| WebhookUri |URI da saudação webhook. |
| Expiry |Olá data de expiração de webhook hello.  Se Olá webhook não tiver uma expiração, isso pode ser qualquer data futura válida. |

Veja a seguir uma resposta de exemplo para uma ação de correção com um limite.

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

Use o método de Put de saudação com uma ID de ação exclusivo toocreate uma nova ação de correção para um agendamento.  Hello exemplo a seguir cria uma solução com um limite para que o runbook Olá é iniciada quando resultados Olá Olá pesquisa salva excederem o limite de saudação.

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

Use o método de Put de saudação com um toomodify de ID de ação uma ação de correção existente para um agendamento.  corpo de saudação da solicitação de saudação deve incluir Olá etag da ação de saudação.

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a>Exemplo
A seguir está um exemplo completo de toocreate um novo alerta de email.  Ele cria um novo agendamento juntamente com uma ação que contém um limite e um email.

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a>Ações de Webhook
Ações de Webhook iniciar um processo chamar uma URL e, opcionalmente, fornecendo um toobe carga enviada.  Eles são ações tooRemediation semelhantes, exceto que eles se destinam a webhooks que podem chamar outros processos além do runbooks de automação do Azure.  Eles também fornecem a opção adicional de saudação do fornecimento de um processo remoto do toobe entregue toohello de carga.

Ações de Webhook não têm um limite, mas em vez disso, devem ser adicionadas agenda tooa que tem uma ação com um limite de alerta.  Você pode adicionar várias ações de Webhook todos funcionará quando Olá limite é atingido.

Ações de Webhook incluem propriedades Olá no Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| WebhookUri |assunto Olá mail hello. |
| CustomPayload |Carga personalizada toobe enviado toohello webhook.  formato Olá dependerá de quais webhook hello está esperando. |

Veja a seguir um exemplo de resposta para a ação de webhook e uma ação de alerta associada com um limite.

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a>Criar ou editar uma ação de webhook
Use o método de Put de saudação com uma ID de ação exclusivo toocreate uma nova ação de webhook para um agendamento.  Olá exemplo a seguir cria uma ação de Webhook e uma ação de alerta com um limite para que o webhook Olá será disparada quando resultados Olá Olá pesquisa salva excederem o limite de saudação.

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

Use o método de Put de saudação com um toomodify de ID de ação uma ação de webhook existente para um agendamento.  corpo de saudação da solicitação de saudação deve incluir Olá etag da ação de saudação.

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a>Próximas etapas
* Saudação de uso [pesquisas de log do REST API tooperform](log-analytics-log-search-api.md) na análise de Log.

