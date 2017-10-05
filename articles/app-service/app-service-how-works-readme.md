---
title: "Como funciona o Serviço de Aplicativo do Azure"
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
ms.openlocfilehash: 2d830963d3d2adba71a6ca99f79eac0fc8cbfb12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-app-service-works"></a><span data-ttu-id="defad-104">Como funciona o Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="defad-104">How App Service works</span></span>
<span data-ttu-id="defad-105">O Serviço de Aplicativo do Azure é um serviço de nuvem projetado para resolver os problemas práticos enfrentados atualmente pelos engenheiros.</span><span class="sxs-lookup"><span data-stu-id="defad-105">Azure App Service is a cloud service that's designed to solve the practical problems that engineers face today.</span></span>
<span data-ttu-id="defad-106">O Serviço de Aplicativo se concentra em permitir uma produtividade superior ao desenvolvedor sem comprometer a necessidade de fornecer aplicativos em escala de nuvem.</span><span class="sxs-lookup"><span data-stu-id="defad-106">App Service focuses on providing superior developer productivity without compromising on the need to deliver applications at cloud scale.</span></span> 

<span data-ttu-id="defad-107">O Serviço de Aplicativo também fornece os recursos e as estruturas que são necessárias para a criação de aplicativos corporativos de linha de negócios.</span><span class="sxs-lookup"><span data-stu-id="defad-107">App Service also provides the features and frameworks that are necessary for creating enterprise line-of-business applications.</span></span> <span data-ttu-id="defad-108">O Serviço de Aplicativo permite que você desenvolva aplicativos nas linguagens de desenvolvimento mais populares, incluindo Java, PHP, Node.js, Python e as linguagens do Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="defad-108">App Service lets you develop apps in most popular development languages, including Java, PHP, Node.js, Python, and the Microsoft .NET languages.</span></span> <span data-ttu-id="defad-109">Com o Serviço de Aplicativo, você pode:</span><span class="sxs-lookup"><span data-stu-id="defad-109">With App Service, you can:</span></span>

* <span data-ttu-id="defad-110">Criar Aplicativos Web altamente escalonáveis.</span><span class="sxs-lookup"><span data-stu-id="defad-110">Build highly scalable web apps.</span></span>
* <span data-ttu-id="defad-111">Criar rapidamente back-ends de Aplicativos Móveis com um conjunto de recursos móveis fácil de usar, por exemplo, back-ends de dados, autenticação de usuário e notificações por push.</span><span class="sxs-lookup"><span data-stu-id="defad-111">Quickly build Mobile Apps back ends with a set of easy-to-use mobile capabilities such as data back ends, user authentication, and push notifications.</span></span>
* <span data-ttu-id="defad-112">Implementar, implantar e publicar APIs com Aplicativos de API.</span><span class="sxs-lookup"><span data-stu-id="defad-112">Implement, deploy, and publish APIs with API Apps.</span></span>
* <span data-ttu-id="defad-113">Reúna aplicativos de negócios em fluxos de trabalho e transforme dados com aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="defad-113">Tie business applications together into workflows and transform data with Logic Apps.</span></span>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

<span data-ttu-id="defad-114">Todos os tipos de aplicativo contam com a plataforma de Aplicativos Web escalonável e flexível, que permite aos desenvolvedores uma experiência otimizada de ciclo de vida completo, do design à manutenção do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="defad-114">All app types rely on the scalable and flexible Web Apps platform, which enables developers to have an optimized full lifecycle experience from app design to app maintenance.</span></span> <span data-ttu-id="defad-115">Os recursos de ciclo de vida permitem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="defad-115">The lifecycle capabilities enable the following:</span></span>

