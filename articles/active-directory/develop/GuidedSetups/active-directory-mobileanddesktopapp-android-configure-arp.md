---
title: "Introdução ao Android no Azure AD v2 – Configurar | Microsoft Docs"
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
ms.openlocfilehash: c09937582118ebcc5b8cbc1f43a0a2019f2f7a89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="a14a8-103">Adicionar as informações de registro do aplicativo ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="a14a8-103">Add the application’s registration information to your app</span></span>

<span data-ttu-id="a14a8-104">Nesta etapa, você precisa adicionar a ID do Cliente ao projeto.</span><span class="sxs-lookup"><span data-stu-id="a14a8-104">In this step, you need to add the Client ID to your project.</span></span>

1.  <span data-ttu-id="a14a8-105">Abra `MainActivity` (em `app` > `java` > *`{host}.{namespace}`*)</span><span class="sxs-lookup"><span data-stu-id="a14a8-105">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
2.  <span data-ttu-id="a14a8-106">Substitua a linha que começa com `final static String CLIENT_ID` por:</span><span class="sxs-lookup"><span data-stu-id="a14a8-106">Replace the line starting with `final static String CLIENT_ID` with:</span></span>
```java
final static String CLIENT_ID = "[Enter the application Id here]";
```
3. <span data-ttu-id="a14a8-107">Abra: `app` > `manifests` > `AndroidManifest.xml`</span><span class="sxs-lookup"><span data-stu-id="a14a8-107">Open: `app` > `manifests` > `AndroidManifest.xml`</span></span>
4. <span data-ttu-id="a14a8-108">Adicione a atividade a seguir ao nó `manifest\application`.</span><span class="sxs-lookup"><span data-stu-id="a14a8-108">Add the following activity to `manifest\application` node.</span></span> <span data-ttu-id="a14a8-109">Isso registra um `BrowserTabActivity` para permitir que o sistema operacional continue executando o aplicativo depois de concluir a autenticação:</span><span class="sxs-lookup"><span data-stu-id="a14a8-109">This register a `BrowserTabActivity` to allow the OS to resume your application after completing the authentication:</span></span>

```xml
<!--Intent filter to capture System Browser calling back to our app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />

        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, the scheme should be similar to 'msal[appId]' -->
        <data android:scheme="msal[Enter the application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```

### <a name="what-is-next"></a><span data-ttu-id="a14a8-110">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a14a8-110">What is Next</span></span>

[<span data-ttu-id="a14a8-111">Testar e validar</span><span class="sxs-lookup"><span data-stu-id="a14a8-111">Test and Validate</span></span>](active-directory-mobileanddesktopapp-android-test.md)
