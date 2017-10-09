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
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a>Chamar hello Microsoft Graph API a partir de um aplicativo do Android

Este guia demonstra como um aplicativo nativo do Android pode obter um token de acesso e chamar a API do Microsoft Graph ou outras APIs que exigem tokens de acesso por meio do ponto de extremidade do Azure Active Directory v2.

No final da saudação deste guia, seu aplicativo será ser capaz de toocall uma API protegida usando contas pessoais (incluindo o outlook.com, live.com e outros) bem como trabalhar e contas de estudante de qualquer empresa ou organização que possui o Active Directory do Azure.  

### <a name="how-this-sample-works"></a>Como funciona esta amostra
![Como funciona esta amostra](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

exemplo Hello criado por este guia se baseia em um cenário em que um aplicativo do Android é tooquery usado um API da Web que aceita tokens do Active Directory do Azure v2 ponto de extremidade – nesse caso, a API do Microsoft Graph. Para este cenário, um token é adicionado tooHTTP solicitações por meio do cabeçalho de autorização de saudação. Renovação e aquisição de token é tratado por Olá biblioteca de autenticação da Microsoft (MSAL).

### <a name="pre-requisites"></a>Pré-requisitos
* Esta instalação guiada se concentra no Android Studio, mas qualquer outro ambiente de desenvolvimento de aplicativos do Android também é aceitável. 
* O SDK 21 ou mais novo do Android é necessário (o recomendado é o SDK 25).
* O Google Chrome ou um navegador da Web que usa Guias Personalizadas é necessário para esta versão da MSAL (Biblioteca de Autenticação da Microsoft) para Android.

> Observação: o Google Chrome não está incluído no Emulador do Visual Studio para Android. Recomendamos que você tootest esse código em um emulador com 25 de API ou uma imagem com API 21 ou mais recente com o Google Chrome instalados.


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a>Como toohandle token tooaccess de aquisição de uma API da Web protegida

Após a autenticação do usuário Olá, o aplicativo de exemplo hello recebe um token que pode ser usado tooquery Microsoft Graph API ou uma API da Web protegida pelo Microsoft Azure Active Directory v2.

APIs, como o Microsoft Graph exigem um tooallow de token de acesso ao acessar recursos específicos – por exemplo, tooread um perfil de usuário, acessar o calendário do usuário ou enviar um email. Seu aplicativo pode solicitar um token de acesso usando MSAL tooaccess esses recursos especificando escopos de API. Esse token de acesso é, em seguida, o recurso protegido de toohello adicionado cabeçalho de autorização HTTP para todas as chamadas feitas em relação a saudação. 

A MSAL gerencia o armazenamento em cache e a atualização de tokens de acesso para você, de forma que o aplicativo não precise fazer isso.

### <a name="libraries"></a>Bibliotecas

Este guia usa Olá bibliotecas a seguir:

|Biblioteca|Descrição|
|---|---|
|[com.microsoft.identity.client](http://javadoc.io/doc/com.microsoft.identity.client/msal)|MSAL (Biblioteca de Autenticação da Microsoft)|
