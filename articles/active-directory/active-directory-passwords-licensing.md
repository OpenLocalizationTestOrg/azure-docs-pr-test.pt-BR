---
title: 'Licenciamento: SSPR do Azure AD | Microsoft Docs'
description: "Requisitos de licenciamento para redefinição da senha de autoatendimento do Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a>Requisitos de licenciamento para redefinição da senha de autoatendimento do Azure AD

Para que toofunction de redefinição de senha do AD do Azure, você **deve ter pelo menos uma licença atribuída na sua organização**. Não podemos impor Olá experiência de redefinição de senha de licenciamento por usuário. toomaintain conformidade com seu contrato de licença da Microsoft, você precisa de usuários tooassign de tooany de licenças que usam recursos premium.

* **Somente usuários de nuvem** – Qualquer SKU pago do Office 365 (O365) ou Azure AD Basic
* Usuários na **nuvem** e/ou **locais** – Azure AD Premium P1 ou P2, Enterprise Mobility + Security (EMS) ou Secure Productive Enterprise (SPE)

## <a name="licenses-required-for-password-writeback"></a>Licenças necessárias para write-back de senha

Write-back de senha toouse, você deve ter uma saudação após a licenças atribuídas no seu locatário.

* Azure AD Premium P1
* Azure AD Premium P2
* Enterprise Mobility + Security E3
* Enterprise Mobility + Security E5
* Secure Productive Enterprise E3
* Secure Productive Enterprise E5

> [!NOTE]
> Autônomo Office 365 planos de licenciamento por **não oferecem suporte a write-back de senha** e exigir uma saudação anterior planos para toowork essa funcionalidade.

Informações de licenciamento adicionais, incluindo os custos podem ser encontradas no hello páginas a seguir

* [Site de Preços do Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Secure Productive Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a>Habilitar licenciamento com base em grupo ou usuário

AD do Azure agora oferece suporte baseado em grupo licenciamento permitindo licenças tooassign de administradores no grupo de tooa em massa de usuários, em vez de atribuir um de cada vez. [Atribuir, verificar e resolver problemas com licenças](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

Alguns serviços da Microsoft não estão disponíveis em todos os locais. Usuário tooa possa ser atribuídos uma licença, administrador Olá deve especificar a propriedade de "Local de uso" de saudação em usuário hello. Atribuição de licenças pode ser feita em User > perfil > seção configurações Olá portal do Azure. **Ao usar a atribuição do grupo de licença, todos os usuários sem um local de uso especificado herdam o local de saudação do diretório de saudação.**

## <a name="next-steps"></a>Próximas etapas

Olá links a seguir fornece informações adicionais sobre a redefinição de senha usando o AD do Azure

* [**Início Rápido**](active-directory-passwords-getting-started.md): comece agora mesmo a usar o gerenciamento de autoatendimento de senhas do Azure AD 
* [**Dados** ](active-directory-passwords-data.md) - entender dados Olá necessários e como ele é usado para gerenciamento de senha
* [**Distribuição** ](active-directory-passwords-best-practices.md) -planejar e implantar os usuários de tooyour SSPR usando Olá diretrizes encontradas aqui
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Olá aparência de saudação SSPR experiência para sua empresa.
* [**Relatórios**](active-directory-passwords-reporting.md): descubra se, quando e onde os usuários estão acessando a funcionalidade SSPR
* [**Mergulho profundo técnica** ](active-directory-passwords-how-it-works.md) -vá atrás Olá cortina toounderstand como ele funciona
* [**Perguntas frequentes**](active-directory-passwords-faq.md): como? Por quê? O quê? Onde? Quem? Quando? -Respostas tooquestions você sempre quis tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Saiba como problemas comuns de tooresolve que vemos com SSPR

