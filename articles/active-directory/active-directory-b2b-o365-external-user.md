---
title: "aaaOffice 365 compartilhamento externo e colaboração B2B do Azure Active Directory | Microsoft Docs"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a>Compartilhamento externo do Office 365 e colaboração B2B do Azure Active Directory

Externa de compartilhamento no Office 365 (OneDrive, o SharePoint Online, grupos unificados, etc.) e o Azure Active Directory (AD do Azure) B2B colaboração são tecnicamente Olá mesmo significado. Compartilhamento externo todos (exceto OneDrive/SharePoint Online), inclusive convidados em grupos do Office 365, já usa o convite de colaboração de saudação do Azure AD B2B APIs para o compartilhamento.

O OneDrive/SharePoint Online tem um gerenciador de convite separado. Suporte para compartilhamento externo no OneDrive/SharePoint Online iniciado antes de o Azure AD ter desenvolvido o suporte. Ao longo do tempo, o compartilhamento externo OneDrive/SharePoint Online tem acumulada vários recursos e muitos milhões de usuários que usam o produto de saudação do interno padrão de compartilhamento. No entanto, há algumas diferenças sutis entre o funcionamento do compartilhamento externo do OneDrive/SharePoint Online e a colaboração do Azure AD B2B:

- OneDrive/SharePoint Online adiciona diretório de toohello usuários depois que os usuários têm resgatado seus convites. Portanto, antes de resgate, você não vir o usuário Olá no portal do AD do Azure. Se outro site convida um usuário no hello enquanto isso, é gerado um novo convite. No entanto, quando você usa a colaboração B2B do Azure AD, os usuários são adicionados imediatamente no convite para que eles apareçam em todos os lugares.

- Olá resgate experiência no OneDrive/SharePoint Online é diferente da saudação experiência em colaboração B2B do Azure AD. Depois que um usuário resgata um convite, Olá experiências parecem.

- A colaboração B2B do Azure AD convidou usuários que possam ser escolhidos das caixas de diálogo de compartilhamento do OneDrive/SharePoint Online. Os usuários convidados do OneDrive/SharePoint Online também aparecem no Azure AD após o resgate do convite.

- toomanage externo de compartilhamento no OneDrive/SharePoint Online com colaboração B2B do Azure AD, definir Olá OneDrive/SharePoint Online externo de compartilhamento de configuração muito**apenas permitir compartilhamento com usuários externos já no diretório Olá**. Os usuários podem acessar sites tooexternally compartilhado e escolha de parceiros externos que Olá administrador tenha adicionado. Olá administrador pode adicionar parceiros externos de saudação por meio de saudação convite de colaboração B2B APIs.

![Olá externo de configuração de compartilhamento OneDrive/SharePoint Online](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a>Próximas etapas

Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:

* [O que é a colaboração B2B do AD do Azure?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriedades de usuário de colaboração B2B](active-directory-b2b-user-properties.md)
* [Adicionando uma função de tooa de usuário de colaboração B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegação de convites de colaboração B2B](active-directory-b2b-delegate-invitations.md)
* [Grupos dinâmicos e colaboração B2B](active-directory-b2b-dynamic-groups.md)
* [Código de colaboração B2B e exemplos do PowerShell](active-directory-b2b-code-samples.md)
* [Configurar aplicativos SaaS para colaboração B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokens de usuário de colaboração B2B](active-directory-b2b-user-token.md)
* [Mapeamento de declarações do usuário de colaboração B2B](active-directory-b2b-claims-mapping.md)
* [Limitações atuais da colaboração B2B](active-directory-b2b-current-limitations.md)
