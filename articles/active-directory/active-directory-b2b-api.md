---
title: "aaaAzure B2B do Active Directory personalização e colaboração API | Microsoft Docs"
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
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a>API e personalização da colaboração B2B do Azure Active Directory

Tivemos muitos clientes Conte-nos se quiserem que o processo de convite Olá toocustomize de maneira que funciona melhor para suas organizações. Com nossa API, você pode fazer exatamente isso. [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a>Recursos do convite Olá API
Olá API oferece Olá recursos a seguir:

1. Convidar um usuário com *qualquer* endereço de email.

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. Personalize onde deseja que seus usuários tooland depois de aceitar o convite.

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. Escolha o email de convite padrão toosend hello através de nós

    ```
    "sendInvitationMessage": true
    ```

  com um destinatário da mensagem toohello que você pode personalizar

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. E escolha toocc: pessoas que você deseja tookeep em Olá loop sobre o seu convite a esse parceiro.

5. Ou, personalize o convite e o fluxo de trabalho de integração escolhendo não toosend notificações por meio do AD do Azure.

    ```
    "sendInvitationMessage": false
    ```

  Nesse caso, é obtido um URL de resgate da saudação API que você pode inserir em um modelo de email, mensagem Instantânea ou outro método de distribuição de sua escolha.

6. Por fim, se você for um administrador, você pode escolher o usuário de saudação tooinvite como membro.

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a>Modelo de autorização
Olá API pode ser executado em Olá modos de autorização a seguir:

### <a name="app--user-mode"></a>Modo Aplicativo + Usuário
Nesse modo, quem está usando Olá API necessidades toohave Olá permissões toobe criar convites de B2B.

### <a name="app-only-mode"></a>Modo Somente aplicativo
No contexto do aplicativo somente, Olá aplicativo precisa ser User.ReadWrite.All ou Directory.ReadWrite.All escopos para toosucceed de convite Olá Olá.

Para obter mais informações, consulte: https://graph.microsoft.io/docs/authorization/permission_scopes


## <a name="powershell"></a>PowerShell
É agora possíveis toouse PowerShell tooadd e convidar usuários externos tooan organização facilmente. Crie um convite usando o cmdlet hello:

```
New-AzureADMSInvitation
```

Você pode usar o hello as opções a seguir:

* -InvitedUserDisplayName
* -InvitedUserEmailAddress
* -SendInvitationMessage
* -InvitedUserMessageInfo

Você pode conferir as referência de API do convite Olá em [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

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
