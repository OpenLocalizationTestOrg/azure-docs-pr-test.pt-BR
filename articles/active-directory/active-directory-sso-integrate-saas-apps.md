---
title: "aaaIntegrate logon único do Active Directory do Azure com aplicativos SaaS | Microsoft Docs"
description: "Habilitar o gerenciamento de acesso centralizado da autenticação de logon único e do provisionamento de usuário dos aplicativos SaaS no Active Directory do Azure. Uma visão geral de como toointegrate Active Directory do Azure tooSaaS aplicativos."
services: active-directory
keywords: integrar o AD do Azure a aplicativos SaaS
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 53b9d341-d1fc-4bbb-ac7c-3f4c68fcf00a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: aaronsm
ms.openlocfilehash: fe621a30429c81c32470635d105ae3e95184efa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-single-sign-on-with-saas-apps"></a>Integrar o logon único do Azure AD com aplicativos de SaaS
> [!div class="op_single_selector"]
> * [Portal do Azure](active-directory-enterprise-apps-manage-sso.md)
> * [Portal clássico do Azure](active-directory-sso-integrate-saas-apps.md)
>
>

[!INCLUDE [active-directory-sso-use-case-intro](../../includes/active-directory-sso-use-case-intro.md)]

tooget iniciada a configuração de logon único para um aplicativo que você está colocando em sua organização, você usará um diretório existente no Azure Active Directory (AD do Azure). Você pode usar um diretório do Azure AD que você obtém por meio do Microsoft Azure, Office 365 ou Windows Intune. Se você tiver dois ou mais dos seguintes, consulte [administrar seu diretório do AD do Azure](active-directory-administer.md) toodetermine toouse que um.

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo. Para como centralizar tooassign funções de administrador na administração de saudação do AD do Azure, consulte [atribuindo funções de administrador no Azure Active Directory](active-directory-enterprise-apps-manage-sso.md).

## <a name="authentication"></a>Autenticação
Para aplicativos que dão suporte a saudação SAML 2.0, WS-Federation, ou protocolos de OpenID Connect, Active Directory do Azure usa relações de confiança tooestablish certificados de assinatura. Para obter mais informações sobre isso, consulte [Gerenciando certificados para logon único federado](active-directory-sso-certs.md).

Para aplicativos que suportam apenas HTML baseada em formulários entrar, relações de confiança do Active Directory do Azure usa 'compartimentação de senha' tooestablish. Essa saudação de permite que os usuários em sua organização toobe conectado automaticamente tooa aplicativo SaaS pelo AD do Azure usando as informações de conta de usuário de saudação do hello aplicativo SaaS. O AD do Azure coleta e armazena com segurança informações de conta de usuário de saudação e a senha relacionada hello. Para obter mais informações, consulte [Logon único baseado em senha](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).

## <a name="authorization"></a>Autorização
Uma conta provisionada habilita um toouse toobe autorizada do usuário um aplicativo após terem autenticado por meio de logon único. Provisionamento de usuário pode ser feito manualmente ou, em alguns casos, você pode adicionar e remover as informações de usuário de aplicativo de SaaS Olá com base nas alterações feitas no Active Directory do Azure. Para saber mais sobre o uso dos conectores existentes do Azure AD para o provisionamento automatizado, consulte [Provisionamento e desprovisionamento do usuário automatizados para os aplicativos de SaaS](active-directory-saas-app-provisioning.md).

Caso contrário, você pode manualmente Adicionar aplicativo de tooan de informações do usuário, ou usar outras soluções de provisionamento que estão disponíveis no mercado de saudação.

## <a name="access"></a>Access
O AD do Azure fornece várias maneiras de personalizáveis toodeploy aplicativos tooend os usuários em sua organização. Você não está limitado a nenhuma implantação ou solução de acesso específica. Você pode usar [Olá a solução que melhor atenda às suas necessidades](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

## <a name="additional-considerations-for-applications-already-in-use"></a>Considerações adicionais sobre os aplicativos já em uso
Configurando o logon único em um aplicativo que usa sua organização já é um processo diferente do processo de saudação de criação de novas contas para um novo aplicativo. Há algumas etapas preliminares incluindo: mapeamento de identidades de usuário em identidades de tooAzure AD aplicativo hello e entender como os usuários terão log no aplicativo tooan depois que ele é integrado.

> [!NOTE]
> tooset o logon único para um aplicativo existente, você precisa ter direitos de administrador global toohave no AD do Azure e Olá aplicativo SaaS.
>
>

### <a name="mapping-user-accounts"></a>Mapeamento das contas de usuário
A identidade de um usuário geralmente tem um identificador exclusivo que pode ser um endereço de email ou um nome UPN. Você precisará toolink (map) cada aplicativo identidade tootheir AD do Azure respectivo identidade de usuário. Há duas maneiras tooaccomplish isso dependendo de como o requisito de saudação de autenticação do seu aplicativo.

Para obter mais informações sobre o mapeamento de identidades de aplicativo com identidades do AD do Azure, consulte [personalizando declarações emitidas no token SAML Olá](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx) e [personalizar mapeamentos de atributos para provisionamento](active-directory-saas-customizing-attribute-mappings.md).

### <a name="understanding-hello-users-log-in-experience"></a>Noções básicas sobre a experiência de login do usuário Olá
Quando você integra o SSO para um aplicativo que já está em uso, é importante toorealize que Olá a experiência do usuário será afetada. Para todos os aplicativos, os usuários começarão a usar seu toosign de credenciais do AD do Azure no. Também é possível que eles devem usar um aplicativo de saudação tooaccess portal diferente.

SSO para alguns aplicativos pode ser feito na entrada do aplicativo hello interface, mas para outros aplicativos, Olá usuário terá toogo através de um portal central, como ([meus aplicativos](http://myapps.microsoft.com) ou [Office365](http://portal.office.com/myapps)) toosign no. Saiba mais sobre os diferentes tipos de saudação do SSO e suas experiências do usuário em [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).

Outro recurso valioso é *suprimindo o consentimento do usuário* em Olá [Guiding desenvolvedores](active-directory-applications-guiding-developers-for-lob-applications.md) artigo.

## <a name="next-steps"></a>Próximas etapas
Para aplicativos SaaS que você encontrar no hello Galeria de aplicativos, o AD do Azure fornece um número de [tutoriais sobre como aplicativos de SaaS toointegrate](active-directory-saas-tutorial-list.md).

Se o aplicativo não estiver na Galeria de aplicativo, você pode [adicioná-lo toohello Galeria de aplicativo do Azure AD como um aplicativo personalizado](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

Há muito mais detalhes em todos esses problemas na biblioteca de Azure.com hello, começando com [o que é o acesso ao aplicativo e logon único com o Active Directory do Azure?](active-directory-appssoaccess-whatis.md).

Além disso, não perca Olá [índice do artigo para gerenciamento de aplicativos no Active Directory do Azure](active-directory-apps-index.md).
