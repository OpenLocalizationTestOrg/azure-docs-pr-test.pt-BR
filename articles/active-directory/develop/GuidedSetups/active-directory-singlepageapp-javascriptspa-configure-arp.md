---
title: "aaaAzure AD v2 JS SPA interativa instalação - configurar ARP () | Microsoft Docs"
description: Como aplicativos JavaScript SPA podem chamar uma API que exige tokens de acesso pelo ponto de extremidade do Azure Active Directory v2 (ARP)
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
ms.openlocfilehash: 157f4e342cd684294e24da6ee1fad8a7c2fc266a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Adicionar tooyour informações de registro do aplicativo hello aplicativo

Nesta etapa, você precisa tooconfigure Olá URL de redirecionamento das suas informações de registro de aplicativo e adicionar aplicativo de JavaScript SPA hello Id do aplicativo tooyour.

### <a name="configure-redirect-url"></a>Configurar a URL de redirecionamento

Configurar Olá `Redirect URL` campo acima com hello URL para a sua página index com base em seu servidor web, em seguida, clique em *atualização*.


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Instruções do Visual Studio para obter a URL de redirecionamento
> tooobtain sua URL de redirecionamento, siga Olá instruções abaixo:
> 1.    Em *Solution Explorer*, selecione o projeto hello e examinar Olá `Properties` janela (se você não vir uma janela de propriedades, pressione `F4`)
> 2.    Copie o valor de saudação do `URL` toohello área de transferência:<br/> ![Propriedades do projeto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Cole o valor de saudação como um `Redirect URL` no hello parte superior desta página, em seguida, clique em`Update`

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Definir a URL de Redirecionamento para o Python
> Para Python, você pode definir a porta do servidor web hello por meio da linha de comando. Esta instalação interativa usa a saudação porta 8080 para referência, mas se sentir livre toouse qualquer porta disponível. Em qualquer caso, siga as instruções de saudação abaixo tooset uma URL de redirecionamento nas informações de registro de aplicativo hello:<br/>
> Definir `http://localhost:8080/` como um `Redirect URL` na Olá parte superior desta página, ou use `http://localhost:[port]/` se você estiver usando uma porta TCP personalizada (onde *[port]* é o número da porta TCP personalizado Olá) e, em seguida, clique em 'Atualizar'

### <a name="configure-your-javascript-spa-application"></a>Configure seu aplicativo JavaScript SPA

1.  Crie um arquivo chamado `msalconfig.js` que contém informações de registro de aplicativo hello. Se você estiver usando um projeto Visual Studio, selecione hello (pasta raiz do projeto), com o botão direito e selecione: `Add`  >  `New Item`  >  `JavaScript File`. Nomeie-o `msalconfig.js`
2.  Adicionar Olá tooyour de código a seguir `msalconfig.js` arquivo:

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
