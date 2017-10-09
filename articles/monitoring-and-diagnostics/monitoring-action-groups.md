---
title: "aaaCreate e gerenciar grupos de ação no hello portal do Azure | Microsoft Docs"
description: "Saiba como toocreate e gerenciar grupos de ação no hello portal do Azure."
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
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a>Criar e gerenciar grupos de ação no hello portal do Azure
## <a name="overview"></a>Visão geral ##
Este artigo mostra como toocreate e gerenciar grupos de ação no hello portal do Azure.

Você pode configurar uma lista de ações com grupos de ações. Então, esses grupos podem ser usados quando você define alertas de log de atividades. Esses grupos podem ser reutilizados por cada alerta do log de atividade que definir, garantindo que Olá mesmo ações são executadas a cada hora hello atividade log alerta for disparado.

Um grupo pode ter até too10 de cada tipo de ação. Cada ação é composta por Olá propriedades a seguir:

* **Nome**: um identificador exclusivo dentro do grupo de ação de saudação.  
* **Tipo de ação**: envie um SMS, envie um email ou chame um webhook.  
* **Detalhes**: Olá webhook URI, endereço de email ou número de telefone correspondente.

Para obter informações sobre como grupos de ação de tooconfigure toouse do Azure Resource Manager modelos, consulte [modelos do Gerenciador de recursos de grupo de ação](monitoring-create-action-group-with-resource-manager-template.md).

## <a name="create-an-action-group-by-using-hello-azure-portal"></a>Criar um grupo de ação usando Olá portal do Azure ##
1. Em Olá [portal](https://portal.azure.com), selecione **Monitor**. Olá **Monitor** folha consolida todas as suas configurações e dados em uma exibição de monitoramento.

    ![saudação de serviço do "Monitor"](./media/monitoring-action-groups/home-monitor.png)
2. Em Olá **log de atividades** seção, selecione **grupos de ação**.

    ![Guia de "Grupos de ação" Hello](./media/monitoring-action-groups/action-groups-blade.png)
3. Selecione **adicionar grupo de ação**e preencha os campos de saudação.

    ![Olá "Adicionar grupo de ação de" comando](./media/monitoring-action-groups/add-action-group.png)
4. Insira um nome no hello **nome do grupo de ação** caixa e, em seguida, digite um nome em hello **nome curto** caixa. nome curto de saudação é usado no lugar de um nome de grupo de ação completo quando as notificações são enviadas usando esse grupo.

      ![caixa de diálogo do grupo de ação de adicionar Hello"](./media/monitoring-action-groups/action-group-define.png)

5. Olá **assinatura** caixa autofills com sua assinatura atual. Esta assinatura está Olá um no qual grupo de ação de saudação é salvo.

6. Selecione Olá **grupo de recursos** qual ação Olá grupo é salvo.

7. Defina uma lista de ações fornecendo estas ações:

    a. **Nome**: insira um identificador exclusivo para esta ação.

    b. **Tipo de Ação**: selecione SMS, email ou webhook.

    c. **Detalhes**: com base no tipo de ação de hello, insira um número de telefone, endereço de email ou webhook URI.

8. Selecione **Okey** toocreate grupo de ação de saudação.

## <a name="manage-your-action-groups"></a>Gerenciar seus grupos de ação ##
Depois de criar um grupo, ela é visível no hello **grupos de ação** seção Olá **Monitor** folha. Selecione o grupo de ações de saudação desejado toomanage para:

* Adicionar, editar ou remover ações.
* Exclua grupo de ação de saudação.

## <a name="next-steps"></a>Próximas etapas ##
* Saiba mais sobre o [comportamento de alertas por SMS](monitoring-sms-alert-behavior.md).  
* Obter um [entendimento do esquema de webhook alerta do log de atividade de saudação](monitoring-activity-log-alerts-webhook.md).  
* Saiba mais sobre a [limitação de taxa](monitoring-alerts-rate-limiting.md) para alertas. 
* Obter um [visão geral de alertas de log de atividade](monitoring-overview-alerts.md)e saiba como tooreceive alertas.  
* Saiba como muito[configurar alertas sempre que uma notificação de integridade do serviço é postada](monitoring-activity-log-alerts-on-service-notifications.md).
