---
title: Perguntas frequentes sobre integridade de recursos de aaaAzure | Microsoft Docs
description: "Visão geral do Azure Resource Health"
services: Resource health
documentationcenter: dev-center-name
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/05/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fe29b2df1f9fee4b77d0100c7d872df837dc4b4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-faq"></a>Perguntas frequentes sobre o Azure Resource Health
Saiba Olá responde perguntas toocommon sobre integridade de recursos do Azure.

## <a name="what-is-azure-resource-health"></a>O que é o Azure Resource Health?
O Resource Health ajuda a diagnosticar e obter suporte quando um problema do Azure afeta seus recursos. Ele informa sobre integridade de saudação atuais e anteriores de seus recursos e ajuda a mitigar os problemas. O Resource Health fornece suporte técnico quando você precisa de ajuda com problemas de serviço do Azure.  

## <a name="what-is-hello-resource-health-intended-for"></a>O que é destinada a integridade dos recursos de saudação?
Depois que foi detectado um problema com um recurso, integridade de recursos pode ajudá-lo a diagnosticar a causa raiz de saudação. Ele fornece ajuda toomitigate Olá problema e o suporte técnico quando precisar de mais ajuda com problemas de serviço do Azure.

## <a name="what-health-checks-are-performed-by-resource-health"></a>Quais verificações de integridade são realizadas pelo Resource Health?
Integridade de recursos executa várias verificações com base em Olá [tipo de recurso](resource-health-checks-resource-types.md). Essas verificações são projetadas tooimplement três tipos de problemas: 
- Eventos não planejados, por exemplo, uma reinicialização inesperada do host
- Eventos planejados, como atualizações agendadas do sistema operacional host
- Eventos disparados por ações do usuário, por exemplo, um usuário que reinicializa uma máquina virtual

## <a name="what-does-each-of-hello-health-status-mean"></a>O que cada status de integridade Olá significa?
Há três status de integridade diferentes:
- Disponível: Não existem problemas conhecidos no hello plataforma Windows Azure que pode estar impactando esse recurso
- Indisponível: Integridade do recurso detectou problemas que estão afetando recursos Olá
- Desconhecido: Integridade de recursos não é possível determinar a integridade Olá de um recurso porque ele parou de receber informações sobre ele. 

## <a name="what-does-hello-unknown-status-mean-is-something-wrong-with-my-resource"></a>O que Olá média de status desconhecido? Há algo errado com meu recurso?
status de integridade de saudação é definido toounknown quando integridade de recursos para receber informações sobre um recurso específico. Enquanto esse status não é uma indicação definitiva do estado de saudação do recurso hello, nos casos em que você estiver tendo problemas, isso pode indicar que um problema do Azure.

## <a name="how-can-i-get-help-for-a-resource-that-is-unavailable"></a>Como posso obter ajuda para um recurso que não está disponível?
Você pode enviar uma solicitação de suporte da folha de integridade de recursos de saudação. Não é necessário um contrato de suporte com o Microsoft tooopen uma solicitação quando o recurso de saudação não está disponível porque os eventos de plataforma.

## <a name="does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did"></a>O Resource Health diferencia a indisponibilidade causada por problemas de plataforma de uma ação executada por mim?
Sim, quando um recurso não estiver disponível, integridade do recurso identifica causa hello dentro de uma dessas categorias: 
-   Ação iniciada pelo usuário
-   Evento planejado 
-   Evento não planejado

No portal de saudação ações iniciadas pelo usuário são mostradas usando um ícone de notificação azul, enquanto os eventos planejados e são mostrados usando um ícone de aviso vermelho. Mais detalhes são fornecidos no hello [visão geral da integridade de recurso](Resource-health-overview.md).  

## <a name="can-i-integrate-resource-health-with-my-monitoring-tools"></a>Posso integrar o Resource Health com minhas ferramentas de monitoramento?
Integridade do recurso é um toohelp de serviço criado diagnosticar e atenuar problemas de serviço do Azure que afetam seus recursos. Embora você possa usar Olá API de integridade de recursos tooprogrammatically obter status de integridade Olá, é recomendável que você usar métricas toomonitor seus recursos. Quando um problema for detectado, integridade de recursos ajuda a determinar a causa raiz de saudação e orienta você sobre ações tooaddress-los. Visite [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) toolearn mais informações sobre como você pode usar métricas toocheck seus recursos.

