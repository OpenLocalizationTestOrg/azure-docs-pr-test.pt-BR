---
title: ponto de extremidade do aaaAzure do Active Directory v 2.0 | Microsoft Docs
description: "Uma introdução toobuilding os aplicativos com Account da Microsoft e o Azure Active Directory entrar."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a>Conecte-se os usuários da Conta da Microsoft e do Azure AD em um único aplicativo
Em Olá anteriores, um desenvolvedor de aplicativo que desejavam toosupport ambas as contas pessoais da Microsoft e contas de trabalho do Azure Active Directory era necessário toointegrate com dois sistemas separados.  Olá **o ponto de extremidade do AD do Azure v 2.0** introduz uma nova versão de API de autenticação que permite que você toosign em ambos os tipos de contas usando uma integração simples.  Aplicativos que usam o ponto de extremidade do hello v 2.0 também podem consumir APIs REST de saudação [Microsoft Graph](https://graph.microsoft.io) usando qualquer tipo de conta.

## <a name="getting-started"></a>Introdução
Escolha sua plataforma de favorita de saudação toobuild lista a seguir um aplicativo usando nosso bibliotecas de código-fonte aberto e estruturas.  Como alternativa, você pode usar nosso toosend de documentação do protocolo OAuth 2.0 e OpenID Connect e receber mensagens de protocolo diretamente sem usar uma biblioteca de autenticação.

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a>O que há de novo
informações de saudação aqui serão úteis para entender o que é e o que não é possível com o ponto de extremidade do hello v 2.0.

* Saiba mais sobre Olá [tipos de aplicativos, você pode criar com o ponto de extremidade do hello v 2.0](active-directory-v2-flows.md).
* Entender Olá [restrições, restrições e limitações](active-directory-v2-limitations.md) com o ponto de extremidade do hello v 2.0.
* Confira esta visão geral do vídeo para o ponto de extremidade do hello v 2.0:

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a>Referência
Esses links serão úteis para explorar a plataforma de saudação em profundidade:

* [Referência do Protocolo v2.0](active-directory-v2-protocols.md)
* [Referência do Token v2.0](active-directory-v2-tokens.md)
* [Referência da Biblioteca v2.0](active-directory-v2-libraries.md)
* [Escopos e consentimento no ponto de extremidade do hello v 2.0](active-directory-v2-scopes.md)
* [Olá Microsoft Graph](https://graph.microsoft.io)

## <a name="help--support"></a>Ajuda + suporte
Esses são Olá melhores lugares tooget ajuda com o desenvolvimento no Active Directory do Azure.

* [Marcas `azure-active-directory` e `adal` do Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [Feedback no Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> Se você precisar somente toosign em contas corporativas e de estudantes do Active Directory do Azure, você deve começar com nossos [guia do desenvolvedor do AD do Azure](active-directory-developers-guide.md).  o ponto de extremidade do Hello v 2.0 é destinado ao uso por desenvolvedores que precisam explicitamente toosign em contas pessoais da Microsoft.

