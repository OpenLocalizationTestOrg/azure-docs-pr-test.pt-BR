---
title: contas de aaaSharing usando o Azure AD | Microsoft Docs
description: "Descreve como o Active Directory do Azure permite que as contas de compartilhamento do organizações toosecurely para aplicativos locais e serviços de nuvem do consumidor."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e2d77104-d978-46a3-bfea-03ffdf3b61e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 9f98bfa97a6c9ba1566d3f921c1b676d5f3c2a88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sharing-accounts-with-azure-ad"></a>Compartilhar contas com o AD do Azure
## <a name="overview"></a>Visão geral
Às vezes, as organizações precisam toouse um único nome de usuário e senha para várias pessoas. Isso geralmente ocorre em dois casos:

* Ao acessar aplicativos que exigem um logon exclusivo e uma senha para cada usuário, seja aplicativos locais ou serviços em nuvem do consumidor (por exemplo, contas de mídia social corporativa).
* Durante a criação de ambientes de vários usuários. Você pode ter uma única conta local que tenha privilégios elevados e pode ser usado toodo atividades principais instalação, administração e recuperação (por exemplo, hello "global" conta de administrador local para o Office 365 ou hello conta raiz no Salesforce).

Tradicionalmente, essas contas seriam compartilhadas por distribuir indivíduos direito da saudação credenciais (nome de usuário e senha) toohello ou armazená-los em um local compartilhado onde várias confiável agentes possam acessá-los.

modelo tradicional de compartilhamento Olá tem várias desvantagens:

* Habilitando acesso toonew aplicativos requer toodistribute credenciais tooeveryone que precisa acessar.
* Cada aplicativo compartilhado pode exigir o seu próprio conjunto exclusivo de credenciais compartilhadas, exigindo usuários tooremember vários conjuntos de credenciais. Quando os usuários tooremember várias credenciais, o risco de saudação aumenta que eles recorre toorisky práticas. (Por exemplo, anotar senhas).
* Você não pode determinar quem tem acesso tooan aplicativo.
* Você não pode determinar quem *acessou* um aplicativo.
* Quando você precisar de aplicativo de tooan tooremove access, ter tooupdate Olá credenciais e distribuí-los novamente tooeveryone que precisa acessar o aplicativo toothat.

## <a name="azure-active-directory-account-sharing"></a>Compartilhamento de contas do Active Directory do Azure
O AD do Azure fornece uma nova abordagem contas toousing compartilhado que elimina essas desvantagens.

Olá administrador do AD Azure configura os aplicativos que um usuário pode acessar usando Olá painel de acesso e escolhendo o tipo de saudação do logon único mais adequado para o aplicativo. Um desses tipos, *baseada em senha de logon único*, permite que o AD do Azure funcione como um tipo de "agente" durante a saudação processo de logon para esse aplicativo.

Os usuários fazem logon uma vez com sua conta institucional. Isso é hello mesma conta usarem regularmente tooaccess sua área de trabalho ou email. Eles podem descobrir e acessar apenas os aplicativos aos quais eles estão atribuídos. Com contas compartilhadas, essa lista de aplicativos pode incluir qualquer número de credenciais compartilhadas. usuário final de saudação não precisa tooremember ou anote Olá várias contas podem estar utilizando.

As contas compartilhadas não apenas aumentam a supervisão e melhoram a utilização, como também aumentam a segurança. Os usuários com permissões toouse Olá credenciais não vir senha compartilhada hello, mas em vez disso, obter senha de saudação toouse permissões como parte de um fluxo de autenticação orquestrada. Além disso, com alguns aplicativos de SSO de senha, você tem Olá opção toohave AD do Azure periodicamente o senha Olá substituição (atualização) está usando senhas grandes e complexas, aumentar a segurança da conta hello. administrador de saudação pode facilmente conceder ou revogar acesso tooan aplicativo e também saber quem tem acesso toohello conta e quem acessou em Olá anterior.

O AD do Azure oferece suporte a contas compartilhadas para qualquer usuário licenciado do Enterprise Mobility Suite (EMS), Premium ou Basic, em todos os tipos de aplicativos de logon único com senha. Você pode compartilhar contas para qualquer um dos milhares de aplicativos pré-integrados na Galeria de aplicativo hello e pode adicionar seu próprio aplicativo de autenticação de senha com [aplicativos personalizados de SSO](active-directory-sso-integrate-saas-apps.md).

Recursos do AD do Azure que permitem o compartilhamento de contas incluem:

* [Logon único com senha](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Agente de logon único com senha
* [Atribuição de grupo](active-directory-accessmanagement-self-service-group-management.md)
* Aplicativos com senha personalizada
* [Painel/relatórios de uso de aplicativo](active-directory-passwords-get-insights.md)
* Portais de acesso do usuário final
* [Proxy do aplicativo](active-directory-application-proxy-get-started.md)
* [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/all/)

## <a name="sharing-an-account"></a>Compartilhamento de uma conta
tooshare toouse AD do Azure uma conta que você precisará para:

* Adicionar uma [galeria de aplicativos](https://azure.microsoft.com/marketplace/active-directory/) do aplicativo ou um [aplicativo personalizado](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)
* Configurar o aplicativo hello senha Single Sign-On (SSO)
* Use [atribuição baseada em grupo](active-directory-accessmanagement-group-saasapps.md) e selecione uma credencial compartilhada de opção tooenter Olá
* Opcional: em alguns aplicativos, como Facebook, Twitter e LinkedIn, você pode habilitar a opção Olá para [AD do Azure automatizada sobreposição de senha](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)

Você também pode tornar sua conta compartilhada mais segura com o multi-Factor Authentication (MFA) (Saiba mais sobre [proteger aplicativos com o Azure AD](../multi-factor-authentication/multi-factor-authentication-get-started.md)) e você pode delegar Olá capacidade toomanage quem tem acesso toohello aplicativo usando [Autoatendimento do AD do azure](active-directory-accessmanagement-self-service-group-management.md) gerenciamento de grupo.

## <a name="related-articles"></a>Artigos relacionados
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [Proteger aplicativos com acesso condicional](active-directory-conditional-access.md)
* [Gerenciamento de grupo de autoatendimento/SSAA](active-directory-accessmanagement-self-service-group-management.md)