## <a name="where-do-i-find-resource-health"></a>Onde encontro o Resource Health?
Depois de efetuar login toohello portal do Azure, há várias maneiras que você pode acessar a integridade de recursos:
- Navegue tooyour recursos. Na navegação do lado esquerdo hello, selecione **integridade de recursos**
- Vá toohello folha de Monitor do Azure.  Na navegação do lado esquerdo hello, selecione **integridade de recursos**.
- Olá abrir **ajuda + suporte** folha selecionando Olá ponto de interrogação no canto superior direito de saudação do portal hello e, em seguida, selecionando **ajuda + suporte**. Quando abre a folha de saudação, selecione **integridade de recursos**

Você também pode usar o hello API de integridade de recursos tooobtain obter informações sobre integridade de saudação de seus recursos.

## <a name="is-resource-health-available-for-all-resource-types"></a>O Resource Health está disponível para todos os tipos de recursos?
Olá lista de verificações de integridade e tipos de recursos com suporte por meio de integridade de recursos pode ser encontrada [aqui](resource-health-checks-resource-types.md).

## <a name="what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not"></a>O que devo fazer se meu recurso estiver aparecendo disponível, mas eu acreditar que não esteja?
Ao verificar a integridade de saudação de um recurso, imediatamente sob o status de integridade Olá você pode clicar em **relatar status de integridade incorreto**. Antes de enviar relatórios de hello, você tem opção de saudação de fornecer detalhes adicionais sobre por que você acha que o status de integridade atual do hello está incorreto.

## <a name="is-resource-health-available-for-all-azure-regions"></a>O Resource Health está disponível para todas as regiões do Azure? 
Integridade de recursos está disponível em todas as áreas do Azure, exceto Olá regiões a seguir:
- US Gov Virginia
- Gov do Iowa nos EUA
- DoD do Leste dos EUA
- DoD Central dos EUA
- Alemanha Central
- Nordeste da Alemanha
- Leste da China
- Norte da China

## <a name="how-is-resource-health-different-from-hello-service-health-dashboard-or-hello-azure-portal-service-notifications"></a>Integridade de recursos é diferente das notificações de serviço do portal do Azure de painel de integridade do serviço ou Olá Olá?
informações de Olá fornecidas pelo recurso de integridade são mais específicas que é fornecido pelo Olá painel de integridade de serviço do Azure.

Enquanto [Status do Azure](https://status.azure.com) e notificações de serviço do portal Olá informá-lo sobre problemas de serviço que afetam um amplo conjunto de clientes (por exemplo, uma região do Azure), a integridade de recursos expõe mais granulares eventos que são relevantes apenas toohello de recurso específico. Por exemplo, se um host for reinicializado inesperadamente, o Resource Health alertará somente os clientes cujas máquinas virtuais estavam em execução nesse host.

É importante toonotice que tooprovide que visibilidade de afetar seus recursos, também eventos superfícies publicados em notificações de serviço de integridade de recursos de eventos completa e Olá painel de integridade do serviço.

## <a name="do-i-need-tooactivate-resource-health-for-each-resource"></a>É necessário tooactivate integridade de recursos para cada recurso?
Não. As informações de integridade estão disponíveis para todos os tipos de recursos disponíveis por meio do Resource Health. 

## <a name="do-we-need-tooenable-resource-health-for-my-organization"></a>Precisamos tooenable integridade de recursos para minha organização?
Não.  Integridade de recursos do Azure é acessível em Olá portal do Azure sem qualquer requisito de instalação.

## <a name="is-resource-health-available-free-of-charge"></a>O Resource Health está disponível gratuitamente?
Sim.  O Azure Resource Health está disponível gratuitamente.

## <a name="what-are-hello-recommendations-that-resource-health-provides"></a>Quais são as recomendações de saudação que fornece integridade de recursos?
Com base no status de integridade de hello, integridade de recursos fornece recomendações com objetivo de saudação de reduzir o tempo de saudação que gasto a solução de problemas. Para os recursos disponíveis, recomendações de saudação se concentrar em como os clientes de problemas mais comuns do toosolve Olá encontram. Se o recurso de saudação não estiver disponível devido tooan evento não planejado do Azure, Olá foco será está ajudando durante e após o processo de recuperação de saudação. 

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre o Resource Health:
-  [Visão geral do Azure Resource Health](Resource-health-overview.md)
-  [Tipos de recurso e verificações de integridade disponíveis por meio do Azure Resource Health](resource-health-checks-resource-types.md)
