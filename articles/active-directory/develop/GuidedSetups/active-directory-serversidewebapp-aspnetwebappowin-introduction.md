---
title: "Introdução ao servidor Web ASP.NET no Azure AD v2 – Introdução | Microsoft Docs"
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
ms.openlocfilehash: 8062923b6270ec6253dc231a3db4333cf4666b42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-with-microsoft-to-an-aspnet-web-app"></a><span data-ttu-id="e3c18-103">Adicionar a opção Entrar com uma Conta da Microsoft a um aplicativo Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e3c18-103">Add sign-in with Microsoft to an ASP.NET web app</span></span>

<span data-ttu-id="e3c18-104">Este guia demonstra como implementar a opção Entrar com uma Conta da Microsoft usando uma solução ASP.NET MVC com um aplicativo tradicional baseado em navegador da Web usando o OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="e3c18-104">This guide demonstrates how to implement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="e3c18-105">Ao final deste guia, seu aplicativo poderá aceitar conexões de contas pessoais (incluindo outlook.com, live.com e outras), bem como contas corporativas ou de estudante de qualquer empresa ou organização que foi integrada ao Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e3c18-105">At the end of this guide, your application will be able to accept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="e3c18-106">Este guia exige o Visual Studio 2015 Atualização 3 ou o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e3c18-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="e3c18-107">Ainda não tem?</span><span class="sxs-lookup"><span data-stu-id="e3c18-107">Don’t have it?</span></span>  [<span data-ttu-id="e3c18-108">Baixar o Visual Studio 2017 gratuitamente</span><span class="sxs-lookup"><span data-stu-id="e3c18-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="e3c18-109">Como funciona este guia</span><span class="sxs-lookup"><span data-stu-id="e3c18-109">How this guide works</span></span>

![Como funciona este guia](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="e3c18-111">Este guia se baseia no cenário em que um navegador acessa um site ASP.NET, solicitando a autenticação de um usuário por meio de um botão de conexão.</span><span class="sxs-lookup"><span data-stu-id="e3c18-111">This guide is based on the scenario where a browser accesses an ASP.NET web site, requesting a user to authenticate via a sign-in button.</span></span> <span data-ttu-id="e3c18-112">Nesse cenário, a maior parte do trabalho de renderização da página da Web ocorre no lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="e3c18-112">In this scenario, most of the work to render the web page occurs on the server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="e3c18-113">Bibliotecas</span><span class="sxs-lookup"><span data-stu-id="e3c18-113">Libraries</span></span>

<span data-ttu-id="e3c18-114">Este guia usa as seguintes bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="e3c18-114">This guide uses the following libraries:</span></span>

|<span data-ttu-id="e3c18-115">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="e3c18-115">Library</span></span>|<span data-ttu-id="e3c18-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="e3c18-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="e3c18-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="e3c18-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="e3c18-118">Middleware que permite que um aplicativo use OpenIdConnect para autenticação</span><span class="sxs-lookup"><span data-stu-id="e3c18-118">Middleware that enables an application to use OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="e3c18-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="e3c18-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="e3c18-120">Middleware que permite que um aplicativo mantenha a sessão de usuário usando cookies</span><span class="sxs-lookup"><span data-stu-id="e3c18-120">Middleware that enables an application to maintain user session using cookies</span></span>|
|[<span data-ttu-id="e3c18-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="e3c18-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="e3c18-122">Permite que os aplicativos baseado em OWIN sejam executados no IIS usando o pipeline de solicitação do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e3c18-122">Enables OWIN-based applications to run on IIS using the ASP.NET request pipeline</span></span>|

