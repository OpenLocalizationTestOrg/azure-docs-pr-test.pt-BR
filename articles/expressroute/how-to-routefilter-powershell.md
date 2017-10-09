---
title: 'Configurar os filtros de rota para o emparelhamento da Microsoft do Azure ExpressRoute: PowerShell | Microsoft Docs'
description: Este artigo descreve como os filtros de rota tooconfigure para Peering Microsoft usando o PowerShell
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
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="c259f-103">Configurar os filtros de rota para o emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="c259f-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="c259f-104">Filtros de rota são uma maneira tooconsume um subconjunto de serviços com suporte por meio de emparelhamento da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c259f-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="c259f-105">Olá etapas nesta ajuda de artigo, configurar e gerenciar filtros de rotas para circuitos do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c259f-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="c259f-106">Dynamics 365 serviços e serviços do Office 365, como o Exchange Online, SharePoint Online e Skype for Business, são acessíveis por meio de emparelhamento da Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="c259f-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="c259f-107">Quando emparelhamento da Microsoft é configurado em um circuito de rota expressa, todos os serviços de toothese relacionados prefixos são anunciados através de sessões BGP Olá estabelecidas.</span><span class="sxs-lookup"><span data-stu-id="c259f-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="c259f-108">Um valor de comunidade BGP é anexado tooevery prefixo tooidentify Olá serviço oferecido por meio de prefixo hello.</span><span class="sxs-lookup"><span data-stu-id="c259f-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="c259f-109">Para obter uma lista de valores de comunidade BGP hello e serviços de saudação são mapeados para, consulte [comunidades BGP](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="c259f-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="c259f-110">Se você precisar de serviços de conectividade do tooall, um grande número de prefixos é anunciado através do BGP.</span><span class="sxs-lookup"><span data-stu-id="c259f-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="c259f-111">Isso aumenta consideravelmente o tamanho Olá Olá de tabelas de rotas mantida por roteadores na rede.</span><span class="sxs-lookup"><span data-stu-id="c259f-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="c259f-112">Se você planejar tooconsume apenas um subconjunto de serviços oferecido por meio de emparelhamento da Microsoft, você pode reduzir o tamanho de saudação de suas tabelas de rota de duas maneiras.</span><span class="sxs-lookup"><span data-stu-id="c259f-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="c259f-113">Você pode:</span><span class="sxs-lookup"><span data-stu-id="c259f-113">You can:</span></span>

- <span data-ttu-id="c259f-114">Filtre prefixos indesejados aplicando filtros de rota nas comunidades do BGP.</span><span class="sxs-lookup"><span data-stu-id="c259f-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="c259f-115">Essa é uma prática de rede padrão e é usada frequentemente em várias redes.</span><span class="sxs-lookup"><span data-stu-id="c259f-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="c259f-116">Definir filtros de rota e aplicá-las tooyour circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="c259f-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="c259f-117">Um filtro de rota é um novo recurso que permite que você selecione lista de saudação de serviços que você planeje tooconsume por meio de emparelhamento da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c259f-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="c259f-118">Roteadores de rota expressa somente enviam a lista de saudação de prefixos que pertencem a serviços toohello identificados no filtro de rota hello.</span><span class="sxs-lookup"><span data-stu-id="c259f-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="c259f-119"><a name="about"></a>Sobre filtros de rota</span><span class="sxs-lookup"><span data-stu-id="c259f-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="c259f-120">Quando o emparelhamento da Microsoft é configurado no seu circuito de rota expressa, roteadores de borda Microsoft hello estabelecerem um par de sessões BGP com roteadores de borda da saudação (seu ou seu provedor de conectividade).</span><span class="sxs-lookup"><span data-stu-id="c259f-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="c259f-121">Nenhuma rota é rede tooyour anunciado.</span><span class="sxs-lookup"><span data-stu-id="c259f-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="c259f-122">rede de tooyour de anúncios de rota tooenable, você deve associar um filtro de rota.</span><span class="sxs-lookup"><span data-stu-id="c259f-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="c259f-123">Um filtro de roteamento permite identificar os serviços que você deseja tooconsume por meio de emparelhamento da Microsoft do seu circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="c259f-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="c259f-124">É essencialmente uma lista de permissões de todos os valores de comunidade BGP hello.</span><span class="sxs-lookup"><span data-stu-id="c259f-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="c259f-125">Quando o recurso de filtro de rota é definido e anexado tooan circuito de rota expressa, todos os prefixos que mapeiam valores de comunidade BGP toohello são rede tooyour anunciado.</span><span class="sxs-lookup"><span data-stu-id="c259f-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="c259f-126">toobe tooattach capaz de filtros de rota com serviços do Office 365 neles, você deve ter serviços do Office 365 tooconsume autorização por meio de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="c259f-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="c259f-127">Se você não estiver autorizado tooconsume Office 365 services por meio de rota expressa, filtros de rota Olá operação tooattach falhará.</span><span class="sxs-lookup"><span data-stu-id="c259f-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="c259f-128">Para obter mais informações sobre o processo de autorização hello, consulte [rota expressa do Azure para o Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="c259f-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="c259f-129">Os serviços de conectividade tooDynamics 365 não requer nenhuma autorização anterior.</span><span class="sxs-lookup"><span data-stu-id="c259f-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c259f-130">Emparelhamento da Microsoft de circuitos ExpressRoute que foram configurados anterior tooAugust 1, 2017 terá todos os prefixos de serviço anunciados através do emparelhamento da Microsoft, mesmo se os filtros de roteamento não estão definidos.</span><span class="sxs-lookup"><span data-stu-id="c259f-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="c259f-131">Emparelhamento da Microsoft de circuitos de rota expressa configurados em ou após 1 de agosto de 2017 não terá quaisquer prefixos anunciados até que um filtro de rota é anexado toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="c259f-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="c259f-132"><a name="workflow"></a>Fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="c259f-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="c259f-133">toosuccessfully de toobe capaz de se conectar a tooservices por meio de emparelhamento da Microsoft, você deve concluir Olá etapas de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="c259f-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="c259f-134">Você deve ter um circuito de ExpressRoute ativado que tenha o Microsoft emparelhamento provisionado.</span><span class="sxs-lookup"><span data-stu-id="c259f-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="c259f-135">Você pode usar o hello tooaccomplish instruções a seguir estas tarefas:</span><span class="sxs-lookup"><span data-stu-id="c259f-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="c259f-136">[Criar um circuito de rota expressa](expressroute-howto-circuit-arm.md) e ter o circuito Olá habilitado por seu provedor de conectividade antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="c259f-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="c259f-137">Olá circuito de rota expressa deve estar em um estado habilitado e configurado.</span><span class="sxs-lookup"><span data-stu-id="c259f-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="c259f-138">[Criar emparelhamento da Microsoft](expressroute-circuit-peerings.md) se você gerenciar sessões de BGP de saudação diretamente.</span><span class="sxs-lookup"><span data-stu-id="c259f-138">[Create Microsoft peering](expressroute-circuit-peerings.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="c259f-139">Ou então, faça com que seu provedor de conectividade provisione emparelhamento da Microsoft para o circuito.</span><span class="sxs-lookup"><span data-stu-id="c259f-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="c259f-140">Você deve criar e configurar um filtro de rota.</span><span class="sxs-lookup"><span data-stu-id="c259f-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="c259f-141">Identificar Olá serviços tooconsume por meio de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="c259f-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="c259f-142">Identificar Olá lista de valores de comunidade BGP associados aos serviços de saudação</span><span class="sxs-lookup"><span data-stu-id="c259f-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="c259f-143">Criar uma regra tooallow Olá prefixo lista correspondente Olá valores de comunidade do BGP</span><span class="sxs-lookup"><span data-stu-id="c259f-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="c259f-144">Você deve anexar um circuito de rota expressa toohello do filtro de rota hello.</span><span class="sxs-lookup"><span data-stu-id="c259f-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c259f-145">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c259f-145">Before you begin</span></span>

<span data-ttu-id="c259f-146">Antes de começar a configuração, verifique se que você atende Olá critérios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c259f-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="c259f-147">Instale a versão mais recente Olá de saudação cmdlets do PowerShell do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c259f-147">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="c259f-148">Para obter mais informações, consulte [Instalar e configurar o Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c259f-148">For more information, see [Install and configure Azure PowerShelll](/powershell/azure/install-azurerm-ps).</span></span>

  > [!NOTE]
  > <span data-ttu-id="c259f-149">Baixe versão mais recente da saudação da Galeria do PowerShell hello, em vez de usar o hello instalador.</span><span class="sxs-lookup"><span data-stu-id="c259f-149">Download hello latest version from hello PowerShell Gallery, rather than using hello Installer.</span></span> <span data-ttu-id="c259f-150">Olá instalador no momento não oferece suporte a cmdlets Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="c259f-150">hello Installer currently does not support hello required cmdlets.</span></span>
  > 

 - <span data-ttu-id="c259f-151">Saudação de revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="c259f-151">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="c259f-152">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="c259f-152">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="c259f-153">Siga as instruções de saudação muito[criar um circuito de rota expressa](expressroute-howto-circuit-arm.md) e ter o circuito Olá habilitado por seu provedor de conectividade antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="c259f-153">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="c259f-154">Olá circuito de rota expressa deve estar em um estado habilitado e configurado.</span><span class="sxs-lookup"><span data-stu-id="c259f-154">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="c259f-155">Você deve ter um emparelhamento da Microsoft ativo.</span><span class="sxs-lookup"><span data-stu-id="c259f-155">You must have an active Microsoft peering.</span></span> <span data-ttu-id="c259f-156">Siga as instruções em [Criar e modificar a configuração de emparelhamento](expressroute-circuit-peerings.md)</span><span class="sxs-lookup"><span data-stu-id="c259f-156">Follow instructions at [Create and modifying peering configuration](expressroute-circuit-peerings.md)</span></span>

### <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="c259f-157">Faça logon no tooyour conta do Azure</span><span class="sxs-lookup"><span data-stu-id="c259f-157">Log in tooyour Azure account</span></span>

<span data-ttu-id="c259f-158">Antes de começar essa configuração, você deve fazer logon no tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c259f-158">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="c259f-159">Olá cmdlet solicita as credenciais de logon de saudação para sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c259f-159">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="c259f-160">Após o logon, ele baixa as configurações de conta para que eles fiquem disponível tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c259f-160">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="c259f-161">Abra o console do PowerShell com privilégios elevados e conectar-se a conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="c259f-161">Open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="c259f-162">Use Olá toohelp de exemplo que você se conectar a seguir:</span><span class="sxs-lookup"><span data-stu-id="c259f-162">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="c259f-163">Se você tiver várias assinaturas do Azure, verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="c259f-163">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="c259f-164">Especifique que você deseja toouse de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="c259f-164">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="c259f-165"><a name="prefixes"></a>Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="c259f-165"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="c259f-166">Obter uma lista de prefixos e valores de comunidade BGP</span><span class="sxs-lookup"><span data-stu-id="c259f-166">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="c259f-167">1. Obter uma lista de valores de comunidade BGP</span><span class="sxs-lookup"><span data-stu-id="c259f-167">1. Get a list of BGP community values</span></span>

<span data-ttu-id="c259f-168">Use Olá lista de saudação do cmdlet tooget de BGP comunidade valores associados aos serviços acessíveis por meio de emparelhamento da Microsoft a seguir e Olá lista de prefixos associados a eles:</span><span class="sxs-lookup"><span data-stu-id="c259f-168">Use hello following cmdlet tooget hello list of BGP community values associated with services accessible through Microsoft peering, and hello list of prefixes associated with them:</span></span>

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="c259f-169">2. Faça uma lista de valores de saudação que você deseja toouse</span><span class="sxs-lookup"><span data-stu-id="c259f-169">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="c259f-170">Faça uma lista de valores de comunidade BGP, que você deseja toouse no filtro de rota hello.</span><span class="sxs-lookup"><span data-stu-id="c259f-170">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="c259f-171">Por exemplo, Olá valor de comunidade BGP para serviços do Dynamics 365 é 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="c259f-171">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="c259f-172"><a name="filter"></a>Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="c259f-172"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="c259f-173">Criar um filtro de rota e uma regra de filtro</span><span class="sxs-lookup"><span data-stu-id="c259f-173">Create a route filter and a filter rule</span></span>

<span data-ttu-id="c259f-174">Um filtro de rota pode ter apenas uma regra e regra Olá deve ser do tipo 'Permitir'.</span><span class="sxs-lookup"><span data-stu-id="c259f-174">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="c259f-175">Essa regra pode ter uma lista de valores de comunidade BGP associados a ela.</span><span class="sxs-lookup"><span data-stu-id="c259f-175">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="c259f-176">1. Criar um filtro de rota</span><span class="sxs-lookup"><span data-stu-id="c259f-176">1. Create a route filter</span></span>

<span data-ttu-id="c259f-177">Primeiro, crie o filtro de rota hello.</span><span class="sxs-lookup"><span data-stu-id="c259f-177">First, create hello route filter.</span></span> <span data-ttu-id="c259f-178">comando Olá 'New-AzureRmRouteFilter' só cria um recurso de filtro de rota.</span><span class="sxs-lookup"><span data-stu-id="c259f-178">hello command 'New-AzureRmRouteFilter' only creates a route filter resource.</span></span> <span data-ttu-id="c259f-179">Depois de criar o recurso de hello, você deve criar uma regra e anexá-lo toohello objeto de filtro de rota.</span><span class="sxs-lookup"><span data-stu-id="c259f-179">After you create hello resource, you must then create a rule and attach it toohello route filter object.</span></span> <span data-ttu-id="c259f-180">Execute um recurso de filtro de rota de Olá toocreate de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c259f-180">Run hello following command toocreate a route filter resource:</span></span>

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="c259f-181">2. Criar uma regra de filtro</span><span class="sxs-lookup"><span data-stu-id="c259f-181">2. Create a filter rule</span></span>

<span data-ttu-id="c259f-182">Você pode especificar um conjunto de comunidades BGP como uma lista separada por vírgulas, como mostrado no exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="c259f-182">You can specify a set of BGP communities as a comma-separated list, as shown in hello example.</span></span> <span data-ttu-id="c259f-183">Execute uma nova regra de Olá toocreate de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c259f-183">Run hello following command toocreate a new rule:</span></span>
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a><span data-ttu-id="c259f-184">3. Adicionar filtro de rota Olá regra toohello</span><span class="sxs-lookup"><span data-stu-id="c259f-184">3. Add hello rule toohello route filter</span></span>

<span data-ttu-id="c259f-185">Execute Olá filtro de roteamento do comando tooadd Olá filtro regra toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="c259f-185">Run hello following command tooadd hello filter rule toohello route filter:</span></span>
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="c259f-186"><a name="attach"></a>Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="c259f-186"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="c259f-187">Anexar o circuito de rota expressa tooan do filtro de rota Olá</span><span class="sxs-lookup"><span data-stu-id="c259f-187">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="c259f-188">Execute Olá comando tooattach Olá rota filtro toohello circuito de rota expressa, supondo que você tem apenas emparelhamento da Microsoft a seguir:</span><span class="sxs-lookup"><span data-stu-id="c259f-188">Run hello following command tooattach hello route filter toohello ExpressRoute circuit, assuming you have only Microsoft peering:</span></span>

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="c259f-189"><a name="getproperties"></a>Propriedades de saudação tooget de um filtro de rota</span><span class="sxs-lookup"><span data-stu-id="c259f-189"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="c259f-190">Propriedades de saudação tooget de um filtro de rota, Olá use as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c259f-190">tooget hello properties of a route filter, use hello following steps:</span></span>

1. <span data-ttu-id="c259f-191">Execute Olá recurso de filtro de rota do comando tooget Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c259f-191">Run hello following command tooget hello route filter resource:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. <span data-ttu-id="c259f-192">Obter regras de filtro de rota Olá para o recurso de filtro de rota Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c259f-192">Get hello route filter rules for hello route-filter resource by running hello following command:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <span data-ttu-id="c259f-193"><a name="updateproperties"></a>Propriedades de saudação tooupdate de um filtro de rota</span><span class="sxs-lookup"><span data-stu-id="c259f-193"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="c259f-194">Se o filtro de rota Olá já está anexado tooa circuito, lista de comunidade BGP atualizações toohello automaticamente propaga as alterações de anúncio de prefixo apropriado por meio de sessões BGP Olá estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c259f-194">If hello route filter is already attached tooa circuit, updates toohello BGP community list automatically propagates appropriate prefix advertisement changes through hello established BGP sessions.</span></span> <span data-ttu-id="c259f-195">Você pode atualizar a lista de comunidade BGP de saudação do seu filtro de rota usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c259f-195">You can update hello BGP community list of your route filter using hello following command:</span></span>

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="c259f-196"><a name="detach"></a>toodetach um filtro de roteamento de um circuito de rota expressa</span><span class="sxs-lookup"><span data-stu-id="c259f-196"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="c259f-197">Depois que um filtro de rota é separado da saudação circuito de rota expressa, sem prefixos são anunciados por meio da sessão BGP de saudação.</span><span class="sxs-lookup"><span data-stu-id="c259f-197">Once a route filter is detached from hello ExpressRoute circuit, no prefixes are advertised through hello BGP session.</span></span> <span data-ttu-id="c259f-198">Você pode desanexar um filtro de roteamento de um circuito de rota expressa usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c259f-198">You can detach a route filter from an ExpressRoute circuit using hello following command:</span></span>
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="c259f-199"><a name="delete"></a>toodelete um filtro de rota</span><span class="sxs-lookup"><span data-stu-id="c259f-199"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="c259f-200">Você só pode excluir um filtro de rota se não for anexado tooany circuito.</span><span class="sxs-lookup"><span data-stu-id="c259f-200">You can only delete a route filter if it is not attached tooany circuit.</span></span> <span data-ttu-id="c259f-201">Certifique-se de que esse filtro de rota Olá não está anexado tooany circuito antes de tentar toodelete-lo.</span><span class="sxs-lookup"><span data-stu-id="c259f-201">Ensure that hello route filter is not attached tooany circuit before attempting toodelete it.</span></span> <span data-ttu-id="c259f-202">Você pode excluir um filtro de rota usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c259f-202">You can delete a route filter using hello following command:</span></span>

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="c259f-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c259f-203">Next steps</span></span>

<span data-ttu-id="c259f-204">Para obter mais informações sobre a rota expressa, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="c259f-204">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
