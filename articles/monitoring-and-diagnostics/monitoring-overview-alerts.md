---
title: aaaOverview de alertas no Microsoft Azure e Monitor do Azure | Microsoft Docs
description: "Alertas permitem que você toomonitor métricas de recurso do Azure, eventos ou logs e ser notificados quando uma condição especificada for atendida."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a6dea224-57bf-43d8-a292-06523037d70b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: robb
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d080080666fedc9eefda6b35cdea3714785d2223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-alerts-in-microsoft-azure"></a>O que são os alertas no Microsoft Azure?
Este artigo descreve Olá várias fontes de alertas no Microsoft Azure, o que são Olá finalidades desses alertas, seus benefícios e como tooget iniciada com usá-los. Especificamente, ele se aplica a tooAzure Monitor, mas fornece ponteiros tooother serviços com alertas também. Alertas oferecem um método de monitoramento no Azure que permitem a você tooconfigure condições sobre dados e se tornam notificado quando condições Olá encontrar hello mais recentes de dados de monitoramento.

## <a name="taxonomy-of-azure-alerts"></a>Taxonomia de alertas do Azure
A seguir hello Azure usa termos toodescribe alertas e suas funções:
* **Alerta** – uma definição de critérios (uma ou mais regras ou condições) que são ativados quando atendidos.
* **Active** - Olá estado quando hello critérios definidos por um alerta é atendida.
* **Resolvido** - Olá estado quando hello critérios definidos por um alerta não for atendida após anteriormente ter sido atendidos.
* **Notificação** -Olá ação tomada com base de um alerta se torne ativa.
* **Ação** -um receptor de tooa chamada específicos enviado de uma notificação (por exemplo, enviando um endereço ou postar a URL do webhook tooa). As notificações normalmente podem disparar várias ações.

## <a name="alerts-in-different-azure-services"></a>Alertas nos diferentes serviços do Azure
Os alertas estão disponíveis em vários serviços de monitoramento do Azure. Para obter informações sobre como e quando toouse que esses serviços, [consulte este artigo](./monitoring-overview.md). Aqui está uma análise dos tipos de alerta Olá disponíveis no Azure:

| O Barramento de | Tipo de alerta | Serviços com suporte | Descrição |
|---|---|---|---|
| Azure Monitor | [Alertas de métricas](./insights-alerts-portal.md) | [Métricas com suporte do Azure Monitor](./monitoring-supported-metrics.md) | Receber uma notificação quando qualquer métrica de nível de plataforma atende a uma condição específica (por exemplo, % de CPU em uma máquina virtual é maior que 90 para Olá nos últimos 5 minutos). |
| Azure Monitor | [Alertas do log de atividades](./monitoring-activity-log-alerts.md) | Todos os tipos de recursos disponíveis no Azure Resource Manager | Receber uma notificação quando qualquer novo evento no hello [o Log de atividades do Azure](./monitoring-overview-activity-logs.md) corresponde a condições específicas (por exemplo, quando ocorre uma operação "Excluir VM" na myProductionResourceGroup ou quando um novo evento de integridade do serviço com "Ativo" como Olá status será exibido). |
| Application Insights | [Alertas de métricas](../application-insights/app-insights-alerts.md) | Qualquer aplicativo instrumentado toosend dados tooApplication Insights | Receba uma notificação quando qualquer métrica no nível do aplicativo atender a uma condição específica (por exemplo, tempo de resposta do servidor superior a dois segundos). |
| Application Insights | [Alertas de teste da Web](../application-insights/app-insights-monitor-web-app-availability.md) | Qualquer site instrumentado toosend dados tooApplication Insights | Receba uma notificação quando a disponibilidade ou capacidade de resposta de um site estiver abaixo das expectativas. |
| Log Analytics | [Alertas do Log Analytics](../log-analytics/log-analytics-alerts.md) | Qualquer serviço configurado toosend dados para análise de Log | Receba uma notificação quando uma consulta de pesquisa do Log Analytics sobre métricas e/ou dados de evento atender a certos critérios. |

## <a name="alerts-on-azure-monitor-data"></a>Alertas sobre dados do Azure Monitor
Há dois tipos de alertas baseados em dados do Azure Monitor – alertas de métricas e alertas do Log de Atividades.

