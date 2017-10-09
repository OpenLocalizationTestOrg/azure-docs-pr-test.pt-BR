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
## <a name="create-an-application-express"></a><span data-ttu-id="89aee-103">Criar um aplicativo (Expresso)</span><span class="sxs-lookup"><span data-stu-id="89aee-103">Create an application (Express)</span></span>
<span data-ttu-id="89aee-104">Agora você precisa tooregister seu aplicativo no hello *Portal de registro de aplicativo do Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="89aee-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="89aee-105">Registrar seu aplicativo por meio de saudação [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span><span class="sxs-lookup"><span data-stu-id="89aee-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span></span>
2.  <span data-ttu-id="89aee-106">Insira um nome para o aplicativo e seu email</span><span class="sxs-lookup"><span data-stu-id="89aee-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="89aee-107">Verifique se a opção Olá para a instalação interativa está marcada</span><span class="sxs-lookup"><span data-stu-id="89aee-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="89aee-108">Siga a ID do aplicativo hello instruções tooobtain hello e colá-lo em seu código</span><span class="sxs-lookup"><span data-stu-id="89aee-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="89aee-109">Adicionar sua solução de tooyour de informações de registro de aplicativo (Avançado)</span><span class="sxs-lookup"><span data-stu-id="89aee-109">Add your application registration information tooyour solution (Advanced)</span></span>

1.  <span data-ttu-id="89aee-110">Vá muito[Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app)</span><span class="sxs-lookup"><span data-stu-id="89aee-110">Go too[Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app)</span></span>
2.  <span data-ttu-id="89aee-111">Insira um nome para o aplicativo e seu email</span><span class="sxs-lookup"><span data-stu-id="89aee-111">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="89aee-112">Verifique se a opção Olá para a instalação interativa está desmarcada</span><span class="sxs-lookup"><span data-stu-id="89aee-112">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="89aee-113">Clique em `Add Platform` e, em seguida, selecione `Native Application` e clique em `Save`</span><span class="sxs-lookup"><span data-stu-id="89aee-113">Click `Add Platform`, then select `Native Application` and click `Save`</span></span>
5.  <span data-ttu-id="89aee-114">Volte tooXcode.</span><span class="sxs-lookup"><span data-stu-id="89aee-114">Go back tooXcode.</span></span> <span data-ttu-id="89aee-115">Em `ViewController.swift`, substitua a linha hello começando com '`let kClientID`' com a ID de aplicativo hello você acabou de registrar:</span><span class="sxs-lookup"><span data-stu-id="89aee-115">In `ViewController.swift`, replace hello line starting with '`let kClientID`' with hello application ID you just registered:</span></span>

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="89aee-116">CTRL + clique <code>Info.plist</code> toobring até o menu contextual hello e, em seguida, clique em: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="89aee-116">Control+click <code>Info.plist</code> toobring up hello contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="89aee-117">Em Olá <code>dict</code> nó raiz, adicione o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="89aee-117">Under hello <code>dict</code> root node, add hello following:</span></span>
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
<span data-ttu-id="89aee-118">Substituir <i> <code>[Your_Application_Id_Here]</code> </i> com hello Id de aplicativo que você acabou de registrar</span><span class="sxs-lookup"><span data-stu-id="89aee-118">Replace <i><code>[Your_Application_Id_Here]</code></i> with hello Application Id you just registered</span></span>
</li>
</ol>
