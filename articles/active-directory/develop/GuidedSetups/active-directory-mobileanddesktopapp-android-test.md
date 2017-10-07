---
title: "aaaAzure AD v2 Android Introdução - teste | Microsoft Docs"
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Testar seu código

1. Implante seu código tooyour/emulador de dispositivo.
2. Quando você estiver pronto tootest, use um Microsoft Azure Active Directory (conta organizacional) ou um toosign de conta Account da Microsoft (live.com, outlook.com) no. 

![Captura de tela de exemplo](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
<br/><br/>
![Conexão](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)

### <a name="consent"></a>Consentimento
Olá primeira vez que um usuário faz logon no aplicativo tooyour, será apresentada com uma tela consentimento com, semelhante toohello de abaixo, onde precisam aceitar tooexplicitly: 

![Consentimento](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a>Resultados esperados
Você deve ver os resultados de saudação do tooMicrosoft chamada de API do Graph 'me' ponto de extremidade usado tootooobtain perfil de usuário Olá - https://graph.microsoft.com/v1.0/me. Para obter uma lista de pontos de extremidade comuns do Microsoft Graph, consulte este [artigo](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Mais informações sobre escopos e permissões delegadas

Olá Microsoft Graph API requer Olá `user.read` tooread Olá perfil de usuário do escopo. Esse escopo é adicionado automaticamente, por padrão, a cada aplicativo que é registrado em nosso portal de registro. Algumas outras APIs do Microsoft Graph, bem como APIs personalizadas do servidor de back-end, podem exigir escopos adicionais. Por exemplo, para o Microsoft Graph, Olá escopo `Calendars.Read` é calendários do usuário de saudação toolist necessária. Em ordem tooaccess Olá calendário do usuário em um contexto de um aplicativo, você precisa Olá tooadd `Calendars.Read` delegado informações do registro do aplicativo permissão toohello e adicione Olá `Calendars.Read` toohello escopo `acquireTokenSilentAsync` chamar. usuário Olá pode ser solicitado para consente adicionais que você aumenta o número de saudação de escopos.

<!--end-collapse-->
