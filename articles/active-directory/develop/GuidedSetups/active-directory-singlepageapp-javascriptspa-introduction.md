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
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="a3928-103">Saudação de chamada Microsoft Graph API do aplicativo de página única um JavaScript (SPA)</span><span class="sxs-lookup"><span data-stu-id="a3928-103">Call hello Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="a3928-104">Este guia demonstra como um aplicativo de página única JavaScript (SPA) pode entrar no trabalho pessoal e contas de estudante, obter um token de acesso e chamar hello Microsoft Graph API ou outras APIs que exigem os tokens de acesso Olá ponto de extremidade do Active Directory do Azure v2.</span><span class="sxs-lookup"><span data-stu-id="a3928-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call hello Microsoft Graph API or other APIs that require access tokens from hello Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="a3928-105">Como funciona este guia</span><span class="sxs-lookup"><span data-stu-id="a3928-105">How this guide works</span></span>

![Como funciona o aplicativo de exemplo hello gerado por este guia](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="a3928-107">Mais informações</span><span class="sxs-lookup"><span data-stu-id="a3928-107">More Information</span></span>

<span data-ttu-id="a3928-108">aplicativo de exemplo Hello criado por este guia permite que uma saudação do SPA JavaScript tooquery Microsoft Graph API ou uma API da Web que aceita tokens de ponto de extremidade do Active Directory do Azure v2.</span><span class="sxs-lookup"><span data-stu-id="a3928-108">hello sample application created by this guide enables a JavaScript SPA tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="a3928-109">Para este cenário, depois que um usuário entrar, um token de acesso é solicitações tooHTTP solicitada e adicionado por meio do cabeçalho de autorização de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3928-109">For this scenario, after a user signs-in, an access token is requested and added tooHTTP requests via hello authorization header.</span></span> <span data-ttu-id="a3928-110">Renovação e aquisição de token são manipuladas pelo Olá biblioteca de autenticação da Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="a3928-110">Token acquisition and renewal are handled by hello Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="a3928-111">Bibliotecas</span><span class="sxs-lookup"><span data-stu-id="a3928-111">Libraries</span></span>

<span data-ttu-id="a3928-112">Este guia usa Olá biblioteca a seguir:</span><span class="sxs-lookup"><span data-stu-id="a3928-112">This guide uses hello following library:</span></span>

|<span data-ttu-id="a3928-113">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="a3928-113">Library</span></span>|<span data-ttu-id="a3928-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="a3928-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="a3928-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="a3928-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="a3928-116">Versão prévia da Biblioteca de Autenticação da Microsoft para JavaScript</span><span class="sxs-lookup"><span data-stu-id="a3928-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="a3928-117">*msal.js* Olá destinos *o ponto de extremidade do Active Directory do Azure v2* -que permite que contas pessoais, estudante e corporativas toosign no e adquirir tokens.</span><span class="sxs-lookup"><span data-stu-id="a3928-117">*msal.js* targets hello *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts toosign in and acquire tokens.</span></span> <span data-ttu-id="a3928-118">Olá *o ponto de extremidade do Active Directory do Azure v2* tem [algumas limitações](..\active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="a3928-118">hello *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="a3928-119">Se você estiver interessado apenas em contas de estudante e corporativas, use *adal.js* e hello *ponto de extremidade V1*.</span><span class="sxs-lookup"><span data-stu-id="a3928-119">If you are interested only in school and work accounts, use *adal.js* and hello *V1 endpoint*.</span></span> <span data-ttu-id="a3928-120">toounderstand diferenças entre pontos de extremidade v1 e v2 Olá ler Olá [v1-v2 comparação](..\active-directory-v2-compare.md).</span><span class="sxs-lookup"><span data-stu-id="a3928-120">toounderstand differences between hello v1 and v2 endpoints read hello [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->
