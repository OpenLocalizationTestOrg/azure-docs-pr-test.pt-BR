---
title: "Introdução ao Android no Azure AD v2 – Introdução | Microsoft Docs"
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
ms.openlocfilehash: d933781713456f73aa76db557fdf35672dfb2a29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="call-the-microsoft-graph-api-from-an-android-app"></a><span data-ttu-id="9be72-103">Chamar a API do Microsoft Graph em um aplicativo do Android</span><span class="sxs-lookup"><span data-stu-id="9be72-103">Call the Microsoft Graph API from an Android app</span></span>

<span data-ttu-id="9be72-104">Este guia demonstra como um aplicativo nativo do Android pode obter um token de acesso e chamar a API do Microsoft Graph ou outras APIs que exigem tokens de acesso por meio do ponto de extremidade do Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="9be72-104">This guide demonstrates how a native Android application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="9be72-105">Ao final deste guia, seu aplicativo poderá chamar uma API protegida usando contas pessoais (incluindo outlook.com, live.com e outras), bem como contas corporativas ou de estudante de qualquer empresa ou organização que tem o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9be72-105">At the end of this guide, your application will be able to call a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

### <a name="how-this-sample-works"></a><span data-ttu-id="9be72-106">Como funciona esta amostra</span><span class="sxs-lookup"><span data-stu-id="9be72-106">How this sample works</span></span>
![Como funciona esta amostra](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

<span data-ttu-id="9be72-108">A amostra criada por este guia se baseia em um cenário no qual um aplicativo do Android é usado para consultar uma API Web que aceita tokens do ponto de extremidade do Azure Active Directory v2 – nesse caso, a API do Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="9be72-108">The sample created by this guide is based on a scenario where an Android application is used to query a Web API that accepts tokens from Azure Active Directory v2 endpoint – in this case, Microsoft Graph API.</span></span> <span data-ttu-id="9be72-109">Para esse cenário, um token é adicionado às solicitações HTTP por meio do cabeçalho de Autorização.</span><span class="sxs-lookup"><span data-stu-id="9be72-109">For this scenario, a token is added to HTTP requests via the Authorization header.</span></span> <span data-ttu-id="9be72-110">A aquisição e a renovação de tokens são manipuladas pela MSAL (Biblioteca de Autenticação da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="9be72-110">Token acquisition and renewal is handled by the Microsoft Authentication Library (MSAL).</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="9be72-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9be72-111">Pre-requisites</span></span>
* <span data-ttu-id="9be72-112">Esta instalação guiada se concentra no Android Studio, mas qualquer outro ambiente de desenvolvimento de aplicativos do Android também é aceitável.</span><span class="sxs-lookup"><span data-stu-id="9be72-112">This guided setup is focused on Android Studio, but any other Android application development environment is also acceptable.</span></span> 
* <span data-ttu-id="9be72-113">O SDK 21 ou mais novo do Android é necessário (o recomendado é o SDK 25).</span><span class="sxs-lookup"><span data-stu-id="9be72-113">Android SDK 21 or newer is required (SDK 25 is recommended).</span></span>
* <span data-ttu-id="9be72-114">O Google Chrome ou um navegador da Web que usa Guias Personalizadas é necessário para esta versão da MSAL (Biblioteca de Autenticação da Microsoft) para Android.</span><span class="sxs-lookup"><span data-stu-id="9be72-114">Google Chrome or a web browser using Custom Tabs is required for this release of Microsoft Authentication Library (MSAL) for Android.</span></span>

> <span data-ttu-id="9be72-115">Observação: o Google Chrome não está incluído no Emulador do Visual Studio para Android.</span><span class="sxs-lookup"><span data-stu-id="9be72-115">Note: Google Chrome is not included on Visual Studio Emulator for Android.</span></span> <span data-ttu-id="9be72-116">Recomendamos testar esse código em um Emulador com a API 25 ou uma imagem com a API 21 ou mais nova que tem o Google Chrome instalado.</span><span class="sxs-lookup"><span data-stu-id="9be72-116">We recommend you to test this code on an Emulator with API 25 or an image with API 21 or newer that has with Google Chrome installed.</span></span>


### <a name="how-to-handle-token-acquisition-to-access-a-protected-web-api"></a><span data-ttu-id="9be72-117">Como manipular a aquisição de tokens para acessar uma API Web protegida</span><span class="sxs-lookup"><span data-stu-id="9be72-117">How to handle token acquisition to access a protected Web API</span></span>

<span data-ttu-id="9be72-118">Depois que o usuário é autenticado, o aplicativo de exemplo recebe um token que pode ser usado para consultar a API do Microsoft Graph ou uma API Web protegida pelo Microsoft Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="9be72-118">After the user authenticates, the sample application receives a token that can be used to query Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="9be72-119">APIs como o Microsoft Graph exigem um token de acesso para permitir o acesso a recursos específicos – por exemplo, ler um perfil de usuário, acessar o calendário do usuário ou enviar um email.</span><span class="sxs-lookup"><span data-stu-id="9be72-119">APIs such as Microsoft Graph require an access token to allow accessing specific resources – for example, to read a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="9be72-120">O aplicativo pode solicitar um token de acesso que usa a MSAL para acessar esses recursos especificando escopos de API.</span><span class="sxs-lookup"><span data-stu-id="9be72-120">Your application can request an access token using MSAL to access these resources by specifying API scopes.</span></span> <span data-ttu-id="9be72-121">Esse token de acesso é então adicionado ao cabeçalho de Autorização HTTP de cada chamada feita no recurso protegido.</span><span class="sxs-lookup"><span data-stu-id="9be72-121">This access token is then added to the HTTP Authorization header for every call made against the protected resource.</span></span> 

<span data-ttu-id="9be72-122">A MSAL gerencia o armazenamento em cache e a atualização de tokens de acesso para você, de forma que o aplicativo não precise fazer isso.</span><span class="sxs-lookup"><span data-stu-id="9be72-122">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>

### <a name="libraries"></a><span data-ttu-id="9be72-123">Bibliotecas</span><span class="sxs-lookup"><span data-stu-id="9be72-123">Libraries</span></span>

<span data-ttu-id="9be72-124">Este guia usa as seguintes bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="9be72-124">This guide uses the following libraries:</span></span>

|<span data-ttu-id="9be72-125">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="9be72-125">Library</span></span>|<span data-ttu-id="9be72-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="9be72-126">Description</span></span>|
|---|---|
|[<span data-ttu-id="9be72-127">com.microsoft.identity.client</span><span class="sxs-lookup"><span data-stu-id="9be72-127">com.microsoft.identity.client</span></span>](http://javadoc.io/doc/com.microsoft.identity.client/msal)|<span data-ttu-id="9be72-128">MSAL (Biblioteca de Autenticação da Microsoft)</span><span class="sxs-lookup"><span data-stu-id="9be72-128">Microsoft Authentication Library (MSAL)</span></span>|
