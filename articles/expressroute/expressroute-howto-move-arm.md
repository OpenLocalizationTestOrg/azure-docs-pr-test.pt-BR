---
title: "Mover circuitos ExpressRoute de tooResource clássico Manager: PowerShell: Azure | Microsoft Docs"
description: "Esta página descreve como toomove toohello um circuito clássico Gerenciador de recursos de implantação de modelo usando o PowerShell."
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
ms.openlocfilehash: 8dcadafca5e4f40773902cec5786eba1dbe133eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="a1030-103">Mover circuitos ExpressRoute de modelo de implantação do hello clássico toohello Gerenciador de recursos usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1030-103">Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="a1030-104">toouse um circuito de rota expressa para Olá clássico e modelos de implantação do Gerenciador de recursos, você deve mover o modelo de implantação do hello circuito toohello Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="a1030-104">toouse an ExpressRoute circuit for both hello classic and Resource Manager deployment models, you must move hello circuit toohello Resource Manager deployment model.</span></span> <span data-ttu-id="a1030-105">Olá seções a seguir ajudarão-lo a mover seu circuito usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1030-105">hello following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a1030-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="a1030-106">Before you begin</span></span>

* <span data-ttu-id="a1030-107">Verifique se você tem a versão mais recente Olá dos módulos do PowerShell do Azure hello (pelo menos versão 1.0).</span><span class="sxs-lookup"><span data-stu-id="a1030-107">Verify that you have hello latest version of hello Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="a1030-108">Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a1030-108">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="a1030-109">Certifique-se de ter revisado Olá [pré-requisitos](expressroute-prerequisites.md), [requisitos de roteamento](expressroute-routing.md), e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.</span><span class="sxs-lookup"><span data-stu-id="a1030-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="a1030-110">Revise as informações de saudação que são fornecidas em [movendo um circuito de rota expressa de tooResource clássico Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="a1030-110">Review hello information that is provided under [Moving an ExpressRoute circuit from classic tooResource Manager](expressroute-move.md).</span></span> <span data-ttu-id="a1030-111">Certifique-se de que você compreenda plenamente Olá limites e as limitações.</span><span class="sxs-lookup"><span data-stu-id="a1030-111">Make sure that you fully understand hello limits and limitations.</span></span>
* <span data-ttu-id="a1030-112">Verifique se o circuito de saudação é totalmente operacional no modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="a1030-112">Verify that hello circuit is fully operational in hello classic deployment model.</span></span>
* <span data-ttu-id="a1030-113">Certifique-se de que você tenha um grupo de recursos que foi criado no modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1030-113">Ensure that you have a resource group that was created in hello Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="a1030-114">Mover um circuito de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a1030-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a><span data-ttu-id="a1030-115">Etapa 1: Coletar detalhes de circuito de modelo de implantação clássico Olá</span><span class="sxs-lookup"><span data-stu-id="a1030-115">Step 1: Gather circuit details from hello classic deployment model</span></span>

<span data-ttu-id="a1030-116">Entrar toohello ambiente clássico do Azure e obter chave de saudação do serviço.</span><span class="sxs-lookup"><span data-stu-id="a1030-116">Sign in toohello Azure classic environment and gather hello service key.</span></span>

1. <span data-ttu-id="a1030-117">Entre tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1030-117">Sign in tooyour Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="a1030-118">Selecione Olá assinatura apropriada do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1030-118">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="a1030-119">Importe os módulos do PowerShell Olá para o Azure e rota expressa.</span><span class="sxs-lookup"><span data-stu-id="a1030-119">Import hello PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="a1030-120">Use o cmdlet do hello abaixo chaves de serviço tooget Olá para todos os seus circuitos de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="a1030-120">Use hello cmdlet below tooget hello service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="a1030-121">Depois de recuperar chaves hello, copie Olá **chave de serviço** do circuito Olá que você deseja que o modelo de implantação do toomove toohello Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="a1030-121">After retrieving hello keys, copy hello **service key** of hello circuit that you want toomove toohello Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="a1030-122">Etapa 2: Entrar e criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a1030-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="a1030-123">Entrar no ambiente do Gerenciador de recursos de toohello e crie um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a1030-123">Sign in toohello Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="a1030-124">Entrar no ambiente do Azure Resource Manager tooyour.</span><span class="sxs-lookup"><span data-stu-id="a1030-124">Sign in tooyour Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="a1030-125">Selecione Olá assinatura apropriada do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1030-125">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="a1030-126">Modificar trecho Olá abaixo toocreate um novo grupo de recursos se você ainda não tiver um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a1030-126">Modify hello snippet below toocreate a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a><span data-ttu-id="a1030-127">Etapa 3: Mover o modelo de implantação do hello rota expressa circuito toohello Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="a1030-127">Step 3: Move hello ExpressRoute circuit toohello Resource Manager deployment model</span></span>

<span data-ttu-id="a1030-128">Você é agora pronto toomove o circuito de rota expressa do modelo de implantação do hello implantação clássica modelo toohello Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="a1030-128">You are now ready toomove your ExpressRoute circuit from hello classic deployment model toohello Resource Manager deployment model.</span></span> <span data-ttu-id="a1030-129">Antes de continuar, examine informações de saudação fornecidas no [mover um circuito de rota expressa do modelo de implantação do Gerenciador de recursos de toohello clássico de Olá](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="a1030-129">Before proceeding, review hello information provided in [Moving an ExpressRoute circuit from hello classic toohello Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="a1030-130">toomove o seu circuito, modifique e execute Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1030-130">toomove your circuit, modify and run hello following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="a1030-131">Após mover hello, Olá novo nome está listado no cmdlet anterior Olá será usado tooaddress Olá recursos.</span><span class="sxs-lookup"><span data-stu-id="a1030-131">After hello move has finished, hello new name that is listed in hello previous cmdlet will be used tooaddress hello resource.</span></span> <span data-ttu-id="a1030-132">circuito Olá essencialmente será renomeado.</span><span class="sxs-lookup"><span data-stu-id="a1030-132">hello circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="a1030-133">Modificar o acesso de circuito</span><span class="sxs-lookup"><span data-stu-id="a1030-133">Modify circuit access</span></span>

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="a1030-134">tooenable acesso de circuito de rota expressa para ambos os modelos de implantação</span><span class="sxs-lookup"><span data-stu-id="a1030-134">tooenable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="a1030-135">Depois de mover o clássico modelo de implantação de rota expressa circuito toohello Gerenciador de recursos, você pode habilitar modelos de implantação do acesso tooboth.</span><span class="sxs-lookup"><span data-stu-id="a1030-135">After moving your classic ExpressRoute circuit toohello Resource Manager deployment model, you can enable access tooboth deployment models.</span></span> <span data-ttu-id="a1030-136">Execute Olá modelos de implantação cmdlets tooenable acesso tooboth a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1030-136">Run hello following cmdlets tooenable access tooboth deployment models:</span></span>

1. <span data-ttu-id="a1030-137">Obter detalhes de circuito hello.</span><span class="sxs-lookup"><span data-stu-id="a1030-137">Get hello circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="a1030-138">Definir tooTRUE "Permitir operações clássico".</span><span class="sxs-lookup"><span data-stu-id="a1030-138">Set "Allow Classic Operations" tooTRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="a1030-139">Atualize o circuito de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1030-139">Update hello circuit.</span></span> <span data-ttu-id="a1030-140">Depois que a operação seja concluída com êxito, você será tooview capaz de circuito de saudação no modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="a1030-140">After this operation has finished successfully, you will be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="a1030-141">Execute Olá cmdlet tooget Olá detalhes de saudação circuito de rota expressa a seguir.</span><span class="sxs-lookup"><span data-stu-id="a1030-141">Run hello following cmdlet tooget hello details of hello ExpressRoute circuit.</span></span> <span data-ttu-id="a1030-142">Você deve ser capaz de toosee chave de serviço de Olá listado.</span><span class="sxs-lookup"><span data-stu-id="a1030-142">You must be able toosee hello service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="a1030-143">Agora você pode gerenciar o circuito de rota expressa toohello links usando comandos de modelo de implantação clássico Olá para VNets clássico e comandos do Gerenciador de recursos de saudação para VNets do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="a1030-143">You can now manage links toohello ExpressRoute circuit using hello classic deployment model commands for classic VNets, and hello Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="a1030-144">Olá artigos a seguir ajudam a gerenciar links toohello circuito de rota expressa:</span><span class="sxs-lookup"><span data-stu-id="a1030-144">hello following articles help you manage links toohello ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="a1030-145">Vincular seu circuito de rota expressa no modelo de implantação do Gerenciador de recursos de saudação de tooyour de rede virtual</span><span class="sxs-lookup"><span data-stu-id="a1030-145">Link your virtual network tooyour ExpressRoute circuit in hello Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="a1030-146">Vincular sua rede virtual de tooyour circuito de rota expressa no modelo de implantação clássico Olá</span><span class="sxs-lookup"><span data-stu-id="a1030-146">Link your virtual network tooyour ExpressRoute circuit in hello classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a><span data-ttu-id="a1030-147">modelo de implantação clássico toohello do acesso de circuito de rota expressa toodisable</span><span class="sxs-lookup"><span data-stu-id="a1030-147">toodisable ExpressRoute circuit access toohello classic deployment model</span></span>

<span data-ttu-id="a1030-148">Execute Olá modelo de implantação clássico cmdlets toodisable acesso toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="a1030-148">Run hello following cmdlets toodisable access toohello classic deployment model.</span></span>

1. <span data-ttu-id="a1030-149">Obter os detalhes de saudação circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="a1030-149">Get details of hello ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="a1030-150">Definir tooFALSE "Permitir operações clássico".</span><span class="sxs-lookup"><span data-stu-id="a1030-150">Set "Allow Classic Operations" tooFALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="a1030-151">Atualize o circuito de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1030-151">Update hello circuit.</span></span> <span data-ttu-id="a1030-152">Depois que a operação seja concluída com êxito, não será capaz de tooview circuito de Olá no modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="a1030-152">After this operation has finished successfully, you will not be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="a1030-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a1030-153">Next steps</span></span>

* [<span data-ttu-id="a1030-154">Criar e modificar o roteamento do circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a1030-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="a1030-155">Vincular sua rede virtual de tooyour circuito de rota expressa</span><span class="sxs-lookup"><span data-stu-id="a1030-155">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
