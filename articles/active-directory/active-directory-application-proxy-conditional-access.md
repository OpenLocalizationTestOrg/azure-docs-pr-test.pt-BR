---
title: aplicativos de prem tooon acesso aaaConditional - AD do Azure | Microsoft Docs
description: "Aborda como tooset o acesso condicional para aplicativos você publica toobe acessado remotamente usando o Proxy de aplicativo do Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2e97722b-eb4e-4078-b607-9fed210d8a0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7bed25dd4ba17941e77d8c4b2b9ba4edcf0cf597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-conditional-access-in-azure-ad-application-proxy"></a>Trabalhando com acesso condicional no Proxy de Aplicativo do AD do Azure

>[!NOTE]
>Este artigo se aplica a toohello portal clássico do Azure, que está sendo desativado. Recomendamos que você use Olá [portal do Azure](https://portal.azure.com). Olá portal do Azure, o Proxy de aplicativo que os aplicativos tenham Olá mesmos recursos de acesso condicional como qualquer outro aplicativo SaaS. toolearn mais sobre o acesso condicional, consulte [Introdução ao acesso condicional no Active Directory do Azure](active-directory-conditional-access-azure-portal-get-started.md).

Você pode configurar o acesso regras toogrant acesso condicional tooapplications publicados usando o Proxy de aplicativo. Isso permite a você:

* Exigir a autenticação multifator por aplicativo
* Exigir a autenticação multifator somente quando os usuários não estiverem no trabalho
* Impedir que usuários de acessar o aplicativo hello quando eles não estão no trabalho

Essas regras podem ser aplicadas tooall usuários e grupos ou somente toospecific usuários e grupos. Por padrão a regra de saudação se aplica a usuários de tooall que têm acesso toohello aplicativo. No entanto regra Olá também pode ser restrito toousers que são membros de grupos de segurança especificados.  

Regras de acesso são avaliadas quando um usuário acessa um aplicativo federado que usa OAuth 2.0, OpenID Connect, SAML ou WS-Federation. Além disso, as regras de acesso são avaliadas com OAuth 2.0 e OpenID Connect quando um token de atualização é tooacquire usado um token de acesso.

## <a name="conditional-access-prerequisites"></a>Pré-requisitos de acesso condicional
* Assinatura tooAzure Active Directory Premium
* Um locatário do Active Directory do Azure federado ou gerenciado
* Os locatários federados exigem que a autenticação multifator (MFA) esteja habilitado  
    ![Configurar regras de acesso - exigir autenticação multifator](./media/active-directory-application-proxy-conditional-access/application-proxy-conditional-access.png)

## <a name="configure-per-application-multi-factor-authentication"></a>Configure a autenticação multifator por aplicativo
1. Entrar como um administrador no hello portal clássico do Azure.
2. Vá tooActive diretório e selecione Olá diretório no qual você deseja tooenable Proxy de aplicativo.
3. Clique em **aplicativos** e role para baixo toohello **regras de acesso** seção. seção de regras de acesso de saudação aparece somente para aplicativos publicados usando o Proxy de aplicativo que usam a autenticação federada.
4. Habilitar regra Olá selecionando **habilitar regras de acesso** muito**em**.
5. Especifique Olá usuários e grupos toowhom Olá regras se aplicam. Saudação de uso **adicionar grupo** botão tooselect um ou mais grupos toowhich Olá acesso regra se aplica. Essa caixa de diálogo também pode ser usado tooremove selecionada de grupos.  Quando as regras de saudação toogroups tooapply selecionado, as regras de acesso de Olá são aplicadas apenas para usuários que pertencem a tooone de saudação especificada grupos de segurança.  

   * Verificar tooexplicitly excluir grupos de segurança da regra de saudação **exceto** e especifique um ou mais grupos. Os usuários que são membros de um grupo em Olá exceto lista não são necessários tooperform a autenticação multifator.  
   * Se um usuário tiver sido configurado usando o recurso de autenticação multifator por usuário hello, essa configuração prevalece sobre Olá regras de autenticação multifator do aplicativo. Um usuário que foi configurado para a autenticação multifator por usuário é necessária tooperform a autenticação multifator, mesmo se ele tiver sido isentado das regras de autenticação multifator do aplicativo hello. Saiba mais sobre a [autenticação multifator e as configurações por usuário](../multi-factor-authentication/multi-factor-authentication.md).
6. Selecione a regra de acesso de saudação desejado tooset:

   * **Exigir autenticação multifator**: usuários aplicam regras de acesso toowhom são toocomplete necessária a autenticação multifator antes de acessar Olá aplicativo toowhich Olá regra se aplica.
   * **Exigir autenticação multifator quando não estiver no trabalho**: usuários tentando tooaccess aplicativo hello um endereço IP confiável não será necessário tooperform a autenticação multifator. Olá confiável intervalos de endereços IP podem ser configurados na página de configurações de autenticação multifator hello.
   * **Bloquear o acesso quando não estiver no trabalho**: usuários tentando tooaccess Olá aplicativo fora da rede corporativa não será capaz de tooaccess aplicativo de hello.

## <a name="configuring-mfa-for-federation-services"></a>Configurar a MFA para serviços de federação
Para locatários federados, autenticação multifator (MFA) pode ser executada pelo Active Directory do Azure ou por saudação do servidor AD FS local. Por padrão, a MFA ocorre em qualquer página hospedada pelo Active Directory do Azure. tooconfigure MFA local, execute o Windows PowerShell e use hello – SupportsMFA propriedade tooset Olá módulo AD do Azure.

Olá, exemplo a seguir mostra como tooenable local MFA usando Olá [cmdlet Set-MsolDomainFederationSettings](https://msdn.microsoft.com/library/azure/dn194088.aspx) no locatário do hello contoso.com:`Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true `

Em adição toosetting esse sinalizador, Olá locatário federado do AD FS instância deve ser configurado tooperform a autenticação multifator. Siga as instruções de saudação de [Implantando o Microsoft Azure multi-factor authentication local](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="see-also"></a>Consulte também
* [Trabalho com aplicativos com reconhecimento de declaração](active-directory-application-proxy-claims-aware-apps.md)
* [Publique aplicativos com proxy de aplicativo](active-directory-application-proxy-publish.md)
* [Habilitar o logon único](active-directory-application-proxy-sso-using-kcd.md)
* [Publicar aplicativos usando seu próprio nome de domínio](active-directory-application-proxy-custom-domains.md)

Para Olá últimas notícias e atualizações, confira Olá [blog de Proxy de aplicativo](http://blogs.technet.com/b/applicationproxyblog/)
