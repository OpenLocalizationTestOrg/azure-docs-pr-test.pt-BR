---
title: "aaaMutiple VIPs para um serviço de nuvem"
description: "Visão geral de multiVIP e como tooset vários VIPs em um serviço de nuvem"
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
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="67a81-103">Configurar vários VIPs para um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="67a81-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="67a81-104">Você pode acessar os serviços de nuvem do Azure sobre Olá Internet pública usando um endereço IP fornecida pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="67a81-104">You can access Azure cloud services over hello public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="67a81-105">Este endereço IP público é chamado tooas um VIP (IP virtual) pois ela está vinculada toohello Azure balanceador de carga e não Olá instâncias de máquina Virtual (VM) no serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="67a81-105">This public IP address is referred tooas a VIP (virtual IP) since it is linked toohello Azure load balancer, and not hello Virtual Machine (VM) instances within hello cloud service.</span></span> <span data-ttu-id="67a81-106">Você pode acessar qualquer instância VM dentro de um serviço de nuvem usando um único VIP.</span><span class="sxs-lookup"><span data-stu-id="67a81-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="67a81-107">No entanto, há situações em que talvez seja necessário mais de um VIP como um toohello de ponto de entrada mesmo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="67a81-107">However, there are scenarios in which you may need more than one VIP as an entry point toohello same cloud service.</span></span> <span data-ttu-id="67a81-108">Por exemplo, o serviço de nuvem pode hospedar vários sites que exigem conectividade SSL usando Olá porta padrão 443, como cada site é hospedado por um cliente diferente ou locatário.</span><span class="sxs-lookup"><span data-stu-id="67a81-108">For instance, your cloud service may host multiple websites that require SSL connectivity using hello default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="67a81-109">Nesse cenário, você precisa toohave um diferente endereço IP público para cada site.</span><span class="sxs-lookup"><span data-stu-id="67a81-109">In this scenario, you need toohave a different public facing IP address for each website.</span></span> <span data-ttu-id="67a81-110">Olá diagrama abaixo ilustra uma hospedagem web multilocatária típico com uma necessidade SSL vários certificados em Olá mesmo porta pública.</span><span class="sxs-lookup"><span data-stu-id="67a81-110">hello diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on hello same public port.</span></span>

