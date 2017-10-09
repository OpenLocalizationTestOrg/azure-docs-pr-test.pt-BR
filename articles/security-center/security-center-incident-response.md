---
title: "aaaRespond toosecurity incidentes com a Central de segurança do Azure | Microsoft Docs"
description: "Este documento explica como toouse segurança do Azure Center para um cenário de resposta a incidentes."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 8af12f1c-4dce-4212-8ac4-170d4313492d
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: aaf50c0c7e774d03d517c3fd11686dbae48dd29b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-security-center-for-an-incident-response"></a>Usando a Central de Segurança do Azure para uma resposta a incidentes
Muitas organizações Saiba como incidentes de toosecurity toorespond somente depois de sofrer um ataque. tooreduce custos e danos, é importante toohave uma resposta a incidentes plano em vigor antes que um ataque ocorra. A Central de Segurança do Azure pode ser usada em diferentes estágios de uma resposta a incidentes.

## <a name="incident-response-planning"></a>Planejamento de resposta a incidentes
Um plano eficaz depende de três principais recursos: ser capaz de tooprotect, detectar e responder toothreats. Proteção é sobre a prevenção de incidentes, a detecção é sobre como identificar ameaças no início e resposta está prestes a remover invasor hello e restaurar os impactos de saudação toomitigate sistemas de uma violação.

Este artigo usará estágios de resposta a incidentes de segurança Olá da saudação [resposta de segurança do Microsoft Azure na nuvem de saudação](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678) artigo, conforme mostrado no diagrama a seguir de saudação:

![Ciclo de vida da resposta a incidentes](./media/security-center-incident-response/security-center-incident-response-fig1.png)

Você pode usar a Central de segurança durante os estágios de detectar, avaliar e diagnosticar hello. Aqui estão exemplos de como a Central de segurança pode ser útil durante três estágios de resposta a incidentes inicial hello:

* **Detectar**: revisar a primeira indicação saudação de uma investigação de eventos.
  * Exemplo: revisão saudação inicial verificação que um alerta de segurança de alta prioridade foi gerado no painel central de segurança de saudação.
* **Avaliar**: executar Olá avaliação inicial tooobtain obter mais informações sobre atividades suspeitas hello.
  * Exemplo: obter mais informações sobre o alerta de segurança hello.
* **Diagnosticar**: conduzir uma investigação técnica e identificar estratégias de contenção, atenuação e solução.
  * Exemplo: execute as etapas de correção de saudação descritas pela Central de segurança nesse alerta de segurança específico.

cenário Olá seguinte mostra como a Central de segurança tooleverage durante Olá detectar, avaliar e diagnosticar/responder estágios de um incidente de segurança. Na Central de Segurança, um [incidente de segurança](security-center-incident.md) é uma agregação de todos os alertas de um recurso que se alinham com os padrões da [cadeia de desativações](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) . Incidentes aparecem na Olá [alertas de segurança](security-center-managing-and-responding-alerts.md) lado a lado e folha. Um incidente revela a lista de saudação de alertas relacionados, que permite que você tooobtain obter mais informações sobre cada ocorrência. Central de segurança também apresenta autônomo alertas de segurança também podem ser usado tootrack para baixo de uma atividade suspeita.

## <a name="scenario"></a>Cenário
A Contoso migrado recentemente alguns dos seu tooAzure de recursos locais, incluindo algumas cargas de trabalho de linha de negócios baseados em máquina virtual e os bancos de dados SQL. No momento, a principal Equipe de Resposta a Incidentes de Segurança de Computação (CSIRT) da Contoso tem um problema para investigar os problemas de segurança devido à inteligência de segurança não estar integrada em suas ferramentas atuais de resposta a incidentes. Esta falta de integração apresenta um problema durante a saudação detectar estágio (muitos falsos positivos), bem como durante a saudação avaliar e diagnosticar estágios. Como parte da migração, eles decidiram tooopt para a Central de segurança toohelp-los resolva esse problema.

Olá primeira fase da migração terminar depois de serem incorporados todos os recursos e resolvidas todas as recomendações de segurança de saudação da Central de segurança. Contoso CSIRT é o ponto focal de saudação para lidar com incidentes de segurança do computador. equipe de saudação consiste em um grupo de pessoas com a responsabilidade de lidar com qualquer incidente de segurança. os membros da equipe Olá definiu claramente tooensure tarefas que nenhuma área de resposta é deixada coberto.

Finalidade Olá neste cenário, vamos toofocus nas funções de saudação do hello personas que fazem parte da Contoso CSIRT a seguir:

![Ciclo de vida da resposta a incidentes](./media/security-center-incident-response/security-center-incident-response-fig2.png)

A Laura está no setor de operações de segurança. Suas responsabilidades incluem:

