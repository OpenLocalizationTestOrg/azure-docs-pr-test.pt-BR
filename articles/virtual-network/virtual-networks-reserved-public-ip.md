---
title: "aaaManage Azure reservado de endereços IP (clássico) - PowerShell | Microsoft Docs"
description: "Entender os endereços IP reservados (clássico) e como toomanage-los usando o PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="bd802-103">Endereços IP reservados (Clássico)</span><span class="sxs-lookup"><span data-stu-id="bd802-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd802-104">portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bd802-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="bd802-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd802-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="bd802-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="bd802-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="bd802-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="bd802-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="bd802-108">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="bd802-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

<span data-ttu-id="bd802-109">Os endereços IP no Azure recaem em duas categorias: dinâmicos e reservados.</span><span class="sxs-lookup"><span data-stu-id="bd802-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="bd802-110">Os endereços IP públicos gerenciados pelo Azure são dinâmicos por padrão.</span><span class="sxs-lookup"><span data-stu-id="bd802-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="bd802-111">Que significa que Olá endereço IP usado para um determinado serviço de nuvem (VIP) ou tooaccess uma VM ou instância de função diretamente (ILPIP) pode mudar de tootime de tempo, quando os recursos são desligados ou parados (desalocados).</span><span class="sxs-lookup"><span data-stu-id="bd802-111">That means that hello IP address used for a given cloud service (VIP) or tooaccess a VM or role instance directly (ILPIP) can change from time tootime, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="bd802-112">endereços IP tooprevent alterem, você poderá reservar um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="bd802-112">tooprevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="bd802-113">IPs reservados podem ser usados apenas como um VIP, garantindo o endereço IP Olá para o serviço de nuvem Olá permanece Olá iguais, mesmo que os recursos foram desligados ou parada (desalocada).</span><span class="sxs-lookup"><span data-stu-id="bd802-113">Reserved IPs can be used only as a VIP, ensuring that hello IP address for hello cloud service remains hello same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="bd802-114">Além disso, você pode converter existente IPs dinâmico usado como um endereço IP VIP tooa reservado.</span><span class="sxs-lookup"><span data-stu-id="bd802-114">Furthermore, you can convert existing dynamic IPs used as a VIP tooa reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd802-115">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bd802-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bd802-116">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="bd802-116">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="bd802-117">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd802-117">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="bd802-118">Saiba como tooreserve uma estática pública endereço IP usando Olá [modelo de implantação do Gerenciador de recursos](virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="bd802-118">Learn how tooreserve a static public IP address using hello [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="bd802-119">toolearn mais sobre IP endereços no Azure, leia Olá [endereços IP](virtual-network-ip-addresses-overview-classic.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="bd802-119">toolearn more about IP addresses in Azure, read hello [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="bd802-120">Quando eu precisarei de um IP reservado?</span><span class="sxs-lookup"><span data-stu-id="bd802-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="bd802-121">**Você deseja tooensure que Olá IP é reservado em sua assinatura**.</span><span class="sxs-lookup"><span data-stu-id="bd802-121">**You want tooensure that hello IP is reserved in your subscription**.</span></span> <span data-ttu-id="bd802-122">Se você quiser tooreserve um endereço IP que não é liberado da sua assinatura sob nenhuma circunstância, você deve usar um IP público reservado.</span><span class="sxs-lookup"><span data-stu-id="bd802-122">If you want tooreserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="bd802-123">**Você deseja que sua toostay IP com o serviço de nuvem mesmo em interrompido ou desalocadas estado (VMs)**.</span><span class="sxs-lookup"><span data-stu-id="bd802-123">**You want your IP toostay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="bd802-124">Se você quiser que seu toobe serviço acessado usando um endereço IP que não são alterados, mesmo quando a nuvem de máquinas virtuais em Olá serviço foram desligados ou parar (desalocado).</span><span class="sxs-lookup"><span data-stu-id="bd802-124">If you want your service toobe accessed by using an IP address that doesn't change, even when VMs in hello cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="bd802-125">**Você deseja que o tráfego de saída do Azure usa um endereço IP previsível de tooensure**.</span><span class="sxs-lookup"><span data-stu-id="bd802-125">**You want tooensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="bd802-126">Você pode ter seu local firewall configurado tooallow somente do tráfego de endereços IP específicos.</span><span class="sxs-lookup"><span data-stu-id="bd802-126">You may have your on-premises firewall configured tooallow only traffic from specific IP addresses.</span></span> <span data-ttu-id="bd802-127">Ao reservar um IP, você sabe que o IP de origem Olá endereço e não é necessário tooupdate devido a alterações IP tooan de regras de firewall.</span><span class="sxs-lookup"><span data-stu-id="bd802-127">By reserving an IP, you know hello source IP address, and don't need tooupdate your firewall rules due tooan IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="bd802-128">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="bd802-128">FAQ</span></span>
1. <span data-ttu-id="bd802-129">Posso usar um IP reservado para todos os serviços do Azure?</span><span class="sxs-lookup"><span data-stu-id="bd802-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="bd802-130">Não.</span><span class="sxs-lookup"><span data-stu-id="bd802-130">No.</span></span> <span data-ttu-id="bd802-131">Os IPs reservados só podem ser usados para VMs e funções de instância de serviço de nuvem exposto através de um VIP.</span><span class="sxs-lookup"><span data-stu-id="bd802-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="bd802-132">Quantos IPs reservados eu posso ter?</span><span class="sxs-lookup"><span data-stu-id="bd802-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="bd802-133">Para obter detalhes, consulte Olá [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.</span><span class="sxs-lookup"><span data-stu-id="bd802-133">For details, see hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="bd802-134">Há uma cobrança para IPs reservados?</span><span class="sxs-lookup"><span data-stu-id="bd802-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="bd802-135">Às vezes.</span><span class="sxs-lookup"><span data-stu-id="bd802-135">Sometimes.</span></span> <span data-ttu-id="bd802-136">Para obter detalhes sobre preços, consulte Olá [detalhes de preço do endereço de IP reservado](http://go.microsoft.com/fwlink/?LinkID=398482) página.</span><span class="sxs-lookup"><span data-stu-id="bd802-136">For pricing details, see hello [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="bd802-137">Como eu reservo um endereço IP?</span><span class="sxs-lookup"><span data-stu-id="bd802-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="bd802-138">Você pode usar o PowerShell, hello [API de REST de gerenciamento do Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), ou hello [portal do Azure](https://portal.azure.com) tooreserve um endereço IP em uma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd802-138">You can use PowerShell, hello [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or hello [Azure portal](https://portal.azure.com) tooreserve an IP address in an Azure region.</span></span> <span data-ttu-id="bd802-139">Um endereço IP reservado é assinatura tooyour associado.</span><span class="sxs-lookup"><span data-stu-id="bd802-139">A reserved IP address is associated tooyour subscription.</span></span>
5. <span data-ttu-id="bd802-140">Posso usar um IP reservado com VNets baseadas em grupos de afinidades?</span><span class="sxs-lookup"><span data-stu-id="bd802-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="bd802-141">Não.</span><span class="sxs-lookup"><span data-stu-id="bd802-141">No.</span></span> <span data-ttu-id="bd802-142">Os IPs reservados têm suporte apenas em redes virtuais regionais.</span><span class="sxs-lookup"><span data-stu-id="bd802-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="bd802-143">VNets associadas a grupos de afinidades não dão suporte a IPs reservados.</span><span class="sxs-lookup"><span data-stu-id="bd802-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="bd802-144">Para obter mais informações sobre como associar uma rede virtual uma região ou grupo de afinidade, consulte Olá [sobre VNets regionais e grupos de afinidade](virtual-networks-migrate-to-regional-vnet.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="bd802-144">For more information about associating a VNet with a region or affinity group, see hello [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="bd802-145">Gerenciar VIPs reservados</span><span class="sxs-lookup"><span data-stu-id="bd802-145">Manage reserved VIPs</span></span>

<span data-ttu-id="bd802-146">Certifique-se de ter instalado e configurado o PowerShell executando etapas Olá Olá [instalar e configurar o PowerShell](/powershell/azure/overview) artigo.</span><span class="sxs-lookup"><span data-stu-id="bd802-146">Ensure you have installed and configured PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="bd802-147">Antes de usar IPs reservados, você deve adicionar assinatura tooyour.</span><span class="sxs-lookup"><span data-stu-id="bd802-147">Before you can use reserved IPs, you must add it tooyour subscription.</span></span> <span data-ttu-id="bd802-148">toocreate um IP reservado no pool de saudação do IP público de endereços disponíveis no hello *centro dos EUA* local, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd802-148">toocreate a reserved IP from hello pool of public IP addresses available in hello *Central US* location, run hello following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="bd802-149">Observe, entretanto, que você não pode especificar qual IP está sendo reservado.</span><span class="sxs-lookup"><span data-stu-id="bd802-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="bd802-150">tooview quais endereços IP estão reservados em sua assinatura, execute Olá a seguir de comando do PowerShell e observe valores hello *ReservedIPName* e *endereço*:</span><span class="sxs-lookup"><span data-stu-id="bd802-150">tooview what IP addresses are reserved in your subscription, run hello following PowerShell command, and notice hello values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="bd802-151">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="bd802-151">Expected output:</span></span>

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
><span data-ttu-id="bd802-152">Quando você cria um endereço IP reservado com o PowerShell, você não pode especificar um IP de Olá reservada do recurso grupo toocreate no.</span><span class="sxs-lookup"><span data-stu-id="bd802-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group toocreate hello reserved IP in.</span></span> <span data-ttu-id="bd802-153">O Azure o coloca automaticamente em um grupo de recursos denominado *Default-Networking*.</span><span class="sxs-lookup"><span data-stu-id="bd802-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="bd802-154">Se você criar o IP reservada de saudação usando Olá [portal do Azure](http://portal.azure.com), você pode especificar qualquer grupo de recursos que você escolher.</span><span class="sxs-lookup"><span data-stu-id="bd802-154">If you create hello reserved IP using hello [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="bd802-155">Se você criar IP hello reservado em um grupo de recursos diferente de *rede padrão* no entanto, sempre que referenciar Olá IP reservado com comandos como `Get-AzureReservedIP` e `Remove-AzureReservedIP`, você deve fazer referência a nome hello *Reservado-ip-nome de nome do grupo de recursos do grupo*.</span><span class="sxs-lookup"><span data-stu-id="bd802-155">If you create hello reserved IP in a resource group other than *Default-Networking* however, whenever you reference hello reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference hello name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="bd802-156">Por exemplo, se você criar um IP reservado denominado *myReservedIP* em um grupo de recursos denominado *myResourceGroup*, você deve fazer referência a nome de saudação do IP hello reservado como *myResourceGroup de grupo myReservedIP*.</span><span class="sxs-lookup"><span data-stu-id="bd802-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference hello name of hello reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="bd802-157">Quando um IP é reservado, ela permanece associada tooyour assinatura até você excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="bd802-157">Once an IP is reserved, it remains associated tooyour subscription until you delete it.</span></span> <span data-ttu-id="bd802-158">toodelete um IP reservado, Olá executar comandos do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd802-158">toodelete a reserved IP, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="bd802-159">Reservar um endereço IP de saudação de um serviço de nuvem existente</span><span class="sxs-lookup"><span data-stu-id="bd802-159">Reserve hello IP address of an existing cloud service</span></span>
<span data-ttu-id="bd802-160">Você pode reservar o endereço IP de saudação de um serviço de nuvem existente adicionando Olá `-ServiceName` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="bd802-160">You can reserve hello IP address of an existing cloud service by adding hello `-ServiceName` parameter.</span></span> <span data-ttu-id="bd802-161">endereço IP de saudação tooreserve de um serviço de nuvem *TestService* em Olá *centro dos EUA* local, execute Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd802-161">tooreserve hello IP address of a cloud service *TestService* in hello *Central US* location, run hello following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a><span data-ttu-id="bd802-162">Associar um reservado IP tooa novo serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="bd802-162">Associate a reserved IP tooa new cloud service</span></span>
<span data-ttu-id="bd802-163">Olá script a seguir cria um IP reservado novo, em seguida, associa-tooa novo serviço de nuvem chamado *TestService*.</span><span class="sxs-lookup"><span data-stu-id="bd802-163">hello following script creates a new reserved IP, then associates it tooa new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="bd802-164">Quando você cria um toouse IP reservado com um serviço de nuvem, você ainda consultar toohello VM usando *VIP:&lt;número da porta >* para comunicação de entrada.</span><span class="sxs-lookup"><span data-stu-id="bd802-164">When you create a reserved IP toouse with a cloud service, you still refer toohello VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="bd802-165">Reservar um IP não significa que você pode conectar toohello VM diretamente.</span><span class="sxs-lookup"><span data-stu-id="bd802-165">Reserving an IP does not mean you can connect toohello VM directly.</span></span> <span data-ttu-id="bd802-166">Olá IP reservado é atribuído toohello nuvem de serviço que Olá VM foi implantada.</span><span class="sxs-lookup"><span data-stu-id="bd802-166">hello reserved IP is assigned toohello cloud service that hello VM has been deployed to.</span></span> <span data-ttu-id="bd802-167">Se você quiser tooconnect tooa VM por IP diretamente, você tem tooconfigure um IP público em nível de instância.</span><span class="sxs-lookup"><span data-stu-id="bd802-167">If you want tooconnect tooa VM by IP directly, you have tooconfigure an instance-level public IP.</span></span> <span data-ttu-id="bd802-168">Um IP público em nível de instância é um tipo de IP público (chamado de um ILPIP) atribuído diretamente tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="bd802-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly tooyour VM.</span></span> <span data-ttu-id="bd802-169">Ele não pode ser reservado.</span><span class="sxs-lookup"><span data-stu-id="bd802-169">It cannot be reserved.</span></span> <span data-ttu-id="bd802-170">Para obter mais informações, leia Olá [IP público em nível de instância (ILPIP)](virtual-networks-instance-level-public-ip.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="bd802-170">For more information, read hello [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="bd802-171">Remover um IP reservado de uma implantação em execução</span><span class="sxs-lookup"><span data-stu-id="bd802-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="bd802-172">tooremove um IP reservado adicionado um novo serviço de nuvem tooa, execute o hello comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd802-172">tooremove a reserved IP added tooa new cloud service, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="bd802-173">Removendo um IP reservado de uma implantação em execução não remove reserva Olá de sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="bd802-173">Removing a reserved IP from a running deployment does not remove hello reservation from your subscription.</span></span> <span data-ttu-id="bd802-174">Ele simplesmente libera Olá IP toobe usado por outro recurso em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="bd802-174">It simply frees hello IP toobe used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a><span data-ttu-id="bd802-175">Associar um tooa IP reservado executando a implantação</span><span class="sxs-lookup"><span data-stu-id="bd802-175">Associate a reserved IP tooa running deployment</span></span>
<span data-ttu-id="bd802-176">Olá, comandos a seguir criam um serviço de nuvem chamado *TestService2* com uma nova VM denominada *TestVM2*.</span><span class="sxs-lookup"><span data-stu-id="bd802-176">hello following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="bd802-177">Olá existente reservado IP denominado *MyReservedIP* é, em seguida, o serviço de nuvem toohello associado.</span><span class="sxs-lookup"><span data-stu-id="bd802-177">hello existing reserved IP named *MyReservedIP* is then associated toohello cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="bd802-178">Associar um serviço de nuvem tooa IP reservado por meio de um arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="bd802-178">Associate a reserved IP tooa cloud service by using a service configuration file</span></span>
<span data-ttu-id="bd802-179">Você também pode associar um serviço de nuvem tooa IP reservado, usando um arquivo de configuração (CSCFG) do serviço.</span><span class="sxs-lookup"><span data-stu-id="bd802-179">You can also associate a reserved IP tooa cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="bd802-180">Olá xml de exemplo a seguir mostra como tooconfigure um serviço de nuvem toouse um VIP reservado nomeados *MyReservedIP*:</span><span class="sxs-lookup"><span data-stu-id="bd802-180">hello following sample xml shows how tooconfigure a cloud service toouse a reserved VIP named *MyReservedIP*:</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a><span data-ttu-id="bd802-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bd802-181">Next steps</span></span>
* <span data-ttu-id="bd802-182">Entender como [endereçamento IP](virtual-network-ip-addresses-overview-classic.md) funciona no modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="bd802-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="bd802-183">Saiba mais sobre [endereços IP privados reservados](virtual-networks-reserved-private-ip.md).</span><span class="sxs-lookup"><span data-stu-id="bd802-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="bd802-184">Saiba mais sobre [endereços ILPIP (IP Público de Nível de Instância)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="bd802-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

