---
title: "Serviço de Aplicativo do Azure e seu impacto sobre os serviços existentes do Azure"
description: "Explica como o novo Serviço de Aplicativo do Azure e seus recursos afetam os serviços existentes no Azure."
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
ms.openlocfilehash: ed967fda7a216ed49532be54228ebe888cf16b6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="8d6d3-103">Serviço de Aplicativo do Azure e serviços existentes do Azure</span><span class="sxs-lookup"><span data-stu-id="8d6d3-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="8d6d3-104">Este artigo descreve as alterações nos serviços existentes do Azure como parte da alteração para reunir vários serviços do Azure no [Serviço de Aplicativo do Azure](https://azure.microsoft.com/services/app-service/), uma nova oferta integrada.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-104">This article outlines the changes to existing Azure services as part of the change to bring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="8d6d3-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8d6d3-105">Overview</span></span>
<span data-ttu-id="8d6d3-106">[Serviço de Aplicativo do Azure](https://azure.microsoft.com/services/app-service/) é um serviço de nuvem novo e exclusivo que habilita os desenvolvedores a criar aplicativos Web e móveis para qualquer plataforma e qualquer dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers to create web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="8d6d3-107">O Serviço de Aplicativo é uma solução integrada criada para simplificar funções de codificação repetidas, integrar-se a sistemas corporativos e de SaaS e automatizar processos de negócios, além de atender às suas necessidades de segurança, confiabilidade e escalabilidade.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-107">App Service is an integrated solution designed to streamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="8d6d3-108">O Serviço de Aplicativo reúne os seguintes serviços existentes do Azure - [Sites](https://azure.microsoft.com/services/websites/), [Serviços Móveis](https://azure.microsoft.com/services/mobile-services/) e [Serviços Biztalk](https://azure.microsoft.com/services/biztalk-services/) em um único serviço combinado, enquanto acrescenta novas capacidades avançadas.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-108">App Service brings together the following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="8d6d3-109">O Serviço de Aplicativo permite hospedar os seguintes tipos de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="8d6d3-109">App Service allows you to host the following app types:</span></span>

* <span data-ttu-id="8d6d3-110">Aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="8d6d3-110">Web Apps</span></span>
* <span data-ttu-id="8d6d3-111">Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="8d6d3-111">Mobile Apps</span></span>
* <span data-ttu-id="8d6d3-112">Aplicativos de API</span><span class="sxs-lookup"><span data-stu-id="8d6d3-112">API Apps</span></span>
* <span data-ttu-id="8d6d3-113">Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="8d6d3-113">Logic Apps</span></span>

<span data-ttu-id="8d6d3-114">A tabela a seguir explica como os serviços existentes do Azure são mapeados para o Serviço de Aplicativo e os tipos de aplicativos disponíveis nele.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-114">The following table explains how existing Azure services map to App Service and the app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="8d6d3-115">Serviço existente do Azure</span><span class="sxs-lookup"><span data-stu-id="8d6d3-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="8d6d3-116">Serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="8d6d3-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="8d6d3-117">O que mudou</span><span class="sxs-lookup"><span data-stu-id="8d6d3-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="8d6d3-118">Websites do Azure</span><span class="sxs-lookup"><span data-stu-id="8d6d3-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="8d6d3-119">Aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="8d6d3-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="8d6d3-120">Para os Sites do Azure, o Serviço de Aplicativo limita-se estritamente à alteração do nome Sites para Aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-120">For Azure Websites, App Service is strictly limited to changing the name  Websites to Web Apps.</span></span>
<p><li><span data-ttu-id="8d6d3-121">Todas as suas instâncias existentes de Sites agora são Aplicativos Web no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="8d6d3-122">Você pode acessar os sites existentes pelo <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Portal do Azure</a>, onde encontrará todos os sites existentes em <em>Aplicativos Web</em>.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-122">You can access your existing websites via the <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="8d6d3-123"><em>Plano de hospedagem de Web</em> agora é <em>plano do serviço de aplicativo</em>.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="8d6d3-124">Um <em>Plano do Serviço de Aplicativo</em> pode hospedar qualquer tipo do Serviço de Aplicativo, como aplicativos Web, Móveis, Lógicos ou de API.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="8d6d3-125">Os aplicativos Web do Serviço de Aplicativo do Azure têm Disponibilidade Geral.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="8d6d3-126"><a href="http://azure.microsoft.com/services/app-service/web/">Saiba mais sobre aplicativos Web</a>.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="8d6d3-127">Serviços móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="8d6d3-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="8d6d3-128">Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="8d6d3-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="8d6d3-129">Os Serviços Móveis continuam disponíveis como um serviço autônomo e permanecem com suporte completo.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-129">Mobile Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="8d6d3-130">Os Aplicativos Móveis são um tipo de aplicativo do Serviço de Aplicativo, que integram toda a funcionalidade dos Serviços Móveis e muito mais.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-130">Mobile Apps is an app type in App Service, which integrates all of the functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="8d6d3-131">É fácil <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrar dos Serviços Móveis para os Aplicativos Móveis</a>.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-131">It is easy to <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services to Mobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="8d6d3-132">Como parte do Serviço de Aplicativo, os Aplicativos Móveis obtêm novos recursos além de Serviços Móveis, como a integração com sistemas de SaaS e locais, slots de preparação, Trabalhos Web, melhores opções de dimensionamento e muito mais.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="8d6d3-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Saiba mais sobre os aplicativos móveis</a>.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="8d6d3-134">Aplicativos de API</span><span class="sxs-lookup"><span data-stu-id="8d6d3-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="8d6d3-135">Os Aplicativos de API são um novo tipo de aplicativo do Serviço de Aplicativo que permitem que você compile e consuma APIs na nuvem facilmente.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in the cloud.</span></span></p>
<p><li><span data-ttu-id="8d6d3-136"><a href="http://azure.microsoft.com/services/app-service/api/">Saiba mais sobre aplicativos de API</a>.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="8d6d3-137">Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="8d6d3-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="8d6d3-138">Os Aplicativos Lógicos são um novo tipo de aplicativo do Serviço de Aplicativo que permite automatizar facilmente os processos corporativos.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="8d6d3-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Saiba mais sobre aplicativos lógicos</a>.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="8d6d3-140">Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="8d6d3-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="8d6d3-141">Aplicativos de API do BizTalk</span><span class="sxs-lookup"><span data-stu-id="8d6d3-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="8d6d3-142">Os Serviços BizTalk continuam disponíveis como um serviço autônomo e permanecem com suporte completo.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-142">BizTalk Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="8d6d3-143">Todos os recursos dos Serviços BizTalk são integrados ao Serviço de Aplicativo como Aplicativos de API, permitindo aos usuários realizar cenários de integração de aplicativos empresariais e integração B2B com qualquer um dos tipos de aplicativos no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-143">All the capabilities of BizTalk Services are integrated into App Service as API Apps enabling users to perform enterprise application integration and B2B integration scenarios with any of the app types in App Service.</span></span></p>
<li><p><span data-ttu-id="8d6d3-144">Com os Aplicativos Lógicos, agora é possível automatizar processos corporativos usando uma experiência de design visual para criar fluxos de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8d6d3-144">With Logic Apps, you can now automate business processes using a visual design experience to create workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="8d6d3-145">Para saber mais, acesse a documentação do [Serviço de Aplicativo](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="8d6d3-145">To learn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

