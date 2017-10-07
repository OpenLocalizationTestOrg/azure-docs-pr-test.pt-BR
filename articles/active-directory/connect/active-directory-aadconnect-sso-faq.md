---
title: "Azure AD Connect: Logon Único Contínuo – perguntas frequentes | Microsoft Docs"
description: Toofrequently respostas perguntas frequentes sobre o Azure Active Directory perfeita Single Sign-On.
services: active-directory
keywords: "o que é o Azure AD Connect, instalar o Active Directory, componentes necessários do Azure AD, SSO, Logon Único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: e91e7950670633c08c180ece873f7451fa19eef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-frequently-asked-questions"></a>Logon Único Contínuo do Azure Active Directory: perguntas frequentes

Neste artigo abordamos perguntas frequentes sobre o Logon Único Contínuo do Azure Active Directory (SSO contínuo). Continue verificando para ver novo conteúdo.

>[!IMPORTANT]
>recurso de SSO contínuo Hello está atualmente em visualização.

## <a name="what-sign-in-methods-do-seamless-sso-work-with"></a>Com quais métodos de entrada o SSO Contínuo funcionam?

SSO contínuo pode ser combinado com qualquer Olá [sincronização de Hash de senha](active-directory-aadconnectsync-implement-password-synchronization.md) ou [autenticação de passagem](active-directory-aadconnect-pass-through-authentication.md) métodos de entrada. No entanto esse recurso não pode ser usado com os Serviços de Federação do Active Directory (ADFS).

## <a name="is-seamless-sso-a-free-feature"></a>O SSO Contínuo é um recurso gratuito?

SSO contínuo é um recurso gratuito e não é necessário qualquer edições pagas do AD do Azure toouse-lo. Ele permanece livre quando Olá recurso alcança disponibilidade geral.

## <a name="what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso"></a>Quais aplicativos tiram proveito da capacidade de parâmetro `domain_hint` ou `login_hint` do SSO Contínuo?

Estamos no processo de saudação de compilação Olá lista de aplicativos que enviam esses parâmetros e hello aqueles que não. Se você tiver aplicativos que estão interessados, fale na seção de comentários de saudação.

## <a name="does-seamless-sso-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>Oferece suporte a SSO contínuo `Alternate ID` como Olá nome de usuário, em vez de `userPrincipalName`?

Sim. Oferece suporte a SSO contínuo `Alternate ID` como Olá username quando configurado no Azure AD Connect, conforme mostrado [aqui](active-directory-aadconnect-get-started-custom.md). Nem todos os aplicativos do Office 365 dão suporte ao `Alternate ID`. Consulte a documentação do toohello do aplicativo específico de declaração de suporte de saudação.

## <a name="i-want-tooregister-non-windows-10-devices-with-azure-ad-without-using-ad-fs-can-i-use-seamless-sso-instead"></a>Desejo tooregister não - Windows 10 dispositivos com o Azure AD, sem o uso do AD FS. Posso usar o SSO Contínuo em vez disso?

