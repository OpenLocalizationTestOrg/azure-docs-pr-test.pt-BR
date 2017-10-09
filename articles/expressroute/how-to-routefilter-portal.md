---
title: 'Configurar os filtros de rota para o emparelhamento da Microsoft do Azure ExpressRoute: Portal | Microsoft Docs'
description: "Este artigo descreve como os filtros de rota tooconfigure para usar o Microsoft Peering Olá portal do Azure"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="cd916-103">Configurar os filtros de rota para o emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="cd916-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="cd916-104">Filtros de rota são uma maneira tooconsume um subconjunto de serviços com suporte por meio de emparelhamento da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cd916-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="cd916-105">Olá etapas nesta ajuda de artigo, configurar e gerenciar filtros de rotas para circuitos do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="cd916-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="cd916-106">Dynamics 365 serviços e serviços do Office 365, como o Exchange Online, SharePoint Online e Skype for Business, são acessíveis por meio de emparelhamento da Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="cd916-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="cd916-107">Quando emparelhamento da Microsoft é configurado em um circuito de rota expressa, todos os serviços de toothese relacionados prefixos são anunciados através de sessões BGP Olá estabelecidas.</span><span class="sxs-lookup"><span data-stu-id="cd916-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="cd916-108">Um valor de comunidade BGP é anexado tooevery prefixo tooidentify Olá serviço oferecido por meio de prefixo hello.</span><span class="sxs-lookup"><span data-stu-id="cd916-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="cd916-109">Para obter uma lista de valores de comunidade BGP hello e serviços de saudação são mapeados para, consulte [comunidades BGP](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="cd916-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="cd916-110">Se você precisar de serviços de conectividade do tooall, um grande número de prefixos é anunciado através do BGP.</span><span class="sxs-lookup"><span data-stu-id="cd916-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="cd916-111">Isso aumenta consideravelmente o tamanho Olá Olá de tabelas de rotas mantida por roteadores na rede.</span><span class="sxs-lookup"><span data-stu-id="cd916-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="cd916-112">Se você planejar tooconsume apenas um subconjunto de serviços oferecido por meio de emparelhamento da Microsoft, você pode reduzir o tamanho de saudação de suas tabelas de rota de duas maneiras.</span><span class="sxs-lookup"><span data-stu-id="cd916-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="cd916-113">Você pode:</span><span class="sxs-lookup"><span data-stu-id="cd916-113">You can:</span></span>

