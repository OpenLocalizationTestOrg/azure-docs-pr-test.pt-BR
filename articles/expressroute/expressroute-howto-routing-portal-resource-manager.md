---
title: 'Como tooconfigure roteamento (emparelhamento) para um circuito de rota expressa: Gerenciador de recursos: Azure | Microsoft Docs'
description: "Este artigo o orienta pelas etapas de saudação para criar e provisionar Olá privado, público e emparelhamento da Microsoft de um circuito de rota expressa. Este artigo também mostra como status de saudação toocheck, atualizar ou excluir emparelhamentos para o seu circuito."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="fe742-104">Criar e modificar o emparelhamento de um circuito de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fe742-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="fe742-105">Este artigo ajuda você a criar e gerenciar a configuração de roteamento para um circuito de rota expressa no modelo de implantação do Gerenciador de recursos do hello usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe742-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using hello Azure portal.</span></span> <span data-ttu-id="fe742-106">Você também pode verificar status hello, update ou delete e desprovisionar emparelhamentos de um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="fe742-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="fe742-107">Se você quiser toouse toowork um método diferente com o circuito, selecione um artigo de saudação lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="fe742-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="fe742-108">Pré-requisitos de configuração</span><span class="sxs-lookup"><span data-stu-id="fe742-108">Configuration prerequisites</span></span>

