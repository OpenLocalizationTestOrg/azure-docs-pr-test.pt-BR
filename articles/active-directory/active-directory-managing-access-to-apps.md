---
title: aaaManaging tooapps de acesso usando o Azure AD | Microsoft Docs
description: "Descreve como o Active Directory do Azure permite que as organizações toospecify Olá aplicativos toowhich cada usuário tem acesso."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: b0829f18-9e57-4107-925d-5f0457d81671
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: b9461b7a1cc8913cd8fb4a4ce0778afe03274935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-access-tooapps"></a>Gerenciando acesso tooapps
Gerenciamento de acesso em andamento, avaliação de uso e relatórios continuam toobe um desafio depois que um aplicativo é integrado ao sistema de identidade da sua organização. Em muitos casos, os administradores de TI ou suporte técnico com tootake uma função ativa em andamento no gerenciamento de aplicativos de tooyour de acesso. Às vezes, a atribuição é executada por uma equipe de TI geral ou de divisão. Geralmente, decisão de atribuição de saudação é tomador de decisão do toobe pretendido delegado toohello business, exigir aprovação antes de IT torna Olá atribuição.  Outras organizações investem na integração com um sistema de gerenciamento automatizado de identidade e acesso existente, como RBAC (controle de acesso baseado em função) ou ABAC (controle de acesso baseado em atributos). Integração de saudação e desenvolvimento de regra tendem toobe especializada e caro. Em cada abordagem de gerenciamento, monitoramento e relatórios exigem um investimento separado, caro e complexo.

## <a name="how-does-azure-active-directory-help"></a>Como o Active Directory do Azure ajuda?
 Gerenciamento do Azure AD oferece suporte a amplo acesso para aplicativos configurados, permitindo que as organizações tooeasily obter políticas de acesso correto Olá desde a atribuição automática, com base em atributo (cenários de ABAC ou RBAC) por meio da delegação e incluindo gerenciamento de administrador. Com o AD do Azure você pode facilmente obter políticas complexas, combinando vários modelos de gerenciamento de um único aplicativo e podem até mesmo usar novamente as regras de gerenciamento entre aplicativos com hello mesmo públicos.

* [Adicionando aplicativos novos ou existentes](active-directory-sso-integrate-saas-apps.md)

 A atribuição de aplicativo do AD do Azure se concentra em dois modos de atribuição principais:

* **Atribuição individual** TI um administrador com permissões de Administrador Global do diretório pode selecionar contas de usuário individuais e conceder a eles acesso toohello aplicativo.
* **A atribuição baseada em grupo (paga somente do AD do Azure)** TI um administrador com permissões de Administrador Global do diretório pode atribuir um aplicativo de toohello de grupo. Acesso de usuários específicos é determinado pelo se eles são membros do grupo de saudação em tempo de saudação tentativa de aplicativo de hello tooaccess. Em outras palavras, um administrador pode efetivamente criar uma regra de atribuição informando "qualquer membro atual da saudação atribuída grupo tem acesso toohello aplicativo". Usando essa opção de atribuição, os administradores podem se beneficiar de qualquer uma das opções de gerenciamento de grupo do Azure AD, incluindo [grupos dinâmicos baseados em atributo](active-directory-accessmanagement-manage-groups.md), grupos de sistema externo (por exemplo, Active Directory local ou Workday) ou grupos gerenciados de autoatendimento ou gerenciados pelo administrador. Um único grupo pode ser facilmente atribuído toomultiple aplicativos, garantindo que os aplicativos com a afinidade de atribuição podem compartilhar as regras de atribuição, reduzindo a complexidade geral do gerenciamento de hello. Observe que esse grupo aninhado associações não têm suporte para a atribuição baseada em grupo tooapplications neste momento.

Usando esses dois modos de atribuição, os administradores podem obter qualquer abordagem de gerenciamento de atribuição desejada.

Com o AD do Azure, uso e relatórios de atribuição é totalmente integrada, habilitar administradores tooeasily relatório em estado de atribuição, erros de atribuição e uso do mesmo.

