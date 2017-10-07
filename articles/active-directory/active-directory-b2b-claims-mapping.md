---
title: "declarações de usuário de colaboração de aaaB2B mapeamento no Active Directory do Azure | Microsoft Docs"
description: "referência ao mapeamento de declarações para colaboração B2B do Azure Active Directory"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a>Mapeamento de declarações de usuário de colaboração B2B no Azure Active Directory

Azure Active Directory (AD do Azure) é compatível com personalizando Olá declarações emitidas no token SAML Olá para usuários de colaboração B2B. Quando um usuário se autentica toohello aplicativo, o Azure AD emite um aplicativo de toohello token SAML que contém informações (ou declarações) sobre o usuário Olá que identifica com exclusividade. Por padrão, isso inclui o nome de usuário, endereço de email, nome e sobrenome do usuário hello. Você pode exibir ou editar declarações Olá enviadas em Olá aplicativo de toohello token SAML no guia de atributos de saudação.

Há dois motivos possíveis quais declarações de saudação tooedit emitidas no token SAML Olá pode ser necessário.

1. aplicativo Hello foi gravado toorequire outro conjunto de declaração URIs ou valores de declaração

2. Seu aplicativo requer toobe de declaração NameIdentifier Olá algo diferente de nome principal do usuário Olá armazenado no Active Directory do Azure.

  ![exibir declarações no token SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

Para obter informações sobre como tooadd e editar declarações, confira este artigo sobre a personalização de declarações, [personalizando declarações emitidas no token SAML Olá para aplicativos pré-integrados no Azure Active Directory](develop/active-directory-saml-claims-customization.md). Para usuários da colaboração B2B, o mapeamento de NameID e UPN entre locatários é impedido, por motivos de segurança.


## <a name="next-steps"></a>Próximas etapas

Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:

* [O que é a colaboração B2B do AD do Azure?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriedades de usuário de colaboração B2B](active-directory-b2b-user-properties.md)
* [Adicionando uma função de tooa de usuário de colaboração B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegar convites de colaboração B2B](active-directory-b2b-delegate-invitations.md)
* [Grupos dinâmicos e colaboração B2B](active-directory-b2b-dynamic-groups.md)
* [Código de colaboração B2B e exemplos do PowerShell](active-directory-b2b-code-samples.md)
* [Configurar aplicativos SaaS para colaboração B2B](active-directory-b2b-configure-saas-apps.md)
* [Compartilhamento externo do Office 365](active-directory-b2b-o365-external-user.md)
* [Tokens de usuário de colaboração B2B](active-directory-b2b-user-token.md)
* [Limitações atuais da colaboração B2B](active-directory-b2b-current-limitations.md)
