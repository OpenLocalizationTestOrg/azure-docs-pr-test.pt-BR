---
title: "portal inscrição do serviço aaaSelf para colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "As relações entre empresas dá suporte à colaboração B2B do Active Directory do Azure, permitindo que os aplicativos corporativos tooselectively de parceiros de negócios acesso"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a>Portal de autoatendimento para inscrição na colaboração B2B do Azure AD

Os clientes podem fazer muito com recursos internos de saudação que são expostos por meio de nosso administrador de TI [portal do Azure](https://portal.azure.com) e nossa [painel de acesso do aplicativo](https://myapps.microsoft.com) para os usuários finais. Mas também estamos cientes de que as empresas precisam de fluxo de trabalho de integração de saudação toocustomize para B2B usuários toofit as necessidades da sua organização. Eles podem fazer isso com a [nossa API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).

Ao discutir isso com nossos clientes, vimos uma necessidade comum se destacar das outras. Olá convidar organização pode não saber antecipadamente que Olá parceiros externos individuais são que precisam acessar os recursos de tootheir. Quisessem uma maneira para os usuários de empresas parceiras muito inscrever-se com um conjunto de políticas que Olá convidar controles da organização. Esse cenário é possível por meio de nossas APIs, portanto, publicamos um projeto no Github que fez exatamente isso: [exemplo de projeto no Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).

Nosso projeto Github demonstra como as organizações podem usar nossas APIs e fornecem um recurso de inscrição de autoatendimento, baseado em políticas para seus parceiros confiáveis, com as regras que determinam a saudação aplicativos que eles possam acessar. Os usuários do parceiro podem obter acesso tooresources quando necessário, com segurança, sem a necessidade de saudação convidar organização toomanually integrá-los. Você pode facilmente implantar projeto Olá em uma assinatura do Azure de sua escolha.

## <a name="as-is-code"></a>Código no estado em que se encontra

Lembre-se de que esse código é disponibilizado como um exemplo de uso toodemonstrate de convite de saudação do Azure Active Directory B2B API. Ele deve ser personalizado pela sua equipe de desenvolvimento ou por um parceiro e deve ser revisado antes de ser implantado em um cenário de produção.

## <a name="next-steps"></a>Próximas etapas

Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:
* [O que é a colaboração B2B do AD do Azure?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?](active-directory-b2b-admin-add-users.md)
* [Como os operadores de informação adicionam usuários de colaboração B2B?](active-directory-b2b-iw-add-users.md)
* [elementos de saudação do hello email de convite de colaboração B2B](active-directory-b2b-invitation-email.md)
* [Resgate de convite de colaboração B2B](active-directory-b2b-redemption-experience.md)
* [Licenciamento da colaboração B2B do Azure AD](active-directory-b2b-licensing.md)
* [Solução de problemas de colaboração B2B do Azure Active Directory](active-directory-b2b-troubleshooting.md)
* [Perguntas frequentes sobre a colaboração B2B do Azure Active Directory](active-directory-b2b-faq.md)
* [Autenticação multifator para usuários de colaboração B2B](active-directory-b2b-mfa-instructions.md)
* [Adicionar usuários de colaboração B2B sem um convite](active-directory-b2b-add-user-without-invite.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)