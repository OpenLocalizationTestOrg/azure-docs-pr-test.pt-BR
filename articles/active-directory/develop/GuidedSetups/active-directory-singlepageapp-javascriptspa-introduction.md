---
title: "aaaAzure AD v2 JS SPA interativa instalação - Introdução | Microsoft Docs"
description: Como aplicativos JavaScript SPA podem chamar uma API que exige tokens de acesso pelo ponto de extremidade do Azure Active Directory v2
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a>Saudação de chamada Microsoft Graph API do aplicativo de página única um JavaScript (SPA)

Este guia demonstra como um aplicativo de página única JavaScript (SPA) pode entrar no trabalho pessoal e contas de estudante, obter um token de acesso e chamar hello Microsoft Graph API ou outras APIs que exigem os tokens de acesso Olá ponto de extremidade do Active Directory do Azure v2.

### <a name="how-this-guide-works"></a>Como funciona este guia

![Como funciona o aplicativo de exemplo hello gerado por este guia](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a>Mais informações

aplicativo de exemplo Hello criado por este guia permite que uma saudação do SPA JavaScript tooquery Microsoft Graph API ou uma API da Web que aceita tokens de ponto de extremidade do Active Directory do Azure v2. Para este cenário, depois que um usuário entrar, um token de acesso é solicitações tooHTTP solicitada e adicionado por meio do cabeçalho de autorização de saudação. Renovação e aquisição de token são manipuladas pelo Olá biblioteca de autenticação da Microsoft (MSAL).

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a>Bibliotecas

Este guia usa Olá biblioteca a seguir:

|Biblioteca|Descrição|
|---|---|
|[msal.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)|Versão prévia da Biblioteca de Autenticação da Microsoft para JavaScript|

> [!NOTE]
> *msal.js* Olá destinos *o ponto de extremidade do Active Directory do Azure v2* -que permite que contas pessoais, estudante e corporativas toosign no e adquirir tokens. Olá *o ponto de extremidade do Active Directory do Azure v2* tem [algumas limitações](..\active-directory-v2-limitations.md). Se você estiver interessado apenas em contas de estudante e corporativas, use *adal.js* e hello *ponto de extremidade V1*. toounderstand diferenças entre pontos de extremidade v1 e v2 Olá ler Olá [v1-v2 comparação](..\active-directory-v2-compare.md).

<!--end-collapse-->
