---
title: "elementos de aaaThe de email de convite de colaboração de saudação do Azure Active Directory B2B | Microsoft Docs"
description: "Modelo de email de convite para colaboração B2B do Azure Active Directory"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: f4908014d71a63442bbdca2182f54c7a79675a82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-elements-of-hello-b2b-collaboration-invitation-email"></a>elementos de saudação do hello email de convite de colaboração B2B

Emails de convite são parceiros de toobring um componente crítico na placa como usuários de colaboração B2B no AD do Azure. Você pode usá-los confiança tooincrease Olá destinatário. Você pode adicionar legitimidade e email toohello prova sociais, toomake destinatário de saudação se sentir confortável com selecionando Olá **começar** botão tooaccept convite de saudação. Essa relação de confiança é que uma chave significa tooreduce fricção de compartilhamento. E você também desejar toomake Olá email aparência excelente!

![Email de convite de B2b do AD do Azure](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-hello-email"></a>Explicando email Olá
Vamos examinar alguns elementos de email Olá para que você saiba a melhor maneira de toouse seus recursos.

### <a name="subject"></a>Assunto
assunto do email Olá Olá segue saudação padrão a seguir: você está convidado toohello &lt;tenantname&gt; organização

### <a name="from-address"></a>Do endereço
Usamos um LinkedIn padrão de saudação do endereço.  Você deve estar claro que é do emissor do convite hello e do qual da empresa e também esclarecer e-mail Olá vêm de um endereço de email da Microsoft. Olá formato é: &lt;nome para exibição do emissor do convite&gt; de &lt;tenantname&gt; (por meio da Microsoft) <invites@microsoft.com&gt;

### <a name="reply-to"></a>Responder Para
Olá resposta-tooemail é definido email do emissor do convite toohello quando disponível, para que responder toohello email envia um email toohello back quem enviou o convite.

### <a name="branding"></a>Identidade visual
Convite Olá emails do seu locatário usam empresa Olá identidade visual que você pode configurar para seu locatário. Se você quiser tootake proveito dessa funcionalidade, [aqui](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) Olá detalhes sobre como tooconfigure-lo. logotipo do banner Olá aparece no email de saudação. Siga o tamanho da imagem hello e instruções de qualidade [aqui](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) para obter melhores resultados. Além disso, o nome de empresa Olá também aparece na Olá chamada tooaction.

### <a name="call-tooaction"></a>Chamar tooaction
Olá chamada tooaction consiste em duas partes: explicando por que o destinatário Olá recebeu mail Olá e o destinatário hello está sendo solicitado toodo sobre ele.
- Olá "por" seção pode ser resolvida usando saudação padrão a seguir: foi convidado tooaccess aplicativos Olá &lt;tenantname&gt; organização

- E hello a seção "o que você está sendo solicitado toodo" é indicada pela presença de saudação do hello **começar** botão. Quando o destinatário Olá foi adicionado sem necessidade de saudação de convites, esse botão não aparecerá.

### <a name="inviters-information"></a>Informações sobre o emissor do convite
nome para exibição do emissor do convite Olá é incluído no email de saudação. E, além disso, se você tiver configurado uma foto de perfil para a sua conta do AD do Azure, Olá convidar email incluirá imagem também. Ambos é tooincrease pretendido confiança do destinatário no email de saudação.

Se você ainda não configurou a foto do perfil, um ícone com iniciais do emissor do convite Olá no lugar de imagem Olá será mostrado:

  ![Exibindo iniciais do emissor do convite Olá](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a>Corpo
corpo da saudação contém a mensagem de saudação do emissor do convite que Olá compõe ou é passado por convite Olá API. Como é uma área de texto, ela não processa marcas HTML por motivos de segurança.

### <a name="footer-section"></a>Seção de rodapé
rodapé Olá contém a marca de empresa do Microsoft hello e permite que o destinatário Olá se Olá email foi enviado de um alias não monitorado. Casos especiais:

- emissor do convite Olá não tem um endereço de email no hello convidar aluguel

  ![imagem do emissor do convite não tem um endereço de email no hello convidar aluguel](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- destinatário de saudação não precisa de convite de saudação tooredeem

  ![Quando o destinatário não precisa tooredeem convite](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a>Próximas etapas

Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:

* [O que é a colaboração B2B do Azure AD](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?](active-directory-b2b-admin-add-users.md)
* [Como os operadores de informação adicionam usuários de colaboração B2B?](active-directory-b2b-iw-add-users.md)
* [Resgate de convite de colaboração B2B](active-directory-b2b-redemption-experience.md)
* [Licenciamento da colaboração B2B do Azure AD](active-directory-b2b-licensing.md)
* [Solução de problemas de colaboração B2B do Azure Active Directory](active-directory-b2b-troubleshooting.md)
* [Perguntas frequentes sobre a colaboração B2B do Azure Active Directory](active-directory-b2b-faq.md)
* [API e personalização da colaboração B2B do Azure Active Directory](active-directory-b2b-api.md)
* [Autenticação multifator para usuários de colaboração B2B](active-directory-b2b-mfa-instructions.md)
* [Adicionar usuários de colaboração B2B sem um convite](active-directory-b2b-add-user-without-invite.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
