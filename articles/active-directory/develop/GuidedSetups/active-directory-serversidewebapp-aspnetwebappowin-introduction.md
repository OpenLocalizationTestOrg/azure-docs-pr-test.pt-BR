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
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a>Adicionar entrada ao aplicativo web do Microsoft tooan ASP.NET

Este guia demonstra como tooimplement entrar com a Microsoft usando uma solução do ASP.NET MVC com um aplicativo baseado em navegador da web tradicional, usa o OpenID Connect. 

No final da saudação deste guia, o seu aplicativo ser capaz de tooaccept sinal ins de pessoal contas (incluindo o outlook.com, live.com e outros), bem como trabalhar e estudante contas de qualquer empresa ou organização que foi integrado ao Active Directory do Azure. 

> Este guia exige o Visual Studio 2015 Atualização 3 ou o Visual Studio 2017.  Ainda não tem?  [Baixar o Visual Studio 2017 gratuitamente](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a>Como funciona este guia

![Como funciona este guia](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

Este guia se baseia no cenário de saudação em que um navegador acessa um site da web ASP.NET, solicitando uma tooauthenticate de usuário por meio de um botão de login. Nesse cenário, a maior parte da página de web hello trabalho toorender Olá ocorre no lado do servidor de saudação.

## <a name="libraries"></a>Bibliotecas

Este guia usa Olá bibliotecas a seguir:

|Biblioteca|Descrição|
|---|---|
|[Microsoft.Owin.Security.OpenIdConnect](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|Middleware que permite que um aplicativo toouse OpenIdConnect para autenticação|
|[Microsoft.Owin.Security.Cookies](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|Middleware que permite que uma sessão de usuário do aplicativo toomaintain uso de cookies|
|[Microsoft.Owin.Host.SystemWeb](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|Permite que aplicativos baseados no OWIN toorun no IIS usando o pipeline de solicitação do ASP.NET Olá|

