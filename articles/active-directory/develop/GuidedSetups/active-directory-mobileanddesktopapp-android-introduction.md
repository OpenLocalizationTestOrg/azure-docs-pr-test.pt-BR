---
title: "aaaAzure AD v2 Android Introdução - Introdução | Microsoft Docs"
description: Como um aplicativo do Android pode obter um token de acesso e chamar a API do Microsoft Graph ou APIs que exigem tokens de acesso por meio do ponto de extremidade do Azure Active Directory v2
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
ms.openlocfilehash: 7c76ab8bbf1a6c934ab672cccf85ae82f03f601a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a><span data-ttu-id="65c7e-103">Chamar hello Microsoft Graph API a partir de um aplicativo do Android</span><span class="sxs-lookup"><span data-stu-id="65c7e-103">Call hello Microsoft Graph API from an Android app</span></span>

<span data-ttu-id="65c7e-104">Este guia demonstra como um aplicativo nativo do Android pode obter um token de acesso e chamar a API do Microsoft Graph ou outras APIs que exigem tokens de acesso por meio do ponto de extremidade do Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="65c7e-104">This guide demonstrates how a native Android application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="65c7e-105">No final da saudação deste guia, seu aplicativo será ser capaz de toocall uma API protegida usando contas pessoais (incluindo o outlook.com, live.com e outros) bem como trabalhar e contas de estudante de qualquer empresa ou organização que possui o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="65c7e-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

### <a name="how-this-sample-works"></a><span data-ttu-id="65c7e-106">Como funciona esta amostra</span><span class="sxs-lookup"><span data-stu-id="65c7e-106">How this sample works</span></span>
![Como funciona esta amostra](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

<span data-ttu-id="65c7e-108">exemplo Hello criado por este guia se baseia em um cenário em que um aplicativo do Android é tooquery usado um API da Web que aceita tokens do Active Directory do Azure v2 ponto de extremidade – nesse caso, a API do Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="65c7e-108">hello sample created by this guide is based on a scenario where an Android application is used tooquery a Web API that accepts tokens from Azure Active Directory v2 endpoint – in this case, Microsoft Graph API.</span></span> <span data-ttu-id="65c7e-109">Para este cenário, um token é adicionado tooHTTP solicitações por meio do cabeçalho de autorização de saudação.</span><span class="sxs-lookup"><span data-stu-id="65c7e-109">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="65c7e-110">Renovação e aquisição de token é tratado por Olá biblioteca de autenticação da Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="65c7e-110">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="65c7e-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="65c7e-111">Pre-requisites</span></span>
* <span data-ttu-id="65c7e-112">Esta instalação guiada se concentra no Android Studio, mas qualquer outro ambiente de desenvolvimento de aplicativos do Android também é aceitável.</span><span class="sxs-lookup"><span data-stu-id="65c7e-112">This guided setup is focused on Android Studio, but any other Android application development environment is also acceptable.</span></span> 
* <span data-ttu-id="65c7e-113">O SDK 21 ou mais novo do Android é necessário (o recomendado é o SDK 25).</span><span class="sxs-lookup"><span data-stu-id="65c7e-113">Android SDK 21 or newer is required (SDK 25 is recommended).</span></span>
* <span data-ttu-id="65c7e-114">O Google Chrome ou um navegador da Web que usa Guias Personalizadas é necessário para esta versão da MSAL (Biblioteca de Autenticação da Microsoft) para Android.</span><span class="sxs-lookup"><span data-stu-id="65c7e-114">Google Chrome or a web browser using Custom Tabs is required for this release of Microsoft Authentication Library (MSAL) for Android.</span></span>

> <span data-ttu-id="65c7e-115">Observação: o Google Chrome não está incluído no Emulador do Visual Studio para Android.</span><span class="sxs-lookup"><span data-stu-id="65c7e-115">Note: Google Chrome is not included on Visual Studio Emulator for Android.</span></span> <span data-ttu-id="65c7e-116">Recomendamos que você tootest esse código em um emulador com 25 de API ou uma imagem com API 21 ou mais recente com o Google Chrome instalados.</span><span class="sxs-lookup"><span data-stu-id="65c7e-116">We recommend you tootest this code on an Emulator with API 25 or an image with API 21 or newer that has with Google Chrome installed.</span></span>


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a><span data-ttu-id="65c7e-117">Como toohandle token tooaccess de aquisição de uma API da Web protegida</span><span class="sxs-lookup"><span data-stu-id="65c7e-117">How toohandle token acquisition tooaccess a protected Web API</span></span>

<span data-ttu-id="65c7e-118">Após a autenticação do usuário Olá, o aplicativo de exemplo hello recebe um token que pode ser usado tooquery Microsoft Graph API ou uma API da Web protegida pelo Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="65c7e-118">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="65c7e-119">APIs, como o Microsoft Graph exigem um tooallow de token de acesso ao acessar recursos específicos – por exemplo, tooread um perfil de usuário, acessar o calendário do usuário ou enviar um email.</span><span class="sxs-lookup"><span data-stu-id="65c7e-119">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="65c7e-120">Seu aplicativo pode solicitar um token de acesso usando MSAL tooaccess esses recursos especificando escopos de API.</span><span class="sxs-lookup"><span data-stu-id="65c7e-120">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="65c7e-121">Esse token de acesso é, em seguida, o recurso protegido de toohello adicionado cabeçalho de autorização HTTP para todas as chamadas feitas em relação a saudação.</span><span class="sxs-lookup"><span data-stu-id="65c7e-121">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="65c7e-122">A MSAL gerencia o armazenamento em cache e a atualização de tokens de acesso para você, de forma que o aplicativo não precise fazer isso.</span><span class="sxs-lookup"><span data-stu-id="65c7e-122">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>

### <a name="libraries"></a><span data-ttu-id="65c7e-123">Bibliotecas</span><span class="sxs-lookup"><span data-stu-id="65c7e-123">Libraries</span></span>

<span data-ttu-id="65c7e-124">Este guia usa Olá bibliotecas a seguir:</span><span class="sxs-lookup"><span data-stu-id="65c7e-124">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="65c7e-125">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="65c7e-125">Library</span></span>|<span data-ttu-id="65c7e-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="65c7e-126">Description</span></span>|
|---|---|
|[<span data-ttu-id="65c7e-127">com.microsoft.identity.client</span><span class="sxs-lookup"><span data-stu-id="65c7e-127">com.microsoft.identity.client</span></span>](http://javadoc.io/doc/com.microsoft.identity.client/msal)|<span data-ttu-id="65c7e-128">MSAL (Biblioteca de Autenticação da Microsoft)</span><span class="sxs-lookup"><span data-stu-id="65c7e-128">Microsoft Authentication Library (MSAL)</span></span>|
