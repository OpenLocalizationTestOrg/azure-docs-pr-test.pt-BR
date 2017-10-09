---
title: alertas de log de atividade de aaaCreate | Microsoft Docs
description: "Ser notificado por email, SMS e webhook quando ocorrem determinados eventos no log de atividades de saudação."
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
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: ba0716cc12a0b3a0024ee5562a025f3f153f8982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts"></a>Criar alertas do log de atividades

## <a name="overview"></a>Visão geral
Alertas de log de atividade são alertas que ativar quando um novo evento de log de atividade que ocorre atender às condições de saudação especificadas no alerta de saudação. Eles são recursos do Azure e, portanto, podem ser criados usando um modelo do Azure Resource Manager. Eles também podem ser criados, atualizados ou excluídos em Olá portal do Azure. Este artigo apresenta conceitos de saudação dos alertas de log de atividade. Em seguida, mostra como toouse Olá tooset portal do Azure a um alerta em eventos de log de atividade.

Normalmente, você cria os alertas de log de atividade tooreceive notificações quando:

* Alterações específicas ocorrem em recursos na sua assinatura do Azure, grupos de recursos tooparticular geralmente no escopo ou recursos. Por exemplo, convém toobe notificado quando qualquer máquina virtual em myProductionResourceGroup é excluída. Ou, talvez você queira toobe notificado se quaisquer novas funções forem atribuídas tooa usuário em sua assinatura.
* Ocorre um evento de integridade do serviço. Eventos de integridade do serviço incluem uma notificação de incidentes e eventos de manutenção que se aplicam a tooresources em sua assinatura.

Em ambos os casos, um alerta do log de atividade monitora apenas eventos na assinatura Olá no qual Olá alerta é criado.

Você pode configurar um alerta de log de atividade com base em qualquer propriedade de nível superior no objeto JSON de saudação para um evento de log de atividade. No entanto, o portal de saudação mostra opções mais comuns de saudação:

