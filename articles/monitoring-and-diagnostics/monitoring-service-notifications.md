---
title: "aaaWhat são as notificações de integridade do serviço | Microsoft Docs"
description: "As notificações de integridade do serviço permitem que mensagens de integridade do serviço tooview publicar pelo Microsoft Azure."
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
ms.openlocfilehash: 6f2fe72154c3e80d85062655c49dd1799b718e3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-health-notifications"></a>Notificações de integridade do serviço
## <a name="overview"></a>Visão geral

Este artigo mostra como notificações de integridade do serviço tooview usando Olá portal do Azure.

As notificações de integridade do serviço permitem que você tooview integridade mensagens do serviço publicadas pelo Olá, equipe do Azure que possa estar afetando recursos Olá em sua assinatura. Essas notificações são uma subclasse de atividade de log de eventos e também podem ser encontradas na folha de log de atividade de saudação. As notificações de integridade do serviço podem ser informativos ou acionáveis dependendo da classe hello.

Há cinco classes de notificações de integridade do serviço:  

- **Ação necessária:** de tempo tootime pode percebemos algo incomum acontecer em sua conta. Talvez seja necessário toowork com você tooremedy isso. Você receberá uma notificação ou detalhando ações Olá precisará tootake ou com detalhes sobre como toocontact Azure engenharia ou suporte.  
- **Recuperação Assistida:** um evento ocorreu e os engenheiros confirmaram que você ainda está sofrendo um impacto. Engenharia precisará toowork com você diretamente toobring toorestoration seus serviços.  
- **Incidente:** um serviço de evento que está afetando atualmente está afetando um ou mais dos recursos de saudação em sua assinatura.  
- **Manutenção:** esta é uma notificação informando de uma atividade de manutenção planejada que pode afetar um ou mais dos recursos de saudação em sua assinatura.  
- **Informações:** de tempo tootime podemos enviar notificações tooyou uma comunicação sobre otimizações possíveis que podem ajudar a melhora a utilização de recursos.  
- **Segurança:** informações urgentes relacionadas à segurança sobre suas soluções em execução no Azure.

Cada notificação de integridade do serviço terá detalhes nos recursos de tooyour de escopo e impacto de saudação. Os detalhes incluirão:

Nome da Propriedade | Descrição
-------- | -----------
canais | É uma saudação valores a seguir: "Admin", "Operação"
correlationId | É geralmente um GUID no formato de cadeia de caracteres de saudação. Eventos que pertencem a mesma ação uber geralmente compartilham de toohello Olá mesma correlationId.
eventDataId | É o identificador exclusivo de saudação de um evento
eventName | É o título de saudação do evento Olá
level | Nível de evento hello. Uma saudação valores a seguir: "Crítico", "Error", "Aviso", "Informativo" e "Detalhado"
resourceProviderName | Nome do provedor de recursos Olá Olá afetado recursos
resourceType| tipo de saudação do recurso de saudação afetado recursos
subStatus | Geralmente Olá código de status HTTP da saudação correspondente chamada REST, mas também pode incluir outras cadeias de caracteres que descrevam um substatus, como esses valores comuns: Okey (código de Status HTTP: 200), criado (código de Status HTTP: 201), aceito (código de Status HTTP: 202), nenhum conteúdo (HTTP Código de status: 204), solicitação incorreta (código de Status HTTP: 400), não encontrado (código de Status HTTP: 404), conflito (código de Status HTTP: 409), erro de servidor interno (código de Status HTTP: 500), o Service não está disponível (código de Status HTTP: 503), tempo limite do Gateway (código de Status HTTP: 504).
eventTimestamp | Evento Olá correspondente de solicitação de carimbo de hora do evento Olá foi gerado pelo Olá Olá de processamento de serviço do Azure.
submissionTimestamp |   Carimbo de hora do evento Olá se tornaram disponível para consulta.
subscriptionId | Olá assinatura do Azure na qual este evento foi registrado
status | Cadeia de caracteres que descreve o status de saudação da operação de saudação. Alguns valores comuns são: Iniciado, Em Andamento, Êxito, Falha, Ativo, Resolvido.
operationName | Nome da operação de saudação.
categoria | “ServiceHealth”
resourceId | Id do recurso da saudação afetados recursos.
Properties.title | Olá localizado título para essa comunicação. Inglês é o idioma padrão de saudação.
Properties.communication | Olá localizado detalhes de comunicação de saudação com marcação HTML. Inglês é o padrão de saudação.
Properties.incidentType | Possíveis valores: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security
Properties.trackingId | Identifica o incidente Olá que esse evento está associado. Use este incidente de tooan relacionados toocorrelate Olá eventos.
Properties.impactedServices | Um blob com caracteres de escape do JSON que descreve os serviços de saudação e regiões que são afetados pelo incidente de saudação. Uma lista de Services, que, individualmente, tem um ServiceName e uma lista de ImpactedRegions, que têm um RegionName.
Properties.defaultLanguageTitle | comunicação de saudação em inglês
Properties.defaultLanguageContent | comunicação de saudação em inglês como marcação html ou como texto sem formatação
Properties.stage | Os possíveis valores para AssistedRecovery, ActionRequired, Information, Incident e Security são Active e Resolved. Para Maintenance, eles são: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete
Properties.communicationId | comunicação Olá esse evento está associado.


## <a name="viewing-your-service-health-notifications-in-hello-azure-portal"></a>Exibir as notificações de integridade do serviço no hello portal do Azure
1.  Em Olá [portal](https://portal.azure.com), navegar toohello **Monitor** serviço

    ![Monitoramento](./media/monitoring-service-notifications/home-monitor.png)
2.  Clique em Olá **Monitor** tooopen opção a folha de Monitor de saudação. Esta folha reúne todas as suas configurações e dados de monitoramento em uma exibição consolidada. Ele é aberto pela primeira vez toohello **log de atividades** seção.

3.  Agora clique na seção **Notificações de Serviço**

    ![Monitoramento](./media/monitoring-service-notifications/service-health-summary.png)
4.  Clique em qualquer um dos tooview de itens de linha hello mais detalhes

5. Clique em Olá **+ Adicionar atividade de Log de alerta** operação tooreceive notificações tooensure você será notificado para notificações de serviço futuras desse tipo. mais informações sobre como configurar alertas em notificações de serviço de toolearn [clique aqui](monitoring-activity-log-alerts-on-service-notifications.md)

## <a name="next-steps"></a>Próximas etapas:
Receber [notificações de alerta sempre que uma notificação de integridade do serviço](monitoring-activity-log-alerts-on-service-notifications.md) é postada  
Saiba mais sobre os [alertas do log de atividades](monitoring-activity-log-alerts.md)
