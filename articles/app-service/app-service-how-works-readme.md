---
title: "aaaHow do serviço de aplicativo do Azure funciona"
description: "Saber como funciona o Serviço de Aplicativo"
keywords: "serviço de aplicativo, serviço de aplicativo do azure, escala, escalonável, plano de serviço de aplicativo, custo de serviço de aplicativo"
services: app-service
documentationcenter: 
author: yochay
manager: erikre
editor: 
ms.assetid: ae74fc32-969e-4580-8d61-02c922f1f184
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/23/2017
ms.author: yochayk
ms.openlocfilehash: b20733ec8844773d063e2b6918605c4a48db1f5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-app-service-works"></a><span data-ttu-id="a8bf3-104">Como funciona o Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8bf3-104">How App Service works</span></span>
<span data-ttu-id="a8bf3-105">Serviço de aplicativo do Azure é um serviço de nuvem que é projetado toosolve Olá problemas práticos que voltadas para os engenheiros de hoje.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-105">Azure App Service is a cloud service that's designed toosolve hello practical problems that engineers face today.</span></span>
<span data-ttu-id="a8bf3-106">Serviço de aplicativo concentra-se em fornecer a produtividade do desenvolvedor superior sem comprometer Olá precisa de aplicativos de toodeliver em escala de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-106">App Service focuses on providing superior developer productivity without compromising on hello need toodeliver applications at cloud scale.</span></span> 

<span data-ttu-id="a8bf3-107">Serviço de aplicativo também fornece recursos de saudação e estruturas que são necessárias para a criação de aplicativos de linha de negócios de empresa.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-107">App Service also provides hello features and frameworks that are necessary for creating enterprise line-of-business applications.</span></span> <span data-ttu-id="a8bf3-108">Serviço de aplicativo permite que você desenvolva aplicativos em idiomas mais populares de desenvolvimento, incluindo Java, PHP, Node.js, Python e idiomas do Microsoft .NET hello.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-108">App Service lets you develop apps in most popular development languages, including Java, PHP, Node.js, Python, and hello Microsoft .NET languages.</span></span> <span data-ttu-id="a8bf3-109">Com o Serviço de Aplicativo, você pode:</span><span class="sxs-lookup"><span data-stu-id="a8bf3-109">With App Service, you can:</span></span>

* <span data-ttu-id="a8bf3-110">Criar Aplicativos Web altamente escalonáveis.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-110">Build highly scalable web apps.</span></span>
* <span data-ttu-id="a8bf3-111">Criar rapidamente back-ends de Aplicativos Móveis com um conjunto de recursos móveis fácil de usar, por exemplo, back-ends de dados, autenticação de usuário e notificações por push.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-111">Quickly build Mobile Apps back ends with a set of easy-to-use mobile capabilities such as data back ends, user authentication, and push notifications.</span></span>
* <span data-ttu-id="a8bf3-112">Implementar, implantar e publicar APIs com Aplicativos de API.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-112">Implement, deploy, and publish APIs with API Apps.</span></span>
* <span data-ttu-id="a8bf3-113">Reúna aplicativos de negócios em fluxos de trabalho e transforme dados com aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-113">Tie business applications together into workflows and transform data with Logic Apps.</span></span>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

<span data-ttu-id="a8bf3-114">Todos os tipos de aplicativo dependem Olá escalonável e flexível aplicativos Web plataforma, que permite que os desenvolvedores toohave um ciclo de vida completo otimizado experiência de manutenção de tooapp de design do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-114">All app types rely on hello scalable and flexible Web Apps platform, which enables developers toohave an optimized full lifecycle experience from app design tooapp maintenance.</span></span> <span data-ttu-id="a8bf3-115">recursos de ciclo de vida de saudação habilitam seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="a8bf3-115">hello lifecycle capabilities enable hello following:</span></span>