- **Categoria**: Administrativa, Integridade do Serviço, Dimensionamento Automático e Recomendação. Para obter mais informações, consulte [visão geral do log de atividades do Azure Olá](./monitoring-overview-activity-logs.md#categories-in-the-activity-log). toolearn mais informações sobre eventos de integridade do serviço, consulte [receber alertas de log de atividade em notificações de serviço](./monitoring-activity-log-alerts-on-service-notifications.md).
- **Grupo de recursos**
- **Recurso**
- **Tipo de recurso**
- **Nome da operação**: nome de operação de controle de acesso baseado em função do recurso Gerenciador hello.
- **Nível de**: Olá nível de severidade do evento hello (detalhado, informativo, aviso, erro ou crítico).
- **Status**: status de saudação do evento hello, normalmente iniciados, falhou ou foi bem-sucedida.
- **Evento iniciado por**: Olá também conhecido como "chamador". endereço de email de saudação ou identificador de Active Directory do Azure do usuário de saudação que realizou a operação de saudação.

>[!NOTE]
>Você deve especificar pelo menos duas das Olá precedem critérios em seu alerta, com uma categoria de saudação. Você não pode criar um alerta que é ativado sempre que um evento é criado nos logs de atividade de saudação.
>
>

Quando um alerta de log de atividades é ativado, ele usa uma ação toogenerate ações ou notificações de grupo. Um grupo de ações é um conjunto reutilizável de destinatários de notificação, como endereços de email, URLs de webhook ou números de telefone de SMS. receptores de saudação podem ser referenciados de vários toocentralize de alertas e agrupe seus canais de notificação. Quando você define o alerta do log de atividades, tem duas opções. Você pode:

* Use um grupo existente no seu alerta do log de atividades. 
* Crie um novo grupo de ações. 

toolearn mais sobre grupos de ação, consulte [criar e gerenciar grupos de ação no portal do Azure de saudação](monitoring-action-groups.md).

toolearn mais sobre as notificações de integridade do serviço, consulte [receber alertas de log de atividade sobre as notificações de integridade do serviço](monitoring-activity-log-alerts-on-service-notifications.md).

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-hello-azure-portal"></a>Criar um alerta em um evento de log de atividade com um novo grupo de ação usando Olá portal do Azure
1. Em Olá [portal](https://portal.azure.com), selecione **Monitor**.

    ![saudação de serviço do "Monitor"](./media/monitoring-activity-log-alerts/home-monitor.png)
2. Em Olá **log de atividades** seção, selecione **alertas**.

    ![Guia de "Alertas" Hello](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. Selecione **adicionar alerta do log de atividade**e preencha os campos de saudação.

4. Insira um nome no hello **nome do log de atividade alerta** caixa e selecione um **descrição**.

    ![Olá comando "Adicionar alerta do log de atividade"](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. Olá **assinatura** caixa autofills com sua assinatura atual. Esta assinatura está Olá um no qual grupo de ação de saudação é salvo. recurso de alerta de saudação é implantado toothis assinatura e monitores log eventos de atividade dele.

    ![caixa de diálogo "Adicionar alerta do log de atividade" Hello](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. Selecione Olá **grupo de recursos** no qual Olá recursos de alerta é criado. Isso não é um grupo de recursos de saudação que é monitorado pelo alerta hello. Em vez disso, é grupo de recursos de saudação onde o recurso de alerta de saudação está localizado.

7. Opcionalmente, selecione uma **categoria de evento** toomodify Olá filtros adicionais que são mostrados. Para eventos administrativos, filtros de saudação incluem **grupo de recursos**, **recurso**, **tipo de recurso**, **nome da operação**, **Nível**, **Status**, e **evento iniciado por**. Esses valores identificam quais eventos este alerta deverá monitorar.

    >[!NOTE]
    >Você deve especificar pelo menos um dos Olá precedem critérios em seu alerta. Você não pode criar um alerta que é ativado sempre que um evento é criado nos logs de atividade de saudação.
    >
    >

8. Insira um nome no hello **nome do grupo de ação** caixa e, em seguida, digite um nome em hello **nome curto** caixa. nome curto de saudação é usado no lugar de um nome de grupo de ação completo quando as notificações são enviadas usando esse grupo.

9.  Defina uma lista de ações, fornecendo da ação hello:

    a. **Nome**: insira o nome da ação hello, alias ou identificador.

    b. **Tipo de Ação**: selecione SMS, email ou webhook.

    c. **Detalhes**: com base no tipo de ação de hello, insira um número de telefone, endereço de email ou webhook URI.

10. Selecione **Okey** toocreate alerta de saudação.

alerta de saudação leva alguns minutos toofully se propague e, em seguida, se tornar ativa. Ele dispara quando os critérios do alerta Olá correspondem a novos eventos.

Para obter mais informações, consulte [esquema de webhook Olá compreender usada em alertas de log de atividade](monitoring-activity-log-alerts-webhook.md).

>[!NOTE]
>o grupo de ação Olá definido nessas etapas é reutilizável de um grupo existente de ação para todas as definições de alerta futuras.
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-hello-azure-portal"></a>Criar um alerta em um evento de log de atividade para um grupo existente, usando Olá portal do Azure
1. Siga as etapas 1 a 7 em Olá anterior seção toocreate o alerta de log de atividade.

2. Em **notificar**, selecione Olá **existente** botão do grupo de ação. Selecione um grupo existente na lista de saudação.

3. Selecione **Okey** toocreate alerta de saudação.

alerta de saudação leva alguns minutos toofully se propague e, em seguida, se tornar ativa. Ele dispara quando os critérios do alerta Olá correspondem a novos eventos.

## <a name="manage-your-alerts"></a>Gerenciar seus alertas

Depois de criar um alerta, ele está visível na seção de alertas de saudação da folha de Monitor de saudação. Selecione o alerta de saudação desejado toomanage para:

* Edite-o.
* Exclua-o.
* Desabilitar ou habilitá-lo, se você desejar tootemporarily parar ou continuar a receber notificações de alerta de saudação.

## <a name="next-steps"></a>Próximas etapas
- Obtenha uma [visão geral dos alertas](monitoring-overview-alerts.md).
- Saiba mais sobre [limitação de taxa de notificação](monitoring-alerts-rate-limiting.md).
- Saudação de revisão [webhook alerta esquema do log de atividade](monitoring-activity-log-alerts-webhook.md).
- Saiba mais sobre [grupos de ação](monitoring-action-groups.md).  
- Saiba mais sobre as [notificações de integridade do serviço](monitoring-service-notifications.md).
- Criar um [atividade todas as operações de mecanismo de dimensionamento automático em sua assinatura de alerta toomonitor log](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Criar um [atividade todas as operações de escala-em/expansão de dimensionamento automático com falha em sua assinatura de alerta toomonitor log](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
