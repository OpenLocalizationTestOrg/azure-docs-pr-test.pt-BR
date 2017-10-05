---
title: "Como usar io.js com Aplicativos Web do Serviço de Aplicativo do Azure"
description: "Saiba como usar um aplicativo Web no Serviço de Aplicativo do Azure com io.js."
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
ms.openlocfilehash: 4800504e1939a46842d15e8c9d4279a4b9cae787
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="7433e-103">Como usar io.js com Aplicativos Web do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="7433e-103">How to use io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="7433e-104">A bifurcação de nó popular [io.js] apresenta várias diferenças em relação ao projeto do Node.js do Joyent, incluindo um modelo de controle mais aberto, um ciclo de lançamento mais rápido e uma adoção mais rápida de recursos novos e experimentais de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7433e-104">The popular Node fork [io.js] features various differences to Joyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="7433e-105">Embora os Aplicativos Web do [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) tenham várias versões de Node.js pré-instaladas, também é possível usar um binário de Node.js fornecido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="7433e-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="7433e-106">Este artigo discute dois métodos que habilitam o uso de io.js em Aplicativos Web do de Serviço de Aplicativo: o uso de um script de implantação estendido, que configura automaticamente o Azure para usar a última versão do io.js disponível, bem como o carregamento manual de um binário de io.js.</span><span class="sxs-lookup"><span data-stu-id="7433e-106">This article discusses two methods enabling the use of io.js on App Service Web Apps: The use of an extended deployment script, which automatically configures Azure to use the latest available io.js version, as well as the manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="7433e-107">Usando um Script de implantação</span><span class="sxs-lookup"><span data-stu-id="7433e-107">Using a Deployment Script</span></span>
<span data-ttu-id="7433e-108">Após a implantação de um aplicativo de Node.js, os Aplicativos Web do Serviço de Aplicativo executam uma série de pequenos comandos para garantir que o ambiente seja configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="7433e-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands to ensure that the environment is configured properly.</span></span> <span data-ttu-id="7433e-109">Ao usar um script de implantação, esse processo pode ser personalizado para incluir o download e a configuração de io.js.</span><span class="sxs-lookup"><span data-stu-id="7433e-109">Using a deployment script, this process can be customized to include the download and configuration of io.js.</span></span>

<span data-ttu-id="7433e-110">O [Script de Implantação io.js](https://github.com/felixrieseberg/iojs-azure) está disponível no GitHub.</span><span class="sxs-lookup"><span data-stu-id="7433e-110">The [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="7433e-111">Para habilitar io.js em seu aplicativo Web, basta copiar **.deployment**, **deploy.cmd** e **IISNode.yml** para a raiz da pasta do aplicativo e implantar nos Aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="7433e-111">To enable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** to the root of your application folder and deploy to Web Apps.</span></span>  

<span data-ttu-id="7433e-112">O primeiro arquivo, **.deployment**, instrui os Aplicativos Web a executar **deploy.cmd** na implantação.</span><span class="sxs-lookup"><span data-stu-id="7433e-112">The first file, **.deployment**, instructs Web Apps to run **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="7433e-113">Esse script executa todas as etapas normais para um aplicativo Node. js, mas também baixa a versão mais recente do io.js.</span><span class="sxs-lookup"><span data-stu-id="7433e-113">This script runs all the usual steps for a Node.js application, but also downloads the latest version of io.js.</span></span> <span data-ttu-id="7433e-114">Por fim, **IISNode.yml** configura os Aplicativos Web para usar apenas o binário do io.js baixado em vez de um binário pré-instalado do Node.js.</span><span class="sxs-lookup"><span data-stu-id="7433e-114">Finally, **IISNode.yml** configures Web Apps to use just the downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="7433e-115">Para atualizar o binário do io.js usado, apenas reimplante seu aplicativo - o script baixará uma nova versão do io.js toda vez que o aplicativo for implantado.</span><span class="sxs-lookup"><span data-stu-id="7433e-115">To update the used io.js binary, just redeploy your application - the script will download a new version of io.js every single time the application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="7433e-116">Usando a instalação manual</span><span class="sxs-lookup"><span data-stu-id="7433e-116">Using Manual Installation</span></span>
<span data-ttu-id="7433e-117">A instalação manual de uma versão personalizada do io.js inclui apenas duas etapas.</span><span class="sxs-lookup"><span data-stu-id="7433e-117">The manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="7433e-118">Primeiro, baixe o binário de **win-x64** diretamente da [distribuição de io.js].</span><span class="sxs-lookup"><span data-stu-id="7433e-118">First, download the **win-x64** binary directly from the [io.js distribution].</span></span> <span data-ttu-id="7433e-119">São necessários dois arquivos: **iojs.exe** e **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="7433e-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="7433e-120">Salve os dois arquivos e uma pasta dentro de seu aplicativo Web, por exemplo, em **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="7433e-120">Save both files to a folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="7433e-121">Para configurar Aplicativos Web para usar **iojs.exe** em vez de uma versão pré-instalada de Node, crie um arquivo **IISNode.yml** na raiz do aplicativo e adicione a linha a seguir.</span><span class="sxs-lookup"><span data-stu-id="7433e-121">To configure Web Apps to use **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at the root of your application and add the following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="7433e-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7433e-122">Next Steps</span></span>
<span data-ttu-id="7433e-123">Neste artigo, você aprendeu a usar io.js com Aplicativos Web do Serviço de Aplicativo, usando os scripts de implantação fornecidos, bem como a instalação manual.</span><span class="sxs-lookup"><span data-stu-id="7433e-123">In this article you learned how to use io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="7433e-124">O io.js está em desenvolvimento e mais atualizado do que o Node.js.</span><span class="sxs-lookup"><span data-stu-id="7433e-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="7433e-125">Vários módulos de Node.js talvez não funcionem com io.js. Confira [io.js no GitHub] para a solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="7433e-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="7433e-126">O que mudou</span><span class="sxs-lookup"><span data-stu-id="7433e-126">What's changed</span></span>
* <span data-ttu-id="7433e-127">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, confira: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="7433e-127">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="7433e-128">Se desejar começar a usar o Serviço de Aplicativo do Azure antes de inscrever-se em uma conta do Azure, vá para [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7433e-128">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7433e-129">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="7433e-129">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="7433e-130">[io.js]: https://iojs.org</span><span class="sxs-lookup"><span data-stu-id="7433e-130">[io.js]: https://iojs.org</span></span>
<span data-ttu-id="7433e-131">[distribuição de io.js]: https://iojs.org/dist/</span><span class="sxs-lookup"><span data-stu-id="7433e-131">[io.js distribution]: https://iojs.org/dist/</span></span>
<span data-ttu-id="7433e-132">[io.js no GitHub]: https://github.com/iojs/io.js</span><span class="sxs-lookup"><span data-stu-id="7433e-132">[io.js on GitHub]: https://github.com/iojs/io.js</span></span>
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
