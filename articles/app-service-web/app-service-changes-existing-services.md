---
title: "aaaAzure do serviço de aplicativo e seu impacto sobre os serviços do Azure existentes"
description: "Explica como Olá novo serviço de aplicativo do Azure e seus recursos afetam os serviços existentes no Azure."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="a1cb0-103">Serviço de Aplicativo do Azure e serviços existentes do Azure</span><span class="sxs-lookup"><span data-stu-id="a1cb0-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="a1cb0-104">Este artigo descreve Olá alterações tooexisting serviços do Azure como parte da saudação alteração toobring junto vários serviços do Azure em [do serviço de aplicativo do Azure](https://azure.microsoft.com/services/app-service/), uma nova oferta integrada.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-104">This article outlines hello changes tooexisting Azure services as part of hello change toobring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="a1cb0-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a1cb0-105">Overview</span></span>
<span data-ttu-id="a1cb0-106">[Serviço de aplicativo do Azure](https://azure.microsoft.com/services/app-service/) é um serviço de nuvem novos e exclusivos que permite que os desenvolvedores toocreate aplicativos web e móveis para qualquer plataforma e de qualquer dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers toocreate web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="a1cb0-107">Serviço de aplicativo é que uma solução integrada projetada toostreamline repetido funções de codificação, integrar com o enterprise e sistemas de SaaS e automatizar processos de negócios enquanto atende suas necessidades de segurança, confiabilidade e escalabilidade.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-107">App Service is an integrated solution designed toostreamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="a1cb0-108">Serviço de aplicativo reúne saudação do Azure existentes a seguir services - [sites](https://azure.microsoft.com/services/websites/), [serviços móveis](https://azure.microsoft.com/services/mobile-services/), e [serviços Biztalk](https://azure.microsoft.com/services/biztalk-services/) em um único combinado serviço, enquanto adicionando novos recursos eficientes.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-108">App Service brings together hello following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="a1cb0-109">Serviço de aplicativo permite que você toohost Olá seguintes tipos de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="a1cb0-109">App Service allows you toohost hello following app types:</span></span>

* <span data-ttu-id="a1cb0-110">Aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="a1cb0-110">Web Apps</span></span>
* <span data-ttu-id="a1cb0-111">Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="a1cb0-111">Mobile Apps</span></span>
* <span data-ttu-id="a1cb0-112">Aplicativos de API</span><span class="sxs-lookup"><span data-stu-id="a1cb0-112">API Apps</span></span>
* <span data-ttu-id="a1cb0-113">Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="a1cb0-113">Logic Apps</span></span>

<span data-ttu-id="a1cb0-114">Olá, tabela a seguir explica como existente do Azure services mapear tooApp serviço e hello tipos de aplicativo disponíveis dentro dele.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-114">hello following table explains how existing Azure services map tooApp Service and hello app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="a1cb0-115">Serviço existente do Azure</span><span class="sxs-lookup"><span data-stu-id="a1cb0-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="a1cb0-116">Serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="a1cb0-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="a1cb0-117">O que mudou</span><span class="sxs-lookup"><span data-stu-id="a1cb0-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="a1cb0-118">Websites do Azure</span><span class="sxs-lookup"><span data-stu-id="a1cb0-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="a1cb0-119">Aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="a1cb0-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="a1cb0-120">Para sites do Azure, o serviço de aplicativo é estritamente limitada toochanging Olá nome sites tooWeb aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-120">For Azure Websites, App Service is strictly limited toochanging hello name  Websites tooWeb Apps.</span></span>
<p><li><span data-ttu-id="a1cb0-121">Todas as suas instâncias existentes de Sites agora são Aplicativos Web no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="a1cb0-122">Você pode acessar seus sites existentes por meio de saudação <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Portal do Azure</a>, onde você encontrará todos os sites existentes em <em>aplicativos Web</em>.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-122">You can access your existing websites via hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="a1cb0-123"><em>Plano de hospedagem de Web</em> agora é <em>plano do serviço de aplicativo</em>.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="a1cb0-124">Um <em>Plano do Serviço de Aplicativo</em> pode hospedar qualquer tipo do Serviço de Aplicativo, como aplicativos Web, Móveis, Lógicos ou de API.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="a1cb0-125">Os aplicativos Web do Serviço de Aplicativo do Azure têm Disponibilidade Geral.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="a1cb0-126"><a href="http://azure.microsoft.com/services/app-service/web/">Saiba mais sobre aplicativos Web</a>.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="a1cb0-127">Serviços móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="a1cb0-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="a1cb0-128">Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="a1cb0-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="a1cb0-129">Serviços móveis continuar toobe disponível como um serviço autônomo e permanecem totalmente suportados.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-129">Mobile Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="a1cb0-130">Aplicativos móveis é um tipo de aplicativo no serviço de aplicativo, que integra a funcionalidade de saudação de serviços móveis e muito mais.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-130">Mobile Apps is an app type in App Service, which integrates all of hello functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="a1cb0-131">Ele é muito fácil<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrar de serviços móveis tooMobile aplicativos</a>.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-131">It is easy too<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services tooMobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="a1cb0-132">Como parte do Serviço de Aplicativo, os Aplicativos Móveis obtêm novos recursos além de Serviços Móveis, como a integração com sistemas de SaaS e locais, slots de preparação, Trabalhos Web, melhores opções de dimensionamento e muito mais.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="a1cb0-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Saiba mais sobre os aplicativos móveis</a>.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="a1cb0-134">Aplicativos de API</span><span class="sxs-lookup"><span data-stu-id="a1cb0-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="a1cb0-135">Aplicativos de API é um novo tipo de aplicativo no serviço de aplicativo que permite criar e consumir APIs na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in hello cloud.</span></span></p>
<p><li><span data-ttu-id="a1cb0-136"><a href="http://azure.microsoft.com/services/app-service/api/">Saiba mais sobre aplicativos de API</a>.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="a1cb0-137">Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="a1cb0-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="a1cb0-138">Os Aplicativos Lógicos são um novo tipo de aplicativo do Serviço de Aplicativo que permite automatizar facilmente os processos corporativos.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="a1cb0-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Saiba mais sobre aplicativos lógicos</a>.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="a1cb0-140">Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="a1cb0-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="a1cb0-141">Aplicativos de API do BizTalk</span><span class="sxs-lookup"><span data-stu-id="a1cb0-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="a1cb0-142">Os serviços do BizTalk continuar toobe disponível como um serviço autônomo e permanecem totalmente suportados.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-142">BizTalk Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="a1cb0-143">Todos os recursos de saudação dos serviços do BizTalk são integrados ao serviço de aplicativo como aplicativos de API Habilitando usuários tooperform integração de aplicativos empresariais e cenários de integração B2B com nenhum dos tipos de saudação do aplicativo no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-143">All hello capabilities of BizTalk Services are integrated into App Service as API Apps enabling users tooperform enterprise application integration and B2B integration scenarios with any of hello app types in App Service.</span></span></p>
<li><p><span data-ttu-id="a1cb0-144">Com a lógica de aplicativos, agora você pode automatizar processos de negócios usando um fluxos de trabalho de toocreate de experiência de design visual.</span><span class="sxs-lookup"><span data-stu-id="a1cb0-144">With Logic Apps, you can now automate business processes using a visual design experience toocreate workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="a1cb0-145">toolearn mais, visite [documentação do serviço de aplicativo](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="a1cb0-145">toolearn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

