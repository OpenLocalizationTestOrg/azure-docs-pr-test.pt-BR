---
title: "aaaAzure AD v2 iOS guia de Introdução - teste | Microsoft Docs"
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
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a>Testar consulta Olá Microsoft Graph API do seu aplicativo iOS

Pressione `Command`  +  `R` toorun código de saudação no simulador hello.

![Captura de tela de exemplo](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

Quando você estiver pronto tootest, toque em *'Chamar Microsoft Graph API'* e você será solicitado tootype seu nome de usuário e senha.

### <a name="consent"></a>Consentimento
Olá primeira vez que você entrar no aplicativo tooyour, você verá uma tela consentimento com, semelhante toohello de abaixo, onde você precisa aceitar tooexplicitly:

![Tela de consentimento](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a>Resultados esperados
Você deve ver as informações de perfil do usuário retornadas pela chamada de API do Graph Microsoft hello em hello *log* seção.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Mais informações sobre escopos e permissões delegadas

Olá Microsoft Graph API requer Olá `user.read` tooread Olá perfil de usuário do escopo. Esse escopo é adicionado automaticamente, por padrão, a cada aplicativo que é registrado em nosso portal de registro. Algumas outras APIs do Microsoft Graph, bem como APIs personalizadas do servidor de back-end, podem exigir escopos adicionais. Por exemplo, para o Microsoft Graph, Olá escopo `Calendars.Read` é calendários do usuário de saudação toolist necessária. Em ordem tooaccess Olá calendário do usuário em um contexto de um aplicativo, você precisa Olá tooadd `Calendars.Read` delegado informações do registro do aplicativo permissão toohello e adicione Olá `Calendars.Read` toohello escopo `acquireTokenSilent` chamar. usuário Olá pode ser solicitado para consente adicionais que você aumenta o número de saudação de escopos.

<!--end-collapse-->



