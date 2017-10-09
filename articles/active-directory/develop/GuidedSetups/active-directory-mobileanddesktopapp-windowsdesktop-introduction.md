---
title: "aaaAzure AD v2 Windows Desktop Introdução - Introdução | Microsoft Docs"
description: "Como os aplicativos .NET da Área de Trabalho do Windows (XAML) podem chamar uma API que exige tokens de acesso pelo ponto de extremidade do Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 89d98fc46190ba9e47b7c3095f91e32eca455fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a><span data-ttu-id="1a19d-103">Chamar hello Microsoft Graph API a partir de um aplicativo de área de trabalho do Windows</span><span class="sxs-lookup"><span data-stu-id="1a19d-103">Call hello Microsoft Graph API from a Windows Desktop app</span></span>

<span data-ttu-id="1a19d-104">Este guia demonstra como um aplicativo .NET nativo da Área de Trabalho do Windows (XAML) pode obter um token de acesso e chamar a API do Microsoft Graph ou outras APIs que exigem tokens de acesso por meio do ponto de extremidade do Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="1a19d-104">This guide demonstrates how a native Windows Desktop .NET (XAML) application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="1a19d-105">No final da saudação deste guia, seu aplicativo será ser capaz de toocall uma API protegida usando contas pessoais (incluindo o outlook.com, live.com e outros) bem como trabalhar e contas de estudante de qualquer empresa ou organização que possui o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a19d-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

> <span data-ttu-id="1a19d-106">Este guia exige o Visual Studio 2015 Atualização 3 ou o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1a19d-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="1a19d-107">Ainda não tem?</span><span class="sxs-lookup"><span data-stu-id="1a19d-107">Don’t have it?</span></span> [<span data-ttu-id="1a19d-108">Baixar o Visual Studio 2017 gratuitamente</span><span class="sxs-lookup"><span data-stu-id="1a19d-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a><span data-ttu-id="1a19d-109">Como funciona este guia</span><span class="sxs-lookup"><span data-stu-id="1a19d-109">How this guide works</span></span>

![Como funciona este guia](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

<span data-ttu-id="1a19d-111">aplicativo de exemplo Hello criado por este guia permite que um tooquery Microsoft Graph API do aplicativo de área de trabalho do Windows ou uma API da Web que aceita tokens de ponto de extremidade do Active Directory do Azure v2.</span><span class="sxs-lookup"><span data-stu-id="1a19d-111">hello sample application created by this guide enables a Windows Desktop Application tooquery Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="1a19d-112">Para este cenário, um token é adicionado tooHTTP solicitações por meio do cabeçalho de autorização de saudação.</span><span class="sxs-lookup"><span data-stu-id="1a19d-112">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="1a19d-113">Renovação e aquisição de token é tratado por Olá biblioteca de autenticação da Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="1a19d-113">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="1a19d-114">Manipulando a aquisição de token para acessar APIs Web protegidas</span><span class="sxs-lookup"><span data-stu-id="1a19d-114">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="1a19d-115">Após a autenticação do usuário Olá, o aplicativo de exemplo hello recebe um token que pode ser usado tooquery Microsoft Graph API ou uma API da Web protegida pelo Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="1a19d-115">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="1a19d-116">APIs, como o Microsoft Graph exigem um tooallow de token de acesso ao acessar recursos específicos – por exemplo, tooread um perfil de usuário, acessar o calendário do usuário ou enviar um email.</span><span class="sxs-lookup"><span data-stu-id="1a19d-116">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="1a19d-117">Seu aplicativo pode solicitar um token de acesso usando MSAL tooaccess esses recursos especificando escopos de API.</span><span class="sxs-lookup"><span data-stu-id="1a19d-117">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="1a19d-118">Esse token de acesso é, em seguida, o recurso protegido de toohello adicionado cabeçalho de autorização HTTP para todas as chamadas feitas em relação a saudação.</span><span class="sxs-lookup"><span data-stu-id="1a19d-118">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="1a19d-119">A MSAL gerencia o armazenamento em cache e a atualização de tokens de acesso para você, de forma que o aplicativo não precise fazer isso.</span><span class="sxs-lookup"><span data-stu-id="1a19d-119">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="1a19d-120">Pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="1a19d-120">NuGet Packages</span></span>

<span data-ttu-id="1a19d-121">Este guia usa Olá pacotes do NuGet a seguir:</span><span class="sxs-lookup"><span data-stu-id="1a19d-121">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="1a19d-122">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="1a19d-122">Library</span></span>|<span data-ttu-id="1a19d-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a19d-123">Description</span></span>|
|---|---|
|[<span data-ttu-id="1a19d-124">Microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="1a19d-124">Microsoft.Identity.Client</span></span>](https://www.nuget.org/packages/Microsoft.Identity.Client)|<span data-ttu-id="1a19d-125">MSAL (Biblioteca de Autenticação da Microsoft)</span><span class="sxs-lookup"><span data-stu-id="1a19d-125">Microsoft Authentication Library (MSAL)</span></span>|

