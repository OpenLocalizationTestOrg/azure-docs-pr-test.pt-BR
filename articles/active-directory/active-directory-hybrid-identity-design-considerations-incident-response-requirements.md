---
title: "aaaAzure considerações de design do Active Directory híbrida identidade - determinar requisitos de incidente rResponse | Microsoft Docs"
description: "Determinar os recursos de monitoramento e relatórios para solução de identidade híbrida de saudação que podem ser aproveitadas por IT tootake ações tooidentify e reduzir um possíveis ameaças"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: a3d2a459-599b-4b67-8e51-7369ee25082d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 7084096f318ef461e8331fb6edde1b77d4108466
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-incident-response-requirements-for-your-hybrid-identity-solution"></a>Determinar requisitos de resposta a incidentes para sua solução de identidade híbrida
As organizações de médio ou grandes provavelmente terá um [resposta de incidente de segurança](https://technet.microsoft.com/library/cc700825.aspx) no lugar toohelp IT tomar as ações devidas toohello nível de incidente. sistema de gerenciamento de identidade Olá é um componente importante no processo de resposta a incidentes Olá porque ele pode ser usado toohelp identificar quem executou uma ação específica em relação a destino hello. solução de identidade híbrida Olá deve ser capaz de tooprovide monitoramento e relatórios de recursos que podem ser aproveitados por IT tootake ações tooidentify e reduzir as ameaças potenciais. Em um plano de resposta a incidentes típico terá Olá fases a seguir como parte do plano de saudação:

1. Avaliação inicial.
2. Comunicação do incidente.
3. Controle de danos e redução de riscos.
4. Identificação do que foi comprometido e a gravidade.
5. Preservação de provas.
6. Partes de tooappropriate de notificação.
7. Recuperação do sistema.
8. Documentação.
9. Avaliação de danos e custos.
10. Revisão do processo e do plano.

Durante a identificação de saudação do que era o comprometimento e fase de severidade, será necessário tooidentify Olá sistemas que foram comprometidos, arquivos que foram acessados e determinam a confidencialidade Olá desses arquivos. O sistema de identidade híbrida deve ser capaz de toofulfill tooassist esses requisitos identificar o usuário de saudação que fez essas alterações. 

## <a name="monitoring-and-reporting"></a>Monitoramento e emissão de relatórios
Sistema de identidade Olá muitas vezes também pode ajudar na fase de avaliação inicial, principalmente se o sistema Olá foi construído na auditoria e recursos de relatórios. Durante a avaliação inicial do hello, administrador de TI deve ser capaz de tooidentify uma atividade suspeita ou sistema Olá deve ser capaz de tootrigger automaticamente com base em uma tarefa previamente configurada. Muitas atividades podem indicar um possível ataque, no entanto, em outros casos, um sistema mal configurado pode causar tooa o número de falsos positivos em um sistema de detecção de intrusões. 

sistema de gerenciamento de identidade Olá deve auxiliar tooidentify de administradores IT e relatar as atividades suspeitas. Normalmente, esses requisitos técnicos podem ser atendidos monitorando-se todos os sistemas e tendo um recurso de relatório que possa realçar possíveis ameaças. Usar perguntas de saudação abaixo toohelp você projetar sua solução de identidade híbrida levando em requisitos de resposta a incidentes de consideração:

* Sua empresa tem uma resposta a incidentes de segurança em vigor?
  * Em caso afirmativo, é hello sistema de gerenciamento de identidade atual usado como parte do processo de Olá?
* Sua empresa precisa tooidentify suspeitas em tentativas de logon de usuários em diferentes dispositivos?
* Sua empresa precisa toodetect potencial comprometido credenciais do usuário?
* Sua empresa precisa de acesso e a ação do usuário tooaudit?
* Sua empresa precisa tooknow quando um usuário redefine sua senha?

## <a name="policy-enforcement"></a>Aplicação de políticas
Durante o controle de danos e a fase de redução de risco, é importante tooquickly reduzir os efeitos reais e potenciais Olá um ataque. Essa ação que você terá agora pode fazer diferença de Olá entre a menor e maior. resposta exata Olá dependerá de sua organização e da natureza de saudação do ataque Olá que você enfrenta. Se a avaliação inicial Olá concluiu que uma conta foi comprometida, você precisará tooenforce política tooblock essa conta. Isso é apenas um exemplo em que o sistema de gerenciamento de identidade Olá será utilizado. Use perguntas de saudação abaixo toohelp que projetar sua solução de identidade híbrida enquanto levando em consideração como as políticas serão impostas tooreact tooan em andamento incidente:

* Sua empresa tem políticas tooblock os usuários da rede de saudação de acesso se necessário?
  * Em caso afirmativo, Olá atual solução integrada ao sistema de gerenciamento de identidade Olá híbrida que você está indo tooadopt?
* Sua empresa precisa de acesso condicional tooenforce para usuários que estão em quarentena? 

> [!NOTE]
> Verifique se anotações tootake de cada resposta e entender Olá lógica por trás da resposta de saudação. [Definir a estratégia de proteção de dados](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) irá Olá opções disponíveis e as vantagens/desvantagens de cada opção.  Ao responder essas perguntas, você selecionará a opção que melhor se ajusta às necessidades da sua empresa.
> 
> 

## <a name="next-steps"></a>Próximas etapas
[Definir a estratégia de proteção de dados](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)

## <a name="see-also"></a>Consulte também
[Visão geral sobre as considerações de design](active-directory-hybrid-identity-design-considerations-overview.md)