* <span data-ttu-id="defad-116">**Criação rápida de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="defad-116">**Quick app creation**.</span></span> <span data-ttu-id="defad-117">Comece do zero ou escolha um pacote de OSS (sistemas de suporte operacionais) do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="defad-117">Start from scratch or pick an operational support system (OSS) package from the Azure Marketplace.</span></span>
* <span data-ttu-id="defad-118">**Implantação contínua**.</span><span class="sxs-lookup"><span data-stu-id="defad-118">**Continuous deployment**.</span></span> <span data-ttu-id="defad-119">Implante automaticamente o novo código de soluções de controle do código-fonte populares como TFS, GitHub e Bitbucket; além disso, sincronize conteúdo de serviços de armazenamento online como OneDrive e Dropbox.</span><span class="sxs-lookup"><span data-stu-id="defad-119">Automatically deploy new code from popular source control solutions such as TFS, GitHub, and Bitbucket, and sync content from online storage services such as OneDrive and Dropbox.</span></span>
* <span data-ttu-id="defad-120">**Teste em produção**.</span><span class="sxs-lookup"><span data-stu-id="defad-120">**Test in production**.</span></span> <span data-ttu-id="defad-121">Crie ambientes de pré-produção sem dificuldade e gerencie a parte do tráfego que chega a eles.</span><span class="sxs-lookup"><span data-stu-id="defad-121">Smoothly create pre-production environments and manage the amount of traffic that's going to them.</span></span> <span data-ttu-id="defad-122">Depure na nuvem quando necessário e reverta ao encontrar problemas.</span><span class="sxs-lookup"><span data-stu-id="defad-122">Debug in the cloud when needed, and roll back when issues are found.</span></span>
* <span data-ttu-id="defad-123">**Executando tarefas assíncronas e trabalhos em lotes**.</span><span class="sxs-lookup"><span data-stu-id="defad-123">**Running asynchronous tasks and batch jobs**.</span></span> <span data-ttu-id="defad-124">Execute código em um processo em segundo plano ou ative seu código com base em eventos (como massagens que chegam em uma fila do Armazenamento do Azure) e horários programados (CRON).</span><span class="sxs-lookup"><span data-stu-id="defad-124">Run code in a background process or activate your code based on events (such as messages landing in an Azure Storage queue) and scheduled times (CRON).</span></span>
* <span data-ttu-id="defad-125">**Dimensionando o aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="defad-125">**Scaling the app**.</span></span> <span data-ttu-id="defad-126">Use uma das muitas opções para dimensionar seu serviço horizontal e verticalmente de forma automática, com base no tráfego e na utilização de recursos.</span><span class="sxs-lookup"><span data-stu-id="defad-126">Use one of many options to automatically scale your service horizontally and vertically based on traffic and resource utilization.</span></span> <span data-ttu-id="defad-127">Configurar ambientes privados dedicados para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="defad-127">Configure private environments that are dedicated to your apps.</span></span>   
* <span data-ttu-id="defad-128">**Manter o aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="defad-128">**Maintaining the app**.</span></span> <span data-ttu-id="defad-129">Use muitos dos recursos de depuração e diagnóstico para se manter à frente de problemas e resolvê-los de forma eficiente em tempo real (com recursos como recuperação automática e depuração dinâmica) ou após o fato, analisando os logs e despejos de memória.</span><span class="sxs-lookup"><span data-stu-id="defad-129">Use many of the debugging and diagnostics features to stay ahead of problems and to efficiently resolve them either in real time (with features such as auto-healing and live debugging) or after the fact by analyzing logs and memory dumps.</span></span>

<span data-ttu-id="defad-130">Como um todo, as funcionalidades do Serviço de Aplicativo permitem que os desenvolvedores se concentrem no seu código e atinjam rapidamente um estado de produção estável e altamente escalonável.</span><span class="sxs-lookup"><span data-stu-id="defad-130">As a whole, App Service capabilities enable developers to focus on their code and quickly reach a stable and highly scalable production state.</span></span> <span data-ttu-id="defad-131">Com os recursos de Aplicativos de API e de Aplicativos Lógicos, os desenvolvedores podem criar aplicativos empresariais reais que aproximam as soluções de negócios e integram o local à nuvem.</span><span class="sxs-lookup"><span data-stu-id="defad-131">With the API Apps and Logic Apps features, developers can build real-world enterprise applications that bridge barriers between business solutions and on-premises to cloud integration.</span></span> 

## <a name="videos"></a><span data-ttu-id="defad-132">Vídeos</span><span class="sxs-lookup"><span data-stu-id="defad-132">Videos</span></span>
* [<span data-ttu-id="defad-133">Arquitetura de Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="defad-133">Azure App Service Architecture</span></span>](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)

## <a name="next-steps"></a><span data-ttu-id="defad-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="defad-134">Next steps</span></span>

<span data-ttu-id="defad-135">Saiba mais sobre o Serviço de Aplicativo em um dos seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="defad-135">Learn more about App Service in one of the following topics:</span></span>

* [<span data-ttu-id="defad-136">O que é o Serviço de Aplicativo do Azure?</span><span class="sxs-lookup"><span data-stu-id="defad-136">What is Azure App Service?</span></span>](app-service-value-prop-what-is.md)
  * [<span data-ttu-id="defad-137">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="defad-137">Web App</span></span>](../app-service-web/app-service-web-overview.md)
  * [<span data-ttu-id="defad-138">Aplicativo Móvel</span><span class="sxs-lookup"><span data-stu-id="defad-138">Mobile App</span></span>](../app-service-mobile/app-service-mobile-value-prop.md)
  * [<span data-ttu-id="defad-139">Aplicativo de API</span><span class="sxs-lookup"><span data-stu-id="defad-139">API App</span></span>](../app-service-api/app-service-api-apps-why-best-platform.md)
* [<span data-ttu-id="defad-140">Arquitetura de Serviço de Aplicativo do Azure (apresentação)</span><span class="sxs-lookup"><span data-stu-id="defad-140">Azure App Service Architecture (presentation)</span></span>](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [<span data-ttu-id="defad-141">Comparação de Serviço de Aplicativo, Serviços de nuvem e Máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="defad-141">Azure App Service, Cloud Services, and Virtual Machines comparison</span></span>](../app-service-web/choose-web-site-cloud-service-vm.md)
* [<span data-ttu-id="defad-142">Noções básicas sobre Aplicativos Móveis do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="defad-142">Understanding App Service Plans</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [<span data-ttu-id="defad-143">Introdução ao ambiente de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="defad-143">Introduction to App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
  * [<span data-ttu-id="defad-144">Exercício: Criar um Ambiente do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="defad-144">Exercise: Create an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="defad-145">Suporte a Pilhas de Desenvolvimento de Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="defad-145">Azure App Service Development Stacks Support</span></span>](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)



