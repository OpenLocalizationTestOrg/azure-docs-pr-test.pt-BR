---
title: "Guia de Introdução do aaaAzure AD v2 iOS - configurar | Microsoft Docs"
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
ms.openlocfilehash: 537cc7f0de6cd947fe340566c9e93f8bb08d57a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Criar um aplicativo (Expresso)
Agora você precisa tooregister seu aplicativo no hello *Portal de registro de aplicativo do Microsoft*:
1. Registrar seu aplicativo por meio de saudação [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)
2.  Insira um nome para o aplicativo e seu email
3.  Verifique se a opção Olá para a instalação interativa está marcada
4.  Siga a ID do aplicativo hello instruções tooobtain hello e colá-lo em seu código

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Adicionar sua solução de tooyour de informações de registro de aplicativo (Avançado)

1.  Vá muito[Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app)
2.  Insira um nome para o aplicativo e seu email
3.  Verifique se a opção Olá para a instalação interativa está desmarcada
4.  Clique em `Add Platform` e, em seguida, selecione `Native Application` e clique em `Save`
5.  Volte tooXcode. Em `ViewController.swift`, substitua a linha hello começando com '`let kClientID`' com a ID de aplicativo hello você acabou de registrar:

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
CTRL + clique <code>Info.plist</code> toobring até o menu contextual hello e, em seguida, clique em: <code>Open As</code>> <code>Source Code</code>
</li>
<li>
Em Olá <code>dict</code> nó raiz, adicione o seguinte hello:
</li>
</ol>

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>msal[Your_Application_Id_Here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
<ol start="8">
<li>
Substituir <i> <code>[Your_Application_Id_Here]</code> </i> com hello Id de aplicativo que você acabou de registrar
</li>
</ol>
