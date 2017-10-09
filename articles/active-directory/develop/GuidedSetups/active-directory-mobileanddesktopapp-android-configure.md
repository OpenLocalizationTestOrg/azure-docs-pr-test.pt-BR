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
## <a name="create-an-application-express"></a><span data-ttu-id="bd45e-103">Criar um aplicativo (Expresso)</span><span class="sxs-lookup"><span data-stu-id="bd45e-103">Create an application (Express)</span></span>
<span data-ttu-id="bd45e-104">Agora você precisa tooregister seu aplicativo no hello *Portal de registro de aplicativo do Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="bd45e-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="bd45e-105">Registrar seu aplicativo por meio de saudação [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span><span class="sxs-lookup"><span data-stu-id="bd45e-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span></span>
2.  <span data-ttu-id="bd45e-106">Insira um nome para o aplicativo e seu email</span><span class="sxs-lookup"><span data-stu-id="bd45e-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="bd45e-107">Verifique se a opção Olá para a instalação interativa está marcada</span><span class="sxs-lookup"><span data-stu-id="bd45e-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="bd45e-108">Siga a ID do aplicativo hello instruções tooobtain hello e colá-lo em seu código</span><span class="sxs-lookup"><span data-stu-id="bd45e-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="bd45e-109">Adicionar sua solução de tooyour de informações de registro de aplicativo (Avançado)</span><span class="sxs-lookup"><span data-stu-id="bd45e-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="bd45e-110">Agora você precisa tooregister seu aplicativo no hello *Portal de registro de aplicativo do Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="bd45e-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="bd45e-111">Vá toohello [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister um aplicativo</span><span class="sxs-lookup"><span data-stu-id="bd45e-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="bd45e-112">Insira um nome para o aplicativo e seu email</span><span class="sxs-lookup"><span data-stu-id="bd45e-112">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="bd45e-113">Verifique se a opção Olá para a instalação interativa está desmarcada</span><span class="sxs-lookup"><span data-stu-id="bd45e-113">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="bd45e-114">Clique em `Add Platform` e, em seguida, selecione `Native Application` e clique em Salvar</span><span class="sxs-lookup"><span data-stu-id="bd45e-114">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5.  <span data-ttu-id="bd45e-115">Abra `MainActivity` (em `app` > `java` > *`{host}.{namespace}`*)</span><span class="sxs-lookup"><span data-stu-id="bd45e-115">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
6.  <span data-ttu-id="bd45e-116">Substituir saudação *[Insira aqui o aplicativo hello-Id]* na linha de saudação começando com `final static String CLIENT_ID` com a ID de aplicativo hello você acabou de registrar:</span><span class="sxs-lookup"><span data-stu-id="bd45e-116">Replace hello *[Enter hello application Id here]* in hello line starting with `final static String CLIENT_ID` with hello application ID you just registered:</span></span>

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="bd45e-117">Abra `AndroidManifest.xml` (em `app`  >  `manifests`) Olá adicionar atividades a seguir muito`manifest\application` nó.</span><span class="sxs-lookup"><span data-stu-id="bd45e-117">Open `AndroidManifest.xml` (under `app` > `manifests`) Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="bd45e-118">Isso registra um `BrowserTabActivity` tooallow Olá tooresume de sistema operacional de seu aplicativo depois de concluir a autenticação de saudação:</span><span class="sxs-lookup"><span data-stu-id="bd45e-118">This registers a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>
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
<span data-ttu-id="bd45e-119">Em Olá `BrowserTabActivity`, substitua `[Enter hello application Id here]` com ID de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="bd45e-119">In hello `BrowserTabActivity`, replace `[Enter hello application Id here]` with hello application ID.</span></span>
</li>
</ol>
