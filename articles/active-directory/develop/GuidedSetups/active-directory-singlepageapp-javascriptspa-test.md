---
title: "aaaAzure AD v2 JS SPA interativa instalação - teste | Microsoft Docs"
description: Como aplicativos JavaScript SPA podem chamar uma API que exige tokens de acesso pelo ponto de extremidade do Azure Active Directory v2
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Testar seu código

> ### <a name="testing-with-visual-studio"></a>Testes com o Visual Studio
> Se você estiver usando o Visual Studio, pressione `F5` toorun seu projeto: navegador Olá abre e direciona você muito*http://localhost: {port}* onde você pode ver Olá *chamar a API do Microsoft Graph* botão.

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a>Testando com Python ou outro servidor Web
> Se você não estiver usando o Visual Studio, verifique se seu servidor web é iniciado e está configurado a porta TCP de tooa toolisten com base em Olá pasta que contém o *index* arquivo. Para Python, você pode iniciar a escuta a porta toohello executando Olá no comando Olá prompt / terminal, na pasta do aplicativo hello:
> 
> ```bash
> python -m http.server 8080
> ```
>  Em seguida, abra o navegador hello e digite *http://localhost:8080* ou *http://localhost: {port}* - onde hello *porta* corresponde a porta de toohello seu servidor web escuta. Você deve ver o conteúdo de saudação da página do index com hello *chamar a API do Microsoft Graph* botão.

## <a name="test-your-application"></a>Teste seu aplicativo

Depois de navegador Olá carrega sua *index*, clique em hello *chamar a API do Microsoft Graph* botão. Se isso for Olá pela primeira vez, Olá redirecionamentos do navegador você toohello v2 do Active Directory do Microsoft Azure ponto de extremidade, onde você está solicitado toosign no.
 
![Captura de tela de exemplo](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a>Consentimento
Hello primeira vez que entrar no aplicativo tooyour, você verá um consentimento tela semelhante toohello seguinte, em que você precisa tooaccept:

 ![Tela de consentimento](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a>Resultados esperados
Você deve ver as informações de perfil de usuário retornadas pelo hello resposta de chamada de API do Microsoft Graph.
 
 ![Resultados](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

Você também ver informações básicas sobre o token Olá adquirido em Olá *Token de acesso* e *declarações do Token de ID* caixas.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Mais informações sobre escopos e permissões delegadas

Olá Microsoft Graph API requer Olá `user.read` tooread Olá perfil de usuário do escopo. Esse escopo é adicionado automaticamente, por padrão, a cada aplicativo que é registrado em nosso portal de registro. Algumas outras APIs do Microsoft Graph, bem como APIs personalizadas do servidor de back-end, podem exigir escopos adicionais. Por exemplo, para o Microsoft Graph, Olá escopo `Calendars.Read` é calendários do usuário de saudação toolist necessária. Em ordem tooaccess Olá calendário do usuário no contexto de saudação de um aplicativo, você precisa Olá tooadd `Calendars.Read` delegado informações do registro do aplicativo permissão toohello e adicione Olá `Calendars.Read` toohello escopo `acquireTokenSilent` chamar. usuário Olá pode ser solicitado para consente adicionais que você aumenta o número de saudação de escopos.

Se uma API de back-end não exigir um escopo (não recomendado), você pode usar o hello `clientId` como escopo Olá Olá `acquireTokenSilent` e/ou `acquireTokenRedirect` chamadas.

<!--end-collapse-->