* **Alertas de métrica** -este alerta é disparado quando o valor Olá de uma métrica especificada cruza um limite que você atribuir. alerta de Hello gera uma notificação quando Olá alerta estiver "ativado" (quando o limite Olá é cruzado e Olá alerta condição), bem como "Por" (quando o limite Olá seja ultrapassado novamente e Olá não condição). Para obter uma lista crescente de métricas disponíveis com suporte do Azure Monitor, consulte [Lista de métricas com suporte no Azure Monitor](monitoring-supported-metrics.md).
* **Alertas do log de atividade** – um alerta do log de streaming que dispara quando um evento do Log de Atividades for gerado correspondendo aos critérios do filtro que você atribuiu. Esses alertas têm apenas um estado, "Ativado", já que o mecanismo de alerta Olá simplesmente se aplica a saudação filtro critérios tooany novo evento. Esses alertas podem ser usado toobecome notificado quando ocorre um novo incidente a integridade do serviço ou quando um usuário ou aplicativo executa uma operação de sua assinatura, por exemplo, "Excluir a máquina virtual".

Para dados de Log de diagnóstico disponíveis por meio do Monitor do Azure, sugerimos dados Olá roteamento em análise de Log e usando um alerta de análise de Log. Olá diagrama a seguir resume fontes de dados no Monitor do Azure e, conceitualmente, como de alerta de dados.

![Alertas explicados](./media/monitoring-overview-alerts/Alerts_Overview_Resource_v4.png)

## <a name="how-do-i-receive-a-notification-on-an-azure-monitor-alert"></a>Como fazer para receber uma notificação em um alerta do Azure Monitor?
Historicamente, os alertas do Azure de serviços diferentes usavam seus próprios métodos de notificação internos. De agora em diante, o Azure Monitor oferece um agrupamento de notificação reutilizável chamado de Grupos de Ações. Grupos de ação de especificam um conjunto de destinatários de uma notificação – qualquer número de endereços de email, números de telefone (de SMS) ou URLs de webhook – e sempre que um alerta for ativado referências Olá grupo de ação, todos os destinatários recebem essa notificação. Isso permite que você tooreuse um agrupamento de destinatários (por exemplo, sua na chamada engenheiro lista) em vários objetos de alerta. Atualmente, apenas os alertas do Log de Atividades usam os Grupos de Ação, mas vários outros tipos de alerta do Azure também estão trabalhando para usar os Grupos de Ação.

Grupos de ação de dar suporte à notificação pelo lançamento de URL do webhook tooa em endereços de tooemail adição e números SMS. Isso permite a automação e a correção, por exemplo, usando:
    - Runbook de Automação do Azure
    - Azure Function
    - Aplicativo lógico do Azure
    - um serviço de terceiros

Alertas de métricas ainda não usam Grupos de Ação. Em um alerta de métrica individual, você pode configurar notificações para:
* Envie email notificações toohello serviço administrador, administradores tooco ou tooadditional endereços de email que você especificar.
* Chame um webhook, que permite que você toolaunch ações de automação adicionais.

## <a name="next-steps"></a>Próximas etapas
Obter informações sobre as regras de alerta e sobre como configurá-las usando:

* Saiba mais sobre [Métricas](monitoring-overview-metrics.md)
* Configurar [alertas de métrica por meio do Portal do Azure](insights-alerts-portal.md)
* Configurar o [PowerShell de alertas de métrica](insights-alerts-powershell.md)
* Configurar a [CLI (interface de linha de comando) de alertas de métrica](insights-alerts-command-line-interface.md)
* Configurar a [API REST do Azure Monitor de alertas de métrica](https://msdn.microsoft.com/library/azure/dn931945.aspx)
* Saiba mais sobre o [Log de Atividades](monitoring-overview-activity-logs.md)
* Configurar [alertas do Log de Atividades por meio do Portal do Azure](monitoring-activity-log-alerts.md)
* Configurar [alertas do Log de Atividades por meio do Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* Saudação de revisão [esquema webhook alerta do log de atividade](monitoring-activity-log-alerts-webhook.md)
* Saiba mais sobre as [Notificações de Serviço](monitoring-service-notifications.md)
* Saiba mais sobre [Grupos de Ação](monitoring-action-groups.md)
