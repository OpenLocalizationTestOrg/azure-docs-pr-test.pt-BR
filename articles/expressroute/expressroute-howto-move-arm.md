---
title: "Mova os circuitos de ExpressRoute do clássico para o Resource Manager | Microsoft Docs"
description: "Esta página descreve como mover um circuito clássico para o modelo de implantação do Resource Manager usando o PowerShell."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 08152836-23e7-42d1-9a56-8306b341cd91
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/03/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: c407e01e6d881cb8adcfe55faa246468669be883
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="move-expressroute-circuits-from-the-classic-to-the-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="c1c1a-103">Mover os circuitos de ExpressRoute do modelo de implantação clássico para o do Resource Manager usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1c1a-103">Move ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="c1c1a-104">Para usar um circuito do ExpressRoute para os modelos de implantação clássico e do Resource Manager, você deve mover o circuito para o modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-104">To use an ExpressRoute circuit for both the classic and Resource Manager deployment models, you must move the circuit to the Resource Manager deployment model.</span></span> <span data-ttu-id="c1c1a-105">As seções a seguir lhe ajudarão a mover seu circuito usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-105">The following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c1c1a-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c1c1a-106">Before you begin</span></span>

* <span data-ttu-id="c1c1a-107">Verifique se você tem a versão mais recente dos módulos do Azure PowerShell (pelo menos a versão 1.0).</span><span class="sxs-lookup"><span data-stu-id="c1c1a-107">Verify that you have the latest version of the Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="c1c1a-108">Para saber mais, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="c1c1a-108">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="c1c1a-109">Certifique-se de que você leu os [pré-requisitos](expressroute-prerequisites.md), os [requisitos de roteamento](expressroute-routing.md) e os [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="c1c1a-110">Examine as informações fornecidas em [Como mover um circuito de ExpressRoute do clássico para o Resource Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="c1c1a-110">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span> <span data-ttu-id="c1c1a-111">Certifique-se de entender completamente os limites e limitações.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-111">Make sure that you fully understand the limits and limitations.</span></span>
* <span data-ttu-id="c1c1a-112">Verifique se o circuito está totalmente operacional no modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-112">Verify that the circuit is fully operational in the classic deployment model.</span></span>
* <span data-ttu-id="c1c1a-113">Verifique se você tem um grupo de recursos que foi criado no modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-113">Ensure that you have a resource group that was created in the Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="c1c1a-114">Mover um circuito de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c1c1a-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-the-classic-deployment-model"></a><span data-ttu-id="c1c1a-115">Etapa 1: Coletar detalhes do circuito do modelo de implantação clássico</span><span class="sxs-lookup"><span data-stu-id="c1c1a-115">Step 1: Gather circuit details from the classic deployment model</span></span>

<span data-ttu-id="c1c1a-116">Entre no ambiente clássico do Azure e obtenha a chave de serviço.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-116">Sign in to the Azure classic environment and gather the service key.</span></span>

1. <span data-ttu-id="c1c1a-117">Entre na sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-117">Sign in to your Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="c1c1a-118">Selecione a assinatura do Azure apropriada.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-118">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="c1c1a-119">Importar os módulos do PowerShell para Azure e ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-119">Import the PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="c1c1a-120">Use o cmdlet abaixo para obter as chaves de serviço para todos os seus circuitos do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-120">Use the cmdlet below to get the service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="c1c1a-121">Após a recuperação das chaves, copie a **chave de serviço** do circuito que você deseja mover para o modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-121">After retrieving the keys, copy the **service key** of the circuit that you want to move to the Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="c1c1a-122">Etapa 2: Entrar e criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c1c1a-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="c1c1a-123">Entre no ambiente do Resource Manager e crie um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-123">Sign in to the Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="c1c1a-124">Entre no ambiente do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-124">Sign in to your Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="c1c1a-125">Selecione a assinatura do Azure apropriada.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-125">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="c1c1a-126">Modifique o trecho a seguir para criar um novo grupo de recursos se você ainda não tiver um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-126">Modify the snippet below to create a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-the-expressroute-circuit-to-the-resource-manager-deployment-model"></a><span data-ttu-id="c1c1a-127">Etapa 3: Mover o circuito de ExpressRoute para o modelo de implantação do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="c1c1a-127">Step 3: Move the ExpressRoute circuit to the Resource Manager deployment model</span></span>

<span data-ttu-id="c1c1a-128">Agora você está pronto para mover o circuito de ExpressRoute do modelo de implantação clássico para o do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-128">You are now ready to move your ExpressRoute circuit from the classic deployment model to the Resource Manager deployment model.</span></span> <span data-ttu-id="c1c1a-129">Antes de prosseguir, examine as informações fornecidas em [Como mover circuitos de ExpressRoute do modelo de implantação clássico para o Resource Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="c1c1a-129">Before proceeding, review the information provided in [Moving an ExpressRoute circuit from the classic to the Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="c1c1a-130">Para mover o circuito, modifique e execute o trecho a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1c1a-130">To move your circuit, modify and run the following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="c1c1a-131">Após a movimentação, o novo nome que está relacionado no cmdlet anterior será usado para o recurso de endereço.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-131">After the move has finished, the new name that is listed in the previous cmdlet will be used to address the resource.</span></span> <span data-ttu-id="c1c1a-132">O circuito essencialmente será renomeado.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-132">The circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="c1c1a-133">Modificar o acesso de circuito</span><span class="sxs-lookup"><span data-stu-id="c1c1a-133">Modify circuit access</span></span>

### <a name="to-enable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="c1c1a-134">Para habilitar o acesso ao circuito de ExpressRoute para ambos os modelos de implantação</span><span class="sxs-lookup"><span data-stu-id="c1c1a-134">To enable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="c1c1a-135">Depois de mover o circuito do ExpressRoute clássico para o modelo de implantação do Gerenciador de recursos, você pode habilitar o acesso a ambos os modelos de implantação.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-135">After moving your classic ExpressRoute circuit to the Resource Manager deployment model, you can enable access to both deployment models.</span></span> <span data-ttu-id="c1c1a-136">Execute os cmdlets a seguir para habilitar o acesso a ambos os modelos de implantação:</span><span class="sxs-lookup"><span data-stu-id="c1c1a-136">Run the following cmdlets to enable access to both deployment models:</span></span>

1. <span data-ttu-id="c1c1a-137">Obtenha os detalhes do circuito.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-137">Get the circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="c1c1a-138">Defina "Permitir operações clássicas" como TRUE.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-138">Set "Allow Classic Operations" to TRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="c1c1a-139">Atualize o circuito.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-139">Update the circuit.</span></span> <span data-ttu-id="c1c1a-140">Depois que a operação for concluída com êxito, você poderá exibir o circuito no modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-140">After this operation has finished successfully, you will be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="c1c1a-141">Execute o cmdlet a seguir para obter os detalhes do circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-141">Run the following cmdlet to get the details of the ExpressRoute circuit.</span></span> <span data-ttu-id="c1c1a-142">Você deve ser capaz de ver a chave de serviço relacionada.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-142">You must be able to see the service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="c1c1a-143">Agora você pode gerenciar links para o circuito do ExpressRoute usando os comandos do modelo de implantação clássico para redes virtuais clássicas e os comandos do Gerenciador de recursos para VNets do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-143">You can now manage links to the ExpressRoute circuit using the classic deployment model commands for classic VNets, and the Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="c1c1a-144">Os artigos a seguir lhe ajudam a gerenciar links para o circuito de ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="c1c1a-144">The following articles help you manage links to the ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="c1c1a-145">Vincule sua rede virtual ao circuito de ExpressRoute no modelo de implantação do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="c1c1a-145">Link your virtual network to your ExpressRoute circuit in the Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="c1c1a-146">Vincule sua rede virtual ao circuito de ExpressRoute no modelo de implantação clássico</span><span class="sxs-lookup"><span data-stu-id="c1c1a-146">Link your virtual network to your ExpressRoute circuit in the classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="to-disable-expressroute-circuit-access-to-the-classic-deployment-model"></a><span data-ttu-id="c1c1a-147">Para desabilitar o circuito de ExpressRoute para o modelo de implantação clássico</span><span class="sxs-lookup"><span data-stu-id="c1c1a-147">To disable ExpressRoute circuit access to the classic deployment model</span></span>

<span data-ttu-id="c1c1a-148">Execute os cmdlets a seguir para desabilitar o acesso ao modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-148">Run the following cmdlets to disable access to the classic deployment model.</span></span>

1. <span data-ttu-id="c1c1a-149">Obtenha detalhes do circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-149">Get details of the ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="c1c1a-150">Defina "Permitir operações clássicas" como FALSE.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-150">Set "Allow Classic Operations" to FALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="c1c1a-151">Atualize o circuito.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-151">Update the circuit.</span></span> <span data-ttu-id="c1c1a-152">Depois que a operação for concluída com êxito, você não poderá exibir o circuito no modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="c1c1a-152">After this operation has finished successfully, you will not be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="c1c1a-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c1c1a-153">Next steps</span></span>

* [<span data-ttu-id="c1c1a-154">Criar e modificar o roteamento do circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c1c1a-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="c1c1a-155">Vincular a rede virtual ao circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c1c1a-155">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)