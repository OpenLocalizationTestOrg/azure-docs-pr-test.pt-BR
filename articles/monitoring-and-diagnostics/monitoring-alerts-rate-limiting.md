---
title: "limitação de aaaRate para SMS, emails e webhooks | Microsoft Docs"
description: "Entenda como o Azure limita o número de saudação de notificações possíveis de webhook, e-mail ou SMS de um grupo de ação."
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
ms.openlocfilehash: 1cd08a5b982c82bb02e0bf93451aa1fcd9bc34af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a>Taxa de limitação mensagens SMS, emails e postagens de webhook postagens
A limitação de taxa é uma suspensão de notificações que ocorre quando há muitos notificações são enviadas a endereços de email ou número de telefone específico tooa. A limitação de taxa assegura que os alertas sejam gerenciáveis e acionáveis.

regras de saudação para SMS e email são Olá mesmo. limite de taxa de saudação é:

 - **SMS**: 10 mensagens em uma hora.
 - **Email**: 100 mensagens em uma hora.

## <a name="rate-limit-rules"></a>Regras do limite de taxa
- Um determinado número de telefone ou email é limitada ao receber mais mensagens que permite que o limite de saudação de taxa.
- Um número de telefone ou email pode fazer parte de grupos de ações em várias assinaturas. A limitação de taxa aplica-se a todas as assinaturas. Ela se aplica, assim como Olá limite for atingido, mesmo se as mensagens são enviadas de várias assinaturas.  
- Quando um número de telefone ou email é taxa limitada, um adicional de notificação é enviada toocommunicate Olá a limitação de taxa. Olá notificação limitação de taxa de estados quando hello expira.

## <a name="rate-limit-of-webhooks"></a>Limite de taxa de webhooks ##
Não há nenhuma limitação de taxa em vigor para webhooks.

## <a name="next-steps"></a>Próximas etapas ##
* Saiba mais sobre o [comportamento de alertas por SMS](monitoring-sms-alert-behavior.md).
* Obter um [visão geral de alertas de log de atividade](monitoring-overview-alerts.md)e saiba como tooreceive alertas.  
* Saiba como muito[configurar alertas sempre que uma notificação de integridade do serviço é postada](monitoring-activity-log-alerts-on-service-notifications.md).
