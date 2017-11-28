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
ms.openlocfilehash: 945b09ccdb7537987da33d32d94a3ccacd829ffd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="ce5af-103">Criar um aplicativo (Expresso)</span><span class="sxs-lookup"><span data-stu-id="ce5af-103">Create an application (Express)</span></span>
<span data-ttu-id="ce5af-104">Agora você precisa registrar seu aplicativo no *Portal de Registro de Aplicativos da Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="ce5af-104">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="ce5af-105">Registre o aplicativo por meio do [Portal de Registro de Aplicativos da Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span><span class="sxs-lookup"><span data-stu-id="ce5af-105">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span></span>
2.  <span data-ttu-id="ce5af-106">Insira um nome para o aplicativo e seu email</span><span class="sxs-lookup"><span data-stu-id="ce5af-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="ce5af-107">Verifique se a opção Instalação Guiada está marcada</span><span class="sxs-lookup"><span data-stu-id="ce5af-107">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="ce5af-108">Siga as instruções para obter a ID do aplicativo e colá-lo no código</span><span class="sxs-lookup"><span data-stu-id="ce5af-108">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="ce5af-109">Adicionar as informações de registro do aplicativo à sua solução (Avançado)</span><span class="sxs-lookup"><span data-stu-id="ce5af-109">Add your application registration information to your solution (Advanced)</span></span>
<span data-ttu-id="ce5af-110">Agora você precisa registrar seu aplicativo no *Portal de Registro de Aplicativos da Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="ce5af-110">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="ce5af-111">Acesse o [Portal de Registro de Aplicativos da Microsoft](https://apps.dev.microsoft.com/portal/register-app) para registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="ce5af-111">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="ce5af-112">Insira um nome para o aplicativo e seu email</span><span class="sxs-lookup"><span data-stu-id="ce5af-112">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="ce5af-113">Verifique se a opção Instalação Guiada está desmarcada</span><span class="sxs-lookup"><span data-stu-id="ce5af-113">Make sure the option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="ce5af-114">Clique em `Add Platform` e, em seguida, selecione `Native Application` e clique em Salvar</span><span class="sxs-lookup"><span data-stu-id="ce5af-114">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5.  <span data-ttu-id="ce5af-115">Abra `MainActivity` (em `app` > `java` > *`{host}.{namespace}`*)</span><span class="sxs-lookup"><span data-stu-id="ce5af-115">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
6.  <span data-ttu-id="ce5af-116">Substitua *[Inserir a ID do aplicativo aqui]* na linha que começa com `final static String CLIENT_ID` pela ID do aplicativo que você acabou de registrar:</span><span class="sxs-lookup"><span data-stu-id="ce5af-116">Replace the *[Enter the application Id here]* in the line starting with `final static String CLIENT_ID` with the application ID you just registered:</span></span>

```java
final static String CLIENT_ID = "[Enter the application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="ce5af-117">Abra `AndroidManifest.xml` (em `app` > `manifests`) Adicione a atividade a seguir ao nó `manifest\application`.</span><span class="sxs-lookup"><span data-stu-id="ce5af-117">Open `AndroidManifest.xml` (under `app` > `manifests`) Add the following activity to `manifest\application` node.</span></span> <span data-ttu-id="ce5af-118">Isso registra um `BrowserTabActivity` para permitir que o sistema operacional continue executando o aplicativo depois de concluir a autenticação:</span><span class="sxs-lookup"><span data-stu-id="ce5af-118">This registers a `BrowserTabActivity` to allow the OS to resume your application after completing the authentication:</span></span>
</li>
</ol>

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
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
<span data-ttu-id="ce5af-119">Em `BrowserTabActivity`, substitua `[Enter the application Id here]` pela ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce5af-119">In the `BrowserTabActivity`, replace `[Enter the application Id here]` with the application ID.</span></span>
</li>
</ol>
