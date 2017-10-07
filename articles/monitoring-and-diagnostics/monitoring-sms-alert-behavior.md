---
title: "comportamento de alerta aaaSMS em grupos de ação | Microsoft Docs"
description: Formato de mensagem SMS e respondendo toounsubscribe tooSMS de mensagens, assinar novamente ou solicitar ajuda.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a>Comportamento dos alertas por SMS em grupos de ação
## <a name="overview"></a>Visão geral ##
Grupos de ação de habilitar tooconfigure uma lista de destinatários. Esses grupos podem ser aproveitados ao definir alertas de log de atividades; garantir que um grupo de ação em particular seja notificado quando hello atividade log alerta é disparado. Uma saudação suporte de mecanismos de alerta é SMS; alertas de saudação oferecem suporte a comunicação bidirecional. Um usuário pode responder tooan do alerta:

- **Cancelar a assinatura de alertas:** um usuário pode cancelar a assinatura de todos os alertas por SMS de todos os grupos de ação ou de um grupo de ação individual.  
- **Assinar novamente tooalerts:** um usuário pode assinar novamente tooall alertas SMS para todos os grupos de ação ou um grupo de ação singular.  
- **Solicitar ajuda:** um usuário pode pedir para obter mais informações sobre Olá SMS. Eles serão redirecionadas toothis artigo

Este artigo aborda o comportamento de saudação de alertas SMS hello e hello resposta ações Olá usuário pode executar com base na localidade de saudação do usuário hello:

## <a name="usacanada-sms-behavior"></a>Comportamento de SMS nos EUA e no Canadá
### <a name="receiving-an-sms-alert"></a>Recebendo um alerta por SMS
Um receptor de SMS, configurado como parte de um grupo de ação, receberá um SMS quando um alerta for acionado. Olá SMS realizará a saudação informações a seguir:
* Nome curto do grupo de ação Olá este alerta foi enviado para
- Título do alerta Olá

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a>Cancelando a assinatura de alertas por SMS de um grupo de ação
Um usuário pode cancelar a assinatura do SMS para alertas para o grupo de uma ação por shortcode respondendo toohello 20873 com palavras-chave de saudação: "Desabilitar &lt;nome curto do grupo de ação&gt;".

Ex.: Um usuário que toounsubscribe de alertas de um grupo com o nome curto do hello "Azure", poderia enviar um SMS toohello shortcode 20873 que diz "Desabilitar Azure"

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a>Cancelando a assinatura de alertas por SMS de todos os grupos de ação
Um usuário pode cancelar a assinatura de todos os alertas SMS para todos os grupos de ação por shortcode respondendo toohello 20873 com qualquer um de saudação palavras-chave a seguir:
* STOP

Ex.: Um usuário que toounsubscribe de todos os alertas SMS para todos os grupos de ação, poderia enviar um SMS toohello shortcode 20873 que diz "STOP"

>[!NOTE]
>Se um usuário cancelou a assinatura de alertas SMS, mas é adicionado tooa novo grupo de ação. eles serão receber alertas SMS para esse novo grupo de ação, mas permanecem cancelados todos os grupos de ação anterior.
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a>Resubscribing tooSMS alertas para um grupo de ação
Um usuário pode assinar novamente tooSMS para alertas para o grupo de uma ação por shortcode respondendo toohello 20873 com palavras-chave de saudação: "habilitar &lt;nome curto do grupo de ação&gt;".

Ex.: Um usuário que tooalerts tooresubscribe para um grupo de ação com o nome curto do hello "Azure", poderia enviar um SMS toohello shortcode 20873 que diz "Habilitar Azure"

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a>Resubscribing tooSMS alertas para todos os grupos de ação
Um usuário pode assinar novamente tooall SMS para alertas para todos os grupos de ação por shortcode respondendo toohello 20873 com qualquer um de saudação palavras-chave a seguir:

* START

Ex.: Um usuário que toounsubscribe de todos os alertas SMS para todos os grupos de ação, poderia enviar um SMS toohello shortcode 20873 que diz "Iniciar"

### <a name="requesting-help-via-sms"></a>Solicitando ajuda por SMS
Um usuário pode pedir para obter mais informações sobre Olá SMS recebeu por resposta toohello shortcode 20873 com qualquer Olá palavras-chave a seguir:
* HELP

Uma resposta será enviada toohello usuário com um artigo de toothis do link.

## <a name="next-steps"></a>Próximas etapas
Obter um [visão geral de alertas de log de atividade](monitoring-overview-alerts.md) e saiba como tooget alerta  
Saiba mais sobre a [limitação de taxa de SMS](monitoring-alerts-rate-limiting.md)  
Saiba mais sobre [grupos de ação](monitoring-action-groups.md)