* <span data-ttu-id="a8bf3-116">**Criação rápida de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-116">**Quick app creation**.</span></span> <span data-ttu-id="a8bf3-117">Começar do zero ou escolha um pacote de suporte do sistema operacional (sistemas operacionais) do hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-117">Start from scratch or pick an operational support system (OSS) package from hello Azure Marketplace.</span></span>
* <span data-ttu-id="a8bf3-118">**Implantação contínua**.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-118">**Continuous deployment**.</span></span> <span data-ttu-id="a8bf3-119">Implante automaticamente o novo código de soluções de controle do código-fonte populares como TFS, GitHub e Bitbucket; além disso, sincronize conteúdo de serviços de armazenamento online como OneDrive e Dropbox.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-119">Automatically deploy new code from popular source control solutions such as TFS, GitHub, and Bitbucket, and sync content from online storage services such as OneDrive and Dropbox.</span></span>
* <span data-ttu-id="a8bf3-120">**Teste em produção**.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-120">**Test in production**.</span></span> <span data-ttu-id="a8bf3-121">Sem problemas criar ambientes de pré-produção e gerenciar a quantidade de saudação do tráfego que vai toothem.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-121">Smoothly create pre-production environments and manage hello amount of traffic that's going toothem.</span></span> <span data-ttu-id="a8bf3-122">Depurar na nuvem hello quando necessário e rolar quando são encontrados problemas.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-122">Debug in hello cloud when needed, and roll back when issues are found.</span></span>
* <span data-ttu-id="a8bf3-123">**Executando tarefas assíncronas e trabalhos em lotes**.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-123">**Running asynchronous tasks and batch jobs**.</span></span> <span data-ttu-id="a8bf3-124">Execute código em um processo em segundo plano ou ative seu código com base em eventos (como massagens que chegam em uma fila do Armazenamento do Azure) e horários programados (CRON).</span><span class="sxs-lookup"><span data-stu-id="a8bf3-124">Run code in a background process or activate your code based on events (such as messages landing in an Azure Storage queue) and scheduled times (CRON).</span></span>
* <span data-ttu-id="a8bf3-125">**Aplicativos de dimensionamento Olá**.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-125">**Scaling hello app**.</span></span> <span data-ttu-id="a8bf3-126">Use um dos muitos tooautomatically de opções dimensionar seu serviço horizontalmente e verticalmente com base no tráfego e utilização de recursos.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-126">Use one of many options tooautomatically scale your service horizontally and vertically based on traffic and resource utilization.</span></span> <span data-ttu-id="a8bf3-127">Configure ambientes privadas dedicada tooyour aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-127">Configure private environments that are dedicated tooyour apps.</span></span>   
* <span data-ttu-id="a8bf3-128">**Aplicativo de saudação mantendo**.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-128">**Maintaining hello app**.</span></span> <span data-ttu-id="a8bf3-129">Usar muitos dos Olá depuração e toostay de recursos de diagnóstico à frente de problemas e tooefficiently resolvê-los em tempo real (com recursos como depuração ao vivo e a recuperação automática) ou depois de fato Olá ao analisar logs e memória despejos de memória.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-129">Use many of hello debugging and diagnostics features toostay ahead of problems and tooefficiently resolve them either in real time (with features such as auto-healing and live debugging) or after hello fact by analyzing logs and memory dumps.</span></span>

<span data-ttu-id="a8bf3-130">Como um todo, recursos de serviço de aplicativo permitem aos desenvolvedores toofocus em seu código e rapidamente atingirem um estado estável e altamente escalonável de produção.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-130">As a whole, App Service capabilities enable developers toofocus on their code and quickly reach a stable and highly scalable production state.</span></span> <span data-ttu-id="a8bf3-131">Com hello aplicativos de API e recursos de aplicativos lógicos, os desenvolvedores podem criar aplicativos de empresa do mundo real que ligar as barreiras entre soluções de negócios e integração de toocloud local.</span><span class="sxs-lookup"><span data-stu-id="a8bf3-131">With hello API Apps and Logic Apps features, developers can build real-world enterprise applications that bridge barriers between business solutions and on-premises toocloud integration.</span></span> 

## <a name="videos"></a><span data-ttu-id="a8bf3-132">Vídeos</span><span class="sxs-lookup"><span data-stu-id="a8bf3-132">Videos</span></span>
* [<span data-ttu-id="a8bf3-133">Arquitetura de Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="a8bf3-133">Azure App Service Architecture</span></span>](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)

## <a name="next-steps"></a><span data-ttu-id="a8bf3-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a8bf3-134">Next steps</span></span>

<span data-ttu-id="a8bf3-135">Saiba mais sobre o serviço de aplicativo em um dos seguintes tópicos de saudação:</span><span class="sxs-lookup"><span data-stu-id="a8bf3-135">Learn more about App Service in one of hello following topics:</span></span>

* [<span data-ttu-id="a8bf3-136">O que é o Serviço de Aplicativo do Azure?</span><span class="sxs-lookup"><span data-stu-id="a8bf3-136">What is Azure App Service?</span></span>](app-service-value-prop-what-is.md)
  * [<span data-ttu-id="a8bf3-137">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="a8bf3-137">Web App</span></span>](../app-service-web/app-service-web-overview.md)
  * [<span data-ttu-id="a8bf3-138">Aplicativo Móvel</span><span class="sxs-lookup"><span data-stu-id="a8bf3-138">Mobile App</span></span>](../app-service-mobile/app-service-mobile-value-prop.md)
  * [<span data-ttu-id="a8bf3-139">Aplicativo de API</span><span class="sxs-lookup"><span data-stu-id="a8bf3-139">API App</span></span>](../app-service-api/app-service-api-apps-why-best-platform.md)
* [<span data-ttu-id="a8bf3-140">Arquitetura de Serviço de Aplicativo do Azure (apresentação)</span><span class="sxs-lookup"><span data-stu-id="a8bf3-140">Azure App Service Architecture (presentation)</span></span>](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [<span data-ttu-id="a8bf3-141">Comparação de Serviço de Aplicativo, Serviços de nuvem e Máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="a8bf3-141">Azure App Service, Cloud Services, and Virtual Machines comparison</span></span>](../app-service-web/choose-web-site-cloud-service-vm.md)
* [<span data-ttu-id="a8bf3-142">Noções básicas sobre Aplicativos Móveis do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8bf3-142">Understanding App Service Plans</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [<span data-ttu-id="a8bf3-143">Introdução tooApp ambiente de serviço</span><span class="sxs-lookup"><span data-stu-id="a8bf3-143">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
  * [<span data-ttu-id="a8bf3-144">Exercício: Criar um Ambiente do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8bf3-144">Exercise: Create an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="a8bf3-145">Suporte a Pilhas de Desenvolvimento de Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="a8bf3-145">Azure App Service Development Stacks Support</span></span>](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)



