---
title: "Gerenciar endereços IP reservados do Azure (Clássico) – PowerShell | Microsoft Docs"
description: "Entender os endereços IP reservados (Clássico) e como gerenciá-los usando o PowerShell."
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
ms.openlocfilehash: 5e9c83cebec96c6bc8afd53b0c637d7af899746f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="885c9-103">Endereços IP reservados (Clássico)</span><span class="sxs-lookup"><span data-stu-id="885c9-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="885c9-104">portal do Azure</span><span class="sxs-lookup"><span data-stu-id="885c9-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="885c9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="885c9-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="885c9-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="885c9-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="885c9-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="885c9-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="885c9-108">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="885c9-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

<span data-ttu-id="885c9-109">Os endereços IP no Azure recaem em duas categorias: dinâmicos e reservados.</span><span class="sxs-lookup"><span data-stu-id="885c9-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="885c9-110">Os endereços IP públicos gerenciados pelo Azure são dinâmicos por padrão.</span><span class="sxs-lookup"><span data-stu-id="885c9-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="885c9-111">Isso significa que o endereço IP usado para um determinado serviço de nuvem (VIP) ou para acessar uma VM ou instância de função diretamente (ILPIP) pode mudar de tempos em tempos, quando recursos forem desligados ou interrompidos (desalocados).</span><span class="sxs-lookup"><span data-stu-id="885c9-111">That means that the IP address used for a given cloud service (VIP) or to access a VM or role instance directly (ILPIP) can change from time to time, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="885c9-112">Para evitar que endereços IP sejam alterados, é possível reservar um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="885c9-112">To prevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="885c9-113">Os IPs reservados podem ser usados apenas como um VIP, garantindo que o endereço IP do serviço de nuvem permaneça o mesmo, mesmo se os recursos forem desligados ou interrompidos (desalocados).</span><span class="sxs-lookup"><span data-stu-id="885c9-113">Reserved IPs can be used only as a VIP, ensuring that the IP address for the cloud service remains the same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="885c9-114">Além disso, você pode converter IPs dinâmicos existentes usados como um VIP para um endereço IP reservado.</span><span class="sxs-lookup"><span data-stu-id="885c9-114">Furthermore, you can convert existing dynamic IPs used as a VIP to a reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="885c9-115">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="885c9-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="885c9-116">Este artigo aborda o uso do modelo de implantação clássica.</span><span class="sxs-lookup"><span data-stu-id="885c9-116">This article covers using the classic deployment model.</span></span> <span data-ttu-id="885c9-117">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="885c9-117">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="885c9-118">Saiba como reservar um endereço IP estático público usando o [Modelo de implantação do Gerenciador de Recursos](virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="885c9-118">Learn how to reserve a static public IP address using the [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="885c9-119">Para saber mais sobre endereços IP no Azure, leia o artigo [Endereços IP](virtual-network-ip-addresses-overview-classic.md).</span><span class="sxs-lookup"><span data-stu-id="885c9-119">To learn more about IP addresses in Azure, read the [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="885c9-120">Quando eu precisarei de um IP reservado?</span><span class="sxs-lookup"><span data-stu-id="885c9-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="885c9-121">**Você deseja garantir que o IP seja reservado em sua assinatura**.</span><span class="sxs-lookup"><span data-stu-id="885c9-121">**You want to ensure that the IP is reserved in your subscription**.</span></span> <span data-ttu-id="885c9-122">Se você quiser reservar um endereço IP que não seja liberado da sua assinatura sob nenhuma circunstância, você deverá usar um IP público reservado.</span><span class="sxs-lookup"><span data-stu-id="885c9-122">If you want to reserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="885c9-123">**Você deseja que o IP permaneça com seu serviço de nuvem, mesmo nos estados parados ou desalocados (VMs)**.</span><span class="sxs-lookup"><span data-stu-id="885c9-123">**You want your IP to stay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="885c9-124">Se você quiser que seu serviço seja acessado usando um endereço IP que não seja alterado, mesmo quando VMs do serviço de nuvem estejam paradas ou desalocadas.</span><span class="sxs-lookup"><span data-stu-id="885c9-124">If you want your service to be accessed by using an IP address that doesn't change, even when VMs in the cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="885c9-125">**Você deseja garantir que o tráfego de saída do Azure use um endereço IP previsível**.</span><span class="sxs-lookup"><span data-stu-id="885c9-125">**You want to ensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="885c9-126">Você pode ter seu firewall local configurado para permitir apenas o tráfego de endereços IP específicos.</span><span class="sxs-lookup"><span data-stu-id="885c9-126">You may have your on-premises firewall configured to allow only traffic from specific IP addresses.</span></span> <span data-ttu-id="885c9-127">Ao reservar um IP, você conhecerá o endereço IP de origem e não terá de atualizar suas regras de firewall devido a uma alteração de IP.</span><span class="sxs-lookup"><span data-stu-id="885c9-127">By reserving an IP, you know the source IP address, and don't need to update your firewall rules due to an IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="885c9-128">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="885c9-128">FAQ</span></span>
1. <span data-ttu-id="885c9-129">Posso usar um IP reservado para todos os serviços do Azure?</span><span class="sxs-lookup"><span data-stu-id="885c9-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="885c9-130">Não.</span><span class="sxs-lookup"><span data-stu-id="885c9-130">No.</span></span> <span data-ttu-id="885c9-131">Os IPs reservados só podem ser usados para VMs e funções de instância de serviço de nuvem exposto através de um VIP.</span><span class="sxs-lookup"><span data-stu-id="885c9-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="885c9-132">Quantos IPs reservados eu posso ter?</span><span class="sxs-lookup"><span data-stu-id="885c9-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="885c9-133">Para obter detalhes, consulte o [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.</span><span class="sxs-lookup"><span data-stu-id="885c9-133">For details, see the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="885c9-134">Há uma cobrança para IPs reservados?</span><span class="sxs-lookup"><span data-stu-id="885c9-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="885c9-135">Às vezes.</span><span class="sxs-lookup"><span data-stu-id="885c9-135">Sometimes.</span></span> <span data-ttu-id="885c9-136">Veja [Detalhes Sobre Preços de Endereços IP Reservados](http://go.microsoft.com/fwlink/?LinkID=398482) para obter detalhes sobre preços.</span><span class="sxs-lookup"><span data-stu-id="885c9-136">For pricing details, see the [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="885c9-137">Como eu reservo um endereço IP?</span><span class="sxs-lookup"><span data-stu-id="885c9-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="885c9-138">Você pode usar o PowerShell, o [API de REST de gerenciamento do Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), ou o [portal do Azure](https://portal.azure.com) para reservar um endereço IP em uma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="885c9-138">You can use PowerShell, the [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or the [Azure portal](https://portal.azure.com) to reserve an IP address in an Azure region.</span></span> <span data-ttu-id="885c9-139">Um endereço IP reservado é associado à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="885c9-139">A reserved IP address is associated to your subscription.</span></span>
5. <span data-ttu-id="885c9-140">Posso usar um IP reservado com VNets baseadas em grupos de afinidades?</span><span class="sxs-lookup"><span data-stu-id="885c9-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="885c9-141">Não.</span><span class="sxs-lookup"><span data-stu-id="885c9-141">No.</span></span> <span data-ttu-id="885c9-142">Os IPs reservados têm suporte apenas em redes virtuais regionais.</span><span class="sxs-lookup"><span data-stu-id="885c9-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="885c9-143">VNets associadas a grupos de afinidades não dão suporte a IPs reservados.</span><span class="sxs-lookup"><span data-stu-id="885c9-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="885c9-144">Para obter mais informações sobre a associação de uma VNet a uma região ou a um grupo de afinidades, veja o artigo [Sobre VNets regionais e grupos de afinidades](virtual-networks-migrate-to-regional-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="885c9-144">For more information about associating a VNet with a region or affinity group, see the [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="885c9-145">Gerenciar VIPs reservados</span><span class="sxs-lookup"><span data-stu-id="885c9-145">Manage reserved VIPs</span></span>

<span data-ttu-id="885c9-146">Certifique-se de ter instalado e configurado o Azure PowerShell seguindo as etapas do artigo [Instalar e configurar o PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="885c9-146">Ensure you have installed and configured PowerShell by completing the steps in the [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="885c9-147">Antes de poder usar IPs reservados, você deverá adicioná-los à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="885c9-147">Before you can use reserved IPs, you must add it to your subscription.</span></span> <span data-ttu-id="885c9-148">Para criar um IP reservado do pool de endereços IP públicos disponíveis no local *EUA Central* , execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="885c9-148">To create a reserved IP from the pool of public IP addresses available in the *Central US* location, run the following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="885c9-149">Observe, entretanto, que você não pode especificar qual IP está sendo reservado.</span><span class="sxs-lookup"><span data-stu-id="885c9-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="885c9-150">Para exibir quais endereços IP estão reservados em sua assinatura, execute o seguinte comando do PowerShell e observe os valores de *ReservedIPName* e *Endereço*:</span><span class="sxs-lookup"><span data-stu-id="885c9-150">To view what IP addresses are reserved in your subscription, run the following PowerShell command, and notice the values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="885c9-151">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="885c9-151">Expected output:</span></span>

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
><span data-ttu-id="885c9-152">Quando você cria um endereço IP reservado com o PowerShell, não é possível especificar um grupo de recursos no qual criar o IP reservado.</span><span class="sxs-lookup"><span data-stu-id="885c9-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group to create the reserved IP in.</span></span> <span data-ttu-id="885c9-153">O Azure o coloca automaticamente em um grupo de recursos denominado *Default-Networking*.</span><span class="sxs-lookup"><span data-stu-id="885c9-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="885c9-154">Se você criar o IP reservado usando o [Portal do Azure](http://portal.azure.com), você poderá especificar qualquer grupo de recursos que você escolher.</span><span class="sxs-lookup"><span data-stu-id="885c9-154">If you create the reserved IP using the [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="885c9-155">No entanto, se você criar o IP reservado em um grupo de recursos diferente do *Default-Networking*, sempre que você dizer referência ao IP reservado com comandos como `Get-AzureReservedIP` e `Remove-AzureReservedIP`, você deverá fazer referência ao nome *Group resource-group-name reserved-ip-name*.</span><span class="sxs-lookup"><span data-stu-id="885c9-155">If you create the reserved IP in a resource group other than *Default-Networking* however, whenever you reference the reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference the name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="885c9-156">Por exemplo, se você criar um IP reservado denominado *myReservedIP* em um grupo de recursos denominado *myResourceGroup*, você deverá fazer referência ao nome do IP reservado como *Group myResourceGroup myReservedIP*.</span><span class="sxs-lookup"><span data-stu-id="885c9-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference the name of the reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="885c9-157">Depois que um IP for reservado, ele permanecerá associado à sua assinatura até você excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="885c9-157">Once an IP is reserved, it remains associated to your subscription until you delete it.</span></span> <span data-ttu-id="885c9-158">Para excluir um IP reservado, execute o seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="885c9-158">To delete a reserved IP, run the following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-the-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="885c9-159">Reservar o endereço IP de um serviço de nuvem existente</span><span class="sxs-lookup"><span data-stu-id="885c9-159">Reserve the IP address of an existing cloud service</span></span>
<span data-ttu-id="885c9-160">É possível reservar o endereço IP de um serviço de nuvem existente adicionando o parâmetro `-ServiceName`.</span><span class="sxs-lookup"><span data-stu-id="885c9-160">You can reserve the IP address of an existing cloud service by adding the `-ServiceName` parameter.</span></span> <span data-ttu-id="885c9-161">Para reservar o endereço IP de um serviço de nuvem *TestService* no local *EUA Central*, execute o seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="885c9-161">To reserve the IP address of a cloud service *TestService* in the *Central US* location, run the following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-to-a-new-cloud-service"></a><span data-ttu-id="885c9-162">Associar um IP reservado a um novo serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="885c9-162">Associate a reserved IP to a new cloud service</span></span>
<span data-ttu-id="885c9-163">O script a seguir cria um novo IP reservado e o associa a um novo serviço de nuvem chamado *TestService*.</span><span class="sxs-lookup"><span data-stu-id="885c9-163">The following script creates a new reserved IP, then associates it to a new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="885c9-164">Quando você cria um IP reservado a ser usado com um serviço de nuvem, você ainda fará referência à VM usando *VIP:&lt;número da porta>* para comunicação de entrada.</span><span class="sxs-lookup"><span data-stu-id="885c9-164">When you create a reserved IP to use with a cloud service, you still refer to the VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="885c9-165">Reservar um IP não significa que você pode conectar-se à VM diretamente.</span><span class="sxs-lookup"><span data-stu-id="885c9-165">Reserving an IP does not mean you can connect to the VM directly.</span></span> <span data-ttu-id="885c9-166">O IP reservado é atribuído ao serviço de nuvem no qual a VM foi implantada.</span><span class="sxs-lookup"><span data-stu-id="885c9-166">The reserved IP is assigned to the cloud service that the VM has been deployed to.</span></span> <span data-ttu-id="885c9-167">Se você quiser se conectar diretamente a uma VM por IP, precisará configurar um IP público em nível de instância.</span><span class="sxs-lookup"><span data-stu-id="885c9-167">If you want to connect to a VM by IP directly, you have to configure an instance-level public IP.</span></span> <span data-ttu-id="885c9-168">Um IP público em nível de instância é um tipo de IP público (chamado de ILPIP) atribuído diretamente à sua VM.</span><span class="sxs-lookup"><span data-stu-id="885c9-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly to your VM.</span></span> <span data-ttu-id="885c9-169">Ele não pode ser reservado.</span><span class="sxs-lookup"><span data-stu-id="885c9-169">It cannot be reserved.</span></span> <span data-ttu-id="885c9-170">Para obter mais informações, leia o artigo [IP Público em Nível de Instância (ILPIP)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="885c9-170">For more information, read the [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="885c9-171">Remover um IP reservado de uma implantação em execução</span><span class="sxs-lookup"><span data-stu-id="885c9-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="885c9-172">Para remover um IP reservado adicionado a um novo serviço de nuvem, execute o seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="885c9-172">To remove a reserved IP added to a new cloud service, run the following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="885c9-173">Removendo um IP reservado de uma implantação em execução não remove a reserva de sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="885c9-173">Removing a reserved IP from a running deployment does not remove the reservation from your subscription.</span></span> <span data-ttu-id="885c9-174">Ele simplesmente libera o IP para ser usado por outro recurso em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="885c9-174">It simply frees the IP to be used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-to-a-running-deployment"></a><span data-ttu-id="885c9-175">Associar um IP reservado a uma implantação em execução</span><span class="sxs-lookup"><span data-stu-id="885c9-175">Associate a reserved IP to a running deployment</span></span>
<span data-ttu-id="885c9-176">Os comandos a seguir criam um serviço de nuvem denominado *TestService2* com uma nova VM denominada *TestVM2*.</span><span class="sxs-lookup"><span data-stu-id="885c9-176">The following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="885c9-177">O IP reservado existente chamado *MyReservedIP* é então associado ao serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="885c9-177">The existing reserved IP named *MyReservedIP* is then associated to the cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="885c9-178">Associar um IP reservado a um serviço de nuvem usando um arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="885c9-178">Associate a reserved IP to a cloud service by using a service configuration file</span></span>
<span data-ttu-id="885c9-179">Você também pode associar um IP reservado a um serviço de nuvem usando um arquivo de configuração de serviço (CSCFG).</span><span class="sxs-lookup"><span data-stu-id="885c9-179">You can also associate a reserved IP to a cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="885c9-180">O XML de exemplo a seguir mostra como configurar um serviço de nuvem para usar um VIP reservado denominado *MyReservedIP*:</span><span class="sxs-lookup"><span data-stu-id="885c9-180">The following sample xml shows how to configure a cloud service to use a reserved VIP named *MyReservedIP*:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="885c9-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="885c9-181">Next steps</span></span>
* <span data-ttu-id="885c9-182">Entenda como o [endereçamento IP](virtual-network-ip-addresses-overview-classic.md) funciona no modelo de implantação clássica.</span><span class="sxs-lookup"><span data-stu-id="885c9-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span></span>
* <span data-ttu-id="885c9-183">Saiba mais sobre [endereços IP privados reservados](virtual-networks-reserved-private-ip.md).</span><span class="sxs-lookup"><span data-stu-id="885c9-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="885c9-184">Saiba mais sobre [endereços ILPIP (IP Público de Nível de Instância)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="885c9-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

