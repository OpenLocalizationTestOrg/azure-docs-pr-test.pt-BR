---
title: "aaaGet iniciar a integração do AD do Azure com aplicativos | Microsoft Docs"
description: "Este artigo é um guia de introdução para a integração do AD do Azure (Active Directory do Azure) com aplicativos locais e aplicativos em nuvem."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: db6d210d-c970-49e9-bd20-36d984bcd1c3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 5a7a851e8418083fee72ab58477a9cab75d0d4bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-active-directory-with-applications-getting-started-guide"></a>Guia de introdução: integrando o Active Directory do Azure com aplicativos
## <a name="overview"></a>Visão geral
Este tópico é toogive pretendido é um roteiro para integrar aplicativos com o Azure AD (Active Directory). Cada uma das seções de saudação abaixo contém um resumo de um tópico mais detalhado para que você pode identificar quais partes deste guia de Introdução ao obter são tooyou relevante.  Siga os links de saudação para se aprofundar em cada entidade.

## <a name="before-you-begin-take-inventory"></a>Antes de começar, faça o inventário
Antes de começar toointegrating aplicativos com o Azure AD, é importante tooknow onde você está e onde você deseja toogo.  Olá, perguntas a seguir são pretendido toohelp você pensar em seu projeto de integração de aplicativo do AD do Azure.

### <a name="application-inventory"></a>Inventário de aplicativos
* Onde estão todos os seus aplicativos? Quem é seu proprietário?
* Que tipo de autenticação os aplicativos exigem?
* Quem deve acessar toowhich aplicativos?
* Você deseja toodeploy um novo aplicativo?
  * Ele será criado internamente e implantado em uma instância de computação do Azure?
  * Você usará um que esteja disponível no hello Galeria de aplicativos do Azure?

### <a name="user-and-group-inventory"></a>Inventário de usuários e grupos
* Onde residem suas contas de usuário?
  * Active Directory local
  * AD do Azure
  * Em um banco de dados de aplicativo separado que você possui
  * Em aplicativos não autorizados
  * Todos os Olá acima
* Quais permissões e atribuições de função os usuários individuais têm atualmente? Você precisa tooreview o acesso ou tem certeza de que suas atribuições de função e de acesso do usuário são apropriadas agora?
* Os grupos já estão estabelecidos em seu Active Directory local?
  * Como os grupos são organizados?
  * Quem são membros do grupo Olá?
  * Quais permissões/atribuições grupos Olá atualmente tem?
* Você precisará tooclean dos bancos de dados de usuário/grupo antes de integrar?  (Essa é uma pergunta muito importante. Entrada e saída de lixo.)

### <a name="access-management-inventory"></a>Inventário de gerenciamento de acesso
* Como você gerencia atualmente tooapplications de acesso do usuário? Que precisa toochange?  Você considerou outras maneiras toomanage acesso, como com [RBAC](role-based-access-control-configure.md) por exemplo?
* Quem deve toowhat acesso?

Talvez você não tenha Olá respostas tooall dessas perguntas com antecedência, mas isso é okey.  Este guia pode ajudá-lo a responder a algumas dessas perguntas e tomar algumas decisões informadas.

## <a name="prerequisites"></a>Pré-requisitos
* Uma assinatura do Azure e um diretório do Azure Active Directory.  Se você ainda não tem uma assinatura do Azure, você pode experimentar o Azure gratuitamente por 30 dias. [Experimente!](https://azure.microsoft.com/trial/get-started-active-directory/)

## <a name="application-integration-with-azure-ad"></a>Integração de aplicativos com o AD do Azure
### <a name="finding-unsanctioned-cloud-applications-with-cloud-app-discovery"></a>Encontrando aplicativos em nuvem não autorizados com o Cloud App Discovery
Como mencionado acima, pode haver aplicativos que ainda não foram gerenciados pela sua organização até agora.  Como parte do processo de inventário Olá, é possível toofind não sancionado aplicativos em nuvem. Veja [Encontrando aplicativos em nuvem não autorizados com o Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).

### <a name="authentication-types"></a>Tipos de autenticação
Cada um dos seus aplicativos pode ter requisitos de autenticação diferentes. Com o AD do Azure, pode-se usar certificados de autenticação com aplicativos que usam os Protocolos SAML 2.0, WS-Federation ou OpenID Connect, bem como Logon Único com Senha. Para saber mais sobre os tipos de autenticação de aplicativo para uso com o Azure AD, veja [Gerenciando certificados para Logon Único Federado no Azure Active Directory](active-directory-sso-certs.md) e [Logon único baseado em senha](active-directory-appssoaccess-whatis.md).

### <a name="enabling-sso-with-azure-ad-app-proxy"></a>Habilitando o SSO com o Proxy de Aplicativo do AD do Azure
Com o Proxy de aplicativo do Microsoft Azure AD, você pode fornecer acesso tooapplications localizado dentro de sua rede privada com segurança, de qualquer lugar e em qualquer dispositivo. Depois de instalar um conector de proxy de aplicativo em seu ambiente, ele pode ser facilmente configurado com o Azure AD.

### <a name="integrating-applications-with-azure-ad"></a>Integrando aplicativos com o AD do Azure
Olá artigos a seguir abordam maneiras diferentes de saudação aplicativos integram com o AD do Azure e fornecem uma orientação.

* [Determinando quais toouse do Active Directory](active-directory-administer.md)
* [Usando aplicativos na Galeria de aplicativo do Azure Olá](active-directory-appssoaccess-whatis.md)
* [Integrando a lista de tutoriais de aplicativos SaaS](active-directory-saas-tutorial-list.md)

## <a name="managing-access-tooapplications"></a>Gerenciando acesso tooapplications
Olá, artigos a seguir descrevem maneiras de gerenciar acesso tooapplications depois que eles foram integrados ao AD do Azure usando conectores do AD do Azure e o Azure AD.

* [Gerenciando acesso tooapps usando o Azure AD](active-directory-managing-access-to-apps.md)
* [Automatizando com os Conectores do AD do Azure](active-directory-saas-app-provisioning.md)
* [Atribuir usuários tooan aplicativo](active-directory-applications-guiding-developers-assigning-users.md)
* [Atribuir grupos de aplicativo tooan](active-directory-applications-guiding-developers-assigning-groups.md)
* [Compartilhando contas](active-directory-sharing-accounts.md)

## <a name="integrating-custom-applications"></a>Integrando aplicativos personalizados
Se você estiver escrevendo um novo aplicativo e deseja que os desenvolvedores de tooassist em aproveitando o potencial de saudação do AD do Azure, consulte [Guiding desenvolvedores](active-directory-applications-guiding-developers-for-lob-applications.md).

Se você quiser tooadd toohello seu aplicativo personalizado Galeria de aplicativos do Azure, consulte ["Traga seu próprio aplicativo" com a configuração de autoatendimento do Azure AD SAML](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

## <a name="see-also"></a>Consulte também
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)

