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
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="1492b-103">Adicionar tooyour informações de registro do aplicativo hello aplicativo</span><span class="sxs-lookup"><span data-stu-id="1492b-103">Add hello application’s registration information tooyour App</span></span>

<span data-ttu-id="1492b-104">Nesta etapa, você precisa tooconfigure Olá URL de redirecionamento das suas informações de registro de aplicativo e adicionar aplicativo de JavaScript SPA hello Id do aplicativo tooyour.</span><span class="sxs-lookup"><span data-stu-id="1492b-104">In this step, you need tooconfigure hello Redirect URL of your application registration information and then add hello Application Id tooyour JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="1492b-105">Configurar a URL de redirecionamento</span><span class="sxs-lookup"><span data-stu-id="1492b-105">Configure redirect URL</span></span>

<span data-ttu-id="1492b-106">Configurar Olá `Redirect URL` campo acima com hello URL para a sua página index com base em seu servidor web, em seguida, clique em *atualização*.</span><span class="sxs-lookup"><span data-stu-id="1492b-106">Configure hello `Redirect URL` field above with hello URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="1492b-107">Instruções do Visual Studio para obter a URL de redirecionamento</span><span class="sxs-lookup"><span data-stu-id="1492b-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="1492b-108">tooobtain sua URL de redirecionamento, siga Olá instruções abaixo:</span><span class="sxs-lookup"><span data-stu-id="1492b-108">tooobtain your redirect URL, follow hello instructions below:</span></span>
> 1.    <span data-ttu-id="1492b-109">Em *Solution Explorer*, selecione o projeto hello e examinar Olá `Properties` janela (se você não vir uma janela de propriedades, pressione `F4`)</span><span class="sxs-lookup"><span data-stu-id="1492b-109">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="1492b-110">Copie o valor de saudação do `URL` toohello área de transferência:</span><span class="sxs-lookup"><span data-stu-id="1492b-110">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="1492b-111">![Propriedades do projeto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="1492b-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="1492b-112">Cole o valor de saudação como um `Redirect URL` no hello parte superior desta página, em seguida, clique em`Update`</span><span class="sxs-lookup"><span data-stu-id="1492b-112">Paste hello value as a `Redirect URL` on hello top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="1492b-113">Definir a URL de Redirecionamento para o Python</span><span class="sxs-lookup"><span data-stu-id="1492b-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="1492b-114">Para Python, você pode definir a porta do servidor web hello por meio da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="1492b-114">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="1492b-115">Esta instalação interativa usa a saudação porta 8080 para referência, mas se sentir livre toouse qualquer porta disponível.</span><span class="sxs-lookup"><span data-stu-id="1492b-115">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="1492b-116">Em qualquer caso, siga as instruções de saudação abaixo tooset uma URL de redirecionamento nas informações de registro de aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="1492b-116">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> <span data-ttu-id="1492b-117">Definir `http://localhost:8080/` como um `Redirect URL` na Olá parte superior desta página, ou use `http://localhost:[port]/` se você estiver usando uma porta TCP personalizada (onde *[port]* é o número da porta TCP personalizado Olá) e, em seguida, clique em 'Atualizar'</span><span class="sxs-lookup"><span data-stu-id="1492b-117">Set `http://localhost:8080/` as a `Redirect URL` on hello top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="1492b-118">Configure seu aplicativo JavaScript SPA</span><span class="sxs-lookup"><span data-stu-id="1492b-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="1492b-119">Crie um arquivo chamado `msalconfig.js` que contém informações de registro de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1492b-119">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="1492b-120">Se você estiver usando um projeto Visual Studio, selecione hello (pasta raiz do projeto), com o botão direito e selecione: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="1492b-120">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="1492b-121">Nomeie-o `msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="1492b-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="1492b-122">Adicionar Olá tooyour de código a seguir `msalconfig.js` arquivo:</span><span class="sxs-lookup"><span data-stu-id="1492b-122">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
