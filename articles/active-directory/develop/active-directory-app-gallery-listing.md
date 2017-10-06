---
title: "aaaListing seu aplicativo na Galeria de aplicativo do Active Directory do Azure Olá"
description: "Como toolist um aplicativo que oferece suporte a logon único no hello Galeria do Active Directory do Azure | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a>Listando seu aplicativo na Galeria de aplicativo do Active Directory do Azure Olá
toolist um aplicativo que oferece suporte a logon único com o Azure Active Directory em Olá [Galeria do Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), aplicativo hello primeiro precisa tooimplement de saudação modos de integração a seguir:

* **OpenID Connect** - a integração direta com o Azure AD usando o OpenID Connect para autenticação e Olá consentimento do AD do Azure API para a configuração. Se você estiver apenas começando uma integração e seu aplicativo não suporta SAML, isso é o modo recomendado hello.
* **SAML** – seu aplicativo já tem provedores de identidade de terceiros Olá capacidade tooconfigure usando o protocolo do SAML hello.

Os requisitos de listagem para cada modo estão abaixo.

## <a name="openid-connect-integration"></a>Integração do OpenID Connect
toointegrate seu aplicativo com o Azure AD, Olá seguir [instruções de desenvolvedor](active-directory-authentication-scenarios.md). Em seguida, concluir perguntas de saudação abaixo e enviar toowaadpartners@microsoft.com.

* Forneça credenciais para uma conta ou Locatário de teste com o aplicativo que pode ser usado por Olá integração do AD do Azure team tootest hello.  
* Fornece instruções sobre como team Olá AD do Azure pode entrar e se conectar a uma instância do aplicativo do AD do Azure tooyour usando Olá [estrutura de consentimento do AD do Azure](active-directory-integrating-applications.md#overview-of-the-consent-framework). 
* Forneça quaisquer instruções adicionais necessárias para Olá AD do Azure da equipe tootest logon único com seu aplicativo. 
* Fornece informações de saudação abaixo:

> Nome da empresa:
> 
> Site da empresa:
> 
> Nome do aplicativo:
> 
> Descrição do aplicativo (limite de 200 caracteres):
> 
> Site do aplicativo (informativo):
> 
> Site de suporte técnico do aplicativo ou informações de contato:
> 
> ID do aplicativo hello, conforme mostrado nos detalhes do aplicativo hello em https://portal.azure.com:
> 
> URL de inscrição do aplicativo onde os clientes estão toosign para e/ou comprar o aplicativo hello:
> 
> Escolha as categorias de toothree para sua toobe aplicativo listado em (para categorias disponíveis, consulte Olá Marketplace do Azure Active Directory):
> 
> Anexe o ícone pequeno do aplicativo (arquivo PNG, 45px por 45px, cor de plano de fundo sólida):
> 
> Anexe o ícone grande do aplicativo (arquivo PNG, 215px por 215px, cor de plano de fundo transparente):
> 
> Anexe o logotipo do aplicativo (arquivo PNG, 150px por 122px, cor de plano de fundo transparente):
> 
> 

## <a name="saml-integration"></a>Integração SAML
Qualquer aplicativo que suporte o SAML 2.0 pode ser integrado diretamente com um locatário Azure AD usando [tooadd essas instruções um aplicativo personalizado](../active-directory-saas-custom-apps.md). Depois de testar se a integração de aplicativo funciona com o Azure AD, enviar Olá informações a seguir muito<mailto:waadpartners@microsoft.com>.

* Forneça credenciais para uma conta ou Locatário de teste com o aplicativo que pode ser usado por Olá integração do AD do Azure team tootest hello.  
* Fornecer Olá SAML URL de logon, a URL do emissor (ID da entidade), e valores de URL de resposta (serviço do consumidor de declaração) para seu aplicativo, conforme descrito [aqui](../active-directory-saas-custom-apps.md). Se você geralmente fornece esses valores como parte de um arquivo de metadados do SAML, envie este também.
* Forneça uma breve descrição de como tooconfigure AD do Azure como um provedor de identidade em seu aplicativo usando o SAML 2.0. Se seu aplicativo dá suporte à configuração do AD do Azure como um provedor de identidade por meio de um portal administrativo de autoatendimento, em seguida, verifique se as credenciais de saudação fornecidas acima incluem hello capacidade tooset esse.
* Fornece informações de saudação abaixo:

> Nome da empresa:
> 
> Site da empresa:
> 
> Nome do aplicativo:
> 
> Descrição do aplicativo (limite de 200 caracteres):
> 
> Site do aplicativo (informativo):
> 
> Site de suporte técnico do aplicativo ou informações de contato:
> 
> URL de inscrição do aplicativo onde os clientes estão toosign para e/ou comprar o aplicativo hello:
> 
> Escolha as categorias de toothree para sua toobe aplicativo listado em (para categorias disponíveis, consulte Olá [Marketplace do Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/))):
> 
> Anexe o ícone pequeno do aplicativo (arquivo PNG, 45px por 45px, cor de plano de fundo sólida):
> 
> Anexe o ícone grande do aplicativo (arquivo PNG, 215px por 215px, cor de plano de fundo transparente):
> 
> Anexe o logotipo do aplicativo (arquivo PNG, 150px por 122px, cor de plano de fundo transparente):
> 
> 

