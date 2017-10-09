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
## <a name="register-your-application"></a><span data-ttu-id="8dc50-103">Registre seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="8dc50-103">Register your application</span></span>

<span data-ttu-id="8dc50-104">Há várias maneiras toocreate um aplicativo, selecione um deles:</span><span class="sxs-lookup"><span data-stu-id="8dc50-104">There are multiple ways toocreate an application, please select one of them:</span></span>

### <a name="option-1-register-your-application-express-mode"></a><span data-ttu-id="8dc50-105">Opção 1: Registrar seu aplicativo (modo Expresso)</span><span class="sxs-lookup"><span data-stu-id="8dc50-105">Option 1: Register your application (Express mode)</span></span>
<span data-ttu-id="8dc50-106">Agora você precisa tooregister seu aplicativo no hello *Portal de registro de aplicativo do Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="8dc50-106">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>

1.  <span data-ttu-id="8dc50-107">Registrar seu aplicativo por meio de saudação [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span><span class="sxs-lookup"><span data-stu-id="8dc50-107">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span></span>
2.  <span data-ttu-id="8dc50-108">Insira um nome para o aplicativo e seu email</span><span class="sxs-lookup"><span data-stu-id="8dc50-108">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="8dc50-109">Certifique-se de opção de saudação *instalação interativa* é verificada</span><span class="sxs-lookup"><span data-stu-id="8dc50-109">Make sure hello option for *Guided Setup* is checked</span></span>
4.  <span data-ttu-id="8dc50-110">Siga a ID do aplicativo hello instruções tooobtain hello e colá-lo em seu código</span><span class="sxs-lookup"><span data-stu-id="8dc50-110">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="option-2-register-your-application-advanced-mode"></a><span data-ttu-id="8dc50-111">Opção 2: Registrar seu aplicativo (modo Avançado)</span><span class="sxs-lookup"><span data-stu-id="8dc50-111">Option 2: Register your application (Advanced mode)</span></span>

1. <span data-ttu-id="8dc50-112">Vá toohello [Portal de registro de aplicativo do Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister um aplicativo</span><span class="sxs-lookup"><span data-stu-id="8dc50-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="8dc50-113">Insira um nome para o aplicativo e seu email</span><span class="sxs-lookup"><span data-stu-id="8dc50-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="8dc50-114">Certifique-se de opção de saudação *instalação interativa* está desmarcada</span><span class="sxs-lookup"><span data-stu-id="8dc50-114">Make sure hello option for *Guided Setup* is unchecked</span></span>
4.  <span data-ttu-id="8dc50-115">Clique em `Add Platform` e selecione `Web`</span><span class="sxs-lookup"><span data-stu-id="8dc50-115">Click `Add Platform`, then select `Web`</span></span>
5. <span data-ttu-id="8dc50-116">Adicionar Olá `Redirect URL` que correspondem a URL do aplicativo toohello com base em seu servidor web.</span><span class="sxs-lookup"><span data-stu-id="8dc50-116">Add hello `Redirect URL` that correspond toohello application's URL based on your web server.</span></span> <span data-ttu-id="8dc50-117">Consulte as seções de saudação abaixo para obter instruções sobre como tooset / obter URL de redirecionamento Olá no Visual Studio e Python.</span><span class="sxs-lookup"><span data-stu-id="8dc50-117">See hello sections below for instructions on how tooset/ obtain hello redirect URL in Visual Studio and Python.</span></span>
6. <span data-ttu-id="8dc50-118">Clique em *Salvar*</span><span class="sxs-lookup"><span data-stu-id="8dc50-118">Click *Save*</span></span>

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="8dc50-119">Instruções do Visual Studio para obter a URL de redirecionamento</span><span class="sxs-lookup"><span data-stu-id="8dc50-119">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="8dc50-120">Execute Olá instruções tooobtain sua URL de redirecionamento:</span><span class="sxs-lookup"><span data-stu-id="8dc50-120">Follow hello instructions tooobtain your redirect URL:</span></span>
> 1.    <span data-ttu-id="8dc50-121">Em *Solution Explorer*, selecione o projeto hello e examinar Olá `Properties` janela (se você não vir uma janela de propriedades, pressione `F4`)</span><span class="sxs-lookup"><span data-stu-id="8dc50-121">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="8dc50-122">Copie o valor de saudação do `URL` toohello área de transferência:</span><span class="sxs-lookup"><span data-stu-id="8dc50-122">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="8dc50-123">![Propriedades do projeto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="8dc50-123">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="8dc50-124">Alternar back toohello *Portal de registro de aplicativo* e cole o valor de saudação como um `Redirect URL` e clique em 'Salvar'</span><span class="sxs-lookup"><span data-stu-id="8dc50-124">Switch back toohello *Application Registration Portal* and paste hello value as a `Redirect URL` and click 'Save'</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="8dc50-125">Definir a URL de Redirecionamento para o Python</span><span class="sxs-lookup"><span data-stu-id="8dc50-125">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="8dc50-126">Para Python, você pode definir a porta do servidor web hello por meio da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="8dc50-126">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="8dc50-127">Esta instalação interativa usa a saudação porta 8080 para referência, mas se sentir livre toouse qualquer porta disponível.</span><span class="sxs-lookup"><span data-stu-id="8dc50-127">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="8dc50-128">Em qualquer caso, siga as instruções de saudação abaixo tooset uma URL de redirecionamento nas informações de registro de aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="8dc50-128">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> - <span data-ttu-id="8dc50-129">Alternar back toohello *Portal de registro de aplicativo* e defina `http://localhost:8080/` como um `Redirect URL`, ou use `http://localhost:[port]/` se você estiver usando uma porta TCP personalizada (onde *[port]* é a porta TCP personalizada Olá número) e clique em 'Salvar'</span><span class="sxs-lookup"><span data-stu-id="8dc50-129">Switch back toohello *Application Registration Portal* and set `http://localhost:8080/` as a `Redirect URL`, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number) and click 'Save'</span></span>


#### <a name="configure-your-javascript-spa"></a><span data-ttu-id="8dc50-130">Configurar o JavaScript SPA</span><span class="sxs-lookup"><span data-stu-id="8dc50-130">Configure your JavaScript SPA</span></span>

1.  <span data-ttu-id="8dc50-131">Crie um arquivo chamado `msalconfig.js` que contém informações de registro de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8dc50-131">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="8dc50-132">Se você estiver usando um projeto Visual Studio, selecione hello (pasta raiz do projeto), com o botão direito e selecione: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="8dc50-132">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="8dc50-133">Nomeie-o `msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="8dc50-133">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="8dc50-134">Adicionar Olá tooyour de código a seguir `msalconfig.js` arquivo:</span><span class="sxs-lookup"><span data-stu-id="8dc50-134">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
<span data-ttu-id="8dc50-135">Substituir <code>Enter_the_Application_Id_here</code> com hello Id de aplicativo que você acabou de registrar</span><span class="sxs-lookup"><span data-stu-id="8dc50-135">Replace <code>Enter_the_Application_Id_here</code> with hello Application Id you just registered</span></span>
</li>
</ol>
