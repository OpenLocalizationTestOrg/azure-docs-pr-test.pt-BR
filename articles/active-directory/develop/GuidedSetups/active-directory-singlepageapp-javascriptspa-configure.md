---
title: "AD do Azure v2 JS SPA interativa instalação - configurar | Microsoft Docs"
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
ms.openlocfilehash: adff529bfdc40006666cc643d49a302d7f1d09ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
## <a name="register-your-application"></a><span data-ttu-id="58671-103">Registre seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="58671-103">Register your application</span></span>

<span data-ttu-id="58671-104">Há várias maneiras de criar um aplicativo, selecione um deles:</span><span class="sxs-lookup"><span data-stu-id="58671-104">There are multiple ways to create an application, please select one of them:</span></span>

### <a name="option-1-register-your-application-express-mode"></a><span data-ttu-id="58671-105">Opção 1: Registrar seu aplicativo (modo Express)</span><span class="sxs-lookup"><span data-stu-id="58671-105">Option 1: Register your application (Express mode)</span></span>
<span data-ttu-id="58671-106">Agora você precisa registrar seu aplicativo no *Portal de Registro de Aplicativos da Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="58671-106">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>

1.  <span data-ttu-id="58671-107">Registre o aplicativo por meio do [Portal de Registro de Aplicativos da Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span><span class="sxs-lookup"><span data-stu-id="58671-107">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span></span>
2.  <span data-ttu-id="58671-108">Insira um nome para o aplicativo e seu email</span><span class="sxs-lookup"><span data-stu-id="58671-108">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="58671-109">Certifique-se de que a opção *Instalação Guiada* está marcada</span><span class="sxs-lookup"><span data-stu-id="58671-109">Make sure the option for *Guided Setup* is checked</span></span>
4.  <span data-ttu-id="58671-110">Siga as instruções para obter a ID do aplicativo e colá-lo no código</span><span class="sxs-lookup"><span data-stu-id="58671-110">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="option-2-register-your-application-advanced-mode"></a><span data-ttu-id="58671-111">Opção 2: Registre seu aplicativo (modo avançado)</span><span class="sxs-lookup"><span data-stu-id="58671-111">Option 2: Register your application (Advanced mode)</span></span>

1. <span data-ttu-id="58671-112">Acesse o [Portal de Registro de Aplicativos da Microsoft](https://apps.dev.microsoft.com/portal/register-app) para registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="58671-112">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="58671-113">Insira um nome para o aplicativo e seu email</span><span class="sxs-lookup"><span data-stu-id="58671-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="58671-114">Certifique-se de que a opção *Instalação Guiada* está desmarcada</span><span class="sxs-lookup"><span data-stu-id="58671-114">Make sure the option for *Guided Setup* is unchecked</span></span>
4.  <span data-ttu-id="58671-115">Clique em `Add Platform` e selecione `Web`</span><span class="sxs-lookup"><span data-stu-id="58671-115">Click `Add Platform`, then select `Web`</span></span>
5. <span data-ttu-id="58671-116">Adicionar o `Redirect URL` que correspondem à URL do aplicativo com base em seu servidor web.</span><span class="sxs-lookup"><span data-stu-id="58671-116">Add the `Redirect URL` that correspond to the application's URL based on your web server.</span></span> <span data-ttu-id="58671-117">Consulte as seções a seguir para obter instruções sobre como definir / obter a URL de redirecionamento no Visual Studio e Python.</span><span class="sxs-lookup"><span data-stu-id="58671-117">See the sections below for instructions on how to set/ obtain the redirect URL in Visual Studio and Python.</span></span>
6. <span data-ttu-id="58671-118">Clique em *Salvar*</span><span class="sxs-lookup"><span data-stu-id="58671-118">Click *Save*</span></span>

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="58671-119">Instruções do Visual Studio para obter a URL de redirecionamento</span><span class="sxs-lookup"><span data-stu-id="58671-119">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="58671-120">Siga as instruções para obter a URL de redirecionamento:</span><span class="sxs-lookup"><span data-stu-id="58671-120">Follow the instructions to obtain your redirect URL:</span></span>
> 1.    <span data-ttu-id="58671-121">No *Gerenciador de Soluções*, selecione o projeto e examine a janela `Properties` (se uma janela Propriedades não for exibida, pressione `F4`)</span><span class="sxs-lookup"><span data-stu-id="58671-121">In *Solution Explorer*, select the project and look at the `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="58671-122">Copie o valor de `URL` para a área de transferência:</span><span class="sxs-lookup"><span data-stu-id="58671-122">Copy the value from `URL` to the clipboard:</span></span><br/> <span data-ttu-id="58671-123">![Propriedades do projeto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="58671-123">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="58671-124">Volte para o *Portal de registro de aplicativo* e cole o valor como um `Redirect URL` e clique em 'Salvar'</span><span class="sxs-lookup"><span data-stu-id="58671-124">Switch back to the *Application Registration Portal* and paste the value as a `Redirect URL` and click 'Save'</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="58671-125">Definir a URL de Redirecionamento para o Python</span><span class="sxs-lookup"><span data-stu-id="58671-125">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="58671-126">Para Python, você pode definir a porta do servidor Web por meio da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="58671-126">For Python, you can set the web server port via command line.</span></span> <span data-ttu-id="58671-127">Esta instalação interativa usa a porta 8080 para referência, mas fique à vontade para usar qualquer outra porta disponível.</span><span class="sxs-lookup"><span data-stu-id="58671-127">This guided setup uses the port 8080 for reference but feel free to use any other port available.</span></span> <span data-ttu-id="58671-128">Em qualquer caso, siga as instruções abaixo para configurar uma URL de redirecionamento nas informações de registro do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="58671-128">In any case, follow the instructions below to set up a redirect URL in the application registration information:</span></span><br/>
> - <span data-ttu-id="58671-129">Volte para o *Portal de registro de aplicativo* e defina `http://localhost:8080/` como um `Redirect URL`, ou use `http://localhost:[port]/` se você estiver usando uma porta TCP personalizada (onde *[port]* é a porta TCP personalizada número) e clique em 'Salvar'</span><span class="sxs-lookup"><span data-stu-id="58671-129">Switch back to the *Application Registration Portal* and set `http://localhost:8080/` as a `Redirect URL`, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is the custom TCP port number) and click 'Save'</span></span>


#### <a name="configure-your-javascript-spa"></a><span data-ttu-id="58671-130">Configurar seu JavaScript SPA</span><span class="sxs-lookup"><span data-stu-id="58671-130">Configure your JavaScript SPA</span></span>

1.  <span data-ttu-id="58671-131">Crie um arquivo chamado `msalconfig.js` que contém as informações de registro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="58671-131">Create a file named `msalconfig.js` containing the application registration information.</span></span> <span data-ttu-id="58671-132">Se você estiver usando o Visual Studio, selecione o projeto (pasta raiz do projeto), clique com o botão direito do mouse e selecione: `Add` > `New Item` > `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="58671-132">If you are using Visual Studio, select the project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="58671-133">Nomeie-o `msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="58671-133">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="58671-134">Adicione o seguinte código ao seu arquivo `msalconfig.js`:</span><span class="sxs-lookup"><span data-stu-id="58671-134">Add the following code to your `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
<span data-ttu-id="58671-135">Substitua <code>Enter_the_Application_Id_here</code> pela ID do Aplicativo que você acabou de registrar</span><span class="sxs-lookup"><span data-stu-id="58671-135">Replace <code>Enter_the_Application_Id_here</code> with the Application Id you just registered</span></span>
</li>
</ol>
