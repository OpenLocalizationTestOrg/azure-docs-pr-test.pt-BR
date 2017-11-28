---
title: "aplicativo em execução no Linux da web de aaaCreate do Azure | Microsoft Docs"
description: "Fluxo de trabalho da criação de aplicativo Web para aplicativo Web do Azure no Linux."
keywords: "serviço de aplicativo do azure, aplicativo web, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="01c4d-104">Criar um aplicativo web em execução no Linux</span><span class="sxs-lookup"><span data-stu-id="01c4d-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a><span data-ttu-id="01c4d-105">Use Olá toocreate portal do Azure seu aplicativo web</span><span class="sxs-lookup"><span data-stu-id="01c4d-105">Use hello Azure portal toocreate your web app</span></span>
<span data-ttu-id="01c4d-106">Você pode começar a criar seu aplicativo web no Linux de saudação [portal do Azure](https://portal.azure.com) conforme Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="01c4d-106">You can start creating your web app on Linux from hello [Azure portal](https://portal.azure.com) as shown in hello following image:</span></span>

![Iniciar a criação de um aplicativo web em Olá portal do Azure][1]

<span data-ttu-id="01c4d-108">Em seguida, Olá **criar folha** abre conforme Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="01c4d-108">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![folha de criar Olá][2]

1. <span data-ttu-id="01c4d-110">Dê um nome ao aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="01c4d-110">Give your web app a name.</span></span>
2. <span data-ttu-id="01c4d-111">Escolha um grupo de recursos existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="01c4d-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="01c4d-112">(Consulte regiões disponíveis no hello [seção limitações](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="01c4d-112">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="01c4d-113">Escolha um plano do Serviço de Aplicativo do Azure existente ou crie um.</span><span class="sxs-lookup"><span data-stu-id="01c4d-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="01c4d-114">(Consulte as notas de plano do serviço de aplicativo hello [seção limitações](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="01c4d-114">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="01c4d-115">Escolha o aplicativo hello pilha que você pretende toouse.</span><span class="sxs-lookup"><span data-stu-id="01c4d-115">Choose hello application stack that you intend toouse.</span></span> <span data-ttu-id="01c4d-116">É possível escolher entre várias versões de Node.js, PHP, .Net Core e Ruby.</span><span class="sxs-lookup"><span data-stu-id="01c4d-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="01c4d-117">Depois que você criou um aplicativo hello, você pode alterar a pilha do aplicativo hello em configurações do aplicativo hello conforme Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="01c4d-117">Once you have created hello app, you can change hello application stack from hello application settings as shown in hello following image:</span></span>

![Configurações do aplicativo][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="01c4d-119">Implantar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="01c4d-119">Deploy your web app</span></span>
<span data-ttu-id="01c4d-120">Escolhendo **opções de implantação** de fornece portal de gerenciamento Olá você Olá opção toouse local Git ou GitHub repositório toodeploy seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="01c4d-120">Choosing **deployment options** from hello management portal gives you hello option toouse local Git or GitHub repository toodeploy your application.</span></span> <span data-ttu-id="01c4d-121">Olá demais instruções hello serão toothose semelhante para um aplicativo web do Linux não.</span><span class="sxs-lookup"><span data-stu-id="01c4d-121">hello rest of hello instructions are similar toothose for a non-Linux web app.</span></span> <span data-ttu-id="01c4d-122">Você pode seguir as instruções de saudação em [implantação local do Git](app-service-deploy-local-git.md) ou [implantação contínua](app-service-continuous-deployment.md) toodeploy seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="01c4d-122">You can follow hello instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) toodeploy your app.</span></span>

<span data-ttu-id="01c4d-123">Você também pode usar o site do aplicativo tooyour tooupload FTP.</span><span class="sxs-lookup"><span data-stu-id="01c4d-123">You can also use FTP tooupload your application tooyour site.</span></span> <span data-ttu-id="01c4d-124">Você pode obter o ponto de extremidade do hello FTP para seu aplicativo web do diagnóstico de saudação do seção logs conforme Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="01c4d-124">You can get hello FTP endpoint for your web app from hello diagnostics logs section as shown in hello following image:</span></span>

![Logs de diagnóstico][4]

## <a name="next-steps"></a><span data-ttu-id="01c4d-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="01c4d-126">Next steps</span></span>
* [<span data-ttu-id="01c4d-127">O que é um Aplicativo Web do Azure no Linux?</span><span class="sxs-lookup"><span data-stu-id="01c4d-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="01c4d-128">Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="01c4d-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="01c4d-129">Usando o Ruby em aplicativos Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="01c4d-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="01c4d-130">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="01c4d-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