- <span data-ttu-id="cd916-114">Filtre prefixos indesejados aplicando filtros de rota nas comunidades do BGP.</span><span class="sxs-lookup"><span data-stu-id="cd916-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="cd916-115">Essa é uma prática de rede padrão e é usada frequentemente em várias redes.</span><span class="sxs-lookup"><span data-stu-id="cd916-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="cd916-116">Definir filtros de rota e aplicá-las tooyour circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="cd916-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="cd916-117">Um filtro de rota é um novo recurso que permite que você selecione lista de saudação de serviços que você planeje tooconsume por meio de emparelhamento da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cd916-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="cd916-118">Roteadores de rota expressa somente enviam a lista de saudação de prefixos que pertencem a serviços toohello identificados no filtro de rota hello.</span><span class="sxs-lookup"><span data-stu-id="cd916-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="cd916-119"><a name="about"></a>Sobre filtros de rota</span><span class="sxs-lookup"><span data-stu-id="cd916-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="cd916-120">Quando o emparelhamento da Microsoft é configurado no seu circuito de rota expressa, roteadores de borda Microsoft hello estabelecerem um par de sessões BGP com roteadores de borda da saudação (seu ou seu provedor de conectividade).</span><span class="sxs-lookup"><span data-stu-id="cd916-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="cd916-121">Nenhuma rota é rede tooyour anunciado.</span><span class="sxs-lookup"><span data-stu-id="cd916-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="cd916-122">rede de tooyour de anúncios de rota tooenable, você deve associar um filtro de rota.</span><span class="sxs-lookup"><span data-stu-id="cd916-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="cd916-123">Um filtro de roteamento permite identificar os serviços que você deseja tooconsume por meio de emparelhamento da Microsoft do seu circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="cd916-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="cd916-124">É essencialmente uma lista de permissões de todos os valores de comunidade BGP hello.</span><span class="sxs-lookup"><span data-stu-id="cd916-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="cd916-125">Quando o recurso de filtro de rota é definido e anexado tooan circuito de rota expressa, todos os prefixos que mapeiam valores de comunidade BGP toohello são rede tooyour anunciado.</span><span class="sxs-lookup"><span data-stu-id="cd916-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="cd916-126">toobe tooattach capaz de filtros de rota com serviços do Office 365 neles, você deve ter serviços do Office 365 tooconsume autorização por meio de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="cd916-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="cd916-127">Se você não estiver autorizado tooconsume Office 365 services por meio de rota expressa, filtros de rota Olá operação tooattach falhará.</span><span class="sxs-lookup"><span data-stu-id="cd916-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="cd916-128">Para obter mais informações sobre o processo de autorização hello, consulte [rota expressa do Azure para o Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="cd916-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="cd916-129">Os serviços de conectividade tooDynamics 365 não requer nenhuma autorização anterior.</span><span class="sxs-lookup"><span data-stu-id="cd916-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd916-130">Emparelhamento da Microsoft de circuitos ExpressRoute que foram configurados anterior tooAugust 1, 2017 terá todos os prefixos de serviço anunciados através do emparelhamento da Microsoft, mesmo se os filtros de roteamento não estão definidos.</span><span class="sxs-lookup"><span data-stu-id="cd916-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="cd916-131">Emparelhamento da Microsoft de circuitos de rota expressa configurados em ou após 1 de agosto de 2017 não terá quaisquer prefixos anunciados até que um filtro de rota é anexado toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="cd916-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="cd916-132"><a name="workflow"></a>Fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="cd916-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="cd916-133">toosuccessfully de toobe capaz de se conectar a tooservices por meio de emparelhamento da Microsoft, você deve concluir Olá etapas de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="cd916-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="cd916-134">Você deve ter um circuito de ExpressRoute ativado que tenha o Microsoft emparelhamento provisionado.</span><span class="sxs-lookup"><span data-stu-id="cd916-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="cd916-135">Você pode usar o hello tooaccomplish instruções a seguir estas tarefas:</span><span class="sxs-lookup"><span data-stu-id="cd916-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="cd916-136">[Criar um circuito de rota expressa](expressroute-howto-circuit-portal-resource-manager.md) e ter o circuito Olá habilitado por seu provedor de conectividade antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="cd916-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="cd916-137">Olá circuito de rota expressa deve estar em um estado habilitado e configurado.</span><span class="sxs-lookup"><span data-stu-id="cd916-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="cd916-138">[Criar emparelhamento da Microsoft](expressroute-howto-routing-portal-resource-manager.md) se você gerenciar sessões de BGP de saudação diretamente.</span><span class="sxs-lookup"><span data-stu-id="cd916-138">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="cd916-139">Ou então, faça com que seu provedor de conectividade provisione emparelhamento da Microsoft para o circuito.</span><span class="sxs-lookup"><span data-stu-id="cd916-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="cd916-140">Você deve criar e configurar um filtro de rota.</span><span class="sxs-lookup"><span data-stu-id="cd916-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="cd916-141">Identificar Olá serviços tooconsume por meio de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="cd916-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="cd916-142">Identificar Olá lista de valores de comunidade BGP associados aos serviços de saudação</span><span class="sxs-lookup"><span data-stu-id="cd916-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="cd916-143">Criar uma regra tooallow Olá prefixo lista correspondente Olá valores de comunidade do BGP</span><span class="sxs-lookup"><span data-stu-id="cd916-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="cd916-144">Você deve anexar um circuito de rota expressa toohello do filtro de rota hello.</span><span class="sxs-lookup"><span data-stu-id="cd916-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cd916-145">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="cd916-145">Before you begin</span></span>

<span data-ttu-id="cd916-146">Antes de começar a configuração, verifique se que você atende Olá critérios a seguir:</span><span class="sxs-lookup"><span data-stu-id="cd916-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="cd916-147">Saudação de revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="cd916-147">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="cd916-148">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="cd916-148">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="cd916-149">Siga as instruções de saudação muito[criar um circuito de rota expressa](expressroute-howto-circuit-portal-resource-manager.md) e ter o circuito Olá habilitado por seu provedor de conectividade antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="cd916-149">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="cd916-150">Olá circuito de rota expressa deve estar em um estado habilitado e configurado.</span><span class="sxs-lookup"><span data-stu-id="cd916-150">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="cd916-151">Você deve ter um emparelhamento da Microsoft ativo.</span><span class="sxs-lookup"><span data-stu-id="cd916-151">You must have an active Microsoft peering.</span></span> <span data-ttu-id="cd916-152">Siga as instruções em [Criar e modificar a configuração de emparelhamento](expressroute-howto-routing-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="cd916-152">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <span data-ttu-id="cd916-153"><a name="prefixes"></a>Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="cd916-153"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="cd916-154">Obter uma lista de prefixos e valores de comunidade BGP</span><span class="sxs-lookup"><span data-stu-id="cd916-154">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="cd916-155">1. Obter uma lista de valores de comunidade BGP</span><span class="sxs-lookup"><span data-stu-id="cd916-155">1. Get a list of BGP community values</span></span>