* Monitorando e respondendo toosecurity ameaças em torno de relógio Olá.
* Escalonando toohello proprietário de carga de trabalho de nuvem ou analista de segurança conforme necessário.

Sam é analista de segurança e suas responsabilidades incluem:

* Investigar os ataques.
* Corrigir os alertas.
* Trabalhando com toodetermine de proprietários da carga de trabalho e aplicar atenuantes.

Como você pode ver, Judy e Sam têm responsabilidades diferentes, e eles devem trabalhar juntos tooshare informações de Central de segurança.

## <a name="recommended-solution"></a>Solução recomendada
Como Janete e Sam tem funções diferentes, eles usará áreas diferentes de informações do Centro de segurança tooobtain relevantes para suas atividades diárias. Laura usará os **Alertas de Segurança** como parte do seu monitoramento diário.

![Alertas de segurança](./media/security-center-incident-response/security-center-incident-response-fig3.png)

Janete usará alertas de segurança durante a saudação detectar e estágios de avaliação. Após Judy avaliação inicial hello, ela pode encaminhar Olá problema tooSam se investigação adicional é necessária. Neste ponto, Sam usará Olá informações fornecidas pela Central de segurança, às vezes, em conjunto com outras fontes de dados, toomove toohello diagnosticar estágio.

## <a name="how-tooimplement-this-solution"></a>Como tooimplement nesta solução
toosee como você deseja usar a Central de segurança do Azure em um cenário de resposta a incidentes, vamos siga etapas de Judy estágios de detectar e avaliar Olá e, em seguida, veja o que faz o Sam toodiagnose problema de saudação.

### <a name="detect-and-assess-incident-response-stages"></a>Estágios de resposta a incidentes para detecção e avaliação
Janete conectado toohello portal do Azure e está trabalhando no console do hello Central de segurança. Como parte de seu diário de monitoramento de atividades, ela iniciou a revisão de segurança de alta prioridade Olá de alertas executando as etapas a seguir:

1. Clique em Olá **alertas de segurança** Olá lado a lado e acesso **alertas de segurança** folha.
    ![Folha Alerta de segurança](./media/security-center-incident-response/security-center-incident-response-fig4.png)

   > [!NOTE]
   > Para finalidade Olá neste cenário, Judy é contínuo tooperform uma avaliação de alerta de atividade de SQL mal-intencionado hello, como visto no hello anterior figura.
   >
   >
2. Clique em hello **atividade mal-intencionada SQL** de alerta e analise os recursos de saudação atacado em hello **atividade mal-intencionada SQL** folha: ![detalhes do incidente](./media/security-center-incident-response/security-center-incident-response-fig5.png)

    Nessa folha, Judy pode fazer anotações em relação aos recursos de saudação atacado, como quantas vezes esse ataque aconteceu e quando ele foi detectado.
3. Clique em Olá **atacados recurso** tooobtain obter mais informações sobre esse ataque.

Depois de ler a descrição de hello, Judy é convencida que isso não é um falso positivo e que ela deve escalonar tooSam neste caso.

### <a name="diagnose-incident-response-stage"></a>Estágio para diagnosticar a resposta a incidentes
SAM recebe caso Olá de Janete e começa a analisar as etapas de correção de saudação sugerida Central de segurança.

![Ciclo de vida da resposta a incidentes](./media/security-center-incident-response/security-center-incident-response-fig6.png)

### <a name="additional-resources"></a>Recursos adicionais
equipe de resposta a incidentes Olá também pode tirar proveito da saudação [Power BI do Centro de segurança](security-center-powerbi.md) recurso toosee diferentes tipos de relatórios. Esses relatórios podem ajudá-los durante toovisualize de investigação adicional, analisar e filtrar as recomendações e alertas de segurança. Para empresas que usam suas informações de segurança e a solução de gerenciamento (SIEM) de evento durante o processo de investigação hello, eles também podem [integrar a Central de segurança com sua solução](security-center-integrating-alerts-with-log-integration.md). Você também pode integrar os logs de auditoria do Azure e eventos de segurança de máquina virtual (VM) usando Olá [ferramenta de integração do Azure log](https://blogs.msdn.microsoft.com/azuresecurity/2016/07/21/microsoft-azure-log-integration-preview/). tooinvestigate um ataque, você pode usar essas informações em conjunto com as informações de saudação que fornece a Central de segurança.

## <a name="conclusion"></a>Conclusão
Montar uma equipe antes que ocorra um incidente é muito importante tooyour organização e positivamente influenciarão como são tratados os incidentes. Olá ferramentas toomonitor recursos podem ajudar a tooremediate de instruções precisas de tootake essa equipe um incidente de segurança. Central de segurança [recursos de detecção](security-center-detection-capabilities.md) pode ajudar a incidentes de toosecurity TI tooquickly responder e corrigir problemas de segurança.
