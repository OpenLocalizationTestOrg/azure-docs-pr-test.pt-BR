---
title: "aaaAzure AD visão geral do protocolo .NET | Microsoft Docs"
description: "Como toouse HTTP mensagens tooauthorize acessar tooweb aplicativos e APIs da web em seu locatário usando o Azure AD."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/21/2016
ms.author: priyamo
ms.openlocfilehash: 5bd54af028c445afd3f35d67d47d7c84b476c757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## Registrar seu aplicativo no seu locatário do AD
Primeiro, você precisará tooregister seu aplicativo com seu locatário do Azure Active Directory (AD do Azure). Isso será oferecem uma ID de aplicativo para o seu aplicativo, bem como habilitá-lo tooreceive tokens.

* Entrar toohello [Portal do Azure](https://portal.azure.com).
* Escolha seu locatário do AD do Azure clicando em sua conta no canto superior direito de saudação da página de saudação.
* No painel de navegação à esquerda hello, clique em **Active Directory do Azure**.
* Clique em **Registros do Aplicativo** e clique em **Adicionar**.
* Siga os prompts de saudação e criar um novo aplicativo. Para este tutorial, não importa se é um aplicativo Web ou um aplicativo nativo, mas se você quiser exemplos específicos para aplicativos Web ou para aplicativos nativos, confira nossos [guias de início rápido](../articles/active-directory/develop/active-directory-developers-guide.md).
  * Para aplicativos Web, fornecer Olá **URL de logon** que é Olá a URL base do aplicativo, onde os usuários possam entrar ex `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Para aplicativos nativos, forneça um **URI de redirecionamento**, o AD do Azure usará tooreturn respostas de token. Insira um aplicativo de tooyour específico de valor,. por exemplo`http://MyFirstAADApp`
* Depois de concluir o registro, o AD do Azure será atribuir seu aplicativo um identificador de cliente exclusivo, Olá a ID do aplicativo. Esse valor será necessário nas seções de Avançar Olá, portanto copie-o da página de aplicativo hello.
