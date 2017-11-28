---
title: "aaaCreate interno do Azure PowerShell clássico de Balanceador - carregar | Microsoft Docs"
description: "Saiba como o toocreate um interno balanceador usando o PowerShell no modelo de implantação clássico Olá de carga"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a><span data-ttu-id="adef8-103">Introdução à criação de um balanceador de carga interno (clássico) usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="adef8-103">Get started creating an internal load balancer (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="adef8-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="adef8-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="adef8-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="adef8-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="adef8-106">Serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="adef8-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="adef8-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="adef8-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="adef8-108">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="adef8-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="adef8-109">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="adef8-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="adef8-110">Saiba como muito[executar essas etapas usando o modelo do Gerenciador de recursos de saudação](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="adef8-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="adef8-111">Criar um conjunto de balanceadores de carga internos para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="adef8-111">Create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="adef8-112">toocreate um balanceador de carga interno definido e Olá servidores que enviarão sua tooit de tráfego, você tem a seguir Olá toodo:</span><span class="sxs-lookup"><span data-stu-id="adef8-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you have toodo hello following:</span></span>

1. <span data-ttu-id="adef8-113">Crie uma instância de interno balanceamento de carga que será o ponto de extremidade de saudação da entrada tráfego toobe o balanceamento de carga servidores Olá de um conjunto com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="adef8-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="adef8-114">Adicione pontos de extremidade correspondente máquinas virtuais toohello que irá receber tráfego de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="adef8-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="adef8-115">Configure servidores de saudação que enviará Olá tráfego toobe com balanceamento de carga toosend seu tráfego toohello endereço IP virtual (VIP) da instância de balanceamento de carga interno de saudação.</span><span class="sxs-lookup"><span data-stu-id="adef8-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

### <a name="step-1-create-an-internal-load-balancing-instance"></a><span data-ttu-id="adef8-116">Etapa 1: criar uma instância de Balanceamento de Carga Interno</span><span class="sxs-lookup"><span data-stu-id="adef8-116">Step 1: Create an Internal Load Balancing instance</span></span>

<span data-ttu-id="adef8-117">Para um serviço de nuvem existente ou um serviço de nuvem implantado em uma rede virtual regional, você pode criar uma instância de balanceamento de carga interno com hello comandos do Windows PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="adef8-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with hello following Windows PowerShell commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

<span data-ttu-id="adef8-118">Observe que esse uso do hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Olá de parâmetros defaultprobe usa o cmdlet do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="adef8-118">Note that this use of hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses hello DefaultProbe parameter set.</span></span> <span data-ttu-id="adef8-119">Para obter mais informações sobre conjuntos de parâmetros adicionais, consulte [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="adef8-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span></span>

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a><span data-ttu-id="adef8-120">Etapa 2: Adicionar a instância de balanceamento de carga interno toohello de pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="adef8-120">Step 2: Add endpoints toohello Internal Load Balancing instance</span></span>

<span data-ttu-id="adef8-121">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="adef8-121">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a><span data-ttu-id="adef8-122">Etapa 3: Configurar seu servidores toosend seu tráfego toohello novo balanceamento de carga interno ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="adef8-122">Step 3: Configure your servers toosend their traffic toohello new Internal Load Balancing endpoint</span></span>

<span data-ttu-id="adef8-123">Muito configurados servidores Olá cujo tráfego é contínuo toobe com balanceamento de carga toouse Olá novo endereço IP (Olá VIP) do hello instância balanceamento de carga interno.</span><span class="sxs-lookup"><span data-stu-id="adef8-123">You have too configure hello servers whose traffic is going toobe load balanced toouse hello new IP address (hello VIP) of hello Internal Load Balancing instance.</span></span> <span data-ttu-id="adef8-124">Este é o endereço de saudação na qual Olá balanceamento de carga interno instância está escutando.</span><span class="sxs-lookup"><span data-stu-id="adef8-124">This is hello address on which hello Internal Load Balancing instance is listening.</span></span> <span data-ttu-id="adef8-125">Na maioria dos casos, você precisa toojust adicionar ou modificar um registro DNS para Olá VIP da instância de balanceamento de carga interno hello.</span><span class="sxs-lookup"><span data-stu-id="adef8-125">In most cases, you need toojust add or modify a DNS record for hello VIP of hello Internal Load Balancing instance.</span></span>

<span data-ttu-id="adef8-126">Se você especificou um endereço IP de saudação durante a criação de saudação da instância de balanceamento de carga interno Olá, você já tem Olá VIP.</span><span class="sxs-lookup"><span data-stu-id="adef8-126">If you specified hello IP address during hello creation of hello Internal Load Balancing instance, you already have hello VIP.</span></span> <span data-ttu-id="adef8-127">Caso contrário, você pode ver o VIP de saudação do hello comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="adef8-127">Otherwise, you can see hello VIP from hello following commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="adef8-128">toouse esses comandos, preencha os valores hello e remover hello < e >.</span><span class="sxs-lookup"><span data-stu-id="adef8-128">toouse these commands, fill in hello values and remove hello < and >.</span></span> <span data-ttu-id="adef8-129">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="adef8-129">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="adef8-130">De exibição de saudação do hello comando Get-AzureInternalLoadBalancer, observe o endereço IP hello e torne servidores do hello alterações necessárias tooyour ou tooensure de registros DNS que o tráfego seja enviado toohello VIP.</span><span class="sxs-lookup"><span data-stu-id="adef8-130">From hello display of hello Get-AzureInternalLoadBalancer command, note hello IP address and make hello necessary changes tooyour servers or DNS records tooensure that traffic gets sent toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="adef8-131">plataforma do Microsoft Azure Olá usa um endereço IPv4 estático, roteável publicamente para uma variedade de cenários administrativos.</span><span class="sxs-lookup"><span data-stu-id="adef8-131">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="adef8-132">endereço IP de saudação é 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="adef8-132">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="adef8-133">Esse endereço IP não deve ser bloqueado por nenhum firewall porque ele pode causar um comportamento inesperado.</span><span class="sxs-lookup"><span data-stu-id="adef8-133">This IP address should not be blocked by any firewalls, because it can cause unexpected behavior.</span></span>
> <span data-ttu-id="adef8-134">Com relação tooAzure de balanceamento de carga interno, esse endereço IP é usado pelo monitoramento de testes do estado de integridade de Olá Olá carga balanceador toodetermine para máquinas virtuais em um conjunto com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="adef8-134">With respect tooAzure Internal Load Balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load balanced set.</span></span> <span data-ttu-id="adef8-135">Se um grupo de segurança de rede é usada toorestrict tráfego tooAzure VMs em um conjunto de balanceamento de carga internamente ou tooa aplicada sub-rede de rede Virtual, certifique-se de que uma regra de segurança de rede é adicionada tooallow tráfego de 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="adef8-135">If a Network Security Group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa Virtual Network Subnet, ensure that a Network Security Rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="example-of-internal-load-balancing"></a><span data-ttu-id="adef8-136">Exemplo de balanceamento de carga interna</span><span class="sxs-lookup"><span data-stu-id="adef8-136">Example of internal load balancing</span></span>

<span data-ttu-id="adef8-137">toostep você Olá final tooend processo de criação de um conjunto com balanceamento de carga para duas configurações de exemplo, consulte Olá seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="adef8-137">toostep you through hello end-tooend process of creating a load-balanced set for two example configurations, see hello following sections.</span></span>

### <a name="an-internet-facing-multi-tier-application"></a><span data-ttu-id="adef8-138">Um aplicativo para a Internet de diversas camadas</span><span class="sxs-lookup"><span data-stu-id="adef8-138">An Internet facing, multi-tier application</span></span>

<span data-ttu-id="adef8-139">Você deseja tooprovide um serviço de banco de dados com balanceamento de carga para um conjunto de servidores web voltados para a Internet.</span><span class="sxs-lookup"><span data-stu-id="adef8-139">You want tooprovide a load balanced database service for  a set of Internet-facing web servers.</span></span> <span data-ttu-id="adef8-140">Os dois conjuntos de servidores são hospedados em um único serviço de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="adef8-140">Both sets of servers are hosted in a single Azure cloud service.</span></span> <span data-ttu-id="adef8-141">Servidor Web tráfego tooTCP porta 1433 deve ser distribuída entre duas máquinas virtuais na camada de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="adef8-141">Web server traffic tooTCP port 1433 must be distributed among two virtual machines in hello database tier.</span></span> <span data-ttu-id="adef8-142">A Figura 1 mostra a configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="adef8-142">Figure 1 shows hello configuration.</span></span>

![Conjunto com balanceamento de carga interno para a camada de banco de dados de saudação](./media/load-balancer-internal-getstarted/IC736321.png)

<span data-ttu-id="adef8-144">configuração de Olá consiste das seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="adef8-144">hello configuration consists of hello following:</span></span>

* <span data-ttu-id="adef8-145">serviço de nuvem existente Olá hospedar máquinas virtuais de saudação é denominado mytestcloud.</span><span class="sxs-lookup"><span data-stu-id="adef8-145">hello existing cloud service hosting hello virtual machines is named mytestcloud.</span></span>
* <span data-ttu-id="adef8-146">dois servidores de banco de dados existente Olá são nomeados DB1, DB2.</span><span class="sxs-lookup"><span data-stu-id="adef8-146">hello two existing database servers are named DB1, DB2.</span></span>
* <span data-ttu-id="adef8-147">Servidores Web na camada da web de saudação conectam toohello servidores de banco de dados na camada de banco de dados de saudação usando o endereço IP privado de saudação.</span><span class="sxs-lookup"><span data-stu-id="adef8-147">Web servers in hello web tier connect toohello database servers in hello database tier by using hello private IP address.</span></span> <span data-ttu-id="adef8-148">Outra opção é toouse seu próprio DNS para a rede virtual hello e registrar manualmente um registro a para o conjunto de Balanceador de carga interno hello.</span><span class="sxs-lookup"><span data-stu-id="adef8-148">Another option is toouse your own DNS for hello virtual network and manually register an A record for hello internal load balancer set.</span></span>

<span data-ttu-id="adef8-149">Olá, comandos a seguir configuram uma nova instância de balanceamento de carga interno denominada **ILBset** e adicione máquinas de virtuais toohello de pontos de extremidade correspondente toohello dois servidores de banco de dados:</span><span class="sxs-lookup"><span data-stu-id="adef8-149">hello following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints toohello virtual machines corresponding toohello two database servers:</span></span>

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a><span data-ttu-id="adef8-150">Remover uma configuração de Balanceamento de Carga Interno</span><span class="sxs-lookup"><span data-stu-id="adef8-150">Remove an Internal Load Balancing configuration</span></span>

<span data-ttu-id="adef8-151">tooremove uma máquina virtual como um ponto de extremidade de uma instância de Balanceador de carga interno, Olá use comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="adef8-151">tooremove a virtual machine as an endpoint from an internal load balancer instance, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="adef8-152">toouse esses comandos, preencha os valores hello, removendo hello < e >.</span><span class="sxs-lookup"><span data-stu-id="adef8-152">toouse these commands, fill in hello values, removing hello < and >.</span></span>

<span data-ttu-id="adef8-153">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="adef8-153">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="adef8-154">tooremove uma instância do balanceador de carga interno de um serviço de nuvem, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="adef8-154">tooremove an internal load balancer instance from a cloud service, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

<span data-ttu-id="adef8-155">toouse esses comandos, preencha valor hello e remova hello < e >.</span><span class="sxs-lookup"><span data-stu-id="adef8-155">toouse these commands, fill in hello value and remove hello < and >.</span></span>

<span data-ttu-id="adef8-156">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="adef8-156">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a><span data-ttu-id="adef8-157">Informações adicionais sobre cmdlets de balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="adef8-157">Additional information about internal load balancer cmdlets</span></span>

<span data-ttu-id="adef8-158">tooobtain informações adicionais sobre os cmdlets de balanceamento de carga interna, executados Olá comandos em um prompt do Windows PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="adef8-158">tooobtain additional information about Internal Load Balancing cmdlets, run hello following commands at a Windows PowerShell prompt:</span></span>

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a><span data-ttu-id="adef8-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="adef8-159">Next steps</span></span>

[<span data-ttu-id="adef8-160">Configurar um modo de distribuição do balanceador de carga usando a afinidade de IP de origem</span><span class="sxs-lookup"><span data-stu-id="adef8-160">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="adef8-161">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="adef8-161">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

