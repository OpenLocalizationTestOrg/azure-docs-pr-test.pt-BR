---
title: 'Criar e modificar um circuito ExpressRoute: portal do Azure | Microsoft Docs'
description: Este artigo descreve como criar, provisionar, verificar, atualizar, excluir e desprovisionar um circuito do ExpressRoute.
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
ms.openlocfilehash: e3721cd3c031622788f553e71a6555b844f3f7dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="fa099-103">Criar e modificar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fa099-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fa099-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fa099-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="fa099-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa099-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="fa099-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="fa099-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="fa099-107">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fa099-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="fa099-108">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="fa099-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="fa099-109">Este artigo descreve como criar um circuito da Azure ExpressRoute usando o portal do Azure e o modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fa099-109">This article describes how to create an Azure ExpressRoute circuit by using the Azure portal and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="fa099-110">As etapas a seguir também mostrarão a você como verificar o status do circuito, como atualizá-lo ou como excluí-lo e desprovisioná-lo.</span><span class="sxs-lookup"><span data-stu-id="fa099-110">The following steps also show you how to check the status of the circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="fa099-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="fa099-111">Before you begin</span></span>
* <span data-ttu-id="fa099-112">Examine os [pré-requisitos](expressroute-prerequisites.md) e os [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="fa099-112">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="fa099-113">Verifique se você tem acesso ao [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fa099-113">Ensure that you have access to the [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="fa099-114">Verifique se você tem permissões para criar novos recursos de rede.</span><span class="sxs-lookup"><span data-stu-id="fa099-114">Ensure that you have permissions to create new networking resources.</span></span> <span data-ttu-id="fa099-115">Se você não tiver as permissões corretas, entre em contato com o administrador da conta.</span><span class="sxs-lookup"><span data-stu-id="fa099-115">Contact your account administrator if you do not have the right permissions.</span></span>
* <span data-ttu-id="fa099-116">Você pode [exibir um vídeo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) antes de começar para entender melhor as etapas.</span><span class="sxs-lookup"><span data-stu-id="fa099-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order to better understand the steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="fa099-117">Criar e provisionar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fa099-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-to-the-azure-portal"></a><span data-ttu-id="fa099-118">1. Entrar no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fa099-118">1. Sign in to the Azure portal</span></span>
<span data-ttu-id="fa099-119">Em um navegador, acesse o [Portal do Azure](http://portal.azure.com) e entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa099-119">From a browser, navigate to the [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="fa099-120">2. Criar um novo circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fa099-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fa099-121">O circuito do ExpressRoute será cobrado a partir do momento em que uma chave de serviço for emitida.</span><span class="sxs-lookup"><span data-stu-id="fa099-121">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="fa099-122">Execute esta operação quando o provedor de conectividade estiver pronto para provisionar o circuito.</span><span class="sxs-lookup"><span data-stu-id="fa099-122">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

1. <span data-ttu-id="fa099-123">Você pode criar um circuito do ExpressRoute selecionando a opção de criar um novo recurso.</span><span class="sxs-lookup"><span data-stu-id="fa099-123">You can create an ExpressRoute circuit by selecting the option to create a new resource.</span></span> <span data-ttu-id="fa099-124">Clique em **Novo** > **Rede** > **ExpressRoute**, conforme mostrado na seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="fa099-124">Click **New** > **Networking** > **ExpressRoute**, as shown in the following image:</span></span>
   
    ![Criar um circuito do ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="fa099-126">Após clicar em **ExpressRoute**, você verá a folha **Criar circuito de ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="fa099-126">After you click **ExpressRoute**, you'll see the **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="fa099-127">Ao preencher os valores nessa folha, especifique a camada de SKU e os dados de medição corretos.</span><span class="sxs-lookup"><span data-stu-id="fa099-127">When you're filling in the values on this blade, make sure that you specify the correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="fa099-128">**camada** determina se um complemento padrão ou premium do ExpressRoute está habilitado.</span><span class="sxs-lookup"><span data-stu-id="fa099-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="fa099-129">Você pode especificar **Standard** para obter o SKU padrão ou **Premium** para o complemento premium.</span><span class="sxs-lookup"><span data-stu-id="fa099-129">You can specify **Standard** to get the standard SKU or **Premium** for the premium add-on.</span></span>
   * <span data-ttu-id="fa099-130">**medição de dados** determina o tipo de cobrança.</span><span class="sxs-lookup"><span data-stu-id="fa099-130">**Data metering** determines the billing type.</span></span> <span data-ttu-id="fa099-131">Você pode especificar **Limitado** para um plano de dados limitado e **Ilimitado** para um plano de dados ilimitado.</span><span class="sxs-lookup"><span data-stu-id="fa099-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="fa099-132">Observe que você pode alterar o tipo de cobrança de **Limitado** para **Ilimitado**, mas não pode alterar o tipo de **Ilimitado** para **Limitado**.</span><span class="sxs-lookup"><span data-stu-id="fa099-132">Note that you can change the billing type from **Metered** to **Unlimited**, but you can't change the type from **Unlimited** to **Metered**.</span></span>
     
     ![Configurar a camada da SKU e a medição de dados](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="fa099-134">Esteja ciente de que o Local de Emparelhamento indica o [local físico](expressroute-locations.md) onde você está emparelhamento com a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fa099-134">Please be aware that the Peering Location indicates the [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="fa099-135">Isso **não** tem vínculo à propriedade "Local", que se refere à posição geográfica na qual o Provedor de Recursos de Rede do Azure está localizado.</span><span class="sxs-lookup"><span data-stu-id="fa099-135">This is **not** linked to "Location" property, which refers to the geography where the Azure Network Resource Provider is located.</span></span> <span data-ttu-id="fa099-136">Embora eles não estejam relacionados, é uma boa prática escolher um provedor de recursos de rede geograficamente próximo do Local de Emparelhamento do circuito.</span><span class="sxs-lookup"><span data-stu-id="fa099-136">While they are not related, it is a good practice to choose a Network Resource Provider geographically close to the Peering Location of the circuit.</span></span> 
> 
> 

### <a name="3-view-the-circuits-and-properties"></a><span data-ttu-id="fa099-137">3. Exibir os circuitos e as propriedades</span><span class="sxs-lookup"><span data-stu-id="fa099-137">3. View the circuits and properties</span></span>
<span data-ttu-id="fa099-138">**Exibir todos os circuitos**</span><span class="sxs-lookup"><span data-stu-id="fa099-138">**View all the circuits**</span></span>

<span data-ttu-id="fa099-139">Você pode exibir todos os circuitos que criou selecionando **Todos os recursos** no menu do lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="fa099-139">You can view all the circuits that you created by selecting **All resources** on the left-side menu.</span></span>

![Exibir circuitos](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="fa099-141">**Exibir as propriedades**</span><span class="sxs-lookup"><span data-stu-id="fa099-141">**View the properties**</span></span>

    You can view the properties of the circuit by selecting it. On this blade, note the service key for the circuit. You must copy the circuit key for your circuit and pass it down to the service provider to complete the provisioning process. The circuit key is specific to your circuit.

![Exibir propriedades](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="fa099-143">4. Enviar a chave de serviço ao seu provedor de conectividade para obter provisionamento</span><span class="sxs-lookup"><span data-stu-id="fa099-143">4. Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="fa099-144">Nessa folha, **Status do provedor** fornece informações sobre o estado de provisionamento atual no lado do provedor de serviço.</span><span class="sxs-lookup"><span data-stu-id="fa099-144">On this blade, **Provider status** provides information on the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="fa099-145">**Status de circuito** fornece o estado no lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fa099-145">**Circuit status** provides the state on the Microsoft side.</span></span> <span data-ttu-id="fa099-146">Para saber mais sobre estados de provisionamento do circuito, confira o artigo [Fluxos de trabalho](expressroute-workflows.md#expressroute-circuit-provisioning-states) .</span><span class="sxs-lookup"><span data-stu-id="fa099-146">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="fa099-147">Quando você criar um novo circuito do ExpressRoute, ele estará no seguinte estado:</span><span class="sxs-lookup"><span data-stu-id="fa099-147">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

<span data-ttu-id="fa099-148">Status do provedor: não provisionado</span><span class="sxs-lookup"><span data-stu-id="fa099-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="fa099-149">Status do circuito: habilitado</span><span class="sxs-lookup"><span data-stu-id="fa099-149">Circuit status: Enabled</span></span>

![Iniciar o processo de provisionamento](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="fa099-151">O circuito assumirá o estado a seguir quando o provedor de conectividade estiver no processo de habilitá-lo para você:</span><span class="sxs-lookup"><span data-stu-id="fa099-151">The circuit will change to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

<span data-ttu-id="fa099-152">Status do provedor: provisionando</span><span class="sxs-lookup"><span data-stu-id="fa099-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="fa099-153">Status do circuito: habilitado</span><span class="sxs-lookup"><span data-stu-id="fa099-153">Circuit status: Enabled</span></span>

<span data-ttu-id="fa099-154">Para que você consiga usar um circuito do ExpressRoute, ele deverá estar no seguinte estado:</span><span class="sxs-lookup"><span data-stu-id="fa099-154">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

<span data-ttu-id="fa099-155">Status do provedor: provisionado</span><span class="sxs-lookup"><span data-stu-id="fa099-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="fa099-156">Status do circuito: habilitado</span><span class="sxs-lookup"><span data-stu-id="fa099-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="fa099-157">5. Verifique periodicamente o status e o estado da chave do circuito</span><span class="sxs-lookup"><span data-stu-id="fa099-157">5. Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="fa099-158">Você pode exibir as propriedades do circuito de seu interesse selecionando-o.</span><span class="sxs-lookup"><span data-stu-id="fa099-158">You can view the properties of the circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="fa099-159">Verifique o **Status do provedor** e se ele mudou para **Provisionado** antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="fa099-159">Check the **Provider status** and ensure that it has moved to **Provisioned** before you continue.</span></span>

![Status do circuito e do provedor](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="fa099-161">6. Criar sua configuração de roteamento</span><span class="sxs-lookup"><span data-stu-id="fa099-161">6. Create your routing configuration</span></span>
<span data-ttu-id="fa099-162">Para obter instruções passo a passo, confira o artigo [Configuração do roteamento de circuito do ExpressRoute](expressroute-howto-routing-portal-resource-manager.md) para criar e modificar os emparelhamentos de circuito.</span><span class="sxs-lookup"><span data-stu-id="fa099-162">For step-by-step instructions, refer to the [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa099-163">Estas instruções aplicam-se apenas a circuitos criados com provedores de serviço que oferecem serviços de conectividade de camada 2.</span><span class="sxs-lookup"><span data-stu-id="fa099-163">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="fa099-164">Se você estiver usando um provedor de serviços que oferece serviços gerenciados de camada 3 (normalmente um IP VPN, como MPLS), seu provedor de conectividade configurará e gerenciará o roteamento para você.</span><span class="sxs-lookup"><span data-stu-id="fa099-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="fa099-165">7. Vincular uma rede virtual a um circuito de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fa099-165">7. Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="fa099-166">Em seguida, vincule uma rede virtual a seu circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fa099-166">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="fa099-167">Use o artigo [Vincular redes virtuais a circuitos do ExpressRoute](expressroute-howto-linkvnet-arm.md) ao trabalhar com o modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="fa099-167">Use the [Linking virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with the Resource Manager deployment model.</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="fa099-168">Obtendo o status de um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fa099-168">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="fa099-169">Você pode exibir o status de um circuito selecionando-o.</span><span class="sxs-lookup"><span data-stu-id="fa099-169">You can view the status of a circuit by selecting it.</span></span> 

![Status de um circuito do ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="fa099-171">Modificando um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fa099-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="fa099-172">Você pode modificar certas propriedades de um circuito do ExpressRoute sem afetar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="fa099-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="fa099-173">Você pode fazer o seguinte sem tempo de inatividade:</span><span class="sxs-lookup"><span data-stu-id="fa099-173">You can do the following with no downtime:</span></span>

* <span data-ttu-id="fa099-174">Como habilitar ou desabilitar o complemento premium do ExpressRoute para seu circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fa099-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="fa099-175">Aumente a largura de banda do circuito de ExpressRoute, desde que haja capacidade disponível na porta.</span><span class="sxs-lookup"><span data-stu-id="fa099-175">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="fa099-176">Observe que não há suporte para o downgrade da largura de banda de um circuito.</span><span class="sxs-lookup"><span data-stu-id="fa099-176">Note that downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="fa099-177">Altere o plano de medição de Dados Limitados para Dados Ilimitados.</span><span class="sxs-lookup"><span data-stu-id="fa099-177">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="fa099-178">Observe que a alteração do plano de medição de Dados Ilimitados para Dados Limitados não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="fa099-178">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="fa099-179">Você pode habilitar e desabilitar *Permitir Operações Clássicas*.</span><span class="sxs-lookup"><span data-stu-id="fa099-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="fa099-180">Para saber mais sobre limites e limitações, confira as [Perguntas frequentes sobre o ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="fa099-180">For more information on limits and limitations, refer to the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="fa099-181">Para modificar um circuito do ExpressRoute, clique na **Configuração**, conforme mostrado na figura abaixo.</span><span class="sxs-lookup"><span data-stu-id="fa099-181">To modify an ExpressRoute circuit, click on the **Configuration** as shown in the figure below.</span></span>

![Modificar o circuito](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="fa099-183">É possível modificar a largura de banda, o SKU, o modelo de cobrança e permitir operações clássicas na folha de configuração.</span><span class="sxs-lookup"><span data-stu-id="fa099-183">You can modify the bandwidth, SKU, billing model and allow classic operations within the configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa099-184">Talvez seja necessário recriar o circuito de ExpressRoute se não houver capacidade adequada na porta existente.</span><span class="sxs-lookup"><span data-stu-id="fa099-184">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="fa099-185">Você não pode atualizar o circuito não se houver capacidade adicional disponível nesse local.</span><span class="sxs-lookup"><span data-stu-id="fa099-185">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="fa099-186">Não é possível reduzir a largura de banda de um circuito do ExpressRoute sem interrupções.</span><span class="sxs-lookup"><span data-stu-id="fa099-186">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="fa099-187">O downgrade da largura de banda exige o desprovisionamento do circuito do ExpressRoute e um reprovisionamento de um novo circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fa099-187">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="fa099-188">A desabilitação da operação de complemento premium poderá falhar se você estiver usando recursos que ultrapassam o que é permitido para o circuito padrão.</span><span class="sxs-lookup"><span data-stu-id="fa099-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="fa099-189">Desprovisionamento e exclusão de um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fa099-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="fa099-190">Você pode excluir seu circuito do ExpressRoute selecionando o ícone **Excluir** .</span><span class="sxs-lookup"><span data-stu-id="fa099-190">You can delete your ExpressRoute circuit by selecting the **delete** icon.</span></span> <span data-ttu-id="fa099-191">Observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fa099-191">Note the following:</span></span>

* <span data-ttu-id="fa099-192">Você deve desvincular todas as redes virtuais do circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fa099-192">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="fa099-193">Se essa operação falhar, verifique se há redes virtuais vinculadas ao circuito.</span><span class="sxs-lookup"><span data-stu-id="fa099-193">If this operation fails, check whether any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="fa099-194">Se o estado de provisionamento do provedor de serviço de circuito de ExpressRoute for **Provisionando** ou **Provisionado**, você deverá trabalhar com seu provedor de serviços para que ele desprovisione o circuito.</span><span class="sxs-lookup"><span data-stu-id="fa099-194">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="fa099-195">Continuaremos a reservar recursos e a cobrar de você até que o provedor de serviços complete o desprovisionamento do circuito e nos notifique.</span><span class="sxs-lookup"><span data-stu-id="fa099-195">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="fa099-196">Se o provedor de serviços tiver desprovisionado o circuito (o estado de provisionamento do provedor de serviços estiver definido como **Não provisionado**), exclua o circuito.</span><span class="sxs-lookup"><span data-stu-id="fa099-196">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="fa099-197">Isso interromperá a cobrança do circuito</span><span class="sxs-lookup"><span data-stu-id="fa099-197">This will stop billing for the circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa099-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fa099-198">Next steps</span></span>
<span data-ttu-id="fa099-199">Depois de criar seu circuito, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fa099-199">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="fa099-200">Criar e modificar o roteamento do circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fa099-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="fa099-201">Vincular a rede virtual ao circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fa099-201">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