<span data-ttu-id="cd916-156">Os valores de comunidade BGP associados aos serviços acessíveis por meio de emparelhamento da Microsoft está disponível em Olá [requisitos de roteamento de rota expressa](expressroute-routing.md) página.</span><span class="sxs-lookup"><span data-stu-id="cd916-156">BGP community values associated with services accessible through Microsoft peering is available in hello [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="cd916-157">2. Faça uma lista de valores de saudação que você deseja toouse</span><span class="sxs-lookup"><span data-stu-id="cd916-157">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="cd916-158">Faça uma lista de valores de comunidade BGP, que você deseja toouse no filtro de rota hello.</span><span class="sxs-lookup"><span data-stu-id="cd916-158">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="cd916-159">Por exemplo, Olá valor de comunidade BGP para serviços do Dynamics 365 é 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="cd916-159">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="cd916-160"><a name="filter"></a>Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="cd916-160"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="cd916-161">Criar um filtro de rota e uma regra de filtro</span><span class="sxs-lookup"><span data-stu-id="cd916-161">Create a route filter and a filter rule</span></span>

<span data-ttu-id="cd916-162">Um filtro de rota pode ter apenas uma regra e regra Olá deve ser do tipo 'Permitir'.</span><span class="sxs-lookup"><span data-stu-id="cd916-162">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="cd916-163">Essa regra pode ter uma lista de valores de comunidade BGP associados a ela.</span><span class="sxs-lookup"><span data-stu-id="cd916-163">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="cd916-164">1. Criar um filtro de rota</span><span class="sxs-lookup"><span data-stu-id="cd916-164">1. Create a route filter</span></span>
<span data-ttu-id="cd916-165">Você pode criar um filtro de rota selecionando Olá opção toocreate um novo recurso.</span><span class="sxs-lookup"><span data-stu-id="cd916-165">You can create a route filter by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="cd916-166">Clique em **novo** > **rede** > **RouteFilter**, conforme mostrado no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="cd916-166">Click **New** > **Networking** > **RouteFilter**, as shown in hello following image:</span></span>

![Criar um filtro de rota](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="cd916-168">Você deve colocar o filtro de rota Olá em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cd916-168">You must place hello route filter in a resource group.</span></span> 

![Criar um filtro de rota](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="cd916-170">2. Criar uma regra de filtro</span><span class="sxs-lookup"><span data-stu-id="cd916-170">2. Create a filter rule</span></span>

<span data-ttu-id="cd916-171">Você pode adicionar e atualizar regras selecionando Olá gerenciar guia de regra para o filtro de rota.</span><span class="sxs-lookup"><span data-stu-id="cd916-171">You can add and update rules by selecting hello manage rule tab for your route filter.</span></span>

![Criar um filtro de rota](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="cd916-173">Você pode selecionar Olá serviços que você deseja tooconnect toofrom Olá lista suspensa e salvar a regra de saudação quando terminar.</span><span class="sxs-lookup"><span data-stu-id="cd916-173">You can select hello services you want tooconnect toofrom hello drop down list and save hello rule when done.</span></span>

![Criar um filtro de rota](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <span data-ttu-id="cd916-175"><a name="attach"></a>Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="cd916-175"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="cd916-176">Anexar o circuito de rota expressa tooan do filtro de rota Olá</span><span class="sxs-lookup"><span data-stu-id="cd916-176">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="cd916-177">Você pode anexar o circuito de tooa de filtro de rota Olá selecionando o botão de "Adicionar circuito" hello e selecionando circuito de rota expressa Olá na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd916-177">You can attach hello route filter tooa circuit by selecting hello "add Circuit" button and selecting hello ExpressRoute circuit from hello drop down list.</span></span>

![Criar um filtro de rota](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <span data-ttu-id="cd916-179"><a name="getproperties"></a>Propriedades de saudação tooget de um filtro de rota</span><span class="sxs-lookup"><span data-stu-id="cd916-179"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="cd916-180">Você pode exibir as propriedades de um filtro de rota quando você abre o recurso Olá no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd916-180">You can view properties of a route filter when you open hello resource in hello portal.</span></span>

![Criar um filtro de rota](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <span data-ttu-id="cd916-182"><a name="updateproperties"></a>Propriedades de saudação tooupdate de um filtro de rota</span><span class="sxs-lookup"><span data-stu-id="cd916-182"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="cd916-183">Você pode atualizar a lista de saudação do BGP comunidade valores tooa anexado circuito selecionando o botão hello "Gerenciar regra".</span><span class="sxs-lookup"><span data-stu-id="cd916-183">You can update hello list of BGP community values attached tooa circuit by selecting hello "Manage rule" button.</span></span>


![Criar um filtro de rota](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Criar um filtro de rota](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <span data-ttu-id="cd916-186"><a name="detach"></a>toodetach um filtro de roteamento de um circuito de rota expressa</span><span class="sxs-lookup"><span data-stu-id="cd916-186"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="cd916-187">toodetach um circuito do filtro de rota hello, clique com o botão direito no circuito hello e clique no "desassociar".</span><span class="sxs-lookup"><span data-stu-id="cd916-187">toodetach a circuit from hello route filter, right click on hello circuit and click on "disassociate".</span></span>

![Criar um filtro de rota](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <span data-ttu-id="cd916-189"><a name="delete"></a>toodelete um filtro de rota</span><span class="sxs-lookup"><span data-stu-id="cd916-189"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="cd916-190">Você pode excluir um filtro de rota, selecionando o botão de exclusão de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd916-190">You can delete a route filter by selecting hello delete button.</span></span> 

![Criar um filtro de rota](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="cd916-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cd916-192">Next steps</span></span>

<span data-ttu-id="cd916-193">Para obter mais informações sobre a rota expressa, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="cd916-193">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
