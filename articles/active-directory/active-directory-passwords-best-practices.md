---
title: "Implementação: Azure AD SSPR | Microsoft Docs"
description: "Dicas para uma distribuição bem-sucedida da redefinição da senha de autoatendimento do Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: f8cd7e68-2c8e-4f30-b326-b22b16de9787
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 73d31679b38ff009a767335adaebc49fbc5a75b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="roll-out-password-reset-for-users"></a>Implementação da redefinição de senha para usuários

A maioria dos clientes siga as etapas de saudação que seguem tooensure uma distribuição suave da funcionalidade SSPR.

1. [Habilitar a redefinição de senha em seu diretório](active-directory-passwords-getting-started.md)
2. [Como configurar permissões do AD locais para write-back de senha](active-directory-passwords-how-it-works.md#active-directory-permissions)
3. [Configurar o write-back de senha](active-directory-passwords-writeback.md#configuring-password-writeback) toowrite senhas do AD do Azure faça tooyour diretório de local
4. [Como atribuir e verificar as licenças necessárias](active-directory-passwords-licensing.md)
5. Se você quiser tooroll gradualmente, você pode, opcionalmente, limite de redefinição de senha tooa grupo de usuários tooroll recurso Olá lentamente ao longo do tempo. toodo isso definido Olá **Self Service senha redefinida habilitado** alternar de **todos** muito**um grupo** e selecione um tooenable do grupo de segurança para redefinição de senha. Olá membros desse grupo devem ter licenças atribuídas toothem e é uma ótima maneira tooenable [grupo com base em licenciamento](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing).
6. Preencher o conjunto mínimo de saudação do [dados de autenticação](active-directory-passwords-data.md), com base em sua política.
7. Ensinar aos seus usuários como toouse SSPR, enviando instruções tooshow-los como tooregister e como tooreset.
    > [!NOTE]
    > Teste a SSPR com um usuário e não como um administrador, uma vez que a Microsoft impõe requisitos de autenticação fortes para contas de administrador do Azure. Para obter mais informações sobre a política de senha de administrador hello, consulte nosso [artigo mergulho profundo](active-directory-passwords-how-it-works.md).

8. Você pode escolher registro tooenforce a qualquer momento e exigem usuários tooreconfirm suas informações de autenticação após um determinado período de tempo. Se não quiser que seu tooregister toohave de usuários, você pode [implantar redefinição de senha sem a necessidade de registro do usuário final](active-directory-passwords-data.md).
9. Ao longo do tempo, examine os usuários Registrando e usando exibindo Olá [reporting fornecidos pelo AD do Azure](active-directory-passwords-reporting.md).

## <a name="email-based-rollout"></a>Distribuição baseada em email

Muitos clientes encontrar que uma campanha de email com instruções de toouse simples é hello mais fácil maneira tooget usuários toouse SSPR. [Você criou três emails simples que você pode usar como modelos toohelp na sua distribuição.](https://onedrive.live.com/?authkey=%21AD5ZP%2D8RyJ2Cc6M&id=A0B59A91C740AB16%2125063&cid=A0B59A91C740AB16)

* **Em breve** toobe modelo usado em semanas hello ou dias antes que os usuários toolet de distribuição sabem que precisam toodo algo de email.
* **Agora disponível** dia de saudação do modelo toobe usado de inicialização toodrive usuários tooregister de email e confirmar seus dados de autenticação para que possam usar SSPR quando necessário.
* **Inscreva-se lembrete** modelo para tooweeks de alguns dias de email após a implantação tooremind usuários tooregister e confirmar seus dados de autenticação.

## <a name="creating-your-own-password-portal"></a>Criando seu próprio portal de senha

Muitos de nossos clientes maior escolha toohost página da Web e criar uma entrada DNS, como https://passwords.contoso.com raiz. Eles preencher a página com links de redefinição de senha toohello AD do Azure, registro, portais de alteração de senha e outras informações específicas da organização de redefinição de senha. Em comunicações por email ou folhetos, você envia, em seguida, você pode incluir uma marca, fácil de lembrar, URL que os usuários podem acessar toowhen precisam toouse serviços de saudação.

* Redefinição de senha do portal - https://passwordreset.microsoftonline.com/
* Portal de registro de redefinição de senha - http://aka.ms/ssprsetup
* Portal de alteração de senha - https://account.activedirectory.windowsazure.com/ChangePassword.aspx

## <a name="using-enforced-registration"></a>Usando o registro imposto

Se você quiser tooregister seus usuários para redefinição de senha, você pode forçá-los tooregister quando entrarem no usando o Azure AD. Você pode habilitar essa opção do seu diretório **de redefinição de senha** folha habilitando Olá **tooRegister solicitar que os usuários ao entrar** opção em Olá **registro** guia.

Os administradores podem exigir registro usuários toore após um período de tempo por configuração Olá **número de dias antes dos usuários frequentes tooreconfirm suas informações de autenticação** entre 0 e 730 dias.

Depois de habilitar essa opção, os usuários de assinatura verá uma mensagem informando que o administrador precisa que eles tooverify suas informações de autenticação.

## <a name="populate-authentication-data"></a>Popular os dados de autenticação

Se você [popular os dados de autenticação para os usuários](active-directory-passwords-data.md), em seguida, os usuários não precisarem tooregister para redefinição de senha antes de ser capaz de toouse SSPR. Como os usuários tiverem dados de autenticação de Olá definidos que atenda a política de redefinição de senha Olá você definiu, os usuários são tooreset capaz de suas senhas.

## <a name="disabling-self-service-password-reset"></a>Desabilitação da redefinição da senha de autoatendimento

Desabilitar a redefinição de senha de autoatendimento é tão simple quanto abrir seu locatário Azure AD e vai muito**de redefinição de senha**, **propriedades**e escolhendo **ninguém** em  **Autoatendimento de redefinição de senha habilitada**

## <a name="next-steps"></a>Próximas etapas

Olá links a seguir fornece informações adicionais sobre a redefinição de senha usando o AD do Azure

* [**Início Rápido**](active-directory-passwords-getting-started.md): comece agora mesmo a usar o gerenciamento de autoatendimento de senhas do Azure AD 
* [**Licenciamento** ](active-directory-passwords-licensing.md) - Configuração do licenciamento do Azure AD
* [**Dados** ](active-directory-passwords-data.md) - entender dados Olá necessários e como ele é usado para gerenciamento de senha
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Olá aparência de saudação SSPR experiência para sua empresa.
* [**Política** ](active-directory-passwords-policy.md) - Como entender e definir políticas de senha do Azure AD
* [**Write-back de senha** ](active-directory-passwords-writeback.md) - Como o write-back de senha opera com o seu diretório local
* [**Relatórios**](active-directory-passwords-reporting.md): descubra se, quando e onde os usuários estão acessando a funcionalidade SSPR
* [**Mergulho profundo técnica** ](active-directory-passwords-how-it-works.md) -vá atrás Olá cortina toounderstand como ele funciona
* [**Perguntas frequentes**](active-directory-passwords-faq.md): como? Por quê? O quê? Onde? Quem? Quando? -Respostas tooquestions você sempre quis tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Saiba como problemas comuns de tooresolve que vemos com SSPR
