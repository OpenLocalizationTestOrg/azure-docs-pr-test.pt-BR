---
title: "exemplo de ação de alerta de aaaWebhook na análise de Log do OMS | Microsoft Docs"
description: "Uma das ações de saudação, você pode executar em resposta tooa alerta de análise de Log é um * webhook *, que permite que você tooinvoke um processo externo por meio de uma única solicitação HTTP. Neste artigo, vamos examinar um exemplo de como criar uma ação de webhook em um alerta do Log Analytics usando o Slack."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 13c39f0f-fd3c-472d-8324-ddf7538be45e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.openlocfilehash: e60bdc4922347073d572c2e4719461b13e8e7d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a>Criar uma ação de alerta do webhook na análise de logs do OMS toosend mensagem tooSlack
Uma das ações de saudação, você pode executar em resposta tooa [alerta de análise de Log](log-analytics-alerts.md) é um *webhook*, que permite a você tooinvoke um processo externo por meio de uma única solicitação HTTP.  Você pode ler sobre os detalhes de alertas e webhooks em [Alertas no Log Analytics](log-analytics-alerts.md)

Neste artigo, vamos examinar um exemplo de como criar uma ação de webhook em um alerta do Log Analytics usando o Slack, que é um serviço de mensagens.

> [!NOTE]
> Você deve ter uma conta do Slack toocomplete Este exemplo.  Inscreva-se para uma conta gratuita em [slack.com](http://slack.com).
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a>Etapa 1: Habilitar webhooks no Slack
1. Entrar tooSlack em [slack.com](http://slack.com).
2. Selecione um canal em Olá **canais** seção no painel esquerdo da saudação.  Este é o canal de saudação essa mensagem de saudação será enviada para.  Você pode selecionar um dos canais de padrão de saudação como **geral** ou **aleatório**.  Em um cenário de produção, você provavelmente criaria um canal especial como **alertasdeserviçocríticos**. <br>
   
   ![Canais do Slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. Clique em **adicionar um aplicativo ou a integração personalizados** tooopen Olá diretório de aplicativo.
4. Tipo *webhooks* na caixa de pesquisa de saudação e, em seguida, selecione **WebHooks entrada**. <br>
   
   ![Canais do Slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. Clique em **instalar** nome da equipe tooyour Avançar.
6. Clique em **Adicionar Configuração**.
7. Canal de Olá Olá selecione que você vai toouse para este exemplo e, em seguida, clique em **Adicionar entrada WebHooks integração**.  
8. Saudação de cópia **URL do Webhook**.  Você estará colando isso na configuração de alerta de saudação. <br>
   
    ![Canais do Slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a>Etapa 2: Criar a regra de alerta no Log Analytics
1. [Criar uma regra de alerta](log-analytics-alerts.md) com hello configurações a seguir.
   * Consulta: ```    Type=Event EventLevelName=error ```
   * Verificar esse alerta a cada: 5 minutos
   * saudação de número de resultados é: maior que 10
   * Durante o período de: 60 minutos
   * Selecione **Sim** para **Webhook** e **não** para Olá outras ações.
2. Olá colar a URL de margem de atraso em Olá **URL do Webhook** campo.
3. Selecione a opção de saudação muito**incluem uma carga JSON personalizada**.
4. O Slack espera uma carga formatada em JSON com um parâmetro chamado *text*.  Esse é o texto de saudação que ela será exibida na mensagem de saudação, que ele cria.  Você pode usar um ou mais dos parâmetros de alerta hello usando Olá  *#*  símbolo, como no exemplo a seguir de saudação.
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![carga JSON de exemplo](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. Clique em **salvar** toosave regra de alerta de saudação.
6. Aguarde tempo suficiente para um alerta toobe criado e verifique se a margem de atraso para uma mensagem que será a seguir toohello semelhante.
   
   ![webhook de exemplo no Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a>Carga de webhook avançada para o Slack
É possível personalizar amplamente as mensagens de entrada com o Slack. Para obter mais informações, consulte [Webhooks entrada](https://api.slack.com/incoming-webhooks) no site de margem de atraso de saudação. A seguir está uma toocreate de carga uma mensagem rich com formatação mais complexo:

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link tooSearchResults",
                        "value": "<#linktosearchresults|OMS Search Results>"},
                    {
                        "title": "Search Interval",
                        "value": "#searchinterval"},
                    {
                        "title": "Threshold Operator",
                        "value": "#thresholdoperator"},
                    {
                        "title": "Threshold Value",
                        "value": "#thresholdvalue"}
                ],
                "color": "#F35A00"
            }
        ]
    }


Isso poderia gerar uma mensagem de atraso seguir toohello semelhante.

![mensagem de exemplo no Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a>Resumo
Com esta regra de alerta em vigor, você teria tooSlack uma mensagem enviada sempre Olá critérios forem atendidos.  

Isso é apenas um exemplo de uma ação que você pode criar no alerta de tooan de resposta.  Você pode criar uma ação de webhook que chama outro serviço externo, um toostart de ação de runbook um runbook na automação do Azure ou um toosend de ação de email tooyourself um email ou outros destinatários.   

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre outras [ações de alerta no Log Analytics](log-analytics-alerts-actions.md), incluindo outras ações.


