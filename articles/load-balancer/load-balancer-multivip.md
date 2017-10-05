---
title: "Vários VIPs para um serviço de nuvem"
description: "Visão geral de vários VIPs e como definir vários VIPs em um serviço de nuvem"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: f40e0501eed8d5f296e7c79d8a35705a695ae6fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="5c0fb-103">Configurar vários VIPs para um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="5c0fb-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="5c0fb-104">Você pode acessar os serviços de nuvem do Azure pela Internet pública usando um endereço IP fornecido pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-104">You can access Azure cloud services over the public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="5c0fb-105">Este endereço IP público é conhecido como um VIP (IP virtual), uma vez que está vinculado ao Azure Load Balancer, e não às instâncias VM (máquina virtual) no serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-105">This public IP address is referred to as a VIP (virtual IP) since it is linked to the Azure load balancer, and not the Virtual Machine (VM) instances within the cloud service.</span></span> <span data-ttu-id="5c0fb-106">Você pode acessar qualquer instância VM dentro de um serviço de nuvem usando um único VIP.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="5c0fb-107">No entanto, há situações em que você terá mais de um VIP como ponto de entrada para o mesmo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-107">However, there are scenarios in which you may need more than one VIP as an entry point to the same cloud service.</span></span> <span data-ttu-id="5c0fb-108">Por exemplo, seu serviço de nuvem pode hospedar vários sites que exigem conectividade SSL usando a porta padrão de 443, uma vez que cada site é hospedado para um cliente, ou locatário, diferente.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-108">For instance, your cloud service may host multiple websites that require SSL connectivity using the default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="5c0fb-109">Nesse caso, é necessário ter outro endereço IP público para cada site.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-109">In this scenario, you need to have a different public facing IP address for each website.</span></span> <span data-ttu-id="5c0fb-110">O diagrama a seguir ilustra uma hospedagem multilocatário típica na Web, com a necessidade de vários certificados SSL na mesma porta pública.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-110">The diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on the same public port.</span></span>

