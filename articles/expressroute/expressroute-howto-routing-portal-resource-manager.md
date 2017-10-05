---
title: 'Como configurar o roteamento (emparelhamento) para um circuito do ExpressRoute: Resource Manager: Azure | Microsoft Docs'
description: "Este artigo fornece uma orientação sobre as etapas de criação e de provisionamento do emparelhamento público, privado e da Microsoft de um circuito do ExpressRoute. Este artigo também mostra como verificar o status, atualizar ou excluir emparelhamentos de seu circuito."
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
ms.openlocfilehash: 55ccadfea55b8098ee58dcaef942f6ba54093665
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="c18cd-104">Criar e modificar o emparelhamento de um circuito de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c18cd-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="c18cd-105">Esse artigo ajuda você a criar e gerenciar a configuração de roteamento de um circuito do ExpressRoute no modelo de implantação do Resource Manager, usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c18cd-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using the Azure portal.</span></span> <span data-ttu-id="c18cd-106">Você também pode verificar o status, atualizar ou excluir e desprovisionar emparelhamentos de um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c18cd-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="c18cd-107">Se quiser usar um método diferente para trabalhar com seu circuito, selecione um artigo na lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="c18cd-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="c18cd-108">Pré-requisitos de configuração</span><span class="sxs-lookup"><span data-stu-id="c18cd-108">Configuration prerequisites</span></span>

