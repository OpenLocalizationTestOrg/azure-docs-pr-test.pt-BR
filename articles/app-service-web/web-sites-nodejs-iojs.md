---
title: "aaaHow toouse io.js com aplicativos de Web do serviço de aplicativo do Azure"
description: "Saiba como toouse um aplicativo web no serviço de aplicativo do Azure com io.js."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="c9b74-103">Como io.js toouse com aplicativos de Web do serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="c9b74-103">How toouse io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="c9b74-104">bifurcação de nó popular Olá [io.js] recursos de projeto de Node.js do várias diferenças tooJoyent, incluindo um modelo de controle mais aberto, um ciclo de lançamento mais rápido e uma adoção mais rápida de novo e experimentais recursos de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c9b74-104">hello popular Node fork [io.js] features various differences tooJoyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="c9b74-105">Embora os Aplicativos Web do [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) tenham várias versões de Node.js pré-instaladas, também é possível usar um binário de Node.js fornecido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="c9b74-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="c9b74-106">Este artigo descreve dois métodos habilitar uso de saudação do io.js em aplicativos de Web do serviço de aplicativo: Olá o uso de um script de implantação estendida, que configura automaticamente a versão mais recente de io.js disponíveis do Azure toouse hello, bem como carregamento manual de saudação de um binário io.js.</span><span class="sxs-lookup"><span data-stu-id="c9b74-106">This article discusses two methods enabling hello use of io.js on App Service Web Apps: hello use of an extended deployment script, which automatically configures Azure toouse hello latest available io.js version, as well as hello manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="c9b74-107">Usando um Script de implantação</span><span class="sxs-lookup"><span data-stu-id="c9b74-107">Using a Deployment Script</span></span>
<span data-ttu-id="c9b74-108">Após a implantação de um aplicativo Node. js, aplicativos de Web do serviço de aplicativo executa uma série de comandos pequenos tooensure que Olá ambiente está configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="c9b74-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands tooensure that hello environment is configured properly.</span></span> <span data-ttu-id="c9b74-109">Usando um script de implantação, esse processo pode ser personalizado tooinclude download de saudação e a configuração de io.js.</span><span class="sxs-lookup"><span data-stu-id="c9b74-109">Using a deployment script, this process can be customized tooinclude hello download and configuration of io.js.</span></span>

<span data-ttu-id="c9b74-110">Olá [io.js Script de implantação](https://github.com/felixrieseberg/iojs-azure) está disponível no GitHub.</span><span class="sxs-lookup"><span data-stu-id="c9b74-110">hello [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="c9b74-111">io.js tooenable em seu aplicativo web, basta copiar **.deployment**, **Deploy** e **IISNode.yml** toohello pasta raiz do seu aplicativo e implante aplicativos tooWeb.</span><span class="sxs-lookup"><span data-stu-id="c9b74-111">tooenable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** toohello root of your application folder and deploy tooWeb Apps.</span></span>  

<span data-ttu-id="c9b74-112">primeiro arquivo de saudação, **.deployment**, instrui a aplicativos Web toorun **Deploy** após a implantação.</span><span class="sxs-lookup"><span data-stu-id="c9b74-112">hello first file, **.deployment**, instructs Web Apps toorun **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="c9b74-113">Esse script é executado todas as etapas de saudação normal para um aplicativo Node. js, mas também baixa a versão mais recente de saudação do io.js.</span><span class="sxs-lookup"><span data-stu-id="c9b74-113">This script runs all hello usual steps for a Node.js application, but also downloads hello latest version of io.js.</span></span> <span data-ttu-id="c9b74-114">Por fim, **IISNode.yml** configura aplicativos Web toouse apenas Olá baixado io.js binário em vez de um binário Node. js pré-instalados.</span><span class="sxs-lookup"><span data-stu-id="c9b74-114">Finally, **IISNode.yml** configures Web Apps toouse just hello downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="c9b74-115">Olá tooupdate usada io.js binário, apenas reimplante o aplicativo - script hello baixará uma nova versão do io.js que cada aplicativo de saudação única vez é implantado.</span><span class="sxs-lookup"><span data-stu-id="c9b74-115">tooupdate hello used io.js binary, just redeploy your application - hello script will download a new version of io.js every single time hello application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="c9b74-116">Usando a instalação manual</span><span class="sxs-lookup"><span data-stu-id="c9b74-116">Using Manual Installation</span></span>
<span data-ttu-id="c9b74-117">instalação manual de saudação de uma versão personalizada io.js inclui apenas duas etapas.</span><span class="sxs-lookup"><span data-stu-id="c9b74-117">hello manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="c9b74-118">Primeiro, baixe o hello **win-x64** binário diretamente da saudação [io.js distribuição].</span><span class="sxs-lookup"><span data-stu-id="c9b74-118">First, download hello **win-x64** binary directly from hello [io.js distribution].</span></span> <span data-ttu-id="c9b74-119">São necessários dois arquivos: **iojs.exe** e **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="c9b74-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="c9b74-120">Salvar os dois arquivos tooa pasta dentro de seu aplicativo web, por exemplo **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="c9b74-120">Save both files tooa folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="c9b74-121">tooconfigure aplicativos Web toouse **iojs.exe** em vez de uma versão previamente instalada do nó, cria um **IISNode.yml** arquivo na raiz de saudação do seu aplicativo e adicionar a seguinte linha de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9b74-121">tooconfigure Web Apps toouse **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at hello root of your application and add hello following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="c9b74-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c9b74-122">Next Steps</span></span>
<span data-ttu-id="c9b74-123">Neste artigo, você aprendeu como io.js toouse com aplicativos de Web do serviço de aplicativo, usando os dois fornecidos scripts de implantação, bem como instalação manual.</span><span class="sxs-lookup"><span data-stu-id="c9b74-123">In this article you learned how toouse io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="c9b74-124">O io.js está em desenvolvimento e mais atualizado do que o Node.js.</span><span class="sxs-lookup"><span data-stu-id="c9b74-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="c9b74-125">Vários módulos de Node.js talvez não funcionem com io.js. Confira [io.js no GitHub] para a solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="c9b74-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="c9b74-126">O que mudou</span><span class="sxs-lookup"><span data-stu-id="c9b74-126">What's changed</span></span>
* <span data-ttu-id="c9b74-127">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c9b74-127">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="c9b74-128">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c9b74-128">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c9b74-129">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="c9b74-129">No credit cards required; no commitments.</span></span>
> 
> 

[io.js]: https://iojs.org
[io.js distribuição]: https://iojs.org/dist/
[io.js no GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
