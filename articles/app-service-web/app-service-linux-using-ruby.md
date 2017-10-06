---
title: "aaaUsing Ruby no Azure serviço de aplicativo Web App no Linux | Microsoft Docs"
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
ms.openlocfilehash: 45692cb3bf1da9ff65b9466055029bfaef8b7d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="e6fec-104">Usando o Ruby no Aplicativo Web no Linux</span><span class="sxs-lookup"><span data-stu-id="e6fec-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="e6fec-105">Com hello mais recente atualização tooour back-end, introduzimos o suporte para v.2.3 Ruby.</span><span class="sxs-lookup"><span data-stu-id="e6fec-105">With hello latest update tooour backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="e6fec-106">Ao definir a configuração de saudação de seu aplicativo da web de Linux, você pode alterar pilha do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e6fec-106">By setting hello configuration of your Linux web app, you can change hello application stack.</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="e6fec-107">Usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e6fec-107">Using hello Azure portal</span></span> ##

<span data-ttu-id="e6fec-108">No menu novo, Olá no hello [portal do Azure](https://portal.azure.com), você pode escolher que toocreate um aplicativo Web no Linux de Olá Web + móvel opção conforme Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6fec-108">From hello new menu in hello [Azure portal](https://portal.azure.com), you can choose toocreate a Web App on Linux from hello Web + Mobile option as shown in hello following image:</span></span>

![Iniciar a criação de um aplicativo web em Olá portal do Azure][1]

<span data-ttu-id="e6fec-110">Em seguida, Olá **criar folha** abre conforme Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6fec-110">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![folha de criar Olá][2]

1. <span data-ttu-id="e6fec-112">Dê um nome ao aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e6fec-112">Give your web app a name.</span></span>
2. <span data-ttu-id="e6fec-113">Escolha um grupo de recursos existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="e6fec-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="e6fec-114">(Consulte regiões disponíveis no hello [seção limitações](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="e6fec-114">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="e6fec-115">Escolha um plano do Serviço de Aplicativo do Azure existente ou crie um.</span><span class="sxs-lookup"><span data-stu-id="e6fec-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="e6fec-116">(Consulte as notas de plano do serviço de aplicativo hello [seção limitações](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="e6fec-116">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="e6fec-117">Escolha pilhas de tempo de execução interna Olá Olá Ruby.</span><span class="sxs-lookup"><span data-stu-id="e6fec-117">Choose hello Ruby from hello Built-in Runtime stacks.</span></span>

<span data-ttu-id="e6fec-118">Depois que seu aplicativo web Ruby é criado, você pode implantar tooit usando Git ou FTP.</span><span class="sxs-lookup"><span data-stu-id="e6fec-118">After your Ruby web app gets created, you can deploy tooit using Git or FTP.</span></span>

<span data-ttu-id="e6fec-119">toolearn mais sobre a criação de um aplicativo Ruby, verifique Olá [get guia de Introdução](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="e6fec-119">toolearn more about creating a Ruby app, check hello [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6fec-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e6fec-120">Next steps</span></span>
* [<span data-ttu-id="e6fec-121">O que é o Aplicativo Web no Linux?</span><span class="sxs-lookup"><span data-stu-id="e6fec-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="e6fec-122">TooAzure local de implantação do Git do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="e6fec-122">Local Git Deployment tooAzure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="e6fec-123">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="e6fec-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="e6fec-124">Criar um aplicativo Ruby com o Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="e6fec-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png