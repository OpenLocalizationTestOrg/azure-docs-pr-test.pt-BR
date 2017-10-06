---
title: "aaaAzure identidades do Active Directory híbrida considerações de design - Determine a tarefas de gerenciamento de identidade híbrida | Microsoft Docs"
description: "Com controle de acesso condicional, o Active Directory do Azure verifica condições específicas hello, que você escolhe ao autenticar usuário hello e antes de permitir acesso toohello aplicativo. Quando essas condições forem atendidas, o usuário de Olá é autenticado e acesso toohello aplicativo autorizado."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 65f80aea-0426-4072-83e1-faf5b76df034
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: d3c0e9b23f43127b3d8e0b3a4e8f03d4bc148c27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-hybrid-identity-lifecycle"></a>Plano para o ciclo de vida de identidade híbrida
Identidade é um dos fundamentos de saudação de sua estratégia de acesso de aplicativo e mobilidade empresarial. Se você está entrando no dispositivo móvel tooyour ou aplicativo SaaS, sua identidade é Olá toogaining chave acesso tooeverything. Em seu nível mais alto, uma solução de gerenciamento de identidade abrange Unificando e sincronizar entre os repositórios de identidade que inclui automatizar e centralizar o processo de saudação do provisionamento de recursos. solução de identidade Olá deve ser uma identidade centralizada no local e na nuvem e também usar alguma forma de autenticação centralizada de toomaintain de federação de identidade e com segurança compartilham e colaboram com empresas e usuários externos. Recursos variam de sistemas operacionais e aplicativos toopeople em ou associado a uma organização. Estrutura organizacional pode ser alterado tooaccommodate Olá provisionamento políticas e procedimentos.

Também é importante toohave uma solução de identidade destinam tooempower seus usuários, fornecendo a eles com experiências de autoatendimento tookeep-los produtivos. Sua solução de identidade é mais robusta se possibilita o logon único para usuários em todos os recursos de saudação que precisam acessar os administradores em todos os níveis podem usar procedimentos padronizados para gerenciar as credenciais do usuário. Alguns níveis de administração podem ser reduzidas ou eliminadas, dependendo da gama de saudação de saudação provisionamento de solução de gerenciamento. Além disso, você pode distribuir recursos de administração, manualmente ou automaticamente, entre várias organizações. Por exemplo, um administrador de domínio pode servir somente pessoas hello e recursos nesse domínio. Este usuário pode executar tarefas administrativas e de provisionamento, mas é toodo não autorizado tarefas de configuração, como a criação de fluxos de trabalho.

## <a name="determine-hybrid-identity-management-tasks"></a>Determinar tarefas de gerenciamento de identidade híbrida
Distribuir tarefas administrativas em sua organização melhora a precisão de saudação e a eficácia de administração e melhora o saldo de saudação de carga de trabalho de saudação de uma organização. Seguem pontos Olá que definem um sistema de gerenciamento de identidade robusta.

 ![](./media/hybrid-id-design-considerations/Identity_management_considerations.png)

tarefas de gerenciamento de identidade do toodefine híbrida, você deve entender algumas características essenciais de organização de saudação que adotarão identidade híbridas. É importante toounderstand repositórios de atual hello está sendo usados para fontes de identidade. Conhecendo os elementos principais, você terá requisitos fundamentais hello e com base no que você precisará tooask mais granular de perguntas que levará tooa melhor decisão de design para sua solução de identidade.  

Ao definir esses requisitos, certifique-se de que pelo menos Olá seguintes perguntas foram respondidas

* Opções de provisionamento: 
  
  * Solução de identidade híbrida Olá dá suporte a um sistema de provisionamento e o gerenciamento de acesso à conta robusto?
  * Como são usuários, grupos e senhas vai toobe gerenciado?
  * Gerenciamento de ciclo de vida de identidade hello está respondendo? 
    * Quanto tempo dura a suspensão de conta de atualizações de senha?
* Gerenciamento de licenças: 
  
  * Olá gerenciamento de licença de identificadores de solução de identidade híbrida?
    * Em caso afirmativo, quais recursos estão disponíveis?
* Olá gerenciamento de licença baseada em grupo de identificadores de solução? 
  
      - Em caso afirmativo, é possível tooassign um tooit do grupo de segurança? 
       - Em caso afirmativo, diretório de nuvem Olá atribuirá automaticamente licenças tooall membros de saudação do grupo Olá? 
        - O que acontece se um usuário subsequentemente é adicionado ou removido do grupo de saudação, será uma licença automaticamente atribuída ou removida conforme apropriada? 
* Integração com outros provedores de identidade de terceiros:
* Essa solução híbrida pode ser integrada com a identidade de terceiros provedores tooimplement logon único?
* É possível toounify todos Olá diferentes provedores de identidade em um sistema de identidade coesa?
* Se sim, como, quais são elas e quais recursos estão disponíveis?

## <a name="synchronization-management"></a>Gerenciamento de sincronização
Uma das metas de saudação de um Gerenciador de identidade, toobring capaz de toobe Olá a todos os provedores de identidade e mantê-los sincronizados. Manter dados Olá sincronizados com base em um provedor de identidade mestre autoritativa. Em um cenário de identidade híbrida, com um modelo de gerenciamento sincronizados, gerenciar todas as identidades de usuários e dispositivos em um servidor local e sincronizar contas hello e, opcionalmente, nuvem de toohello de senhas. usuário de saudação insere Olá a mesma senha local como ele faz na nuvem hello e no, Olá senha é verificada pela solução de identidade hello. Esse modelo usa uma ferramenta de sincronização de diretório.

![](./media/hybrid-id-design-considerations/Directory_synchronization.png)Certifique-se de sincronização de saudação do tooproper design de sua solução de identidade híbrida que Olá perguntas a seguir são atendidos: • quais são as soluções de sincronização de saudação disponíveis para solução de identidade híbrida Olá?
• O que são o logon único Olá nos recursos disponíveis?
• Quais são as opções de saudação para federação de identidade entre B2B e B2C?

## <a name="next-steps"></a>Próximas etapas
[Determinar a estratégia de adoção do gerenciamento de identidade híbrida](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)

## <a name="see-also"></a>Consulte também
[Visão geral sobre as considerações de design](active-directory-hybrid-identity-design-considerations-overview.md)

