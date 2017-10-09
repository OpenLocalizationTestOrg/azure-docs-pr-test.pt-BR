---
title: "alertas de aaaCreate para serviços do Azure - CLI plataforma cruzada | Microsoft Docs"
description: "Disparar emails, notificações, URLs de sites de chamada (webhooks) ou automação quando Olá que especificar condições."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a>Criar alertas de métricas no Azure Monitor para Serviços do Azure – CLI de plataforma cruzada
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Visão geral
Este artigo mostra como tooset alertas de métrica do Azure usando Olá multiplataforma Interface de linha de comando (CLI).

> [!NOTE]
> Monitor do Azure é Olá novo nome para o que era chamado de "Azure Insights" até 25 de setembro de 2016. No entanto, Olá namespaces e, portanto, comandos de saudação abaixo ainda contêm insights"Olá".
>
>

Você pode receber um alerta com base em métricas de monitoramento ou em eventos nos serviços do Azure.

* **Valores da métrica** - Olá gatilhos de alerta quando o valor de saudação de uma métrica especificada cruza um limite que você atribui em qualquer direção. Ou seja, ela aciona ambos quando Olá primeiro condição e, em seguida, posteriormente quando que condição é não está sendo atendida.    
* **Eventos do log de atividades** – um alerta pode disparar em *cada* evento ou somente quando determinados eventos ocorrem. mais sobre alertas de log de atividade de toolearn [clique aqui](monitoring-activity-log-alerts.md)

Você pode configurar uma saudação de métrica toodo alerta após quando ele dispara:

* enviar o administrador do serviço de toohello de notificações de email e coadministradores
* Envie email tooadditional emails que você especificar.
* chamar um webhook
* Iniciar a execução de um runbook do Azure (apenas de saudação portal do Azure no momento)

Você pode configurar e obter informações sobre regras de alerta de métrica usando

* [Portal do Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [CLI (Interface de linha de comando)](insights-alerts-command-line-interface.md)
* [API REST do Monitor do Azure](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Você pode sempre receber ajuda para os comandos digitando um comando e colocando - a Ajuda no final de saudação. Por exemplo:

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a>Criar regras de alerta usando Olá CLI
1. Execute Olá pré-requisitos e tooAzure de logon. Consulte [Exemplos de CLI do Azure Monitor](insights-cli-samples.md). Em resumo, Olá CLI de instalar e executar esses comandos. Eles se conectado, mostrar quais assinatura que você está usando e prepará-lo toorun comandos de Monitor do Azure.

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. as regras existentes em um grupo de recursos, toolist usar Olá formulário a seguir **insights do azure lista de regras de alertas** *[Opções] &lt;resourceGroup&gt;*

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. toocreate uma regra, você precisa toohave várias partes importantes de informações pela primeira vez.
  * Olá **ID de recurso** para os recursos de saudação deseja tooset um alerta para
  * Olá **definições de métrica** disponíveis para esse recurso

     Olá unidirecional tooget ID de recurso é toouse Olá portal do Azure. Supondo que o recurso de saudação já foi criada, selecione-o no portal de saudação. Na folha da próxima hello, selecione *propriedades* em Olá *configurações* seção. Olá *ID de recurso* é um campo na folha de saudação Avançar. Outra maneira é Olá toouse [Gerenciador de recursos do Azure](https://resources.azure.com/).

     Um exemplo de ID de recurso para um aplicativo Web é

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     tooget uma lista de métricas disponíveis hello e as unidades para as métricas para exemplo de recursos anterior hello, use Olá CLI comando a seguir:  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     *PT1M* é a granularidade de saudação de medida disponíveis da saudação (intervalos de 1 minuto). O uso de diferentes granularidades oferece opções diferentes de métrica.
4. toocreate uma regra de alerta com base em métrica, use um comando de saudação formulário a seguir:

    **azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*

    Olá exemplo configura um alerta a seguir em um recurso de site da web. Olá alerta gatilhos sempre que ele recebe consistentemente qualquer tráfego de 5 minutos e, novamente, quando ele recebe nenhum tráfego de 5 minutos.

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. toocreate webhook ou enviar email quando um alerta de métrica é acionado, primeiro crie email hello e/ou webhooks. Criar a regra de saudação imediatamente posteriormente. Você não pode associar webhook ou emails com já criou regras usando Olá CLI.

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. Você pode verificar se os alertas foram criados corretamente examinando uma regra individual.

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. regras de toodelete, use um comando do formulário de saudação:

    **insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;

    Esses comandos excluem regras Olá criadas anteriormente neste artigo.

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a>Próximas etapas
* [Obter uma visão geral do monitoramento do Azure](monitoring-overview.md) incluindo Olá tipos de informações você pode coletar e monitorar.
* Saiba mais sobre como [configurar webhooks em alertas](insights-webhooks-alerts.md).
* Saiba mais sobre [Configurar alertas em eventos de Log de Atividades](monitoring-activity-log-alerts.md).
* Saiba mais sobre [Runbooks da Automação do Azure](../automation/automation-starting-a-runbook.md).
* Obter um [visão geral de coleta de logs de diagnóstico](monitoring-overview-of-diagnostic-logs.md) toocollect detalhadas métricas de alta frequência em seu serviço.
* Obter um [visão geral da coleção de métricas](insights-how-to-customize-monitoring.md) toomake-se de que o serviço está disponível e respondendo.
