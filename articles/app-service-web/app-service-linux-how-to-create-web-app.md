---
title: "Criar um aplicativo web em execução no Linux | Microsoft Docs"
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
ms.openlocfilehash: 49091d4a85bed23927850f9c0bbc5ea8b6e8c9e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="15a4f-104">Criar um aplicativo web em execução no Linux</span><span class="sxs-lookup"><span data-stu-id="15a4f-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-the-azure-portal-to-create-your-web-app"></a><span data-ttu-id="15a4f-105">Usar o portal do Azure para criar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="15a4f-105">Use the Azure portal to create your web app</span></span>
<span data-ttu-id="15a4f-106">Você pode começar a criar seu aplicativo Web em Linux no [portal do Azure](https://portal.azure.com), conforme mostrado na imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="15a4f-106">You can start creating your web app on Linux from the [Azure portal](https://portal.azure.com) as shown in the following image:</span></span>

![Iniciar a criação de um aplicativo Web no portal do Azure][1]

<span data-ttu-id="15a4f-108">A folha **Criar** é aberta, conforme mostrado na seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="15a4f-108">Next, the **Create blade** opens as shown in the following image:</span></span>

![A folha Criar][2]

1. <span data-ttu-id="15a4f-110">Dê um nome ao aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="15a4f-110">Give your web app a name.</span></span>
2. <span data-ttu-id="15a4f-111">Escolha um grupo de recursos existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="15a4f-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="15a4f-112">(Veja as regiões disponíveis na [seção de limitações](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="15a4f-112">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="15a4f-113">Escolha um plano do Serviço de Aplicativo do Azure existente ou crie um.</span><span class="sxs-lookup"><span data-stu-id="15a4f-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="15a4f-114">(Veja as observações do plano do Serviço de Aplicativo na [seção de limitações](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="15a4f-114">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="15a4f-115">Escolha a pilha de aplicativos que você pretende usar.</span><span class="sxs-lookup"><span data-stu-id="15a4f-115">Choose the application stack that you intend to use.</span></span> <span data-ttu-id="15a4f-116">É possível escolher entre várias versões de Node.js, PHP, .Net Core e Ruby.</span><span class="sxs-lookup"><span data-stu-id="15a4f-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="15a4f-117">Depois de criar o aplicativo, você pode alterar a pilha de aplicativos nas configurações do aplicativo, conforme mostrado na seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="15a4f-117">Once you have created the app, you can change the application stack from the application settings as shown in the following image:</span></span>

![Configurações do aplicativo][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="15a4f-119">Implantar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="15a4f-119">Deploy your web app</span></span>
<span data-ttu-id="15a4f-120">A escolha das **opções de implantação** no portal de gerenciamento permite usar um repositório local Git ou GitHub para implantar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="15a4f-120">Choosing **deployment options** from the management portal gives you the option to use local Git or GitHub repository to deploy your application.</span></span> <span data-ttu-id="15a4f-121">O restante das instruções são semelhantes àquelas de um aplicativo Web não Linux.</span><span class="sxs-lookup"><span data-stu-id="15a4f-121">The rest of the instructions are similar to those for a non-Linux web app.</span></span> <span data-ttu-id="15a4f-122">Você pode seguir as instruções em [implantação do Git local](app-service-deploy-local-git.md) ou [implantação contínua](app-service-continuous-deployment.md) para implantar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="15a4f-122">You can follow the instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) to deploy your app.</span></span>

<span data-ttu-id="15a4f-123">Você também pode usar o FTP para carregar o aplicativo no site.</span><span class="sxs-lookup"><span data-stu-id="15a4f-123">You can also use FTP to upload your application to your site.</span></span> <span data-ttu-id="15a4f-124">É possível obter o ponto de extremidade FTP para o aplicativo Web na seção de logs de diagnóstico, conforme mostrado na seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="15a4f-124">You can get the FTP endpoint for your web app from the diagnostics logs section as shown in the following image:</span></span>

![Logs de diagnóstico][4]

## <a name="next-steps"></a><span data-ttu-id="15a4f-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="15a4f-126">Next steps</span></span>
* [<span data-ttu-id="15a4f-127">O que é um Aplicativo Web do Azure no Linux?</span><span class="sxs-lookup"><span data-stu-id="15a4f-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="15a4f-128">Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="15a4f-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="15a4f-129">Usando o Ruby em aplicativos Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="15a4f-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="15a4f-130">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="15a4f-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
