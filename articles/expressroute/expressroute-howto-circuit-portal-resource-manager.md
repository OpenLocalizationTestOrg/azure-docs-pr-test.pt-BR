---
title: 'Criar e modificar um circuito ExpressRoute: portal do Azure | Microsoft Docs'
description: Este artigo descreve como toocreate, provisionar, verifique se, atualizar, excluir e cancelar o provisionamento de um circuito de rota expressa.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="43613-103">Criar e modificar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="43613-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="43613-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="43613-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="43613-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="43613-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="43613-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="43613-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="43613-107">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="43613-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="43613-108">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="43613-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="43613-109">Este artigo descreve como toocreate um circuito de rota expressa do Azure usando hello Azure modelo de implantação de Gerenciador de recursos do Azure do portal e hello.</span><span class="sxs-lookup"><span data-stu-id="43613-109">This article describes how toocreate an Azure ExpressRoute circuit by using hello Azure portal and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="43613-110">Olá também etapas a seguir mostra como toocheck Olá status do circuito hello, atualizá-lo, ou excluir e seu provisionamento.</span><span class="sxs-lookup"><span data-stu-id="43613-110">hello following steps also show you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="43613-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="43613-111">Before you begin</span></span>
* <span data-ttu-id="43613-112">Saudação de revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="43613-112">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="43613-113">Verifique se você tem acesso toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="43613-113">Ensure that you have access toohello [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="43613-114">Certifique-se de que você tenha recursos de rede novas permissões toocreate.</span><span class="sxs-lookup"><span data-stu-id="43613-114">Ensure that you have permissions toocreate new networking resources.</span></span> <span data-ttu-id="43613-115">Se você não tem permissões corretas hello, entre em contato com o administrador da conta.</span><span class="sxs-lookup"><span data-stu-id="43613-115">Contact your account administrator if you do not have hello right permissions.</span></span>
* <span data-ttu-id="43613-116">Você pode [exibir um vídeo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) antes de começar em ordem toobetter entender as etapas de saudação.</span><span class="sxs-lookup"><span data-stu-id="43613-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order toobetter understand hello steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="43613-117">Criar e provisionar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="43613-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-toohello-azure-portal"></a><span data-ttu-id="43613-118">1. Entrar toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="43613-118">1. Sign in toohello Azure portal</span></span>
<span data-ttu-id="43613-119">Em um navegador, navegue toohello [portal do Azure](http://portal.azure.com) e entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="43613-119">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="43613-120">2. Criar um novo circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="43613-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="43613-121">O circuito de rota expressa será cobrado do momento Olá que uma chave de serviço é emitida.</span><span class="sxs-lookup"><span data-stu-id="43613-121">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="43613-122">Certifique-se de que você executar esta operação quando o provedor de conectividade de saudação circuito de saudação tooprovision pronto.</span><span class="sxs-lookup"><span data-stu-id="43613-122">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

1. <span data-ttu-id="43613-123">Você pode criar um circuito de rota expressa selecionando Olá opção toocreate um novo recurso.</span><span class="sxs-lookup"><span data-stu-id="43613-123">You can create an ExpressRoute circuit by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="43613-124">Clique em **novo** > **rede** > **ExpressRoute**, conforme mostrado no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="43613-124">Click **New** > **Networking** > **ExpressRoute**, as shown in hello following image:</span></span>
   
    ![Criar um circuito do ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="43613-126">Depois de clicar em **ExpressRoute**, você verá Olá **circuito de rota expressa criar** folha.</span><span class="sxs-lookup"><span data-stu-id="43613-126">After you click **ExpressRoute**, you'll see hello **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="43613-127">Quando você estiver preenchendo valores hello nesta folha, certifique-se de que você especifique a camada SKU correta hello e medição de dados.</span><span class="sxs-lookup"><span data-stu-id="43613-127">When you're filling in hello values on this blade, make sure that you specify hello correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="43613-128">**camada** determina se um complemento padrão ou premium do ExpressRoute está habilitado.</span><span class="sxs-lookup"><span data-stu-id="43613-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="43613-129">Você pode especificar **padrão** tooget Olá SKU standard ou **Premium** para o complemento do premium Olá.</span><span class="sxs-lookup"><span data-stu-id="43613-129">You can specify **Standard** tooget hello standard SKU or **Premium** for hello premium add-on.</span></span>
   * <span data-ttu-id="43613-130">**Dados de medição** determina o tipo de saudação de cobrança.</span><span class="sxs-lookup"><span data-stu-id="43613-130">**Data metering** determines hello billing type.</span></span> <span data-ttu-id="43613-131">Você pode especificar **Limitado** para um plano de dados limitado e **Ilimitado** para um plano de dados ilimitado.</span><span class="sxs-lookup"><span data-stu-id="43613-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="43613-132">Observe que você pode alterar o tipo de cobrança de saudação do **Metered** muito**Unlimited**, mas você não pode alterar o tipo de saudação do **Unlimited** muito**Metered**.</span><span class="sxs-lookup"><span data-stu-id="43613-132">Note that you can change hello billing type from **Metered** too**Unlimited**, but you can't change hello type from **Unlimited** too**Metered**.</span></span>
     
     ![Configurar a camada de SKU hello e medição de dados](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="43613-134">Esteja ciente de que Olá local de emparelhamento indica Olá [local físico](expressroute-locations.md) onde você é emparelhamento com a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="43613-134">Please be aware that hello Peering Location indicates hello [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="43613-135">Isso é **não** vinculado muito propriedade "Local", que se refere a geografia toohello onde se encontra Olá provedor de recursos de rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="43613-135">This is **not** linked too"Location" property, which refers toohello geography where hello Azure Network Resource Provider is located.</span></span> <span data-ttu-id="43613-136">Embora eles não estão relacionados, é toochoose uma boa prática toohello de geograficamente fechar um provedor de recursos de rede local de emparelhamento do circuito hello.</span><span class="sxs-lookup"><span data-stu-id="43613-136">While they are not related, it is a good practice toochoose a Network Resource Provider geographically close toohello Peering Location of hello circuit.</span></span> 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a><span data-ttu-id="43613-137">3. Circuitos de saudação do modo de exibição e propriedades</span><span class="sxs-lookup"><span data-stu-id="43613-137">3. View hello circuits and properties</span></span>
<span data-ttu-id="43613-138">**Exibir todos os circuitos Olá**</span><span class="sxs-lookup"><span data-stu-id="43613-138">**View all hello circuits**</span></span>

<span data-ttu-id="43613-139">Você pode exibir todos os circuitos Olá criado selecionando **todos os recursos** no menu do lado esquerdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="43613-139">You can view all hello circuits that you created by selecting **All resources** on hello left-side menu.</span></span>

![Exibir circuitos](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="43613-141">**Exibir propriedades de saudação**</span><span class="sxs-lookup"><span data-stu-id="43613-141">**View hello properties**</span></span>

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Exibir propriedades](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="43613-143">4. Enviar Olá tooyour chave conectividade provedor para provisionamento</span><span class="sxs-lookup"><span data-stu-id="43613-143">4. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="43613-144">Nesta folha **status do provedor** fornece informações sobre o estado atual de saudação do provisionamento no lado do provedor de serviços de saudação.</span><span class="sxs-lookup"><span data-stu-id="43613-144">On this blade, **Provider status** provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="43613-145">**Status de circuito** informa o estado de saudação em Olá lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="43613-145">**Circuit status** provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="43613-146">Para obter mais informações sobre estados de provisionamento do circuito, consulte Olá [fluxos de trabalho](expressroute-workflows.md#expressroute-circuit-provisioning-states) artigo.</span><span class="sxs-lookup"><span data-stu-id="43613-146">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="43613-147">Quando você cria um novo circuito de rota expressa, circuito Olá estará em Olá estado a seguir:</span><span class="sxs-lookup"><span data-stu-id="43613-147">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

<span data-ttu-id="43613-148">Status do provedor: não provisionado</span><span class="sxs-lookup"><span data-stu-id="43613-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="43613-149">Status do circuito: habilitado</span><span class="sxs-lookup"><span data-stu-id="43613-149">Circuit status: Enabled</span></span>

![Iniciar o processo de provisionamento](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="43613-151">circuito Olá alterará toohello estado a seguir quando o provedor de conectividade Olá está no processo de saudação de habilitá-la para você:</span><span class="sxs-lookup"><span data-stu-id="43613-151">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

<span data-ttu-id="43613-152">Status do provedor: provisionando</span><span class="sxs-lookup"><span data-stu-id="43613-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="43613-153">Status do circuito: habilitado</span><span class="sxs-lookup"><span data-stu-id="43613-153">Circuit status: Enabled</span></span>

<span data-ttu-id="43613-154">Para você toobe capaz de toouse um circuito de rota expressa, ele deve ser Olá estado a seguir:</span><span class="sxs-lookup"><span data-stu-id="43613-154">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

<span data-ttu-id="43613-155">Status do provedor: provisionado</span><span class="sxs-lookup"><span data-stu-id="43613-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="43613-156">Status do circuito: habilitado</span><span class="sxs-lookup"><span data-stu-id="43613-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="43613-157">5. Verifique periodicamente o status de saudação e o estado de saudação da chave de circuito de saudação</span><span class="sxs-lookup"><span data-stu-id="43613-157">5. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="43613-158">Você pode exibir as propriedades de saudação do circuito Olá que você está interessado em selecionando-a.</span><span class="sxs-lookup"><span data-stu-id="43613-158">You can view hello properties of hello circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="43613-159">Verificar Olá **status do provedor** e certifique-se de que ele foi movido muito**provisionado** antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="43613-159">Check hello **Provider status** and ensure that it has moved too**Provisioned** before you continue.</span></span>

![Status do circuito e do provedor](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="43613-161">6. Criar sua configuração de roteamento</span><span class="sxs-lookup"><span data-stu-id="43613-161">6. Create your routing configuration</span></span>
<span data-ttu-id="43613-162">Para obter instruções passo a passo, consulte toohello [configuração de roteamento de circuito de rota expressa](expressroute-howto-routing-portal-resource-manager.md) artigo toocreate e modificar os emparelhamentos de circuito.</span><span class="sxs-lookup"><span data-stu-id="43613-162">For step-by-step instructions, refer toohello [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43613-163">Essas instruções se aplicam somente a toocircuits que são criados com provedores de serviços que oferecem serviços da camada 2 de conectividade.</span><span class="sxs-lookup"><span data-stu-id="43613-163">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="43613-164">Se você estiver usando um provedor de serviços que oferece serviços gerenciados de camada 3 (normalmente um IP VPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.</span><span class="sxs-lookup"><span data-stu-id="43613-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="43613-165">7. Vincular um circuito de rota expressa do tooan de rede virtual</span><span class="sxs-lookup"><span data-stu-id="43613-165">7. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="43613-166">Em seguida, vincule um circuito de rota expressa do tooyour de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="43613-166">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="43613-167">Saudação de uso [vinculação virtual redes circuitos tooExpressRoute](expressroute-howto-linkvnet-arm.md) quando você trabalha com o modelo de implantação do Gerenciador de recursos de saudação do artigo.</span><span class="sxs-lookup"><span data-stu-id="43613-167">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="43613-168">Obter status de saudação de um circuito de rota expressa</span><span class="sxs-lookup"><span data-stu-id="43613-168">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="43613-169">Você pode exibir o status de saudação de um circuito, selecionando-o.</span><span class="sxs-lookup"><span data-stu-id="43613-169">You can view hello status of a circuit by selecting it.</span></span> 

![Status de um circuito do ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="43613-171">Modificando um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="43613-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="43613-172">Você pode modificar certas propriedades de um circuito do ExpressRoute sem afetar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="43613-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="43613-173">Você pode fazer Olá sem tempo de inatividade a seguir:</span><span class="sxs-lookup"><span data-stu-id="43613-173">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="43613-174">Como habilitar ou desabilitar o complemento premium do ExpressRoute para seu circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="43613-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="43613-175">Aumento de largura de banda de saudação do circuito ExpressRoute fornecido há capacidade disponível na porta hello.</span><span class="sxs-lookup"><span data-stu-id="43613-175">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="43613-176">Observe que a largura de banda de saudação de um circuito de downgrade não é suportado.</span><span class="sxs-lookup"><span data-stu-id="43613-176">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="43613-177">Alterar o plano de dados limitados tooUnlimited dados de medição de saudação.</span><span class="sxs-lookup"><span data-stu-id="43613-177">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="43613-178">Observe que esse plano de medição Olá alteração de dados ilimitada tooMetered que dados não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="43613-178">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="43613-179">Você pode habilitar e desabilitar *Permitir Operações Clássicas*.</span><span class="sxs-lookup"><span data-stu-id="43613-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="43613-180">Para obter mais informações sobre limitações e limites, consulte toohello [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="43613-180">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="43613-181">toomodify um circuito de rota expressa, clique em Olá **configuração** conforme mostrado na figura abaixo a saudação.</span><span class="sxs-lookup"><span data-stu-id="43613-181">toomodify an ExpressRoute circuit, click on hello **Configuration** as shown in hello figure below.</span></span>

![Modificar o circuito](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="43613-183">Você pode modificar a largura de banda hello, SKU, modelo de cobrança e permitem operações clássicas dentro de folha de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="43613-183">You can modify hello bandwidth, SKU, billing model and allow classic operations within hello configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43613-184">Você pode ter o circuito de rota expressa Olá toorecreate se não houver capacidade insuficiente na porta existente Olá.</span><span class="sxs-lookup"><span data-stu-id="43613-184">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="43613-185">Não é possível atualizar o circuito de saudação se não houver nenhuma capacidade adicional disponível nesse local.</span><span class="sxs-lookup"><span data-stu-id="43613-185">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="43613-186">Você não pode reduzir a largura de banda de saudação de um circuito de rota expressa sem interrupções.</span><span class="sxs-lookup"><span data-stu-id="43613-186">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="43613-187">Downgrade da largura de banda requer que o circuito de rota expressa Olá toodeprovision e, em seguida, Reprovisionar um novo circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="43613-187">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="43613-188">Desabilitar complemento premium operação pode falhar se você estiver usando recursos que são maiores do que o que é permitido para o circuito de saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="43613-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="43613-189">Desprovisionamento e exclusão de um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="43613-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="43613-190">Você pode excluir o circuito de rota expressa selecionando Olá **excluir** ícone.</span><span class="sxs-lookup"><span data-stu-id="43613-190">You can delete your ExpressRoute circuit by selecting hello **delete** icon.</span></span> <span data-ttu-id="43613-191">Observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="43613-191">Note hello following:</span></span>

* <span data-ttu-id="43613-192">Você deve desvincular todas as redes virtuais da saudação circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="43613-192">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="43613-193">Se essa operação falhar, verifique se as redes virtuais são vinculadas toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="43613-193">If this operation fails, check whether any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="43613-194">Se o provedor de serviços de circuito ExpressRoute Olá estado de provisionamento é **provisionamento** ou **provisionado** você deve trabalhar com o circuito de saudação do serviço provedor toodeprovision em seu lado.</span><span class="sxs-lookup"><span data-stu-id="43613-194">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="43613-195">Vamos continuar tooreserve recursos e cobrar você até que o provedor de serviços Olá Complete desprovisionamento circuito de saudação e nos notifica.</span><span class="sxs-lookup"><span data-stu-id="43613-195">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="43613-196">Se o provedor de serviços de saudação tem desprovisionada circuito hello (provedor de serviços de saudação estado de provisionamento está definido muito**não provisionado**), em seguida, você pode excluir o circuito de saudação.</span><span class="sxs-lookup"><span data-stu-id="43613-196">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="43613-197">Isso interromperá a cobrança para o circuito Olá</span><span class="sxs-lookup"><span data-stu-id="43613-197">This will stop billing for hello circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="43613-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="43613-198">Next steps</span></span>
<span data-ttu-id="43613-199">Depois de criar o circuito, certifique-se de que Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="43613-199">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="43613-200">Criar e modificar o roteamento do circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="43613-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="43613-201">Vincular sua rede virtual de tooyour circuito de rota expressa</span><span class="sxs-lookup"><span data-stu-id="43613-201">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