![Cenário SSL de vários VIPs](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="5c0fb-112">No exemplo acima, todos os VIPs usam a mesma porta pública (443) e o tráfego é redirecionado para um ou VMs com balanceamento de carga em uma porta privada exclusiva para o endereço IP interno do serviço de nuvem que hospeda todos os sites.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-112">In the example above, all VIPs use the same public port (443) and traffic is redirected to one or more load balanced VMs on a unique private port for the internal IP address of the cloud service hosting all the websites.</span></span>

> [!NOTE]
> <span data-ttu-id="5c0fb-113">Outra situação que exige o uso de vários VIPs é a hospedagem de vários ouvintes do Grupo de Disponibilidade do SQL AlwaysOn no mesmo conjunto de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-113">Another situation requiring the use the multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on the same set of Virtual Machines.</span></span>

<span data-ttu-id="5c0fb-114">VIPs são dinâmicos por padrão, o que significa que o endereço IP real atribuído ao serviço de nuvem pode mudar ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-114">VIPs are dynamic by default, which means that the actual IP address assigned to the cloud service may change over time.</span></span> <span data-ttu-id="5c0fb-115">Para evitar isso, você pode reservar um VIP para o serviço.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-115">To prevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="5c0fb-116">Para saber mais sobre VIPs reservados, consulte [IP público reservado](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="5c0fb-116">To learn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5c0fb-117">Consulte [Preços de endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses/) para obter informações sobre preços em VIPs e IPs reservados.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="5c0fb-118">Você pode usar o PowerShell para verificar os VIPs usados por seus serviços de nuvem, bem como adicionar e remover VIPs, associar um VIP para um ponto de extremidade e configurar o balanceamento de carga em um VIP específico.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-118">You can use PowerShell to verify the VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP to an endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="5c0fb-119">Limitações</span><span class="sxs-lookup"><span data-stu-id="5c0fb-119">Limitations</span></span>

<span data-ttu-id="5c0fb-120">Nesse momento, a funcionalidade Multi VIP está limitada aos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="5c0fb-120">At this time, Multi VIP functionality is limited to the following scenarios:</span></span>

* <span data-ttu-id="5c0fb-121">**IaaS apenas**.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-121">**IaaS only**.</span></span> <span data-ttu-id="5c0fb-122">Só é possível habilitar o Multi VIP para serviços de nuvem que contêm VMs.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="5c0fb-123">Não é possível usar o Multi VIP em cenários de PaaS com instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="5c0fb-124">**PowerShell apenas**.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-124">**PowerShell only**.</span></span> <span data-ttu-id="5c0fb-125">Só é possível gerenciar o Multi VIP usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="5c0fb-126">Essas limitações são temporárias e podem ser alteradas a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="5c0fb-127">Certifique-se de visitar novamente esta página para verificar as alterações futuras.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-127">Make sure to revisit this page to verify future changes.</span></span>

## <a name="how-to-add-a-vip-to-a-cloud-service"></a><span data-ttu-id="5c0fb-128">Como adicionar um VIP a um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="5c0fb-128">How to add a VIP to a cloud service</span></span>
<span data-ttu-id="5c0fb-129">Para adicionar um VIP ao seu serviço, execute o seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5c0fb-129">To add a VIP to your service, run the following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="5c0fb-130">Esse comando exibe um resultado semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="5c0fb-130">This command displays a result similar to the following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-to-remove-a-vip-from-a-cloud-service"></a><span data-ttu-id="5c0fb-131">Como remover um VIP de um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="5c0fb-131">How to remove a VIP from a cloud service</span></span>
<span data-ttu-id="5c0fb-132">Para remover o VIP adicionado ao serviço no exemplo acima, execute o seguinte comando PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5c0fb-132">To remove the VIP added to your service in the example above, run the following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="5c0fb-133">Você só pode remover um VIP, se ele não tiver pontos de extremidade associados a ele.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-133">You can only remove a VIP if it has no endpoints associated to it.</span></span>


## <a name="how-to-retrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="5c0fb-134">Como recuperar informações de VIP de um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="5c0fb-134">How to retrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="5c0fb-135">Para recuperar VIPs associados a um serviço de nuvem, execute o seguinte script do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5c0fb-135">To retrieve the VIPs associated with a cloud service, run the following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="5c0fb-136">Esse script exibe um resultado semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="5c0fb-136">The script displays a result similar to the following sample:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

<span data-ttu-id="5c0fb-137">Neste exemplo, o serviço de nuvem tem 3 VIPs:</span><span class="sxs-lookup"><span data-stu-id="5c0fb-137">In this example, the cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="5c0fb-138">**Vip1** é o VIP padrão e você sabe disso porque o valor IsDnsProgrammedName está definido como verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-138">**Vip1** is the default VIP, you know that because the value for IsDnsProgrammedName is set to true.</span></span>
* <span data-ttu-id="5c0fb-139">**Vip2** e **Vip3** não são usados porque não têm endereços IP.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="5c0fb-140">Eles só serão usados se você associar um ponto de extremidade ao VIP.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-140">They will only be used if you associate an endpoint to the VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="5c0fb-141">Sua assinatura só será cobrada por VIPs extras quando eles estiverem associados a um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="5c0fb-142">Para obter mais informações sobre preços, consulte [Preços de endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="5c0fb-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-to-associate-a-vip-to-an-endpoint"></a><span data-ttu-id="5c0fb-143">Como associar um VIP a um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="5c0fb-143">How to associate a VIP to an endpoint</span></span>

<span data-ttu-id="5c0fb-144">Para associar um VIP em um serviço de nuvem a um ponto de extremidade, execute o seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5c0fb-144">To associate a VIP on a cloud service to an endpoint, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="5c0fb-145">O comando cria um ponto de extremidade vinculado ao VIP denominado *Vip2* na porta *80* e o vincula à VM denominada *myVM1* em um serviço de nuvem denominado *myService* usando *TCP* na porta *8080*.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-145">The command creates an endpoint linked to the VIP called *Vip2* on port *80*, and links it to the VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="5c0fb-146">Para verificar a configuração, execute o seguinte comando PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5c0fb-146">To verify the configuration, run the following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="5c0fb-147">A saída deve ser semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="5c0fb-147">The output looks similar to the following example:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-to-enable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="5c0fb-148">Como habilitar balanceamento de carga em um VIP específico</span><span class="sxs-lookup"><span data-stu-id="5c0fb-148">How to enable load balancing on a specific VIP</span></span>

<span data-ttu-id="5c0fb-149">Você pode associar um único VIP com várias máquinas virtuais para fins de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="5c0fb-150">Por exemplo, você tem um serviço de nuvem chamado *myService* e duas máquinas virtuais chamadas *myVM1* e *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="5c0fb-151">E o serviço de nuvem tem vários VIPs, um deles chamado *Vip2*.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="5c0fb-152">Se você quiser garantir que todo o tráfego para a porta *81* no *Vip2* seja equilibrado entre *myVM1* e *myVM2* na porta *8181*, execute o seguinte script do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5c0fb-152">If you want to ensure that all traffic to port *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run the following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="5c0fb-153">Você também pode atualizar o balanceador de carga para usar um VIP diferente.</span><span class="sxs-lookup"><span data-stu-id="5c0fb-153">You can also update your load balancer to use a different VIP.</span></span> <span data-ttu-id="5c0fb-154">Por exemplo, se você executar o comando PowerShell a seguir, alterará o conjunto de balanceamento de carga para usar um VIP denominado Vip1:</span><span class="sxs-lookup"><span data-stu-id="5c0fb-154">For example, if you run the PowerShell command below, you will change the load balancing set to use a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="5c0fb-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5c0fb-155">Next Steps</span></span>

[<span data-ttu-id="5c0fb-156">Log Analytics para o Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5c0fb-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="5c0fb-157">Visão geral do balanceador de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="5c0fb-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="5c0fb-158">Introdução ao balanceador de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="5c0fb-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="5c0fb-159">Visão geral da Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="5c0fb-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="5c0fb-160">APIs REST com IP Reservado</span><span class="sxs-lookup"><span data-stu-id="5c0fb-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
