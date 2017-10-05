---
title: "Usando o Ruby no Aplicativo Web do Serviço de Aplicativo do Azure no Linux | Microsoft Docs"
description: "Usando o Ruby no Aplicativo Web do Serviço de Aplicativo do Azure no Linux."
keywords: "serviço de aplicativo do azure, aplicativo Web, perguntas frequentes, linux, oss, ruby"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 56105d1bc153e552e12c0c408c8f6075e4eff9d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="cb3b5-104">Usando o Ruby no Aplicativo Web no Linux</span><span class="sxs-lookup"><span data-stu-id="cb3b5-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="cb3b5-105">Com a atualização mais recente para nosso back-end, introduzimos o suporte ao Ruby v.2.3.</span><span class="sxs-lookup"><span data-stu-id="cb3b5-105">With the latest update to our backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="cb3b5-106">Ao definir a configuração do seu aplicativo Web Linux, você pode alterar a pilha de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="cb3b5-106">By setting the configuration of your Linux web app, you can change the application stack.</span></span>

## <a name="using-the-azure-portal"></a><span data-ttu-id="cb3b5-107">Usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cb3b5-107">Using the Azure portal</span></span> ##

<span data-ttu-id="cb3b5-108">Do novo menu no [Portal do Azure](https://portal.azure.com), você pode optar por criar um aplicativo Web no Linux utilizando a opção Web + Móvel, conforme mostrado na imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb3b5-108">From the new menu in the [Azure portal](https://portal.azure.com), you can choose to create a Web App on Linux from the Web + Mobile option as shown in the following image:</span></span>

![Iniciar a criação de um aplicativo Web no portal do Azure][1]

<span data-ttu-id="cb3b5-110">A folha **Criar** é aberta, conforme mostrado na seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="cb3b5-110">Next, the **Create blade** opens as shown in the following image:</span></span>

![A folha Criar][2]

1. <span data-ttu-id="cb3b5-112">Dê um nome ao aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="cb3b5-112">Give your web app a name.</span></span>
2. <span data-ttu-id="cb3b5-113">Escolha um grupo de recursos existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="cb3b5-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="cb3b5-114">(Veja as regiões disponíveis na [seção de limitações](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="cb3b5-114">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="cb3b5-115">Escolha um plano do Serviço de Aplicativo do Azure existente ou crie um.</span><span class="sxs-lookup"><span data-stu-id="cb3b5-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="cb3b5-116">(Veja as observações do plano do Serviço de Aplicativo na [seção de limitações](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="cb3b5-116">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="cb3b5-117">Escolha o Ruby das pilhas de tempo de execução internas.</span><span class="sxs-lookup"><span data-stu-id="cb3b5-117">Choose the Ruby from the Built-in Runtime stacks.</span></span>

<span data-ttu-id="cb3b5-118">Depois que seu aplicativo Web Ruby é criado, você pode implantar para ele usando Git ou FTP.</span><span class="sxs-lookup"><span data-stu-id="cb3b5-118">After your Ruby web app gets created, you can deploy to it using Git or FTP.</span></span>

<span data-ttu-id="cb3b5-119">Para saber mais sobre como criar um aplicativo Ruby, confira o [guia de introdução](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="cb3b5-119">To learn more about creating a Ruby app, check the [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb3b5-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cb3b5-120">Next steps</span></span>
* [<span data-ttu-id="cb3b5-121">O que é o Aplicativo Web no Linux?</span><span class="sxs-lookup"><span data-stu-id="cb3b5-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="cb3b5-122">Implantação do Git local no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="cb3b5-122">Local Git Deployment to Azure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="cb3b5-123">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="cb3b5-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="cb3b5-124">Criar um aplicativo Ruby com o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="cb3b5-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png