![Cenário SSL de vários VIPs](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="67a81-112">No exemplo hello acima, a saudação de uso todos os VIPs mesma porta pública (443) e o tráfego é redirecionado tooone ou mais carga equilibradas VMs em uma porta privada exclusiva para o endereço IP interno de Olá Olá do serviço de nuvem hospedagem todos os sites de saudação.</span><span class="sxs-lookup"><span data-stu-id="67a81-112">In hello example above, all VIPs use hello same public port (443) and traffic is redirected tooone or more load balanced VMs on a unique private port for hello internal IP address of hello cloud service hosting all hello websites.</span></span>

> [!NOTE]
> <span data-ttu-id="67a81-113">Outra situação exigindo Olá use Olá vários VIPs está hospedando vários ouvintes de grupo de disponibilidade AlwaysOn do SQL no mesmo conjunto de máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="67a81-113">Another situation requiring hello use hello multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on hello same set of Virtual Machines.</span></span>

<span data-ttu-id="67a81-114">VIPs são dinâmicos por padrão, o que significa que o endereço IP real Olá atribuído toohello serviço de nuvem pode mudar ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="67a81-114">VIPs are dynamic by default, which means that hello actual IP address assigned toohello cloud service may change over time.</span></span> <span data-ttu-id="67a81-115">tooprevent que aconteça, você poderá reservar um VIP para seu serviço.</span><span class="sxs-lookup"><span data-stu-id="67a81-115">tooprevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="67a81-116">toolearn mais sobre o VIP reservado, consulte [IP público reservado](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="67a81-116">toolearn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="67a81-117">Consulte [Preços de endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses/) para obter informações sobre preços em VIPs e IPs reservados.</span><span class="sxs-lookup"><span data-stu-id="67a81-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="67a81-118">Você pode usar o PowerShell tooverify Olá VIPs usados por seus serviços de nuvem, bem como adicionar e remover VIPs, associar um ponto de extremidade do VIP tooan e configurar o balanceamento de carga em um VIP específico.</span><span class="sxs-lookup"><span data-stu-id="67a81-118">You can use PowerShell tooverify hello VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP tooan endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="67a81-119">Limitações</span><span class="sxs-lookup"><span data-stu-id="67a81-119">Limitations</span></span>

<span data-ttu-id="67a81-120">Neste momento, a funcionalidade de várias VIP é limitado toohello os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="67a81-120">At this time, Multi VIP functionality is limited toohello following scenarios:</span></span>

* <span data-ttu-id="67a81-121">**IaaS apenas**.</span><span class="sxs-lookup"><span data-stu-id="67a81-121">**IaaS only**.</span></span> <span data-ttu-id="67a81-122">Só é possível habilitar o Multi VIP para serviços de nuvem que contêm VMs.</span><span class="sxs-lookup"><span data-stu-id="67a81-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="67a81-123">Não é possível usar o Multi VIP em cenários de PaaS com instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="67a81-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="67a81-124">**PowerShell apenas**.</span><span class="sxs-lookup"><span data-stu-id="67a81-124">**PowerShell only**.</span></span> <span data-ttu-id="67a81-125">Só é possível gerenciar o Multi VIP usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="67a81-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="67a81-126">Essas limitações são temporárias e podem ser alteradas a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="67a81-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="67a81-127">Verifique se toorevisit essa página tooverify as alterações futuras.</span><span class="sxs-lookup"><span data-stu-id="67a81-127">Make sure toorevisit this page tooverify future changes.</span></span>

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a><span data-ttu-id="67a81-128">Como o serviço de nuvem tooa tooadd um VIP</span><span class="sxs-lookup"><span data-stu-id="67a81-128">How tooadd a VIP tooa cloud service</span></span>
<span data-ttu-id="67a81-129">serviço de tooyour tooadd um VIP, execute o hello comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="67a81-129">tooadd a VIP tooyour service, run hello following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="67a81-130">Este comando exibe uma toohello semelhante resultado exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="67a81-130">This command displays a result similar toohello following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a><span data-ttu-id="67a81-131">Como tooremove um VIP de um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="67a81-131">How tooremove a VIP from a cloud service</span></span>
<span data-ttu-id="67a81-132">Olá tooremove VIP adicionado tooyour serviço exemplo hello acima, Olá executar comandos do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="67a81-132">tooremove hello VIP added tooyour service in hello example above, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="67a81-133">Você só pode remover um VIP, se nenhum tooit de pontos de extremidade associados.</span><span class="sxs-lookup"><span data-stu-id="67a81-133">You can only remove a VIP if it has no endpoints associated tooit.</span></span>


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="67a81-134">Como as informações de tooretrieve VIP de um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="67a81-134">How tooretrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="67a81-135">Olá tooretrieve VIPs associado com um serviço de nuvem, executar Olá script do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="67a81-135">tooretrieve hello VIPs associated with a cloud service, run hello following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="67a81-136">script Hello exibe um toohello semelhante resultado exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="67a81-136">hello script displays a result similar toohello following sample:</span></span>

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

<span data-ttu-id="67a81-137">Neste exemplo, o serviço de nuvem Olá tem 3 VIPs:</span><span class="sxs-lookup"><span data-stu-id="67a81-137">In this example, hello cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="67a81-138">**Vip1** é Olá padrão VIP, você sabe que porque o valor Olá IsDnsProgrammedName é definido tootrue.</span><span class="sxs-lookup"><span data-stu-id="67a81-138">**Vip1** is hello default VIP, you know that because hello value for IsDnsProgrammedName is set tootrue.</span></span>
* <span data-ttu-id="67a81-139">**Vip2** e **Vip3** não são usados porque não têm endereços IP.</span><span class="sxs-lookup"><span data-stu-id="67a81-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="67a81-140">Eles só serão usados se você associar um ponto de extremidade toohello VIP.</span><span class="sxs-lookup"><span data-stu-id="67a81-140">They will only be used if you associate an endpoint toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="67a81-141">Sua assinatura só será cobrada por VIPs extras quando eles estiverem associados a um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="67a81-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="67a81-142">Para obter mais informações sobre preços, consulte [Preços de endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="67a81-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a><span data-ttu-id="67a81-143">Como ponto de extremidade de tooan tooassociate um VIP</span><span class="sxs-lookup"><span data-stu-id="67a81-143">How tooassociate a VIP tooan endpoint</span></span>

<span data-ttu-id="67a81-144">tooassociate um VIP em um nuvem serviço tooan ponto de extremidade, execute Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="67a81-144">tooassociate a VIP on a cloud service tooan endpoint, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="67a81-145">comando Hello cria um ponto de extremidade chamado VIP vinculado toohello *Vip2* na porta *80*e o vincula toohello VM denominada *myVM1* em um serviço de nuvem chamado  *myService* usando *TCP* na porta *8080*.</span><span class="sxs-lookup"><span data-stu-id="67a81-145">hello command creates an endpoint linked toohello VIP called *Vip2* on port *80*, and links it toohello VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="67a81-146">configuração tooverify hello, executar Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="67a81-146">tooverify hello configuration, run hello following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="67a81-147">saída de Hello parece semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="67a81-147">hello output looks similar toohello following example:</span></span>

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

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="67a81-148">Como tooenable o balanceamento de carga em um VIP específico</span><span class="sxs-lookup"><span data-stu-id="67a81-148">How tooenable load balancing on a specific VIP</span></span>

<span data-ttu-id="67a81-149">Você pode associar um único VIP com várias máquinas virtuais para fins de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="67a81-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="67a81-150">Por exemplo, você tem um serviço de nuvem chamado *myService* e duas máquinas virtuais chamadas *myVM1* e *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="67a81-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="67a81-151">E o serviço de nuvem tem vários VIPs, um deles chamado *Vip2*.</span><span class="sxs-lookup"><span data-stu-id="67a81-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="67a81-152">Se você quiser que todo o tráfego tooport de tooensure *81* na *Vip2* é equilibrada entre *myVM1* e *myVM2* na porta *8181* , execute hello script do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="67a81-152">If you want tooensure that all traffic tooport *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run hello following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="67a81-153">Você também pode atualizar o balanceador de carga toouse um VIP diferente.</span><span class="sxs-lookup"><span data-stu-id="67a81-153">You can also update your load balancer toouse a different VIP.</span></span> <span data-ttu-id="67a81-154">Por exemplo, se você executar Olá comando PowerShell a seguir, você alterará conjunto toouse um VIP denominado Vip1 de balanceamento de carga de saudação:</span><span class="sxs-lookup"><span data-stu-id="67a81-154">For example, if you run hello PowerShell command below, you will change hello load balancing set toouse a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="67a81-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="67a81-155">Next Steps</span></span>

[<span data-ttu-id="67a81-156">Log Analytics para o Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="67a81-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="67a81-157">Visão geral do balanceador de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="67a81-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="67a81-158">Introdução ao balanceador de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="67a81-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="67a81-159">Visão geral da Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="67a81-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="67a81-160">APIs REST com IP Reservado</span><span class="sxs-lookup"><span data-stu-id="67a81-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