Sim, esse cenário precisa da versão 2.1 ou posterior do hello [cliente de ingresso](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="how-can-i-roll-over-hello-kerberos-decryption-key-of-hello-azureadssoacct-computer-account"></a>Como pode sobrepor chave de descriptografia Olá Kerberos de saudação `AZUREADSSOACCT` conta de computador?

É importante toofrequently sobrepor a chave de descriptografia Olá Kerberos de saudação `AZUREADSSOACCT` conta de computador (que representa o AD do Azure) criada em seu local de floresta do AD.

>[!IMPORTANT]
>É altamente recomendável que você sobrepor chave de descriptografia de Kerberos Olá pelo menos a cada 30 dias.

Siga estas etapas no servidor de local de saudação onde você está executando o Azure AD Connect:

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>Etapa 1. Obter lista de florestas do AD em que o SSO Contínuo foi habilitado

1. Primeiro, baixe e instale Olá [assistente Microsoft Online Services entrar](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Baixe e instale Olá [módulo do Active Directory do Azure de 64 bits do Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Navegue toohello `%programfiles%\Microsoft Azure Active Directory Connect` pasta.
4. Módulo do PowerShell de SSO contínuo de Olá de importação usando este comando: `Import-Module .\AzureADSSO.psd1`.
5. Execute o PowerShell como um Administrador. No PowerShell, chame `New-AzureADSSOAuthenticationContext`. Este comando deve dar um pop-up tooenter credenciais de Administrador Global do locatário.
6. Chame `Get-AzureADSSOStatus`. Esse comando fornece que Olá lista de florestas do AD (consulte a lista de domínios"hello") em que esse recurso foi habilitado.

### <a name="step-2-update-hello-kerberos-decryption-key-on-each-ad-forest-that-it-was-set-it-up-on"></a>Etapa 2. Atualizar a chave de descriptografia Olá Kerberos em cada floresta do AD que ele foi configurá-lo em

1. Chame `$creds = Get-Credential`. Quando solicitado, insira as credenciais de administrador de domínio Olá para Olá se destina a floresta do AD.
2. Chame `Update-AzureADSSOForest -OnPremCredentials $creds`. Este comando atualizações Olá chave de descriptografia do Kerberos para Olá `AZUREADSSOACCT` conta de computador nessa floresta AD específico e o atualiza no AD do Azure.
3. Repita Olá etapas para cada floresta do AD que você configurou o recurso de saudação em anteriores.

>[!IMPORTANT]
>Certifique-se de que você _não_ executar Olá `Update-AzureADSSOForest` comando mais de uma vez. Caso contrário, o recurso de saudação parar de funcionar até o tempo de saudação tíquetes do Kerberos dos usuários expirem e são reemitidos pelo Active Directory local.

## <a name="how-can-i-disable-seamless-sso"></a>Como faço para desabilitar o SSO Contínuo?

O SSO Contínuo pode ser desabilitado usando o Azure AD Connect.

Execute o Azure AD Connect, escolha “Alterar página de conexão do usuário” e clique em “Avançar”. Em seguida, desmarque a opção "Habilitar logon único" de saudação. Prossiga com o Assistente de saudação. Após a conclusão do Assistente de saudação, SSO contínua está desabilitada em seu locatário.

No entanto, você verá uma mensagem na tela que informa o seguinte:

"O logon único está desabilitado agora, mas há etapas manuais adicionais tooperform em ordem toocomplete limpeza. Saiba mais”

toocomplete Olá processo, siga estas etapas manuais no servidor de local de saudação onde você está executando o Azure AD Connect:

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>Etapa 1. Obter lista de florestas do AD em que o SSO Contínuo foi habilitado

1. Primeiro, baixe e instale Olá [assistente Microsoft Online Services entrar](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Baixe e instale Olá [módulo do Active Directory do Azure de 64 bits do Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Navegue toohello `%programfiles%\Microsoft Azure Active Directory Connect` pasta.
4. Módulo do PowerShell de SSO contínuo de Olá de importação usando este comando: `Import-Module .\AzureADSSO.psd1`.
5. Execute o PowerShell como um Administrador. No PowerShell, chame `New-AzureADSSOAuthenticationContext`. Este comando deve dar um pop-up tooenter credenciais de Administrador Global do locatário.
6. Chame `Get-AzureADSSOStatus`. Esse comando fornece que Olá lista de florestas do AD (consulte a lista de domínios"hello") em que esse recurso foi habilitado.

### <a name="step-2-manually-delete-hello-azureadssoacct-computer-account-from-each-ad-forest-that-you-see-listed"></a>Etapa 2. Exclua manualmente Olá `AZUREADSSOACCT` conta de computador de cada floresta do AD que você vê listadas.

## <a name="next-steps"></a>Próximas etapas

- [**Início Rápido** ](active-directory-aadconnect-sso-quick-start.md) – colocar o SSO Contínuo do Azure AD em funcionamento.
- [**Aprofundamento técnico**](active-directory-aadconnect-sso-how-it-works.md) – entenda como esse recurso funciona.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-sso.md) -Saiba como tooresolve comum problemas com o recurso de saudação.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.
