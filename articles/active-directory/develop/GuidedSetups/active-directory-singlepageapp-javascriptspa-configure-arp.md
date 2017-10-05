---
title: "Instalação guiada do JS SPA no Azure AD v2 –Configurar (ARP) | Microsoft Docs"
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
ms.openlocfilehash: 708f4ff606d79639de979918a9cacd4ed75db311
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="1754b-103">Adicionar as informações de registro do aplicativo ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1754b-103">Add the application’s registration information to your App</span></span>

<span data-ttu-id="1754b-104">Nesta etapa, é necessário configurar a URL de Redirecionamento das suas informações de registro do aplicativo e, em seguida, adicionar a Id do Aplicativo ao seu aplicativo JavaScript SPA.</span><span class="sxs-lookup"><span data-stu-id="1754b-104">In this step, you need to configure the Redirect URL of your application registration information and then add the Application Id to your JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="1754b-105">Configurar a URL de redirecionamento</span><span class="sxs-lookup"><span data-stu-id="1754b-105">Configure redirect URL</span></span>

<span data-ttu-id="1754b-106">Configure o campo `Redirect URL` acima com a URL para a sua página index.html com base em seu servidor Web, em seguida, clique em *Atualizar*.</span><span class="sxs-lookup"><span data-stu-id="1754b-106">Configure the `Redirect URL` field above with the URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="1754b-107">Instruções do Visual Studio para obter a URL de redirecionamento</span><span class="sxs-lookup"><span data-stu-id="1754b-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="1754b-108">Para obter a URL de redirecionamento, siga as instruções abaixo:</span><span class="sxs-lookup"><span data-stu-id="1754b-108">To obtain your redirect URL, follow the instructions below:</span></span>
> 1.    <span data-ttu-id="1754b-109">No *Gerenciador de Soluções*, selecione o projeto e examine a janela `Properties` (se uma janela Propriedades não for exibida, pressione `F4`)</span><span class="sxs-lookup"><span data-stu-id="1754b-109">In *Solution Explorer*, select the project and look at the `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="1754b-110">Copie o valor de `URL` para a área de transferência:</span><span class="sxs-lookup"><span data-stu-id="1754b-110">Copy the value from `URL` to the clipboard:</span></span><br/> <span data-ttu-id="1754b-111">![Propriedades do projeto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="1754b-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="1754b-112">Cole o valor como um `Redirect URL` no topo desta página e, em seguida, clique em `Update`</span><span class="sxs-lookup"><span data-stu-id="1754b-112">Paste the value as a `Redirect URL` on the top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="1754b-113">Definir a URL de Redirecionamento para o Python</span><span class="sxs-lookup"><span data-stu-id="1754b-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="1754b-114">Para Python, você pode definir a porta do servidor Web por meio da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="1754b-114">For Python, you can set the web server port via command line.</span></span> <span data-ttu-id="1754b-115">Esta instalação interativa usa a porta 8080 para referência, mas fique à vontade para usar qualquer outra porta disponível.</span><span class="sxs-lookup"><span data-stu-id="1754b-115">This guided setup uses the port 8080 for reference but feel free to use any other port available.</span></span> <span data-ttu-id="1754b-116">Em qualquer caso, siga as instruções abaixo para configurar uma URL de redirecionamento nas informações de registro do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="1754b-116">In any case, follow the instructions below to set up a redirect URL in the application registration information:</span></span><br/>
> <span data-ttu-id="1754b-117">Defina `http://localhost:8080/` como um `Redirect URL` na parte superior dessa página ou use `http://localhost:[port]/` se você estiver usando uma porta TCP personalizada (em que *[port]* é o número da porta TCP personalizada) e, em seguida, clique em 'Atualizar'</span><span class="sxs-lookup"><span data-stu-id="1754b-117">Set `http://localhost:8080/` as a `Redirect URL` on the top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is the custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="1754b-118">Configure seu aplicativo JavaScript SPA</span><span class="sxs-lookup"><span data-stu-id="1754b-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="1754b-119">Crie um arquivo chamado `msalconfig.js` que contém as informações de registro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1754b-119">Create a file named `msalconfig.js` containing the application registration information.</span></span> <span data-ttu-id="1754b-120">Se você estiver usando o Visual Studio, selecione o projeto (pasta raiz do projeto), clique com o botão direito do mouse e selecione: `Add` > `New Item` > `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="1754b-120">If you are using Visual Studio, select the project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="1754b-121">Nomeie-o `msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="1754b-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="1754b-122">Adicione o seguinte código ao seu arquivo `msalconfig.js`:</span><span class="sxs-lookup"><span data-stu-id="1754b-122">Add the following code to your `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter the application Id here]",
    redirectUri: location.origin
};
``` 
