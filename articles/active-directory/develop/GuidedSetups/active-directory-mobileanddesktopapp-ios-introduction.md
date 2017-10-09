---
title: "aaaAzure AD v2 iOS guia de Introdução - Introdução | Microsoft Docs"
description: Como aplicativos iOS (Swift) podem chamar uma API que exige tokens de acesso pelo ponto de extremidade do Azure Active Directory v2
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: f40aebbb75490912e533aecc7eedfb2b2dcd8c6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a>Chamar hello Microsoft Graph API a partir de um aplicativo iOS

Este guia demonstra como um aplicativo iOS nativo (Swift) pode acessar um token e chamar hello Microsoft Graph API ou outras APIs que requerem tokens de acesso do ponto de extremidade do Active Directory do Azure v2.

No final da saudação deste guia, seu aplicativo será ser capaz de toocall uma API protegida usando contas pessoais (incluindo o outlook.com, live.com e outros) bem como trabalhar e contas de estudante de qualquer empresa ou organização que possui o Active Directory do Azure.

> ### <a name="pre-requisites"></a>Pré-requisitos
> - O XCode 8.x é necessário para este guia. Você pode baixar o XCode [aqui](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "URL de download do XCode").
> - [Carthage](https://github.com/Carthage/Carthage) para gerenciamento de pacotes

### <a name="how-this-guide-works"></a>Como funciona este guia

![Como funciona este guia](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

aplicativo de exemplo Hello criado por este guia permite que uma saudação de tooquery de aplicativo do iOS Microsoft Graph API ou uma API da Web que aceita tokens de ponto de extremidade do Active Directory do Azure v2. Para este cenário, um token é adicionado tooHTTP solicitações por meio do cabeçalho de autorização de saudação. Renovação e aquisição de token é tratado por Olá biblioteca de autenticação da Microsoft (MSAL).


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Manipulando a aquisição de token para acessar APIs Web protegidas

Após a autenticação do usuário Olá, o aplicativo de exemplo hello recebe um token que pode ser usado tooquery Olá Microsoft Graph API ou uma API da Web protegida pelo Microsoft Azure Active Directory v2.

APIs, como o Microsoft Graph exigem um tooallow de token de acesso ao acessar recursos específicos – por exemplo, tooread um perfil de usuário, acessar o calendário do usuário ou enviar um email. O aplicativo pode solicitar um token de acesso que usa a MSAL especificando escopos de API. Esse token de acesso é, em seguida, o recurso protegido de toohello adicionado cabeçalho de autorização HTTP para todas as chamadas feitas em relação a saudação.

A MSAL gerencia o armazenamento em cache e a atualização de tokens de acesso para você, de forma que o aplicativo não precise fazer isso.


### <a name="nuget-packages"></a>Pacotes NuGet

Este guia usa Olá pacotes do NuGet a seguir:

|Biblioteca|Descrição|
|---|---|
|[MSAL.framework](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|Versão prévia da Biblioteca de Autenticação da Microsoft para iOS|