* <span data-ttu-id="fe742-109">Certifique-se de ter revisado Olá [pré-requisitos](expressroute-prerequisites.md) página hello [requisitos de roteamento](expressroute-routing.md) página e hello [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração de página.</span><span class="sxs-lookup"><span data-stu-id="fe742-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="fe742-110">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="fe742-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="fe742-111">Siga as instruções de saudação muito[criar um circuito de rota expressa](expressroute-howto-circuit-portal-resource-manager.md) e ter o circuito Olá habilitado por seu provedor de conectividade antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="fe742-111">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="fe742-112">Olá circuito de rota expressa deve ser em um estado habilitado e configurado para você toobe toorun capaz de saudação cmdlets nas seções próximas hello.</span><span class="sxs-lookup"><span data-stu-id="fe742-112">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in hello next sections.</span></span>
* <span data-ttu-id="fe742-113">Se você planeja toouse um hash MD5/chave compartilhado, ser toouse-se de que isso em ambos os lados da saudação túnel e limite Olá o número de máximo de tooa de caracteres de 25.</span><span class="sxs-lookup"><span data-stu-id="fe742-113">If you plan toouse a shared key/MD5 hash, be sure toouse this on both sides of hello tunnel and limit hello number of characters tooa maximum of 25.</span></span>

<span data-ttu-id="fe742-114">Essas instruções se aplicam somente a toocircuits criado com provedores de serviço oferece serviços de conectividade de camada 2.</span><span class="sxs-lookup"><span data-stu-id="fe742-114">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="fe742-115">Se você estiver usando um provedor de serviços que ofereça serviços gerenciados de Camada 3 (normalmente um IPVPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.</span><span class="sxs-lookup"><span data-stu-id="fe742-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="fe742-116">Estamos atualmente não anuncie emparelhamentos configurados pelos provedores de serviço por meio do portal de gerenciamento de serviços de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe742-116">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="fe742-117">Estamos trabalhando para habilitar esse recurso em breve.</span><span class="sxs-lookup"><span data-stu-id="fe742-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="fe742-118">Verifique com seu provedor de serviços antes de configurar os emparelhamentos via protocolo BGP.</span><span class="sxs-lookup"><span data-stu-id="fe742-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="fe742-119">Você pode configurar um, dois ou todos os três emparelhamentos (privado e público do Azure e da Microsoft) para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fe742-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="fe742-120">Você pode configurar emparelhamentos em qualquer ordem escolhida.</span><span class="sxs-lookup"><span data-stu-id="fe742-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="fe742-121">No entanto, você deve garantir que você conclua a configuração de saudação de cada um emparelhamento de cada vez.</span><span class="sxs-lookup"><span data-stu-id="fe742-121">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="fe742-122">Emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="fe742-122">Azure private peering</span></span>

<span data-ttu-id="fe742-123">Esta seção ajuda você a criar, obter, atualizar e excluir Olá configuração emparelhamento particular do Azure para um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="fe742-123">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="fe742-124">toocreate emparelhamento particular do Azure</span><span class="sxs-lookup"><span data-stu-id="fe742-124">toocreate Azure private peering</span></span>

1. <span data-ttu-id="fe742-125">Configure o circuito de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="fe742-125">Configure hello ExpressRoute circuit.</span></span> <span data-ttu-id="fe742-126">Certifique-se de que o circuito de saudação está totalmente provisionado pelo provedor de conectividade de saudação antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="fe742-126">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing.</span></span>

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="fe742-128">Configure o emparelhamento particular do Azure para o circuito de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe742-128">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="fe742-129">Certifique-se de que você tenha Olá itens a seguir antes de prosseguir com as próximas etapas hello:</span><span class="sxs-lookup"><span data-stu-id="fe742-129">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="fe742-130">Um /30 sub-rede para o link primário hello.</span><span class="sxs-lookup"><span data-stu-id="fe742-130">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="fe742-131">subrede Olá não deve fazer parte de qualquer espaço de endereço reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="fe742-131">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="fe742-132">Um /30 sub-rede para o link secundário hello.</span><span class="sxs-lookup"><span data-stu-id="fe742-132">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="fe742-133">subrede Olá não deve fazer parte de qualquer espaço de endereço reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="fe742-133">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="fe742-134">Um tooestablish de ID de VLAN válida esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="fe742-134">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="fe742-135">Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="fe742-135">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="fe742-136">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="fe742-136">AS number for peering.</span></span> <span data-ttu-id="fe742-137">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="fe742-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="fe742-138">Você pode usar um número de AS privado para esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="fe742-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="fe742-139">Não use 65515.</span><span class="sxs-lookup"><span data-stu-id="fe742-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="fe742-140">**Opcional -** um hash MD5 se você escolher toouse um.</span><span class="sxs-lookup"><span data-stu-id="fe742-140">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="fe742-141">Selecione a linha hello de emparelhamento particular do Azure, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="fe742-141">Select hello Azure Private peering row, as shown in hello following example:</span></span>

  ![privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="fe742-143">Configure o emparelhamento privado.</span><span class="sxs-lookup"><span data-stu-id="fe742-143">Configure private peering.</span></span> <span data-ttu-id="fe742-144">Olá a imagem a seguir mostra um exemplo de configuração:</span><span class="sxs-lookup"><span data-stu-id="fe742-144">hello following image shows a configuration example:</span></span>

  ![configurar o emparelhamento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="fe742-146">Salve configuração Olá depois que você especificou todos os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="fe742-146">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="fe742-147">Após a configuração de saudação foi aceita com êxito, você verá algo semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="fe742-147">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![salvar emparelhamento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="fe742-149">tooview privado emparelhamento detalhes do Azure</span><span class="sxs-lookup"><span data-stu-id="fe742-149">tooview Azure private peering details</span></span>

<span data-ttu-id="fe742-150">Você pode exibir as propriedades de saudação do emparelhamento particular do Azure, selecionando o emparelhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe742-150">You can view hello properties of Azure private peering by selecting hello peering.</span></span>

![exibir emparelhamento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="fe742-152">tooupdate configuração emparelhamento particular do Azure</span><span class="sxs-lookup"><span data-stu-id="fe742-152">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="fe742-153">Você pode selecionar a linha hello para emparelhamento e modificar propriedades de emparelhamento hello.</span><span class="sxs-lookup"><span data-stu-id="fe742-153">You can select hello row for peering and modify hello peering properties.</span></span>

![atualizar emparelhamento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="fe742-155">toodelete emparelhamento particular do Azure</span><span class="sxs-lookup"><span data-stu-id="fe742-155">toodelete Azure private peering</span></span>

<span data-ttu-id="fe742-156">Você pode remover a configuração do emparelhamento selecionando o ícone de excluir hello, conforme mostrado no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="fe742-156">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![excluir emparelhamento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="fe742-158">Emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="fe742-158">Azure public peering</span></span>

<span data-ttu-id="fe742-159">Esta seção ajuda você a criar, obter, atualizar e excluir Olá a configuração de emparelhamento pública do Azure para um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="fe742-159">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="fe742-160">toocreate emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="fe742-160">toocreate Azure public peering</span></span>

1. <span data-ttu-id="fe742-161">Configure o circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fe742-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="fe742-162">Certifique-se de que o circuito de saudação está totalmente provisionado pelo provedor de conectividade de saudação antes de continuar ainda mais.</span><span class="sxs-lookup"><span data-stu-id="fe742-162">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![listar emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="fe742-164">Configure o emparelhamento público do Azure para o circuito de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe742-164">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="fe742-165">Certifique-se de que você tenha Olá itens a seguir antes de prosseguir com as próximas etapas hello:</span><span class="sxs-lookup"><span data-stu-id="fe742-165">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="fe742-166">Um /30 sub-rede para o link primário hello.</span><span class="sxs-lookup"><span data-stu-id="fe742-166">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="fe742-167">Precisa ser um prefixo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="fe742-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="fe742-168">Um /30 sub-rede para o link secundário hello.</span><span class="sxs-lookup"><span data-stu-id="fe742-168">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="fe742-169">Precisa ser um prefixo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="fe742-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="fe742-170">Um tooestablish de ID de VLAN válida esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="fe742-170">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="fe742-171">Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="fe742-171">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="fe742-172">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="fe742-172">AS number for peering.</span></span> <span data-ttu-id="fe742-173">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="fe742-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="fe742-174">**Opcional -** um hash MD5 se você escolher toouse um.</span><span class="sxs-lookup"><span data-stu-id="fe742-174">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="fe742-175">Selecione Olá linha emparelhamento pública do Azure, conforme mostrado na Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="fe742-175">Select hello Azure public peering row, as shown in hello following image:</span></span>

  ![selecionar linha de emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="fe742-177">Configure o emparelhamento público.</span><span class="sxs-lookup"><span data-stu-id="fe742-177">Configure public peering.</span></span> <span data-ttu-id="fe742-178">Olá a imagem a seguir mostra um exemplo de configuração:</span><span class="sxs-lookup"><span data-stu-id="fe742-178">hello following image shows a configuration example:</span></span>

  ![Configurar o emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="fe742-180">Salve configuração Olá depois que você especificou todos os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="fe742-180">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="fe742-181">Após a configuração de saudação foi aceita com êxito, você verá algo semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="fe742-181">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![Salvar a configuração do emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="fe742-183">tooview público emparelhamento detalhes do Azure</span><span class="sxs-lookup"><span data-stu-id="fe742-183">tooview Azure public peering details</span></span>

<span data-ttu-id="fe742-184">Você pode exibir as propriedades de saudação do emparelhamento público do Azure, selecionando o emparelhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe742-184">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![exibir propriedades do emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="fe742-186">tooupdate configuração de emparelhamento pública do Azure</span><span class="sxs-lookup"><span data-stu-id="fe742-186">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="fe742-187">Você pode selecionar a linha hello para emparelhamento e modificar propriedades de emparelhamento hello.</span><span class="sxs-lookup"><span data-stu-id="fe742-187">You can select hello row for peering and modify hello peering properties.</span></span>

![selecionar linha de emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="fe742-189">toodelete emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="fe742-189">toodelete Azure public peering</span></span>

<span data-ttu-id="fe742-190">Você pode remover a configuração do emparelhamento selecionando o ícone de excluir hello, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="fe742-190">You can remove your peering configuration by selecting hello delete icon, as shown in hello following example:</span></span>

![excluir emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="fe742-192">Emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="fe742-192">Microsoft peering</span></span>

<span data-ttu-id="fe742-193">Esta seção ajuda você a criar, obter, atualizar e excluir a configuração de emparelhamento Microsoft hello por um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="fe742-193">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe742-194">Emparelhamento da Microsoft de circuitos ExpressRoute que foram configurados anterior tooAugust 1, 2017 terá todos os prefixos de serviço anunciados através do emparelhamento da Microsoft hello, mesmo se os filtros de roteamento não estão definidos.</span><span class="sxs-lookup"><span data-stu-id="fe742-194">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="fe742-195">Emparelhamento da Microsoft de circuitos de rota expressa configurados em ou após 1 de agosto de 2017 não terá quaisquer prefixos anunciados até que um filtro de rota é anexado toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="fe742-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="fe742-196">Para obter mais informações, consulte [Configurar um filtro de rota para o emparelhamento da Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fe742-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="fe742-197">toocreate emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="fe742-197">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="fe742-198">Configure o circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fe742-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="fe742-199">Certifique-se de que o circuito de saudação está totalmente provisionado pelo provedor de conectividade de saudação antes de continuar ainda mais.</span><span class="sxs-lookup"><span data-stu-id="fe742-199">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![listar emparelhamento da Microsoft](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="fe742-201">Configure o emparelhamento do circuito de saudação do Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fe742-201">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="fe742-202">Certifique-se de que você tenha Olá seguintes informações antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="fe742-202">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="fe742-203">Um /30 sub-rede para o link primário hello.</span><span class="sxs-lookup"><span data-stu-id="fe742-203">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="fe742-204">Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="fe742-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="fe742-205">Um /30 sub-rede para o link secundário hello.</span><span class="sxs-lookup"><span data-stu-id="fe742-205">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="fe742-206">Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="fe742-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="fe742-207">Um tooestablish de ID de VLAN válida esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="fe742-207">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="fe742-208">Certifique-se de que nenhum outro emparelhamento no circuito de saudação usa Olá a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="fe742-208">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="fe742-209">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="fe742-209">AS number for peering.</span></span> <span data-ttu-id="fe742-210">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="fe742-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="fe742-211">Anunciado prefixos: você deve fornecer uma lista de todos os prefixos planejar tooadvertise sobre a sessão BGP de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe742-211">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="fe742-212">Somente prefixos de endereços IP públicos são aceitos.</span><span class="sxs-lookup"><span data-stu-id="fe742-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="fe742-213">Se você planejar toosend um conjunto de prefixos, você pode enviar uma lista separada por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="fe742-213">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="fe742-214">Esses prefixos devem ser registrado tooyou em um RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="fe742-214">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="fe742-215">**Opcional -** cliente ASN: se você estiver prefixos de anúncios que não são registrado toohello emparelhamento como número, você pode especificar hello como número toowhich, eles são registrados.</span><span class="sxs-lookup"><span data-stu-id="fe742-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="fe742-216">Nome de roteamento do registro: Você pode especificar Olá RIR / IRR no qual hello como número e prefixos estão registrados.</span><span class="sxs-lookup"><span data-stu-id="fe742-216">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="fe742-217">**Opcional -** um hash MD5 se você escolher toouse um.</span><span class="sxs-lookup"><span data-stu-id="fe742-217">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="fe742-218">Você pode selecionar Olá emparelhamento desejar tooconfigure, conforme mostrado no Olá a seguir exemplo.</span><span class="sxs-lookup"><span data-stu-id="fe742-218">You can select hello peering you wish tooconfigure, as shown in hello following example.</span></span> <span data-ttu-id="fe742-219">Selecione a linha de emparelhamento de Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="fe742-219">Select hello Microsoft peering row.</span></span>

  ![selecionar linha de emparelhamento da Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="fe742-221">Configure o emparelhamento da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fe742-221">Configure Microsoft peering.</span></span> <span data-ttu-id="fe742-222">Olá a imagem a seguir mostra um exemplo de configuração:</span><span class="sxs-lookup"><span data-stu-id="fe742-222">hello following image shows a configuration example:</span></span>

  ![configurar emparelhamento da Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="fe742-224">Salve configuração Olá depois que você especificou todos os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="fe742-224">Save hello configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="fe742-225">Se o seu circuito obtém tooa 'Validação necessária' estado (conforme mostrado na imagem Olá), você deve abrir um tooshow de tíquete de suporte prova de propriedade da equipe de suporte de tooour Olá prefixos.</span><span class="sxs-lookup"><span data-stu-id="fe742-225">If your circuit gets tooa 'Validation needed' state (as shown in hello image), you must open a support ticket tooshow proof of ownership of hello prefixes tooour support team.</span></span>

  ![Salvar a configuração de emparelhamento da Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="fe742-227">Você pode abrir um tíquete de suporte diretamente do portal hello, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="fe742-227">You can open a support ticket directly from hello portal, as shown in hello following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="fe742-228">Após a configuração de saudação foi aceita com êxito, você verá algo semelhante toohello imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="fe742-228">After hello configuration has been accepted successfully, you see something similar toohello following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="fe742-229">tooview detalhes de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="fe742-229">tooview Microsoft peering details</span></span>

<span data-ttu-id="fe742-230">Você pode exibir as propriedades de saudação do emparelhamento público do Azure, selecionando o emparelhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe742-230">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="fe742-231">tooupdate configuração de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="fe742-231">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="fe742-232">Você pode selecionar a linha hello para emparelhamento e modificar propriedades de emparelhamento hello.</span><span class="sxs-lookup"><span data-stu-id="fe742-232">You can select hello row for peering and modify hello peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="fe742-233">toodelete emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="fe742-233">toodelete Microsoft peering</span></span>

<span data-ttu-id="fe742-234">Você pode remover a configuração do emparelhamento selecionando o ícone de excluir hello, conforme mostrado no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="fe742-234">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="fe742-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fe742-235">Next steps</span></span>

<span data-ttu-id="fe742-236">Próxima etapa, [vincular um circuito de rota expressa do tooan de rede virtual](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="fe742-236">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="fe742-237">Para saber mais sobre fluxos de trabalho do ExpressRoute, confira [Fluxos de trabalho do ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="fe742-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="fe742-238">Para obter mais informações sobre o emparelhamento de circuito, veja [Circuitos e domínios de roteamento do ExpressRoute](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="fe742-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="fe742-239">Para saber mais sobre redes virtuais, confira [Visão geral da rede virtual](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe742-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