## <a name="complex-application-assignment-with-azure-ad"></a>Atribuição de aplicativo complexo com o AD do Azure
Considere um aplicativo como o Salesforce. Em muitas organizações, a equipe de vendas é usada principalmente por organizações de marketing e vendas hello. Em geral, membros da equipe de marketing de saudação tem altamente privilegiado tooSalesforce de acesso, enquanto os membros da equipe de vendas Olá tem acesso limitado. Em muitos casos, uma população amplo de operadores de informações ter restringido o acesso toohello aplicativo. Regras de toothese exceções complicam as coisas. Ele geralmente é prerrogativa de saudação do hello marketing ou vendas liderança toogrant de equipes acesso a um usuário ou alterar suas funções independentemente dessas regras genéricas.

Com o AD do Azure, aplicativos como o Salesforce podem ser pré-configurados para logon único (SSO) e provisionamento automatizado. Depois da configuração do aplicativo hello, um administrador pode levar Olá ação única toocreate e atribuir grupos apropriados hello. Neste exemplo, um administrador pode executar Olá atribuições a seguir:

* [Grupos dinâmicos](active-directory-accessmanagement-manage-groups.md) pode ser definido tooautomatically representar todos os membros de equipes de marketing e vendas de saudação usando atributos como departamento ou função:
  
  * Todos os membros de grupos de marketing seriam atribuídos a função "marketing" toohello no Salesforce
  * Todos os membros de vendas da equipe grupos seriam atribuídos a função "vendas" toohello no Salesforce. Um ajuste adicional pode usar vários grupos que representam as equipes de vendas regionais toodifferent Salesforce funções atribuídas.
* mecanismo de exceção Olá tooenable, um grupo de autoatendimento foi criado para cada função. Por exemplo, o grupo de "Exceção de marketing de vendas" de saudação pode ser criado como um grupo de autoatendimento. grupo de saudação pode ser atribuído a função de marketing de vendas toohello e equipe de liderança Olá marketing pode ser feita proprietários. Membros da equipe de liderança marketing Olá podem adicionar ou remover usuários, definir uma política de junção, ou até mesmo aprovar ou negar toojoin de solicitações de usuários individuais. Isso é suportado por meio de uma experiência adequada ao operador de informações que não exige treinamento especializado para os proprietários ou membros.

Nesse caso, todos os usuários atribuídos seria tooSalesforce provisionado automaticamente, conforme elas são grupos adicionados toodifferent que sua atribuição de função deve ser atualizada no Salesforce. Os usuários seriam capaz de toodiscover e acessar a equipe de vendas por meio do painel de acesso de aplicativo do Microsoft hello, os clientes da web do Office, ou até mesmo navegando pela página de logon de Salesforce organizacional tootheir. Os administradores seria tooeasily capaz de exibir uso e atribuição de status usando os relatórios do AD do Azure.

Os administradores podem empregar [acesso condicional do Azure AD](active-directory-conditional-access.md) tooset as políticas de acesso para funções específicas. Essas políticas podem incluir se o acesso é permitido fora do ambiente corporativo hello e até mesmo autenticação multifator ou o acesso ao dispositivo requisitos tooachieve em vários casos.

## <a name="how-can-i-get-started"></a>Como posso começar?
Primeiro, se você ainda não estiver usando o AD do Azure e for um administrador de TI:

* [Experimente!](https://azure.microsoft.com/trial/get-started-active-directory/) - você pode se inscrever em uma avaliação gratuita de 30 dias hoje mesmo e implantar sua primeira solução de nuvem em menos de 5 minutos usando este link

Recursos do AD do Azure que permitem o compartilhamento de contas incluem:

* [Atribuição de grupo](active-directory-accessmanagement-self-service-group-management.md)
* Adicionar aplicativos tooAzure AD
* Introdução à atribuição
* Perguntas frequentes sobre a atribuição de aplicativo
* [Painel/relatórios de uso de aplicativo](active-directory-passwords-get-insights.md)

## <a name="where-can-i-learn-more"></a>Onde posso saber mais?
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [Proteger aplicativos com acesso condicional](active-directory-conditional-access.md)
* [Gerenciamento de grupo de autoatendimento/SSAA](active-directory-accessmanagement-self-service-group-management.md)

