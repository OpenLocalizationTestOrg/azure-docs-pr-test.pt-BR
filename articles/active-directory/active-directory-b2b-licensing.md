---
title: "colaboração aaaAzure B2B do Active Directory licenciamento orientação | Microsoft Docs"
description: "A colaboração do Azure do Azure Active Directory B2B não exige licenças pagas do Azure AD, mas você pode também obter recursos pagos para usuários convidados de B2B"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: sasubram
ms.custom: it-pro
ms.openlocfilehash: 8e15d66209b090bff210674ecdacc88cd642dcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-licensing-guidance"></a>Diretrizes de licenciamento da colaboração B2B do Azure Active Directory

Você pode usar usuários convidados do Azure AD B2B colaboração recursos tooinvite em seu tooallow de locatário do AD do Azure-los tooaccess serviços do AD do Azure e outros recursos em sua organização. Se você deseja que os recursos do tooprovide acesso toopaid AD do Azure, B2B usuários convidados de colaboração devem ser licenciados com licenças de AD do Azure apropriadas. 

Especificamente:
* Os recursos do Azure AD Gratuito estão disponíveis para usuários convidados sem licenciamento adicional.
* Se desejar que os usuários tooB2B de recursos do AD do Azure da toopaid tooprovide acesso, você deve ter suficiente toosupport licenças aos usuários de convidado B2B.
* Um locatário convidar com paga a licença do AD do Azure tem B2B colaboração use direitos tooan adicionais cinco B2B convidado usuários convidados toohello locatário.
* Prezado cliente proprietária Olá convidar locatário deve ser Olá um toodetermine precisam de quantos usuários de colaboração B2B paga recursos do AD do Azure. Dependendo Olá paga do Azure AD recursos que você deseja para os usuários de convidado, você deve ter o suficiente do Azure AD paga licenças de usuários de colaboração B2B do toocover Olá mesma proporção 5:1.

Um usuário convidado da colaboração B2B é adicionado como um usuário de uma empresa parceira, não como um funcionário da sua organização nem como um funcionário de outra empresa do seu conglomerado. Um usuário convidado B2B pode entrar com credenciais externas ou pertencentes à sua organização, conforme descrito neste artigo. 

Em outras palavras, licenciamento B2B é definido não por como autentica o usuário Olá mas em vez pela relação de saudação de organização de tooyour saudação do usuário. Se os usuários não forem parceiros, eles serão tratados de modo diferente nos termos do licenciamento. Eles não são considerados toobe um usuário de colaboração B2B para fins de licenciamento, mesmo se seus UserType está marcado como "Convidado". Eles devem ser licenciados normalmente, com uma licença por usuário. Esses usuários incluem:
* Seus funcionários
* Equipe que se conecta usando identidades externas
* Um funcionário de outra empresa em seu conglomerado


## <a name="licensing-examples"></a>Exemplos de licenciamento
- Um cliente deseja tooinvite 100 B2B colaboração usuários tooits locatário do AD do Azure. Prezado cliente atribui o gerenciamento de acesso e o provisionamento de todos os usuários, mas 50 usuários também exigem o MFA e o acesso condicional. O cliente deve adquirir licenças do Azure AD Basic 10 e 10 toocover de licenças do Azure AD Premium P1 esses usuários B2B corretamente. Se o cliente Olá planos toouse recursos de proteção de identidade com usuários B2B, deve têm Azure AD Premium P2 licenças toocover Olá convidado usuários em Olá mesma proporção 5:1.
- Um cliente tem 10 funcionários que no momento estão licenciados com Azure AD Premium P1. Agora, eles querem tooinvite 60 B2B usuários que exigem a autenticação multifator (MFA). Em regra de licenciamento de 5:1 hello, Prezado cliente deve ter pelo menos 12 toocover de licenças do Azure AD Premium P1 todos os usuários de colaboração B2B 60. Porque eles já tem 10 Premium P1 licenças para seus 10 funcionários, têm direitos tooinvite 50 B2B usuários com recursos Premium P1 como MFA. Neste exemplo, em seguida, eles devem adquirir 2 Premium P1 licenças adicionais toocover Olá 10 B2B colaboração usuários restantes.