* <span data-ttu-id="c18cd-109">Verifique se você leu a página de [pré-requisitos](expressroute-prerequisites.md), a página de [requisitos do roteamento](expressroute-routing.md) e a página [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="c18cd-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="c18cd-110">Você deve ter um circuito do ExpressRoute ativo.</span><span class="sxs-lookup"><span data-stu-id="c18cd-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="c18cd-111">Antes de continuar, siga as instruções para [criar um circuito do ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e para que o circuito seja habilitado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="c18cd-111">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="c18cd-112">O circuito do ExpressRoute deve estar em um estado provisionado e habilitado para que você possa executar os cmdlets das próximas seções.</span><span class="sxs-lookup"><span data-stu-id="c18cd-112">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in the next sections.</span></span>
* <span data-ttu-id="c18cd-113">Se você planeja usar uma chave compartilhada/hash MD5, use-os em ambos os lados do túnel e limite o número de caracteres a 25, no máximo.</span><span class="sxs-lookup"><span data-stu-id="c18cd-113">If you plan to use a shared key/MD5 hash, be sure to use this on both sides of the tunnel and limit the number of characters to a maximum of 25.</span></span>

<span data-ttu-id="c18cd-114">Estas instruções se aplicam apenas a circuitos criados com provedores de serviço que oferecem serviços de conectividade de Camada 2.</span><span class="sxs-lookup"><span data-stu-id="c18cd-114">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="c18cd-115">Se você estiver usando um provedor de serviços que ofereça serviços gerenciados de Camada 3 (normalmente um IPVPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.</span><span class="sxs-lookup"><span data-stu-id="c18cd-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c18cd-116">Atualmente, não anunciamos emparelhamentos configurados pelos provedores de serviço por meio do portal de gerenciamento de serviço.</span><span class="sxs-lookup"><span data-stu-id="c18cd-116">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="c18cd-117">Estamos trabalhando para habilitar esse recurso em breve.</span><span class="sxs-lookup"><span data-stu-id="c18cd-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="c18cd-118">Verifique com seu provedor de serviços antes de configurar os emparelhamentos via protocolo BGP.</span><span class="sxs-lookup"><span data-stu-id="c18cd-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="c18cd-119">Você pode configurar um, dois ou todos os três emparelhamentos (privado e público do Azure e da Microsoft) para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c18cd-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="c18cd-120">Você pode configurar emparelhamentos em qualquer ordem escolhida.</span><span class="sxs-lookup"><span data-stu-id="c18cd-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="c18cd-121">No entanto, você deve concluir a configuração de um emparelhamento por vez.</span><span class="sxs-lookup"><span data-stu-id="c18cd-121">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="c18cd-122">Emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="c18cd-122">Azure private peering</span></span>

<span data-ttu-id="c18cd-123">Esta seção ajuda você a criar, obter, atualizar e excluir a configuração de emparelhamento privado do Azure para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c18cd-123">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="c18cd-124">Criar um emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="c18cd-124">To create Azure private peering</span></span>

1. <span data-ttu-id="c18cd-125">Configure o circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c18cd-125">Configure the ExpressRoute circuit.</span></span> <span data-ttu-id="c18cd-126">Verifique se o circuito foi totalmente provisionado pelo provedor de conectividade antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="c18cd-126">Ensure that the circuit is fully provisioned by the connectivity provider before continuing.</span></span>

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="c18cd-128">Configure o emparelhamento privado do Azure para o circuito.</span><span class="sxs-lookup"><span data-stu-id="c18cd-128">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="c18cd-129">Verifique se você tem os seguintes itens antes de continuar com as próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="c18cd-129">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="c18cd-130">Uma sub-rede /30 para o link principal.</span><span class="sxs-lookup"><span data-stu-id="c18cd-130">A /30 subnet for the primary link.</span></span> <span data-ttu-id="c18cd-131">A sub-rede não deve fazer parte de nenhum espaço de endereçamento reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="c18cd-131">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="c18cd-132">Uma sub-rede /30 para o link secundário.</span><span class="sxs-lookup"><span data-stu-id="c18cd-132">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="c18cd-133">A sub-rede não deve fazer parte de nenhum espaço de endereçamento reservado para redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="c18cd-133">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="c18cd-134">Uma ID válida de VLAN para estabelecer esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="c18cd-134">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="c18cd-135">Verifique se nenhum outro emparelhamento no circuito usa a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="c18cd-135">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="c18cd-136">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="c18cd-136">AS number for peering.</span></span> <span data-ttu-id="c18cd-137">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="c18cd-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="c18cd-138">Você pode usar um número de AS privado para esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="c18cd-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="c18cd-139">Não use 65515.</span><span class="sxs-lookup"><span data-stu-id="c18cd-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="c18cd-140">**Opcional –** Um hash MD5 se você optar por usar um.</span><span class="sxs-lookup"><span data-stu-id="c18cd-140">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="c18cd-141">Selecione a linha de emparelhamento privado do Azure, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c18cd-141">Select the Azure Private peering row, as shown in the following example:</span></span>

  ![privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="c18cd-143">Configure o emparelhamento privado.</span><span class="sxs-lookup"><span data-stu-id="c18cd-143">Configure private peering.</span></span> <span data-ttu-id="c18cd-144">A imagem a seguir mostra um exemplo de configuração:</span><span class="sxs-lookup"><span data-stu-id="c18cd-144">The following image shows a configuration example:</span></span>

  ![configurar o emparelhamento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="c18cd-146">Salve a configuração depois que você tiver especificado todos os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="c18cd-146">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="c18cd-147">Depois que a configuração é aceita com êxito, você vê algo semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c18cd-147">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![salvar emparelhamento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="c18cd-149">Para exibir detalhes sobre o emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="c18cd-149">To view Azure private peering details</span></span>

<span data-ttu-id="c18cd-150">Você pode exibir as propriedades de emparelhamento privado do Azure selecionando o emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="c18cd-150">You can view the properties of Azure private peering by selecting the peering.</span></span>

![exibir emparelhamento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="c18cd-152">Atualizar a configuração de emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="c18cd-152">To update Azure private peering configuration</span></span>

<span data-ttu-id="c18cd-153">Você pode selecionar a linha para emparelhamento e modificar as propriedades de emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="c18cd-153">You can select the row for peering and modify the peering properties.</span></span>

![atualizar emparelhamento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="c18cd-155">Excluir um emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="c18cd-155">To delete Azure private peering</span></span>

<span data-ttu-id="c18cd-156">Você pode remover a configuração de emparelhamento selecionando o ícone Excluir, conforme mostrado na imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="c18cd-156">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![excluir emparelhamento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="c18cd-158">Emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="c18cd-158">Azure public peering</span></span>

<span data-ttu-id="c18cd-159">Esta seção ajuda você a criar, obter, atualizar e excluir a configuração de emparelhamento público do Azure para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c18cd-159">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="c18cd-160">Criar o emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="c18cd-160">To create Azure public peering</span></span>

1. <span data-ttu-id="c18cd-161">Configure o circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c18cd-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="c18cd-162">Verifique se o circuito foi totalmente provisionado pelo provedor de conectividade antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="c18cd-162">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![listar emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="c18cd-164">Configure o emparelhamento público do Azure para o circuito.</span><span class="sxs-lookup"><span data-stu-id="c18cd-164">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="c18cd-165">Verifique se você tem os seguintes itens antes de continuar com as próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="c18cd-165">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="c18cd-166">Uma sub-rede /30 para o link principal.</span><span class="sxs-lookup"><span data-stu-id="c18cd-166">A /30 subnet for the primary link.</span></span> <span data-ttu-id="c18cd-167">Precisa ser um prefixo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="c18cd-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="c18cd-168">Uma sub-rede /30 para o link secundário.</span><span class="sxs-lookup"><span data-stu-id="c18cd-168">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="c18cd-169">Precisa ser um prefixo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="c18cd-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="c18cd-170">Uma ID válida de VLAN para estabelecer esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="c18cd-170">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="c18cd-171">Verifique se nenhum outro emparelhamento no circuito usa a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="c18cd-171">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="c18cd-172">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="c18cd-172">AS number for peering.</span></span> <span data-ttu-id="c18cd-173">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="c18cd-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="c18cd-174">**Opcional –** Um hash MD5 se você optar por usar um.</span><span class="sxs-lookup"><span data-stu-id="c18cd-174">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="c18cd-175">Selecione a linha de emparelhamento público do Azure, conforme mostrado na imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="c18cd-175">Select the Azure public peering row, as shown in the following image:</span></span>

  ![selecionar linha de emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="c18cd-177">Configure o emparelhamento público.</span><span class="sxs-lookup"><span data-stu-id="c18cd-177">Configure public peering.</span></span> <span data-ttu-id="c18cd-178">A imagem a seguir mostra um exemplo de configuração:</span><span class="sxs-lookup"><span data-stu-id="c18cd-178">The following image shows a configuration example:</span></span>

  ![Configurar o emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="c18cd-180">Salve a configuração depois que você tiver especificado todos os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="c18cd-180">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="c18cd-181">Depois que a configuração é aceita com êxito, você vê algo semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c18cd-181">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![Salvar a configuração do emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="c18cd-183">Para exibir detalhes sobre o emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="c18cd-183">To view Azure public peering details</span></span>

<span data-ttu-id="c18cd-184">Você pode exibir as propriedades de emparelhamento público do Azure selecionando o emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="c18cd-184">You can view the properties of Azure public peering by selecting the peering.</span></span>

![exibir propriedades do emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="c18cd-186">Atualizar a configuração de emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="c18cd-186">To update Azure public peering configuration</span></span>

<span data-ttu-id="c18cd-187">Você pode selecionar a linha para emparelhamento e modificar as propriedades de emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="c18cd-187">You can select the row for peering and modify the peering properties.</span></span>

![selecionar linha de emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="c18cd-189">Excluir o emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="c18cd-189">To delete Azure public peering</span></span>

<span data-ttu-id="c18cd-190">Você pode remover a configuração de emparelhamento selecionando o ícone Excluir, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c18cd-190">You can remove your peering configuration by selecting the delete icon, as shown in the following example:</span></span>

![excluir emparelhamento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="c18cd-192">Emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="c18cd-192">Microsoft peering</span></span>

<span data-ttu-id="c18cd-193">Esta seção ajuda você a criar, obter, atualizar e excluir a configuração de emparelhamento da Microsoft para um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c18cd-193">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c18cd-194">O emparelhamento da Microsoft de circuitos do ExpressRoute configurados antes de 1º de agosto de 2017 terá todos os prefixos de serviço anunciados através do emparelhamento da Microsoft, mesmo que os filtros de rota não estejam definidos.</span><span class="sxs-lookup"><span data-stu-id="c18cd-194">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="c18cd-195">O emparelhamento da Microsoft de circuitos de ExpressRoute configurados em ou após 1º de agosto de 2017 não terá nenhum prefixo anunciado até que um filtro de rota seja anexado ao circuito.</span><span class="sxs-lookup"><span data-stu-id="c18cd-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="c18cd-196">Para obter mais informações, consulte [Configurar um filtro de rota para o emparelhamento da Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c18cd-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="c18cd-197">Criar emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="c18cd-197">To create Microsoft peering</span></span>

1. <span data-ttu-id="c18cd-198">Configure o circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c18cd-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="c18cd-199">Verifique se o circuito foi totalmente provisionado pelo provedor de conectividade antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="c18cd-199">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![listar emparelhamento da Microsoft](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="c18cd-201">Configurar o emparelhamento da Microsoft para o circuito.</span><span class="sxs-lookup"><span data-stu-id="c18cd-201">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="c18cd-202">Você precisa ter as seguintes informações antes de continuar:</span><span class="sxs-lookup"><span data-stu-id="c18cd-202">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="c18cd-203">Uma sub-rede /30 para o link principal.</span><span class="sxs-lookup"><span data-stu-id="c18cd-203">A /30 subnet for the primary link.</span></span> <span data-ttu-id="c18cd-204">Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="c18cd-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="c18cd-205">Uma sub-rede /30 para o link secundário.</span><span class="sxs-lookup"><span data-stu-id="c18cd-205">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="c18cd-206">Este valor deve ser um prefixo IPv4 público válido próprio e registrado em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="c18cd-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="c18cd-207">Uma ID válida de VLAN para estabelecer esse emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="c18cd-207">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="c18cd-208">Verifique se nenhum outro emparelhamento no circuito usa a mesma ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="c18cd-208">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="c18cd-209">Número de AS para emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="c18cd-209">AS number for peering.</span></span> <span data-ttu-id="c18cd-210">Você pode usar um número de AS de 2 e de 4 bytes.</span><span class="sxs-lookup"><span data-stu-id="c18cd-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="c18cd-211">Prefixos anunciados: forneça uma lista com todos os prefixos que você pretende anunciar na sessão BGP.</span><span class="sxs-lookup"><span data-stu-id="c18cd-211">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="c18cd-212">Somente prefixos de endereços IP públicos são aceitos.</span><span class="sxs-lookup"><span data-stu-id="c18cd-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="c18cd-213">Caso você planeje enviar um conjunto de prefixos, poderá enviar uma lista separada por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="c18cd-213">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="c18cd-214">Esses prefixos devem ser registrados em seu nome em um RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="c18cd-214">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="c18cd-215">**Opcional –** ASN de cliente: se você estiver anunciando prefixos não registrados com o número AS de emparelhamento, especifique o número AS com o qual eles estão registrados.</span><span class="sxs-lookup"><span data-stu-id="c18cd-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="c18cd-216">Nome do registro de roteamento: você pode especificar o RIR/IRR com base no qual o número de AS e os prefixos estão registrados.</span><span class="sxs-lookup"><span data-stu-id="c18cd-216">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="c18cd-217">**Opcional –** Um hash MD5 se você optar por usar um.</span><span class="sxs-lookup"><span data-stu-id="c18cd-217">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="c18cd-218">Você pode selecionar o emparelhamento que deseja configurar, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c18cd-218">You can select the peering you wish to configure, as shown in the following example.</span></span> <span data-ttu-id="c18cd-219">Selecione a linha de emparelhamento da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c18cd-219">Select the Microsoft peering row.</span></span>

  ![selecionar linha de emparelhamento da Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="c18cd-221">Configure o emparelhamento da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c18cd-221">Configure Microsoft peering.</span></span> <span data-ttu-id="c18cd-222">A imagem a seguir mostra um exemplo de configuração:</span><span class="sxs-lookup"><span data-stu-id="c18cd-222">The following image shows a configuration example:</span></span>

  ![configurar emparelhamento da Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="c18cd-224">Salve a configuração depois que você tiver especificado todos os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="c18cd-224">Save the configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="c18cd-225">Se o circuito for para um estado de "A validação é necessária" (como mostrado na imagem), você deverá abrir um tíquete de suporte para mostrar a prova de propriedade dos prefixos à nossa equipe de suporte.</span><span class="sxs-lookup"><span data-stu-id="c18cd-225">If your circuit gets to a 'Validation needed' state (as shown in the image), you must open a support ticket to show proof of ownership of the prefixes to our support team.</span></span>

  ![Salvar a configuração de emparelhamento da Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="c18cd-227">Você pode abrir um tíquete de suporte diretamente no portal, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c18cd-227">You can open a support ticket directly from the portal, as shown in the following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="c18cd-228">Depois que a configuração é aceita com êxito, você vê algo semelhante à seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="c18cd-228">After the configuration has been accepted successfully, you see something similar to the following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="c18cd-229">Para exibir detalhes de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="c18cd-229">To view Microsoft peering details</span></span>

<span data-ttu-id="c18cd-230">Você pode exibir as propriedades de emparelhamento público do Azure selecionando o emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="c18cd-230">You can view the properties of Azure public peering by selecting the peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="c18cd-231">Atualizar a configuração de emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="c18cd-231">To update Microsoft peering configuration</span></span>

<span data-ttu-id="c18cd-232">Você pode selecionar a linha para emparelhamento e modificar as propriedades de emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="c18cd-232">You can select the row for peering and modify the peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="c18cd-233">Excluir emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="c18cd-233">To delete Microsoft peering</span></span>

<span data-ttu-id="c18cd-234">Você pode remover a configuração de emparelhamento selecionando o ícone Excluir, conforme mostrado na imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="c18cd-234">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="c18cd-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c18cd-235">Next steps</span></span>

<span data-ttu-id="c18cd-236">A próxima etapa será [Vincular uma Rede Virtual a um circuito de ExpressRoute](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="c18cd-236">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="c18cd-237">Para saber mais sobre fluxos de trabalho do ExpressRoute, confira [Fluxos de trabalho do ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="c18cd-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="c18cd-238">Para obter mais informações sobre o emparelhamento de circuito, veja [Circuitos e domínios de roteamento do ExpressRoute](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="c18cd-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="c18cd-239">Para saber mais sobre redes virtuais, confira [Visão geral da rede virtual](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c18cd-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
