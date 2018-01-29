---
title: Compartilhando contas usando o Azure AD | Microsoft Docs
description: "Descreve como o Active Directory do Azure permite que as organizações compartilhem com segurança contas para aplicativos locais e serviços de nuvem do consumidor."
services: active-directory
documentationcenter: 
author: curtand
manager: mtillman
editor: 
ms.assetid: e2d77104-d978-46a3-bfea-03ffdf3b61e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: it-pro
ms.openlocfilehash: 3b6a83d91ec5d8466669655d6c3bd7ae7b42dd2f
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="sharing-accounts-with-azure-ad"></a>Compartilhar contas com o AD do Azure
## <a name="overview"></a>Visão geral
Às vezes, as organizações precisam usar um único nome de usuário e senha para várias pessoas, o que normalmente acontece em dois casos:

* Ao acessar aplicativos que exigem um logon único e uma senha para cada usuário, seja em aplicativos locais ou em serviços de nuvem do consumidor (por exemplo, contas corporativas de mídias sociais).
* Durante a criação de ambientes de vários usuários. Você pode ter uma conta local única que tenha privilégios elevados e que seja usada para fazer atividades de instalação, administração e recuperação de núcleo. Por exemplo, a conta local do "administrador global" do Office 365 ou a conta raiz no Salesforce.

Tradicionalmente, essas contas são compartilhadas distribuindo as credenciais (nome de usuário e senha) para os indivíduos certos ou armazenando-as em um local compartilhado onde vários agentes confiáveis podem acessá-las.

O modelo tradicional de compartilhamento tem várias desvantagens:

* Habilitar o acesso a novos aplicativos exige que você distribua credenciais para qualquer pessoa que precise de acesso.
* Cada aplicativo compartilhado pode exigir seu próprio conjunto exclusivo de credenciais compartilhadas, exigindo que os usuários se lembrem de vários conjuntos de credenciais. Quando os usuários precisam lembrar de várias credenciais, o risco de eles recorrerem a práticas arriscadas aumenta. (Por exemplo, anotar senhas).
* Você não pode determinar quem tem acesso a um aplicativo.
* Você não pode determinar quem *acessou* um aplicativo.
* Quando você quiser remover o acesso a um aplicativo, é necessário atualizar as credenciais e redistribuí-las para todos que precisarem acessar o aplicativo.

## <a name="azure-active-directory-account-sharing"></a>Compartilhamento de contas do Active Directory do Azure
O AD do Azure fornece uma nova abordagem para usar contas compartilhadas que elimina essas desvantagens.

O administrador do AD do Azure configura quais aplicativos um usuário pode acessar usando o Painel de Acesso e escolhendo o tipo de logon único mais adequado para o aplicativo. Um desses tipos, *logon único baseado em senha*, permite ao AD do Azure agir como um tipo de “agente” durante o processo de logon do aplicativo.

Os usuários fazem logon uma vez com sua conta institucional. Essa conta é a mesma usada regularmente para acessar a área de trabalho ou o e-mail. Eles podem descobrir e acessar apenas os aplicativos aos quais eles estão atribuídos. Com contas compartilhadas, essa lista de aplicativos pode incluir qualquer número de credenciais compartilhadas. O usuário final não precisa se lembrar ou anotar as diversas contas que ele pode estar utilizando.

As contas compartilhadas não apenas aumentam a supervisão e melhoram a utilização, como também aumentam a segurança. Os usuários com permissões para usar as credenciais não vejam a senha compartilhada, mas em vez disso, obtém as permissões para usar a senha como parte de um fluxo de autenticação orquestrado. Além disso, alguns aplicativos de SSO de senha oferecem a opção de usar o Azure Active Directory para substituir (atualizar) periodicamente as senhas. O sistema usa senhas grandes e complexas, o que aumenta a segurança da conta. O administrador pode conceder ou revogar o acesso a um aplicativo facilmente, e também sabe quem tem acesso à conta e quem a acessou no passado.

O Azure Active Directory oferece suporte a contas compartilhadas para qualquer usuário licenciado do Enterprise Mobility Suite (EMS), Premium ou Basic, em todos os tipos de aplicativos de logon único com senha. Você pode compartilhar as contas para qualquer um dos milhares de aplicativos previamente integrados na galeria de aplicativos e pode adicionar seu próprio aplicativo de autenticação de senha com os [aplicativos personalizados de SSO](active-directory-enterprise-apps-manage-sso.md).

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
Para usar o Azure Active Directory para compartilhar uma conta, você precisará:

* Adicionar uma [galeria de aplicativos](https://azure.microsoft.com/marketplace/active-directory/) do aplicativo ou um [aplicativo personalizado](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)
* Configurar o aplicativo para logon único (SSO) com senha
* Usar a [atribuição baseada em grupo](active-directory-accessmanagement-group-saasapps.md) e selecionar a opção para inserir uma credencial compartilhada
* Opcional: em alguns aplicativos, como o Facebook, Twitter ou LinkedIn, você pode habilitar a opção para a [Substituição de senha automatizada do AD do Azure](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)

Você também pode tornar sua conta compartilhada mais segura com a MFA (Autenticação Multifator) (saiba mais sobre [como proteger os aplicativos com o Azure AD](../multi-factor-authentication/multi-factor-authentication-get-started.md)) e pode delegar a capacidade de gerenciar quem tem acesso ao aplicativo usando o Gerenciamento de Grupo do [Autoatendimento do Azure AD](active-directory-accessmanagement-self-service-group-management.md).

## <a name="related-articles"></a>Artigos relacionados
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [Proteger aplicativos com acesso condicional](active-directory-conditional-access-azure-portal.md)
* [Gerenciamento de grupo de autoatendimento/SSAA](active-directory-accessmanagement-self-service-group-management.md)

