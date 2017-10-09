---
title: "aaaAzure AD v2 Android Introdução - configurar | Microsoft Docs"
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
ms.openlocfilehash: e14796c37ab0c30d948b6f783dac80059375afa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Criar um aplicativo (Expresso)
Agora você precisa tooregister seu aplicativo no hello *Portal de registro de aplicativo do Microsoft*:
1. Registrar seu aplicativo por meio de saudação [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)
2.  Insira um nome para o aplicativo e seu email
3.  Verifique se a opção Olá para a instalação interativa está marcada
4.  Siga a ID do aplicativo hello instruções tooobtain hello e colá-lo em seu código

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Adicionar sua solução de tooyour de informações de registro de aplicativo (Avançado)
Agora você precisa tooregister seu aplicativo no hello *Portal de registro de aplicativo do Microsoft*:
1. Vá toohello [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister um aplicativo
2. Insira um nome para o aplicativo e seu email 
3. Verifique se a opção Olá para a instalação interativa está desmarcada
4. Clique em `Add Platform` e, em seguida, selecione `Native Application` e clique em Salvar
5.  Abra `MainActivity` (em `app` > `java` > *`{host}.{namespace}`*)
6.  Substituir saudação *[Insira aqui o aplicativo hello-Id]* na linha de saudação começando com `final static String CLIENT_ID` com a ID de aplicativo hello você acabou de registrar:

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Abra `AndroidManifest.xml` (em `app`  >  `manifests`) Olá adicionar atividades a seguir muito`manifest\application` nó. Isso registra um `BrowserTabActivity` tooallow Olá tooresume de sistema operacional de seu aplicativo depois de concluir a autenticação de saudação:
</li>
</ol>

```xml
<!--Intent filter toocapture System Browser calling back tooour app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        
        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, hello scheme should be similar too'msal[appId]' -->
        <data android:scheme="msal[Enter hello application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
Em Olá `BrowserTabActivity`, substitua `[Enter hello application Id here]` com ID de aplicativo hello.
</li>
</ol>
