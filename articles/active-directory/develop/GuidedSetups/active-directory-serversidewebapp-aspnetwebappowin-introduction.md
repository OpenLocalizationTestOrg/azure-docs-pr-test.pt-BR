---
title: "aaaAzure AD v2 ASP.NET Web Server Introdução - Introdução | Microsoft Docs"
description: "Implementando a opção Entrar com uma Conta da Microsoft em uma solução ASP.NET com um aplicativo tradicional baseado em navegador da Web usando o padrão OpenID Connect"
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
ms.openlocfilehash: d6449926af2bdad24cbc8e91f74885a08f909103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a><span data-ttu-id="f2992-103">Adicionar entrada ao aplicativo web do Microsoft tooan ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f2992-103">Add sign-in with Microsoft tooan ASP.NET web app</span></span>

<span data-ttu-id="f2992-104">Este guia demonstra como tooimplement entrar com a Microsoft usando uma solução do ASP.NET MVC com um aplicativo baseado em navegador da web tradicional, usa o OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f2992-104">This guide demonstrates how tooimplement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="f2992-105">No final da saudação deste guia, o seu aplicativo ser capaz de tooaccept sinal ins de pessoal contas (incluindo o outlook.com, live.com e outros), bem como trabalhar e estudante contas de qualquer empresa ou organização que foi integrado ao Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2992-105">At hello end of this guide, your application will be able tooaccept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="f2992-106">Este guia exige o Visual Studio 2015 Atualização 3 ou o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="f2992-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="f2992-107">Ainda não tem?</span><span class="sxs-lookup"><span data-stu-id="f2992-107">Don’t have it?</span></span>  [<span data-ttu-id="f2992-108">Baixar o Visual Studio 2017 gratuitamente</span><span class="sxs-lookup"><span data-stu-id="f2992-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="f2992-109">Como funciona este guia</span><span class="sxs-lookup"><span data-stu-id="f2992-109">How this guide works</span></span>

![Como funciona este guia](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="f2992-111">Este guia se baseia no cenário de saudação em que um navegador acessa um site da web ASP.NET, solicitando uma tooauthenticate de usuário por meio de um botão de login.</span><span class="sxs-lookup"><span data-stu-id="f2992-111">This guide is based on hello scenario where a browser accesses an ASP.NET web site, requesting a user tooauthenticate via a sign-in button.</span></span> <span data-ttu-id="f2992-112">Nesse cenário, a maior parte da página de web hello trabalho toorender Olá ocorre no lado do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2992-112">In this scenario, most of hello work toorender hello web page occurs on hello server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="f2992-113">Bibliotecas</span><span class="sxs-lookup"><span data-stu-id="f2992-113">Libraries</span></span>

<span data-ttu-id="f2992-114">Este guia usa Olá bibliotecas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2992-114">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="f2992-115">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="f2992-115">Library</span></span>|<span data-ttu-id="f2992-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="f2992-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="f2992-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="f2992-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="f2992-118">Middleware que permite que um aplicativo toouse OpenIdConnect para autenticação</span><span class="sxs-lookup"><span data-stu-id="f2992-118">Middleware that enables an application toouse OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="f2992-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="f2992-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="f2992-120">Middleware que permite que uma sessão de usuário do aplicativo toomaintain uso de cookies</span><span class="sxs-lookup"><span data-stu-id="f2992-120">Middleware that enables an application toomaintain user session using cookies</span></span>|
|[<span data-ttu-id="f2992-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="f2992-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="f2992-122">Permite que aplicativos baseados no OWIN toorun no IIS usando o pipeline de solicitação do ASP.NET Olá</span><span class="sxs-lookup"><span data-stu-id="f2992-122">Enables OWIN-based applications toorun on IIS using hello ASP.NET request pipeline</span></span>|

