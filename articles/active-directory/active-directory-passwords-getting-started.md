---
title: "Início rápido: Azure AD SSPR | Microsoft Docs"
description: "Implantar rapidamente a redefinição da senha de autoatendimento do Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: bde8799f-0b42-446a-ad95-7ebb374c3bec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4fed3a1c690fd6423ee5d3e5baef690d8896fbe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-azure-ad-self-service-password-reset"></a>Início rápido: redefinição da senha de autoatendimento do Azure AD

> [!IMPORTANT]
> **Você está aqui por que está enfrentando problemas para iniciar sessão?** Se sim, [veja aqui como alterar e redefinir sua senha](active-directory-passwords-update-your-own-password.md).

## <a name="rapidly-deploy-self-service-password-reset"></a>Implantar rapidamente a redefinição da senha de autoatendimento

Redefinição de senha de autoatendimento (SSPR) oferece um simples significa para IT administradores tooempower usuários tooreset ou desbloquear suas contas ou senhas. Olá sistema inclui tootrack relatórios detalhado quando os usuários utilizam o sistema Olá junto com as notificações tooalert você toomisuse ou abuso.

Este guia pressupõe que você já tem um locatário do Azure AD de trabalho licenciado ou de avaliação. Se precisar de ajuda para configurar o AD do Azure, consulte o artigo Olá [guia de Introdução ao AD do Azure](https://azure.microsoft.com/trial/get-started-active-directory/).

1. No seu locatário existente do Azure AD, selecione **"Redefinir senha"**

2. De saudação **"Propriedades"** tela sob a opção hello "Self Service senha redefinida habilitado" Escolha uma das seguintes Olá
    * Ninguém - ninguém é toouse capaz de funcionalidade SSPR
    * Somente os membros de um AD do Azure específico de um grupo - grupo que você escolha são toouse capaz de funcionalidade SSPR
    * Todos - todos os usuários com contas no seu locatário do AD do Azure são toouse capaz de funcionalidade SSPR

3. De saudação **"Métodos de autenticação"** tela Escolha
    * Número de métodos necessário tooreset - oferecemos suporte a um mínimo de um ou dois máximo
    * Toousers disponível de métodos - precisamos de pelo menos um, mas é aconselhável toohave uma opção extra disponível
        * **Email** envia um email com um usuário de toohello código configurada do endereço de email de autenticação
        * **Telefone celular** fornece Olá usuário Olá escolha tooreceive uma chamada ou texto com um código tootheir configurado o número de telefone celular
        * **Telefone comercial** configurado pelo usuário de saudação de chamadas com um código tootheir número do telefone comercial
        * **Perguntas de segurança** exige que você toochoose
            * Número de perguntas necessárias tooregister - mínimo Olá para o registro bem-sucedido, que significa que um usuário pode escolher tooanswer toocreate mais um conjunto de perguntas toopull do. Essa opção pode ser definida de 3 a 5 e deve ser maior que ou igual a toohello inúmeros tooreset de perguntas necessárias.
                * Perguntas personalizadas podem ser adicionadas clicando o botão de "Custom" hello quando a seleção de perguntas de segurança
            * Número de perguntas obrigatórias tooreset - pode ser definido de 3 a 5 perguntas toobe respondidas corretamente antes de permitir uma toobe de senha de usuários redefinir ou desbloqueada.

4. RECOMENDADO: **"Personalização"** permite que você toochange hello "Entre em contato com seu administrador" link toopoint tooa página ou endereço de email é definir

5. OPCIONAL: Olá **"Registro"** tela fornece aos administradores opções Olá para:
    * Exigir usuários tooregister ao entrar
    * Número de dias antes dos usuários frequentes tooreconfirm suas informações de autenticação

6. OPCIONAL: Olá **"Notificação"** tela fornece aos administradores opções Olá para:
    * Notificar os usuários sobre as redefinições de senha
    * Notificar todos os administradores quando outros administradores redefinirem suas próprias senhas

**Neste ponto, você configurou a SSPR para seu locatário do Azure AD**. Você pode parar aqui ou continuar em tooconfigure a sincronização de senhas tooan domínio do AD local.

> [!NOTE]
> Teste a SSPR com um usuário e não como um administrador, uma vez que a Microsoft impõe requisitos de autenticação fortes para contas de administrador do Azure. Para obter mais informações sobre a política de senha de administrador hello, consulte nosso [artigo de política de senha](active-directory-passwords-policy.md#administrator-password-policy-differences).

## <a name="configure-synchronization-tooexisting-identity-source"></a>Configurar a origem da sincronização tooexisting identidade

tooenable tooAzure de sincronização de identidade AD local, você precisa tooinstall e configura [do Azure AD Connect](./connect/active-directory-aadconnect.md) em um servidor em sua organização. Esse aplicativo manipula sincronizar usuários e grupos do seu locatário existente do identidade fonte tooyour AD do Azure.

* [Atualizar do DirSync ou o Azure AD Sync tooAzure AD Connect](./connect/active-directory-aadconnect-dirsync-deprecated.md)
* [Introdução ao Azure AD Connect usando configurações expressas](./connect/active-directory-aadconnect-get-started-express.md)
* [Configurar o write-back de senha](active-directory-passwords-writeback.md#configuring-password-writeback) toowrite senhas do AD do Azure faça tooyour diretório de local.

## <a name="disabling-self-service-password-reset"></a>Desabilitação da redefinição da senha de autoatendimento

Desabilitar a redefinição de senha de autoatendimento é tão simple quanto abrir seu locatário Azure AD e vai muito**de redefinição de senha > propriedades** > escolha **nenhum** em **redefinição de senha do serviço de autoatendimento Habilitado**

### <a name="learn-more"></a>Saiba mais
Olá links a seguir fornece informações adicionais sobre a redefinição de senha usando o AD do Azure

* [**Licenciamento** ](active-directory-passwords-licensing.md) - Configuração do licenciamento do Azure AD
* [**Dados** ](active-directory-passwords-data.md) - entender dados Olá necessários e como ele é usado para gerenciamento de senha
* [**Distribuição** ](active-directory-passwords-best-practices.md) -planejar e implantar os usuários de tooyour SSPR usando Olá diretrizes encontradas aqui
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Olá aparência de saudação SSPR experiência para sua empresa.
* [**Política** ](active-directory-passwords-policy.md) - Como entender e definir políticas de senha do Azure AD
* [**Relatórios**](active-directory-passwords-reporting.md): descubra se, quando e onde os usuários estão acessando a funcionalidade SSPR
* [**Mergulho profundo técnica** ](active-directory-passwords-how-it-works.md) -vá atrás Olá cortina toounderstand como ele funciona
* [**Perguntas frequentes**](active-directory-passwords-faq.md): como? Por quê? O quê? Onde? Quem? Quando? -Respostas tooquestions você sempre quis tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Saiba como problemas comuns de tooresolve que vemos com SSPR

## <a name="next-steps"></a>Próximas etapas

Este guia de início rápido, você aprendeu como redefinição de senha de autoatendimento tooconfigure para seus usuários. toocontinue toohello toocomplete portal do Azure que siga estas etapas Olá link abaixo toohello portal.

> [!div class="nextstepaction"]
> [Habilitar a redefinição de senha por autoatendimento](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset)

