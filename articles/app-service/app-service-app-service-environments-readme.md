---
title: "aaaApp ambiente de serviço | Microsoft Docs"
description: "O que é um Ambiente do Serviço de Aplicativo do Azure? Uma introdução tooApp ambiente de serviço."
keywords: "ambiente do serviço de aplicativo do azure, rede virtual, rede segura"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 1db5c057-3c56-4537-b580-cdd21fe3f3a7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: stefsch
ms.openlocfilehash: 1b59fed4e5a72d4c4805e1dca203747e07e77103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="b8c96-105">Documentação do Ambiente de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="b8c96-105">App Service Environment Documentation</span></span>
<span data-ttu-id="b8c96-106">Um Ambiente de Serviço de Aplicativo é uma opção de plano de serviço [Premium][PremiumTier] do Serviço de Aplicativo do Azure que fornece um ambiente totalmente isolado e dedicado para executar com segurança todos os seus aplicativos do Serviço de Aplicativo do Azure em alta escala, incluindo [Aplicativos Web][WebApps], [Aplicativos Móveis][MobileApps] e [Aplicativos de API][APIApps].</span><span class="sxs-lookup"><span data-stu-id="b8c96-106">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="b8c96-107">Os Ambientes de Serviço de Aplicativo são ideais para cargas de trabalho de aplicativos que exigem:</span><span class="sxs-lookup"><span data-stu-id="b8c96-107">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="b8c96-108">Escala muito alta</span><span class="sxs-lookup"><span data-stu-id="b8c96-108">Very high scale</span></span>
* <span data-ttu-id="b8c96-109">Isolamento e acesso seguro à rede</span><span class="sxs-lookup"><span data-stu-id="b8c96-109">Isolation and secure network access</span></span>

<span data-ttu-id="b8c96-110">Os clientes podem criar vários Ambientes de Serviço de Aplicativo dentro de uma única região do Azure, bem como entre várias regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8c96-110">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="b8c96-111">Isso faz dos Ambientes de Serviço de Aplicativo ideais para dimensionar horizontalmente camadas de aplicativo sem estado para dar suporte a cargas de trabalho RPS altas.</span><span class="sxs-lookup"><span data-stu-id="b8c96-111">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="b8c96-112">Ambientes de serviço de aplicativo são isolado toorunning apenas os aplicativos de um único cliente e sempre são implantados em uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b8c96-112">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="b8c96-113">Os clientes têm controle refinado sobre o tráfego de rede do aplicativo de entrada e saída usando os [grupos de segurança de rede][NetworkSecurityGroups].</span><span class="sxs-lookup"><span data-stu-id="b8c96-113">Customers have fine-grained control over both inbound and outbound application network traffic using [network security groups][NetworkSecurityGroups].</span></span>  <span data-ttu-id="b8c96-114">Aplicativos também podem estabelecer conexões seguras de alta velocidade sobre recursos corporativos de tooon locais de redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="b8c96-114">Applications can also establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="b8c96-115">Normalmente, os aplicativos precisam tooaccess a recursos corporativos, como bancos de dados internos e serviços da web.</span><span class="sxs-lookup"><span data-stu-id="b8c96-115">Apps frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="b8c96-116">Os aplicativos em execução em Ambientes de Serviço de Aplicativo podem acessar os recursos acessíveis via conexões VPN [Site a Site][SiteToSite] e [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="b8c96-116">Apps running on App Service Environments can access resources reachable via [Site-to-Site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* [<span data-ttu-id="b8c96-117">O que é um Ambiente do Serviço de Aplicativo?</span><span class="sxs-lookup"><span data-stu-id="b8c96-117">What is an App Service Environment?</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
* [<span data-ttu-id="b8c96-118">Criando um Ambiente do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="b8c96-118">Creating an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="b8c96-119">Criando Aplicativos em um Ambiente do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="b8c96-119">Creating Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="b8c96-120">Criando e usando um Balanceador de Carga Interno com Ambientes do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="b8c96-120">Creating and Using an Internal Load Balancer with App Service Environments</span></span>](../app-service-web/app-service-environment-with-internal-load-balancer.md)
* [<span data-ttu-id="b8c96-121">Configurando um Ambiente do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="b8c96-121">Configuring an App Service Environment</span></span>](../app-service-web/app-service-web-configure-an-app-service-environment.md) 
* [<span data-ttu-id="b8c96-122">Dimensionando aplicativos em um Ambiente do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="b8c96-122">Scaling Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-scale-a-web-app-in-an-app-service-environment.md)
* [<span data-ttu-id="b8c96-123">Arquitetura e Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="b8c96-123">Network Security and Architecture</span></span>](../app-service-web/app-service-app-service-environment-network-architecture-overview.md)

## <a name="how-tos"></a><span data-ttu-id="b8c96-124">Instruções</span><span class="sxs-lookup"><span data-stu-id="b8c96-124">How To's</span></span>
[!INCLUDE [app-service-blueprint-app-service-environment](../../includes/app-service-blueprint-app-service-environment.md)]

## <a name="videos"></a><span data-ttu-id="b8c96-125">Vídeos</span><span class="sxs-lookup"><span data-stu-id="b8c96-125">Videos</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]



<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
