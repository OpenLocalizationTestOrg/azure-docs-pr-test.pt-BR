---
title: "Documentação do Operations Management Suite (OMS) - tutoriais de aaaAzure | Microsoft Docs"
description: "O OMS (Microsoft Operations Management Suite) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda a gerenciar e proteger sua infraestrutura local e de nuvem. Este artigo identifica Olá serviços diferentes incluídos no OMS e fornece links tootheir detalhadas conteúdo."
services: operations-management-suite
author: carolz
manager: carolz
layout: LandingPage
ms.assetid: 
ms.service: operations-management-suite
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: landing-page
ms.date: 01/23/2017
ms.author: carolz
ms.openlocfilehash: 11a8f5ecb3d84aed90554510fc1bb43320fdebb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>O que é Operations Management Suite (OMS)?
O OMS (Microsoft Operations Management Suite) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda a gerenciar e proteger sua infraestrutura local e de nuvem.  Como o OMS é implementado como um serviço baseado em nuvem, é possível colocá-lo em funcionamento com investimentos mínimos em serviços de infraestrutura.  Novos recursos são entregues automaticamente, representando uma economia em manutenção contínua e em custos de atualização.

Além disso tooproviding de serviços importantes no seu próprio, OMS pode integrar com componentes do System Center, como System Center Operations Manager tooextend os investimentos de gerenciamento para a nuvem de saudação.  System Center e o OMS podem trabalhar juntos tooprovide experiência um gerenciamento híbrido completa.

Olá seções a seguir fornece uma descrição de alto nível das áreas de valor diferente de saudação de serviços do OMS e hello que implementação-las.  Você pode consultar tooOMS arquitetura para uma visão geral dos diferentes componentes do OMS Olá antes de examinar Olá informações detalhadas sobre cada um.

## <a name="insight-and-analyticsmediaoperations-management-suite-overviewicon-insight-analyticspng-insight-and-analytics"></a>![Insight and Analytics](media/operations-management-suite-overview/icon-insight-analytics.png) Insight and Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) o ajuda a coletar, correlacionar, pesquisar e agir em relação a dados de desempenho e log gerados por sistemas operacionais e aplicativos. Ele fornece informações operacionais em tempo real usando a pesquisa integrada e painéis personalizados tooreadily analisar milhões de registros em todas as suas cargas de trabalho e servidores, independentemente de sua localização física.

Você pode adicionar facilmente soluções tooLog análise que definem toobe dados coletado e Olá lógica para sua análise.  Soluções podem incluir a funcionalidade adicional que é fornecida automaticamente tooagents com pouca ou nenhuma configuração.  Além disso toousing ferramentas de análise fornecidas pelas soluções individuais, você pode executar pesquisas personalizadas em todo conjunto de dados de saudação dados de pedidos toocorrelate entre sistemas e aplicativos.  

## <a name="automation--controlmediaoperations-management-suite-overviewicon-automation-controlpng-automation--control"></a>![Automação e Controle](media/operations-management-suite-overview/icon-automation-control.png) Automação e Controle
Automação do Azure automatiza processos administrativos com [runbooks](../automation/automation-runbook-types.md) que se baseiam no PowerShell e executar em Olá nuvem do Azure.  Os runbooks podem acessar qualquer produto ou serviço que pode ser gerenciado com o PowerShell, incluindo recursos em outras nuvens como o AWS (Amazon Web Services).  Runbooks também podem ser executados em um servidor de recursos de local de toomanage seu local de data center.

A Automação do Azure fornece o gerenciamento de configuração com o [DSC do PowerShell](../automation/automation-dsc-overview.md).  Você pode criar e gerenciar recursos de DSC hospedados no Azure e aplicá-las no local e toocloud toodefine de sistemas e impor suas configurações.

## <a name="protection-and-recoverymediaoperations-management-suite-overviewicon-protection-recoverypng-protection-and-disaster-recovery"></a>![Proteção e recuperação](media/operations-management-suite-overview/icon-protection-recovery.png) Proteção e recuperação de desastre
[Backup do Azure](http://azure.microsoft.com/documentation/services/backup) protege seus dados de aplicativos e os retém por vários anos, sem nenhum investimento de capital e custos operacionais mínimos.  Ele pode fazer o backup de dados de servidores físicos e virtuais do Windows em cargas de trabalho adição tooapplication como o SQL Server e SharePoint.  Ele também pode ser usado por tooAzure de dados do System Center Data Protection Manager (DPM) tooreplicate protegido para armazenamento de longo prazo e redundância.

[O Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) contribui uma estratégia de recuperação (BCDR) de desastre e continuidade de negócios tooyour ao orquestrar a replicação, failover e recuperação de máquinas de virtuais de Hyper-V locais, máquinas virtuais VMware e Windows físico / Servidores Linux. Você pode replicar máquinas tooa data center secundário ou ampliar seu datacenter ao replicá-lo tooAzure. A Recuperação de Site também fornece failover e recuperação simples para cargas de trabalho. Ela integra mecanismos de recuperação de desastre, como o SQL Server AlwaysOn, e fornece planos de recuperação para failover fácil de cargas de trabalho que são organizadas em camadas em vários computadores.

## <a name="oms-security-and-compliancemediaoperations-management-suite-overviewicon-security-compliancepng-security-and-compliance"></a>![Segurança e Conformidade do OMS](media/operations-management-suite-overview/icon-security-compliance.png) Segurança e Conformidade
Segurança e conformidade ajuda a identificar, avaliar e mitigar riscos de segurança tooyour infraestrutura.  Esses recursos do OMS são implementados por meio de várias soluções de análise de Log que analisam dados de log e a configuração do agente sistemas tooassist você garantir a segurança contínua de saudação do seu ambiente.

* Olá [solução de segurança e auditoria](oms-security-getting-started.md) coleta e analisa os eventos de segurança em uma atividade suspeita tooidentify sistemas gerenciados.
* Olá [solução Antimalware](../log-analytics/log-analytics-malware.md) relata status de saudação de proteção antimalware em sistemas gerenciados.  
* Olá solução atualizações do sistema realiza uma análise das atualizações de segurança de saudação e outras atualizações em seus sistemas gerenciados para que você identifique facilmente os sistemas que exigem a aplicação de patch.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre o [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* Saiba mais sobre a [Automação do Azure](../automation/automation-intro.md).
* Saiba mais sobre o [Backup do Azure](http://azure.microsoft.com/documentation/services/backup).
* Saiba mais sobre o [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).

