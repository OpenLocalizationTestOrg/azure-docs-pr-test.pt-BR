---
title: "tooalerts aaaResponses na análise de Log do OMS | Microsoft Docs"
description: "Alertas de análise de Log identificar informações importantes no seu repositório do OMS e podem proativamente notificá-lo de problemas ou invocar ações tooattempt toocorrect-los.  Este artigo descreve como toocreate uma regra de alerta e ações diferentes de saudação de detalhes que podem executar."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a>Adicione regras de tooalert de ações na análise de Log
Quando um [alerta é criado na análise de Log](log-analytics-alerts.md), você tem a opção de saudação do [configurar regra de alerta Olá](log-analytics-alerts.md) tooperform uma ou mais ações.  Este artigo descreve ações diferentes de saudação que estão disponíveis e os detalhes sobre como configurar cada tipo.

| Ação | Descrição |
|:--|:--|
| [Email](#email-actions) | Envie um email com detalhes de saudação do tooone alerta hello ou mais destinatários. |
| [Webhook](#webhook-actions) | Invoque um processo externo por meio de uma única solicitação HTTP POST. |
| [Runbook](#runbook-actions) | Inicie um runbook na Automação do Azure. |


## <a name="email-actions"></a>Ações de email
Ações de email enviar um email com detalhes de saudação do tooone alerta hello ou mais destinatários.  Você pode especificar o assunto de saudação do email hello, mas seu conteúdo é um formato padrão criado pela análise de Log.  Ele inclui informações de resumo, como nome de saudação do alerta de saudação em toodetails de adição de registros tooten retornado pela pesquisa de log de saudação.  Ele também inclui uma pesquisa de log de tooa link na análise de Log que retornará todo o conjunto de registros de saudação da consulta.   Olá remetente do email Olá é *equipe do Microsoft Operations Management Suite &lt; noreply@oms.microsoft.com &gt;* . 

Ações de email exigem propriedades Olá Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| Assunto |Assunto no email de saudação.  Não é possível modificar o corpo de saudação de mensagens de saudação. |
| Destinatários |Endereços de todos os destinatários de email.  Se você especificar mais de um endereço e endereços de saudação separada com um ponto e vírgula (;). |


## <a name="webhook-actions"></a>Ações de Webhook

Ações de Webhook permitem tooinvoke um processo externo por meio de uma única solicitação HTTP POST.  o serviço de Hello está sendo chamado deve suporte webhooks e determinar como ele usará qualquer carga recebe.  Você poderia chamar uma API REST que não dão suporte especificamente às webhooks como solicitação hello está em um formato que Olá que API compreende.  Exemplos de como usar um webhook no alerta de tooan resposta estão enviando uma mensagem no [Slack](http://slack.com) ou criar um incidente no [PagerDuty](http://pagerduty.com/).  Instruções completas para a criação de uma regra de alerta com um atraso de toocall de webhook está disponível em [Webhooks em alertas de análise de Log](log-analytics-alerts-webhooks.md).

Ações de Webhook exigem propriedades Olá Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| URL de Webhook |URL de saudação do webhook hello. |
| Carga JSON personalizada |Carga personalizada toosend com hello webhook.  Confira os detalhes abaixo. |


Webhooks incluir uma URL e uma carga formatada em JSON Olá dados enviados serviço externo toohello.  Por padrão, a carga de saudação incluirá valores hello no Olá a tabela a seguir.  Você pode escolher tooreplace essa carga com um personalizado de sua preferência.  Nesse caso você pode usar variáveis de saudação na tabela de saudação para cada Olá parâmetros tooinclude seu valor em sua carga personalizada.

| Parâmetro | Variável | Descrição |
|:--- |:--- |:--- |
| AlertRuleName |#alertrulename |Nome da regra de alerta de saudação. |
| AlertThresholdOperator |#thresholdoperator |Operador de limite para a regra de alerta de saudação.  *Greater than (Maior que)* ou *Less than (Menor que)*. |
| AlertThresholdValue |#thresholdvalue |Valor de limite para a regra de alerta de saudação. |
| LinkToSearchResults |#linktosearchresults |Vincule a pesquisa de log de análise de tooLog que retorna registros de saudação da consulta de saudação que criou o alerta de saudação. |
| ResultCount |#searchresultcount |Número de registros nos resultados da pesquisa hello. |
| SearchIntervalEndtimeUtc |#searchintervalendtimeutc |Hora de término para a consulta Olá no formato UTC. |
| SearchIntervalInSeconds |#searchinterval |Janela de tempo para a regra de alerta de saudação. |
| SearchIntervalStartTimeUtc |#searchintervalstarttimeutc |Hora de consulta de saudação de início no formato UTC. |
| SearchQuery |#searchquery |Consulta de pesquisa de log usada pela regra de alerta de saudação. |
| SearchResults |Veja abaixo |Registros retornados pela consulta Olá no formato JSON.  Limitado toohello registros primeiros 5.000. |
| WorkspaceID |#workspaceid |ID do seu espaço de trabalho do OMS. |

Por exemplo, você pode especificar Olá carga personalizada que inclui um único parâmetro de chamada a seguir *texto*.  serviço de saudação que chama esse webhook seria esperando esse parâmetro.

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

Essa carga de exemplo resolveria toosomething como Olá a seguir quando enviadas toohello webhook.

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

tooinclude resultados da pesquisa em uma carga personalizada, adicione Olá linha a seguir como uma propriedade de nível superior na carga de json hello.  

    "IncludeSearchResults":true

Por exemplo, toocreate uma carga personalizada que inclui apenas o nome do alerta hello e resultados da pesquisa hello, você pode usar Olá a seguir. 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


Você pode percorrer um exemplo completo de como criar uma regra de alerta com um webhook toostart um serviço externo no [criar uma ação de alerta do webhook na análise de logs do OMS toosend mensagem tooSlack](log-analytics-alerts-webhooks.md).

## <a name="runbook-actions"></a>Ações de runbook
Ações de runbook iniciam um runbook na Automação do Azure.  Em ordem toouse esse tipo de ação, você deve ter Olá [solução de automação](log-analytics-add-solutions.md) instalado e configurado em seu espaço de trabalho do OMS.  Você pode selecionar Olá runbooks na conta de automação de saudação que você configurou no hello solução de automação.

Ações de runbook exigem propriedades Olá Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:---|
| Runbook | Runbook que você deseja toostart quando um alerta é criado. |
| Executar em | Especifique **Azure** toorun Olá runbook na nuvem hello.  Especifique **Hybrid worker** toorun Olá runbook em um agente com [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) instalado.  |

Iniciar o runbook ações Olá runbook usando um [webhook](../automation/automation-webhooks.md).  Quando você criar regra de alerta hello, ele criará automaticamente um webhook novo runbook Olá com nome hello **correção de alerta do OMS** seguido por um GUID.  

Diretamente você não pode preencher quaisquer parâmetros de runbook hello, mas Olá [$WebhookData parâmetro](../automation/automation-webhooks.md) incluirá Olá detalhes do alerta hello, incluindo Olá resultados da pesquisa de log de saudação que o criou.  Olá runbook precisará toodefine **$WebhookData** como um parâmetro para que ele tooaccess Olá propriedades do alerta de saudação.  Olá dados de alerta estão disponíveis no formato json em uma única propriedade chamado **SearchResults** em Olá **RequestBody** propriedade **$WebhookData**.  Isso será necessário com propriedades Olá Olá a tabela a seguir.

| Nó | Descrição |
|:--- |:--- |
| ID |Caminho e o GUID da pesquisa de saudação. |
| __metadata |Informações sobre Olá alerta incluindo Olá número de registros e status Olá dos resultados da pesquisa. |
| valor |Entrada separada para cada registro nos resultados da pesquisa hello.  detalhes de saudação de entrada hello corresponderá propriedades hello e valores de registro de saudação. |

Por exemplo, hello runbook a seguir seria extrair Olá registros retornados pela pesquisa de log hello e atribuir propriedades diferentes com base no tipo de saudação de cada registro.  Observe que esse runbook Olá inicia convertendo **RequestBody** do json para que ele pode ser editado como um objeto no PowerShell.

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a>Próximas etapas
- Conclua um passo a passo para [configurar um webhook](log-analytics-alerts-webhooks.md) com uma regra de alerta.  
- Saiba como toowrite [runbooks na automação do Azure](https://azure.microsoft.com/documentation/services/automation) tooremediate problemas identificados por alertas.
