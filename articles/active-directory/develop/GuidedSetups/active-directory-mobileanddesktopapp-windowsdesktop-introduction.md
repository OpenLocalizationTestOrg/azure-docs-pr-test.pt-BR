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
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a>Chamar hello Microsoft Graph API a partir de um aplicativo de área de trabalho do Windows

Este guia demonstra como um aplicativo .NET nativo da Área de Trabalho do Windows (XAML) pode obter um token de acesso e chamar a API do Microsoft Graph ou outras APIs que exigem tokens de acesso por meio do ponto de extremidade do Azure Active Directory v2.

No final da saudação deste guia, seu aplicativo será ser capaz de toocall uma API protegida usando contas pessoais (incluindo o outlook.com, live.com e outros) bem como trabalhar e contas de estudante de qualquer empresa ou organização que possui o Active Directory do Azure.  

> Este guia exige o Visual Studio 2015 Atualização 3 ou o Visual Studio 2017.  Ainda não tem? [Baixar o Visual Studio 2017 gratuitamente](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a>Como funciona este guia

![Como funciona este guia](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

aplicativo de exemplo Hello criado por este guia permite que um tooquery Microsoft Graph API do aplicativo de área de trabalho do Windows ou uma API da Web que aceita tokens de ponto de extremidade do Active Directory do Azure v2. Para este cenário, um token é adicionado tooHTTP solicitações por meio do cabeçalho de autorização de saudação. Renovação e aquisição de token é tratado por Olá biblioteca de autenticação da Microsoft (MSAL).


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Manipulando a aquisição de token para acessar APIs Web protegidas

Após a autenticação do usuário Olá, o aplicativo de exemplo hello recebe um token que pode ser usado tooquery Microsoft Graph API ou uma API da Web protegida pelo Microsoft Azure Active Directory v2.

APIs, como o Microsoft Graph exigem um tooallow de token de acesso ao acessar recursos específicos – por exemplo, tooread um perfil de usuário, acessar o calendário do usuário ou enviar um email. Seu aplicativo pode solicitar um token de acesso usando MSAL tooaccess esses recursos especificando escopos de API. Esse token de acesso é, em seguida, o recurso protegido de toohello adicionado cabeçalho de autorização HTTP para todas as chamadas feitas em relação a saudação. 

A MSAL gerencia o armazenamento em cache e a atualização de tokens de acesso para você, de forma que o aplicativo não precise fazer isso.


### <a name="nuget-packages"></a>Pacotes NuGet

Este guia usa Olá pacotes do NuGet a seguir:

|Biblioteca|Descrição|
|---|---|
|[Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client)|MSAL (Biblioteca de Autenticação da Microsoft)|

