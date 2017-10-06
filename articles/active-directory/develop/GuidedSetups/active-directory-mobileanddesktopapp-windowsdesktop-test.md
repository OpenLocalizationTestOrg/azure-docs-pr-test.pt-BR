---
title: "aaaAzure AD v2 Windows Desktop Introdução - teste | Microsoft Docs"
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
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Testar seu código

Em ordem tootest seu aplicativo, pressione `F5` toorun seu projeto no Visual Studio. A Janela Principal deve ser exibida:

![Captura de tela de exemplo](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

Quando você estiver pronto tootest, clique em *chamar a API do Microsoft Graph* e usar um Microsoft Azure Active Directory (conta organizacional) ou um toosign de conta Account da Microsoft (live.com, outlook.com) no. Ele é Olá primeira vez, você verá uma janela solicitando que usuário toosign em:

![Conexão](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a>Consentimento
Olá primeira vez que você entrar no aplicativo tooyour, você verá uma tela consentimento com, semelhante toohello de abaixo, onde você precisa aceitar tooexplicitly:

![Tela de consentimento](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a>Resultados esperados
Você deve ver as informações de perfil do usuário retornadas pela chamada de API do Graph Microsoft hello na tela de resultados de chamadas de API de saudação.

Você também verá informações básicas sobre o token Olá adquirido por meio de `AcquireTokenAsync` ou `AcquireTokenSilentAsync` na caixa de informações de Token hello:

|Propriedade  |Formatar  |Descrição |
|---------|---------|---------|
|Nome | {Nome completo do usuário} |primeiro e o último nome de usuário Olá|
|Nome de Usuário |<span>user@domain.com</span> |saudação de nome de usuário usado tooidentify usuário de saudação|
|O Token Expira |{DateTime}         |tempo de saudação na qual Olá token expira. MSAL estenderá a data de validade Olá para você renovando token hello quando necessário|
|Token de acesso |{String}         |cadeia de caracteres de token do Hello enviados que será enviado solicitações tooHTTP que exigem um cabeçalho de autorização|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Mais informações sobre escopos e permissões delegadas
API do Graph requer Olá `user.read` tooread perfil de usuário do escopo. Esse escopo é adicionado automaticamente, por padrão, a cada aplicativo que é registrado em nosso portal de registro. Algumas outras APIs do Graph, bem como APIs personalizadas do servidor de back-end, exigem escopos adicionais. Por exemplo, para o gráfico, `Calendars.Read` é calendários do usuário toolist necessária. Em ordem tooaccess Olá calendário do usuário em um contexto de um aplicativo, você precisa tooadd `Calendars.Read` delegadas informações do registro do aplicativo e, em seguida, adicionar `Calendars.Read` toohello `AcquireTokenAsync` chamar. Usuário pode ser solicitado para consente adicionais que você aumenta o número de saudação de escopos.

<!--end-collapse-->



