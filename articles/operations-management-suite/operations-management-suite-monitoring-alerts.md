---
title: gerenciamento de aaaAlert no monitoramento de produtos da Microsoft | Microsoft Docs
description: "Um alerta indica algum problema que requer atenção de um administrador.  Este artigo descreve as diferenças de saudação em como os alertas são criados e gerenciados no System Center Operations Manager (SCOM) e análise de logs e fornece as práticas recomendadas para aproveitar os dois produtos Olá para uma estratégia de gerenciamento de alertas híbrida."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6572c3f8-78ca-4fa9-8fe1-d0b488590788
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 526a3d92f3b6a5d6dec2f3979a934cc94c13f2e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-alerts-with-microsoft-monitoring"></a>Gerenciando alertas com o monitoramento da Microsoft
Um alerta indica algum problema que requer atenção de um administrador.  Há diferenças marcantes entre o SCOM (System Center Operations Manager) e o Log Analytics no OMS (Operations Management Suite) em termos de como os alertas são criados, como são gerenciados e analisados e como você será notificado de que um problema crítico foi detectado.

## <a name="alerts-in-operations-manager"></a>Alertas no Operations Manager
No SCOM são gerados por regras individuais ou monitores tooindicate um problema específico.  Um monitor pode gerar um alerta quando ele entra em um estado de erro enquanto uma regra pode gerar um alerta tooindicate algum problema crítico que não está diretamente relacionado toohello integridade de um objeto gerenciado.  Pacotes de gerenciamento incluem uma variedade de fluxos de trabalho que criam alertas para o aplicativo hello ou serviço que eles gerenciam.  Parte do processo de saudação de configuração de um novo pacote de gerenciamento é ajuste tooensure que você não recebe alertas excessivas para problemas que não sejam considerados essenciais.

![Exibição de alertas do SCOM](media/operations-management-suite-monitoring-alerts/scom-alert-view.png)

SCOM fornece gerenciamento completo de alerta com alertas com um status que pode ser alterado por administradores como elas funcionam tooresolve problema de saudação.  Quando Olá problema foi resolvido, o administrador Olá define Olá tooclosed alerta quando ele não aparecerá mais nos modos de exibição exibe alertas ativos.  Alertas gerados a partir de monitores podem ser resolvidos automaticamente quando o monitor de saudação retorna tooa o estado íntegro.

![Status do alerta](media/operations-management-suite-monitoring-alerts/scom-alert-status.png)

## <a name="alerts-in-log-analytics"></a>Alertas no Log Analytics
Um alerta no Log Analytics é criado com base em uma consulta de log que é executada automaticamente em intervalos regulares.  É possível criar uma regra de alerta com base em qualquer consulta de log.  Se a consulta de saudação retorna resultados que correspondem aos critérios de saudação que você especificar, um alerta é criado.  Isso pode ser uma consulta específica que cria um alerta se um determinado evento é detectado, ou você pode usar uma consulta mais geral que procura qualquer evento de erro relacionadas tooa determinado aplicativo.

Alertas de análise de log são gravadas toohello repositório do OMS como um evento e podem ser recuperadas com uma consulta de log.  Eles não tem um status como eventos do SCOM para que você pode indicar quando Olá problema foi resolvido.

![Alerta do OMS](media/operations-management-suite-monitoring-alerts/oms-alert.png)

Quando o SCOM é usado como uma fonte de dados para análise de Log, alertas SCOM são gravadas repositório do OMS toohello conforme eles são criados e modificados.  

![Alerta do SCOM](media/operations-management-suite-monitoring-alerts/scom-alert.png)