> [!NOTE]
> Não é possível ainda tooassign licenças diretamente toohello B2B usuários tooenable esses direitos de usuário de colaboração B2B.

Prezado cliente proprietária Olá convidar locatário deve ser Olá um toodetermine precisam de quantos usuários de colaboração B2B paga recursos do AD do Azure. Dependendo de qual paga recursos do AD do Azure que deseja para os usuários de convidado, você deve ter pagos usuários de colaboração do B2B de toocover de licenças na taxa de 5:1 Olá suficiente do Azure AD. 

## <a name="additional-licensing-details"></a>Detalhes adicionais do licenciamento
- Não é necessário contas de usuário tooactually atribuir licenças tooB2B. Com base na taxa de 5:1 hello, licenciamento é automaticamente calculado e relatado.
- Se não paga a licença do AD do Azure existe no locatário hello, cada direitos de saudação do usuário convidado obtém hello Azure AD gratuito ofertas de edição.
- Se um usuário de colaboração já tem um paga do Azure AD de B2B da licença de sua organização, eles não consomem uma das licenças de colaboração Olá B2B do locatário convidar hello.

## <a name="advanced-discussion-what-are-hello-licensing-considerations-when-we-add-users-from-a-conglomerate-organization-as-members-using-your-apis"></a>Advanced discussão: quais são as considerações sobre licenciamento de saudação quando podemos adicionar usuários de uma organização conglomerada como "membros" usando suas APIs?
Um usuário convidado de B2B é aquele que é convidado de uma toowork de organização de parceiro com a organização de saudação do host. Normalmente, nenhum outro caso além desse é qualificado como B2B, embora use recursos B2B. Vejamos dois casos em particular:

1. Se um anfitrião convida um funcionário usando um endereço de consumidor
  * Este cenário não está em conformidade com nossas políticas de licenciamento e não é recomendado.

2. Se uma organização anfitriã adiciona um usuário de outra organização de conglomerado
  1. Nesse caso, o usuário Olá é convidado usando APIs de B2B, mas neste caso, não é tradicionalmente B2B. Idealmente, deve ter essas organizações convite Olá outros usuários de organizações como membros (nossa API permite que). Nesse caso, licenças tem toobe atribuído membros toothese para eles tooaccess recursos Olá convidar organização.

  2. Algumas organizações podem desejar Olá tooadd toobe de usuários de outros org adicionado como "Convidado" como uma política. Há dois casos distintos aqui:
      * Olá conglomerada organização já estiver usando o AD do Azure e os usuários de saudação convidado são licenciados em Olá outra organização: nesse caso, não esperamos Olá de toofollow tooneed usuários convidados 1:5 fórmula disposta no início deste documento. 

      * Olá conglomerada organização não está usando o AD do Azure ou não possui licenças suficientes: nesse caso, siga Olá fórmula 1:5 disposta no início deste documento.

## <a name="next-steps"></a>Próximas etapas

Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:

* [O que é a colaboração B2B do AD do Azure?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?](active-directory-b2b-admin-add-users.md)
* [Como os operadores de informação adicionam usuários de colaboração B2B?](active-directory-b2b-iw-add-users.md)
* [elementos de saudação do hello email de convite de colaboração B2B](active-directory-b2b-invitation-email.md)
* [Resgate de convite de colaboração B2B](active-directory-b2b-redemption-experience.md)
* [Solução de problemas de colaboração B2B do Azure Active Directory](active-directory-b2b-troubleshooting.md)
* [Perguntas frequentes sobre a colaboração B2B do Azure Active Directory](active-directory-b2b-faq.md)
* [API e personalização da colaboração B2B do Azure Active Directory](active-directory-b2b-api.md)
* [Autenticação multifator para usuários de colaboração B2B](active-directory-b2b-mfa-instructions.md)
* [Adicionar usuários de colaboração B2B sem um convite](active-directory-b2b-add-user-without-invite.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
