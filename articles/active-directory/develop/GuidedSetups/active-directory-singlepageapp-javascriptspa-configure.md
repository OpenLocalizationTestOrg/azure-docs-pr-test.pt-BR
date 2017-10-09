---
title: "aaaAzure AD v2 JS SPA interativa de instalação - configurar | Microsoft Docs"
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
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a>Registre seu aplicativo

Há várias maneiras toocreate um aplicativo, selecione um deles:

### <a name="option-1-register-your-application-express-mode"></a>Opção 1: Registrar seu aplicativo (modo Expresso)
Agora você precisa tooregister seu aplicativo no hello *Portal de registro de aplicativo do Microsoft*:

1.  Registrar seu aplicativo por meio de saudação [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)
2.  Insira um nome para o aplicativo e seu email
3.  Certifique-se de opção de saudação *instalação interativa* é verificada
4.  Siga a ID do aplicativo hello instruções tooobtain hello e colá-lo em seu código

### <a name="option-2-register-your-application-advanced-mode"></a>Opção 2: Registrar seu aplicativo (modo Avançado)

1. Vá toohello [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister um aplicativo
2. Insira um nome para o aplicativo e seu email 
3. Certifique-se de opção de saudação *instalação interativa* está desmarcada
4.  Clique em `Add Platform` e selecione `Web`
5. Adicionar Olá `Redirect URL` que correspondem a URL do aplicativo toohello com base em seu servidor web. Consulte as seções de saudação abaixo para obter instruções sobre como tooset / obter URL de redirecionamento Olá no Visual Studio e Python.
6. Clique em *Salvar*

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Instruções do Visual Studio para obter a URL de redirecionamento
> Execute Olá instruções tooobtain sua URL de redirecionamento:
> 1.    Em *Solution Explorer*, selecione o projeto hello e examinar Olá `Properties` janela (se você não vir uma janela de propriedades, pressione `F4`)
> 2.    Copie o valor de saudação do `URL` toohello área de transferência:<br/> ![Propriedades do projeto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Alternar back toohello *Portal de registro de aplicativo* e cole o valor de saudação como um `Redirect URL` e clique em 'Salvar'

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Definir a URL de Redirecionamento para o Python
> Para Python, você pode definir a porta do servidor web hello por meio da linha de comando. Esta instalação interativa usa a saudação porta 8080 para referência, mas se sentir livre toouse qualquer porta disponível. Em qualquer caso, siga as instruções de saudação abaixo tooset uma URL de redirecionamento nas informações de registro de aplicativo hello:<br/>
> - Alternar back toohello *Portal de registro de aplicativo* e defina `http://localhost:8080/` como um `Redirect URL`, ou use `http://localhost:[port]/` se você estiver usando uma porta TCP personalizada (onde *[port]* é a porta TCP personalizada Olá número) e clique em 'Salvar'


#### <a name="configure-your-javascript-spa"></a>Configurar o JavaScript SPA

1.  Crie um arquivo chamado `msalconfig.js` que contém informações de registro de aplicativo hello. Se você estiver usando um projeto Visual Studio, selecione hello (pasta raiz do projeto), com o botão direito e selecione: `Add`  >  `New Item`  >  `JavaScript File`. Nomeie-o `msalconfig.js`
2.  Adicionar Olá tooyour de código a seguir `msalconfig.js` arquivo:

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
Substituir <code>Enter_the_Application_Id_here</code> com hello Id de aplicativo que você acabou de registrar
</li>
</ol>