Olá [solução de gerenciamento de alertas](http://technet.microsoft.com/library/mt484092.aspx) fornece um resumo de alertas ativos e várias consultas comuns tooretrieve diferentes conjuntos de alertas.  Isso proporciona uma análise mais eficiente de seus alertas quando comparado a um relatório no SCOM.  Você pode fazer drill down dos dados do hello resumos toodetailed e criar consultas ad hoc tooretrieve diferentes conjuntos de alertas.

![solução de Gerenciamento de Alertas](media/operations-management-suite-monitoring-alerts/alert-management.png)

## <a name="notifications"></a>Notificações
Notificações no SCOM enviarem um email ou texto na resposta tooalerts que correspondem a critérios específicos.  Você pode criar assinaturas de notificação diferentes com diferentes pessoas notificadas dependendo de critérios, como objeto hello está sendo monitorado, Olá a severidade do alerta hello, tipo de saudação do problema detectado ou Olá hora do dia.

Algumas assinaturas podem ser usada tooimplement uma estratégia completa de notificação para um grande número de pacotes de gerenciamento.

![Alertas do SCOM](media/operations-management-suite-monitoring-alerts/alerts-overview-scom.png)

O Log Analytics pode notificá-lo por email de que um alerta foi criado, definindo uma ação de notificação de email em cada [regra de alerta](http://technet.microsoft.com/library/mt614775.aspx).  Ele não tem capacidade Olá Olá SCOM assinar alertas toomultiple com uma única regra.  Você também precisa toocreate suas próprias regras de alerta como o OMS não fornece qualquer pré-configurado.

![Alertas do Log Analytics](media/operations-management-suite-monitoring-alerts/alerts-overview-oms.png)

Completamente você não pode gerenciar alertas do SCOM em análise de Log embora já que somente você pode modificá-las no Console de operações de saudação.  Apesar disso, o Log Analytics é útil como parte de um processo de gerenciamento de alertas, para fornecer ferramentas de análise das quais o SCOM por si só não dispõe.

## <a name="alert-remediation"></a>Correção de alertas
[Correção](http://technet.microsoft.com/library/mt614775.aspx) refere-se o problema de saudação correto do tooan tentativa tooautomatically identificado por um alerta.

SCOM permite toorun diagnósticos e recuperações no monitor de resposta do tooa entrando em um estado não íntegro.  Isso acontece monitor toohello simultâneos criando Olá alerta.  Diagnósticos e recuperações são normalmente implementadas como um script que é executado no agente de saudação.  Um diagnóstico tentativas toogather obter mais informações sobre Olá problema detectado ao problema de saudação toocorrect tentativas de uma recuperação.

Análise de log permite que você toostart uma [runbook de automação do Azure](https://azure.microsoft.com/documentation/services/automation/) ou ligue para um webhook no alerta de análise de Log de tooa de resposta.  Os runbooks podem conter uma lógica complexa implementada no PowerShell.  script Hello é executado no Azure e pode acessar quaisquer recursos do Azure ou a recursos externos disponíveis da nuvem de saudação.  Automação do Azure tem Olá capacidade tooexecute runbooks em um servidor no seu datacenter local, mas esse recurso não está disponível atualmente ao iniciar o runbook Olá em alertas de análise de tooLog de resposta.

Os runbooks no OMS e recuperações no SCOM pode conter os scripts do PowerShell, mas recuperações são mais difícil toocreate e gerenciar porque elas devem estar contidas em um pacote de gerenciamento.  Os runbooks são armazenados na Automação do Azure, que fornece recursos para criação, teste e gerenciamento de runbooks.

Se você usar o SCOM como uma fonte de dados para análise de Log, você pode criar um alerta de análise de Log usando um tooretrieve de consulta de log SCOM alertas armazenados em Olá repositório do OMS.  Isso lhe permitiria toorun um runbook de automação do Azure no alerta SCOM tooa resposta.  É claro que, como Olá runbook será executado no Azure, isso não seria uma estratégia viável para recuperações de problemas no local.

## <a name="next-steps"></a>Próximas etapas
* Obter detalhes de saudação do [alertas no System Center Operations Manager (SCOM)](https://technet.microsoft.com/library/hh212913.aspx).

