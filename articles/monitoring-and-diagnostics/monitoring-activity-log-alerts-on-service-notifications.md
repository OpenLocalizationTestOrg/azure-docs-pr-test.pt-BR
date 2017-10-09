---
title: "alertas de log de atividade aaaReceive em notificações de serviço | Microsoft Docs"
description: "Seja notificado por SMS, email ou webhook quando um serviço do Azure for executado."
author: johnkemnetz
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
ms.author: johnkem
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a>Criar alertas do log de atividades em notificações de serviço
## <a name="overview"></a>Visão geral
Este artigo mostra como tooset o log de atividades de alertas para notificações de integridade do serviço usando Olá portal do Azure.  

Você pode receber um alerta quando o Azure envia tooyour de notificações de integridade do serviço assinatura do Azure. Você pode configurar um alerta de saudação com base em:

- classe de saudação do serviço de notificação de integridade (incidente, manutenção, informações, etc.).
- Olá serviço (s) afetado.
- regiões de saudação afetados.
- status de saudação de notificação de saudação (ativa versus resolvido).
- nível de saudação de notificações de saudação (informação, aviso, erro).

Você também pode configurar que Olá alerta deve ser enviado para:

- Selecione um grupo de ações existente.
- Crie um novo grupo de ações (que pode ser usado posteriormente para futuros alertas).

toolearn mais sobre grupos de ação, consulte [criar e gerenciar grupos de ação](monitoring-action-groups.md).

Para obter informações sobre como alertas de notificação do serviço de integridade tooconfigure usando modelos do Azure Resource Manager, consulte [modelos do Gerenciador de recursos](monitoring-create-activity-log-alerts-with-resource-manager-template.md).

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a>Criar um alerta em uma notificação de integridade do serviço para um novo grupo de ação usando Olá portal do Azure
1. Em Olá [portal](https://portal.azure.com), selecione **Monitor**.

    ![saudação de serviço do "Monitor"](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. Em Olá **log de atividades** seção, selecione **alertas**.

    ![Guia de "Alertas" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. Selecione **adicionar alerta do log de atividade**e preencha os campos de saudação.

    ![Olá comando "Adicionar alerta do log de atividade"](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. Insira um nome no hello **nome do log de atividade alerta** caixa e forneça um **descrição**.

    ![caixa de diálogo "Adicionar alerta do log de atividade" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. Olá **assinatura** caixa autofills com sua assinatura atual. Esta assinatura é alerta de log de atividade de saudação toosave usado. recursos de alerta Olá está toothis implantado assinatura e monitora eventos no log de atividades de saudação para ele.

6. Selecione Olá **grupo de recursos** no qual Olá recursos de alerta é criado. Isso não é um grupo de recursos de saudação que é monitorado pelo alerta hello. Em vez disso, é grupo de recursos de saudação onde o recurso de alerta de saudação está localizado.

7. Em Olá **categoria de evento** selecione **a integridade do serviço**. Opcionalmente, selecione Olá **Service**, **região**, **tipo**, **Status**, e **nível** de serviço notificações de integridade que você deseja tooreceive.

8. Em **alerta via**, selecione Olá **novo** botão do grupo de ação. Insira um nome no hello **nome do grupo de ação** caixa e, em seguida, digite um nome em hello **nome curto** caixa. nome curto de saudação é referenciado em notificações de saudação que são enviadas quando esse alerta será acionado.

9. Defina uma lista de destinatários, fornecendo o receptor de saudação:

    a. **Nome**: insira o nome do destinatário hello, alias ou identificador.

    b. **Tipo de Ação**: selecione SMS, email ou webhook.

    c. **Detalhes**: com base no tipo de ação de saudação escolhido, digite um número de telefone, endereço de email ou webhook URI.

10. Selecione **Okey** toocreate alerta de saudação.

Em poucos minutos, o alerta de hello está ativa e começa tootrigger com base nas condições de saudação especificado durante a criação.

Para obter informações sobre o esquema de webhook Olá para alertas de log de atividade, consulte [Webhooks para atividades do Azure log alertas](monitoring-activity-log-alerts-webhook.md).

>[!NOTE]
>o grupo de ação Olá definido nessas etapas é reutilizável de um grupo existente de ação para todas as definições de alerta futuras.
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a>Criar um alerta em uma notificação de integridade do serviço para um grupo existente, usando Olá portal do Azure

1. Siga as etapas 1 a 7 em Olá anterior seção toocreate a notificação de integridade do serviço. 

2. Em **alerta via**, selecione Olá **existente** botão do grupo de ação. Selecione o grupo de ação apropriado Olá.

3. Selecione **Okey** toocreate alerta de saudação.

Em poucos minutos, o alerta de hello está ativa e começa tootrigger com base nas condições de saudação especificado durante a criação.

## <a name="manage-your-alerts"></a>Gerenciar seus alertas

Depois de criar um alerta, ela é visível no hello **alertas** seção Olá **Monitor** folha. Selecione o alerta de saudação desejado toomanage para:

* Edite-o.
* Exclua-o.
* Desabilitar ou habilitá-lo, se você desejar tootemporarily parar ou continuar a receber notificações de alerta de saudação.

## <a name="next-steps"></a>Próximas etapas
- Saiba mais sobre as [notificações de integridade do serviço](monitoring-service-notifications.md).
- Saiba mais sobre [limitação de taxa de notificação](monitoring-alerts-rate-limiting.md).
- Saudação de revisão [webhook alerta esquema do log de atividade](monitoring-activity-log-alerts-webhook.md).
- Obter um [visão geral de alertas de log de atividade](monitoring-overview-alerts.md)e saiba como tooreceive alertas. 
- Saiba mais sobre [grupos de ação](monitoring-action-groups.md).
