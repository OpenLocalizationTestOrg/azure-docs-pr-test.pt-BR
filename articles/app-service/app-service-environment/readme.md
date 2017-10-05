---
title: "Leiame Ambiente do Serviço de Aplicativo do Azure"
description: "Lista a documentação que descreve o Ambiente do Serviço de Aplicativo do Azure"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 77452413-5193-4762-8b3d-5fa8e4edf1ca
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 5b1362854dbc3b0098718bd2ea3cffb06366000c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="7f77c-103">Documentação do ambiente do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="7f77c-103">App Service environment documentation</span></span>
 <span data-ttu-id="7f77c-104">Um Ambiente do Serviço de Aplicativo do Azure é um recurso do Serviço de Aplicativo do Azure que fornece um ambiente totalmente isolado e dedicado a executar com segurança os aplicativos do Serviço de Aplicativo em grande escala.</span><span class="sxs-lookup"><span data-stu-id="7f77c-104">Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span></span> <span data-ttu-id="7f77c-105">Esse recurso pode hospedar os [aplicativos Web][webapps], [aplicativos móveis][mobileapps], [aplicativos de API][APIApps] e [funções][Functions].</span><span class="sxs-lookup"><span data-stu-id="7f77c-105">This capability can host your [web apps][webapps], [mobile apps][mobileapps], [API apps][APIApps], and [functions][Functions].</span></span>

<span data-ttu-id="7f77c-106">Os ASE (Ambientes de Serviço de Aplicativo) são ideais para cargas de trabalho de aplicativos que exijam:</span><span class="sxs-lookup"><span data-stu-id="7f77c-106">App Service environments (ASEs) are ideal for application workloads that require:</span></span>

* <span data-ttu-id="7f77c-107">Uma escala muito alta.</span><span class="sxs-lookup"><span data-stu-id="7f77c-107">Very high scale.</span></span>
* <span data-ttu-id="7f77c-108">Isolamento e acesso seguro à rede.</span><span class="sxs-lookup"><span data-stu-id="7f77c-108">Isolation and secure network access.</span></span>

<span data-ttu-id="7f77c-109">Os clientes podem criar vários ASEs dentro de uma única região do Azure, bem como entre várias regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f77c-109">Customers can create multiple ASEs within a single Azure region and across multiple Azure regions.</span></span> <span data-ttu-id="7f77c-110">Essa versatilidade torna os ASEs ideais para escalar horizontalmente camadas de aplicativo sem estado para dar suporte a cargas de trabalho RPS altas.</span><span class="sxs-lookup"><span data-stu-id="7f77c-110">This versatility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="7f77c-111">Os ASEs são isolados para executar somente aplicativos de um único cliente, e sempre são implantados em uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f77c-111">ASEs are isolated to running only a single customer's applications and are always deployed into an Azure virtual network.</span></span> <span data-ttu-id="7f77c-112">Os clientes têm controle refinado sobre o tráfego de rede do aplicativo de entrada e saída usando os [Grupos de Segurança de Rede][NSGs].</span><span class="sxs-lookup"><span data-stu-id="7f77c-112">Customers have fine-grained control over inbound and outbound application network traffic by using [Network Security Groups][NSGs].</span></span> <span data-ttu-id="7f77c-113">Os aplicativos também podem estabelecer conexões seguras de alta velocidade por redes virtuais para recursos corporativos locais.</span><span class="sxs-lookup"><span data-stu-id="7f77c-113">Applications can also establish high-speed secure connections over virtual networks to on-premises corporate resources.</span></span>

<span data-ttu-id="7f77c-114">Os aplicativos muitas vezes precisam acessar recursos corporativos, como bancos de dados internos e serviços Web.</span><span class="sxs-lookup"><span data-stu-id="7f77c-114">Apps frequently need to access corporate resources, such as internal databases and web services.</span></span> <span data-ttu-id="7f77c-115">Os aplicativos executados em ASEs podem acessar recursos por meio de conexões VPN [site a site][SiteToSite] e [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="7f77c-115">Apps that run on ASEs can access resources via [site-to-site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* <span data-ttu-id="7f77c-116">[O que é um Ambiente do Serviço de Aplicativo?][Intro]</span><span class="sxs-lookup"><span data-stu-id="7f77c-116">[What is an App Service environment?][Intro]</span></span>
* <span data-ttu-id="7f77c-117">[Criar um ambiente de serviço de aplicativo][MakeExternalASE]</span><span class="sxs-lookup"><span data-stu-id="7f77c-117">[Create an App Service environment][MakeExternalASE]</span></span>
* <span data-ttu-id="7f77c-118">[Criar um ambiente do Serviço de Aplicativo de balanceador de carga interno][MakeILBASE]</span><span class="sxs-lookup"><span data-stu-id="7f77c-118">[Create an internal load balancer App Service environment][MakeILBASE]</span></span>
* <span data-ttu-id="7f77c-119">[Usar um ambiente do Serviço de Aplicativo][UsingASE]</span><span class="sxs-lookup"><span data-stu-id="7f77c-119">[Use an App Service environment][UsingASE]</span></span>
* <span data-ttu-id="7f77c-120">[Considerações de rede e o ambiente do Serviço de Aplicativo][ASENetwork]</span><span class="sxs-lookup"><span data-stu-id="7f77c-120">[Networking considerations and the App Service environment][ASENetwork]</span></span>
* <span data-ttu-id="7f77c-121">[Criar um ambiente do Serviço de Aplicativo de um modelo][MakeASEfromTemplate]</span><span class="sxs-lookup"><span data-stu-id="7f77c-121">[Create an App Service environment from a template][MakeASEfromTemplate]</span></span>


## <a name="videos"></a><span data-ttu-id="7f77c-122">Vídeos</span><span class="sxs-lookup"><span data-stu-id="7f77c-122">Videos</span></span>
<span data-ttu-id="7f77c-123">Domine a PaaS moderna para a empresa com o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="7f77c-123">Master Modern PaaS for the Enterprise with Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

<span data-ttu-id="7f77c-124">Implantando aplicativos altamente escalonáveis e seguros</span><span class="sxs-lookup"><span data-stu-id="7f77c-124">Deploying Highly Scalable and Secure Apps</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

<span data-ttu-id="7f77c-125">Executando aplicativos Enterprise Web e móveis no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="7f77c-125">Running Enterprise Web and Mobile Apps on Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a><span data-ttu-id="7f77c-126">Ambiente do Serviço de Aplicativo v1</span><span class="sxs-lookup"><span data-stu-id="7f77c-126">App Service Environment v1</span></span> ##
<span data-ttu-id="7f77c-127">Há duas versões do Ambiente do Serviço de Aplicativo: ASEv1 e ASEv2.</span><span class="sxs-lookup"><span data-stu-id="7f77c-127">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="7f77c-128">Para obter informações sobre ASEv1, confira a [documentação do Ambiente do Serviço de Aplicativo v1][ASEv1README].</span><span class="sxs-lookup"><span data-stu-id="7f77c-128">For information on ASEv1, see [App Service Environment v1 documentation][ASEv1README].</span></span>


<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[ASEv1README]: ../app-service-app-service-environments-readme.md
[SiteToSite]: ../../vpn-gateway/vpn-gateway-site-to-site-create.md
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
