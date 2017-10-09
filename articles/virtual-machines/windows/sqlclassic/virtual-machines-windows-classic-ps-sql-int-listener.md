---
title: aaaConfigure um ouvinte ILB para grupos de disponibilidade AlwaysOn no Azure | Microsoft Docs
description: "Este tutorial usa recursos criados com o modelo de implantação clássico hello e cria um ouvinte de disponibilidade do grupo AlwaysOn no Azure que usa um balanceador de carga interno."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="464ca-103">Configurar um ouvinte de ILB para grupos de disponibilidade AlwaysOn no Azure</span><span class="sxs-lookup"><span data-stu-id="464ca-103">Configure an ILB listener for Always On availability groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="464ca-104">Ouvinte interno</span><span class="sxs-lookup"><span data-stu-id="464ca-104">Internal listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="464ca-105">Ouvinte externo</span><span class="sxs-lookup"><span data-stu-id="464ca-105">External listener</span></span>](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a><span data-ttu-id="464ca-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="464ca-106">Overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="464ca-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="464ca-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="464ca-108">Este artigo abrange o uso de saudação do modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="464ca-108">This article covers hello use of hello classic deployment model.</span></span> <span data-ttu-id="464ca-109">É recomendável que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="464ca-109">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="464ca-110">tooconfigure um ouvinte para um grupo de disponibilidade AlwaysOn no modelo do Gerenciador de recursos de hello, consulte [configurar um balanceador de carga para um grupo de disponibilidade AlwaysOn no Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="464ca-110">tooconfigure a listener for an Always On availability group in hello Resource Manager model, see [Configure a load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

<span data-ttu-id="464ca-111">O seu grupo de disponibilidade pode conter réplicas somente locais, somente no Azure ou tanto locais quanto no Azure para configurações híbridas.</span><span class="sxs-lookup"><span data-stu-id="464ca-111">Your availability group can contain replicas that are on-premises only or Azure only, or that span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="464ca-112">Réplicas do Azure podem residir em Olá mesma região ou em várias regiões que usam várias redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="464ca-112">Azure replicas can reside within hello same region or across multiple regions that use multiple virtual networks.</span></span> <span data-ttu-id="464ca-113">Olá procedimentos neste artigo presumem que você tenha já [configurado um grupo de disponibilidade](../classic/portal-sql-alwayson-availability-groups.md) , mas ainda não configurou um ouvinte.</span><span class="sxs-lookup"><span data-stu-id="464ca-113">hello procedures in this article assume that you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not yet configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-internal-listeners"></a><span data-ttu-id="464ca-114">Diretrizes e limitações para ouvintes internos</span><span class="sxs-lookup"><span data-stu-id="464ca-114">Guidelines and limitations for internal listeners</span></span>
<span data-ttu-id="464ca-115">uso de saudação de um balanceador de carga interno (ILB) com um ouvinte de grupo de disponibilidade no Azure é toohello assunto diretrizes a seguir:</span><span class="sxs-lookup"><span data-stu-id="464ca-115">hello use of an internal load balancer (ILB) with an availability group listener in Azure is subject toohello following guidelines:</span></span>

* <span data-ttu-id="464ca-116">há suporte para o ouvinte do grupo de disponibilidade Olá no Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="464ca-116">hello availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="464ca-117">Somente um ouvinte do grupo interno de disponibilidade é suportado para cada serviço de nuvem, pois ouvinte Olá configurado toohello ILB, e há apenas um ILB para cada serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="464ca-117">Only one internal availability group listener is supported for each cloud service, because hello listener is configured toohello ILB, and there is only one ILB for each cloud service.</span></span> <span data-ttu-id="464ca-118">No entanto, é possível toocreate vários ouvintes externos.</span><span class="sxs-lookup"><span data-stu-id="464ca-118">However, it is possible toocreate multiple external listeners.</span></span> <span data-ttu-id="464ca-119">Para obter mais informações, veja [Configurar um ouvinte externo para grupos de disponibilidade AlwaysOn no Azure](../classic/ps-sql-ext-listener.md).</span><span class="sxs-lookup"><span data-stu-id="464ca-119">For more information, see [Configure an external listener for Always On availability groups in Azure](../classic/ps-sql-ext-listener.md).</span></span>

## <a name="determine-hello-accessibility-of-hello-listener"></a><span data-ttu-id="464ca-120">Determinar a acessibilidade de saudação do ouvinte Olá</span><span class="sxs-lookup"><span data-stu-id="464ca-120">Determine hello accessibility of hello listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="464ca-121">Este artigo concentra-se na criação de um ouvinte que use um ILB.</span><span class="sxs-lookup"><span data-stu-id="464ca-121">This article focuses on creating a listener that uses an ILB.</span></span> <span data-ttu-id="464ca-122">Se você precisar de um ouvinte público ou externo, consulte versão Olá deste artigo que aborda a configuração de backup de um [ouvinte externo](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="464ca-122">If you need an public or external listener, see hello version of this article that discusses setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="464ca-123">Criar pontos de extremidade da VM com balanceamento de carga com retorno de servidor direto</span><span class="sxs-lookup"><span data-stu-id="464ca-123">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="464ca-124">Você primeiro crie um ILB, executando o script hello posteriormente nesta seção.</span><span class="sxs-lookup"><span data-stu-id="464ca-124">You first create an ILB by running hello script later in this section.</span></span>

<span data-ttu-id="464ca-125">Crie um ponto de extremidade com carga equilibrada para cada VM que hospeda uma réplica do Azure.</span><span class="sxs-lookup"><span data-stu-id="464ca-125">Create a load-balanced endpoint for each VM that hosts an Azure replica.</span></span> <span data-ttu-id="464ca-126">Se você tiver réplicas em várias regiões, cada réplica para essa região deve estar no mesmo serviço de nuvem de saudação Olá mesma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="464ca-126">If you have replicas in multiple regions, each replica for that region must be in hello same cloud service in hello same Azure virtual network.</span></span> <span data-ttu-id="464ca-127">A criação de réplicas do grupo de disponibilidade que abrangem várias regiões do Azure exige a configuração de diversas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="464ca-127">Creating availability group replicas that span multiple Azure regions requires configuring multiple virtual networks.</span></span> <span data-ttu-id="464ca-128">Para obter mais informações sobre como configurar cruzada conectividade de rede virtual, consulte [configurar conectividade de rede rede virtual toovirtual](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="464ca-128">For more information on configuring cross virtual network connectivity, see [Configure virtual network toovirtual network connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="464ca-129">No hello portal do Azure, vá tooeach VM que hospeda uma réplica tooview Olá os detalhes.</span><span class="sxs-lookup"><span data-stu-id="464ca-129">In hello Azure portal, go tooeach VM that hosts a replica tooview hello details.</span></span>

2. <span data-ttu-id="464ca-130">Clique em Olá **pontos de extremidade** guia para cada VM.</span><span class="sxs-lookup"><span data-stu-id="464ca-130">Click hello **Endpoints** tab for each VM.</span></span>

3. <span data-ttu-id="464ca-131">Verifique se esse Olá **nome** e **porta pública** do ponto de extremidade de escuta Olá que você deseja toouse não já estão em uso.</span><span class="sxs-lookup"><span data-stu-id="464ca-131">Verify that hello **Name** and **Public Port** of hello listener endpoint that you want toouse are not already in use.</span></span> <span data-ttu-id="464ca-132">O exemplo hello nesta seção, Olá nome é *MyEndpoint*, e porta Olá *1433*.</span><span class="sxs-lookup"><span data-stu-id="464ca-132">In hello example in this section, hello name is *MyEndpoint*, and hello port is *1433*.</span></span>

4. <span data-ttu-id="464ca-133">No cliente local, baixe e instale o hello mais recente [módulo PowerShell](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="464ca-133">On your local client, download and install hello latest [PowerShell module](https://azure.microsoft.com/downloads/).</span></span>

5. <span data-ttu-id="464ca-134">Iniciar o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="464ca-134">Start Azure PowerShell.</span></span>  
    <span data-ttu-id="464ca-135">Abre uma nova sessão do PowerShell, com hello Azure administrativos módulos carregados.</span><span class="sxs-lookup"><span data-stu-id="464ca-135">A new PowerShell session opens, with hello Azure administrative modules loaded.</span></span>

6. <span data-ttu-id="464ca-136">Execute `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="464ca-136">Run `Get-AzurePublishSettingsFile`.</span></span> <span data-ttu-id="464ca-137">Esse cmdlet direciona toodownload de navegador tooa um diretório local tooa de arquivo publicar configurações.</span><span class="sxs-lookup"><span data-stu-id="464ca-137">This cmdlet directs you tooa browser toodownload a publish settings file tooa local directory.</span></span> <span data-ttu-id="464ca-138">Talvez você receba uma solicitação para inserir as suas credenciais de entrada de sua assinatura do Aure.</span><span class="sxs-lookup"><span data-stu-id="464ca-138">You might be prompted for your sign-in credentials for your Azure subscription.</span></span>

7. <span data-ttu-id="464ca-139">Execute seguinte Olá `Import-AzurePublishSettingsFile` comando com caminho Olá Olá Publicar arquivo de configurações que você baixou:</span><span class="sxs-lookup"><span data-stu-id="464ca-139">Run hello following `Import-AzurePublishSettingsFile` command with hello path of hello publish settings file that you downloaded:</span></span>

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    <span data-ttu-id="464ca-140">Depois de publicar Olá arquivo de configurações é importado, você pode gerenciar sua assinatura do Azure na sessão do PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="464ca-140">After hello publish settings file is imported, you can manage your Azure subscription in hello PowerShell session.</span></span>

8. <span data-ttu-id="464ca-141">Para o *ILB*, atribua um endereço IP estático.</span><span class="sxs-lookup"><span data-stu-id="464ca-141">For *ILB*, assign a static IP address.</span></span> <span data-ttu-id="464ca-142">Examine a configuração atual de rede virtual Olá executando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="464ca-142">Examine hello current virtual network configuration by running hello following command:</span></span>

        (Get-AzureVNetConfig).XMLConfiguration
9. <span data-ttu-id="464ca-143">Saudação de Observação *sub-rede* nome para a sub-rede de saudação que contém Olá VMs que hospedam réplicas de saudação.</span><span class="sxs-lookup"><span data-stu-id="464ca-143">Note hello *Subnet* name for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="464ca-144">Esse nome é usado no parâmetro hello $SubnetName no script hello.</span><span class="sxs-lookup"><span data-stu-id="464ca-144">This name is used in hello $SubnetName parameter in hello script.</span></span>

10. <span data-ttu-id="464ca-145">Saudação de Observação *VirtualNetworkSite* nomear e Olá iniciando *AddressPrefix* para a sub-rede de saudação que contém Olá VMs que hospedam réplicas de saudação.</span><span class="sxs-lookup"><span data-stu-id="464ca-145">Note hello *VirtualNetworkSite* name and hello starting *AddressPrefix* for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="464ca-146">Procure um endereço IP disponível, passando os dois valores toohello `Test-AzureStaticVNetIP` comando e examinando Olá *AvailableAddresses*.</span><span class="sxs-lookup"><span data-stu-id="464ca-146">Look for an available IP address by passing both values toohello `Test-AzureStaticVNetIP` command and by examining hello *AvailableAddresses*.</span></span> <span data-ttu-id="464ca-147">Por exemplo, se hello rede virtual é chamada *MyVNet* e tem um intervalo de endereços de sub-rede que começa em *172.16.0.128*, seguinte Olá comando lista os endereços disponíveis:</span><span class="sxs-lookup"><span data-stu-id="464ca-147">For example, if hello virtual network is named *MyVNet* and has a subnet address range that starts at *172.16.0.128*, hello following command would list available addresses:</span></span>

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. <span data-ttu-id="464ca-148">Selecione um dos endereços disponíveis hello e usá-lo no parâmetro hello $ILBStaticIP do script hello na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="464ca-148">Select one of hello available addresses, and use it in hello $ILBStaticIP parameter of hello script in hello next step.</span></span>

12. <span data-ttu-id="464ca-149">Copiar Olá editor de texto de tooa de script do PowerShell a seguir e defina Olá valores de variáveis toosuit seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="464ca-149">Copy hello following PowerShell script tooa text editor, and set hello variable values toosuit your environment.</span></span> <span data-ttu-id="464ca-150">Alguns parâmetros já receberam valores padrão.</span><span class="sxs-lookup"><span data-stu-id="464ca-150">Defaults have been provided for some parameters.</span></span>  

    <span data-ttu-id="464ca-151">Observe que as implantações existentes que usam grupos de afinidade não podem adicionar o ILB.</span><span class="sxs-lookup"><span data-stu-id="464ca-151">Existing deployments that use affinity groups cannot add an ILB.</span></span> <span data-ttu-id="464ca-152">Para saber mais sobre os requisitos do ILB, consulte [Visão geral do balanceador de carga interno](../../../load-balancer/load-balancer-internal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="464ca-152">For more information about ILB requirements, see [Internal load balancer overview](../../../load-balancer/load-balancer-internal-overview.md).</span></span>

    <span data-ttu-id="464ca-153">Além disso, se seu grupo de disponibilidade abranger regiões do Azure, você deve executar script hello uma vez em cada data center para o serviço de nuvem hello e nós que residem nesse datacenter.</span><span class="sxs-lookup"><span data-stu-id="464ca-153">Also, if your availability group spans Azure regions, you must run hello script once in each datacenter for hello cloud service and nodes that reside in that datacenter.</span></span>

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. <span data-ttu-id="464ca-154">Depois que você tiver definido as variáveis de Olá, Olá cópia script de saudação texto editor tooyour PowerShell sessão toorun-lo.</span><span class="sxs-lookup"><span data-stu-id="464ca-154">After you have set hello variables, copy hello script from hello text editor tooyour PowerShell session toorun it.</span></span> <span data-ttu-id="464ca-155">Se ainda mostrará o prompt Olá  **>>** , pressione Enter novamente se script de saudação toomake começa a ser executado.</span><span class="sxs-lookup"><span data-stu-id="464ca-155">If hello prompt still shows **>>**, press Enter again toomake sure hello script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="464ca-156">Verifique se KB2854082 está instalado, se necessário</span><span class="sxs-lookup"><span data-stu-id="464ca-156">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="464ca-157">Abrir as portas de firewall Olá em nós do grupo de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="464ca-157">Open hello firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a><span data-ttu-id="464ca-158">Criar o ouvinte do grupo de disponibilidade Olá</span><span class="sxs-lookup"><span data-stu-id="464ca-158">Create hello availability group listener</span></span>

<span data-ttu-id="464ca-159">Crie o ouvinte do grupo de disponibilidade de saudação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="464ca-159">Create hello availability group listener in two steps.</span></span> <span data-ttu-id="464ca-160">Primeiro, crie o recurso de cluster de ponto de acesso do hello cliente e configurar as dependências.</span><span class="sxs-lookup"><span data-stu-id="464ca-160">First, create hello client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="464ca-161">Em seguida, configure recursos de cluster Olá no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="464ca-161">Second, configure hello cluster resources in PowerShell.</span></span>

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a><span data-ttu-id="464ca-162">Criar ponto de acesso para cliente hello e configurar dependências de saudação de cluster</span><span class="sxs-lookup"><span data-stu-id="464ca-162">Create hello client access point and configure hello cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a><span data-ttu-id="464ca-163">Configurar recursos de cluster Olá no PowerShell</span><span class="sxs-lookup"><span data-stu-id="464ca-163">Configure hello cluster resources in PowerShell</span></span>
1. <span data-ttu-id="464ca-164">Para ILB, você deve usar o endereço IP de saudação do hello ILB criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="464ca-164">For ILB, you must use hello IP address of hello ILB that was created earlier.</span></span> <span data-ttu-id="464ca-165">tooobtain esse IP endereço no PowerShell, use Olá script a seguir:</span><span class="sxs-lookup"><span data-stu-id="464ca-165">tooobtain this IP address in PowerShell, use hello following script:</span></span>

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. <span data-ttu-id="464ca-166">Em um dos Olá VMs, copie o script do PowerShell de saudação para seu editor de texto de tooa do sistema operacional e então definir variáveis de saudação toohello valores anotados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="464ca-166">On one of hello VMs, copy hello PowerShell script for your operating system tooa text editor, and then set hello variables toohello values you noted earlier.</span></span>

    <span data-ttu-id="464ca-167">Para o Windows Server 2012 ou posterior, use Olá script a seguir:</span><span class="sxs-lookup"><span data-stu-id="464ca-167">For Windows Server 2012 or later, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    <span data-ttu-id="464ca-168">Para Windows Server 2008 R2, use Olá script a seguir:</span><span class="sxs-lookup"><span data-stu-id="464ca-168">For Windows Server 2008 R2, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. <span data-ttu-id="464ca-169">Depois de ter conjunto Olá variáveis, abra uma janela elevada do Windows PowerShell, Olá colar o script do editor de texto de saudação em seu toorun de sessão do PowerShell-lo.</span><span class="sxs-lookup"><span data-stu-id="464ca-169">After you have set hello variables, open an elevated Windows PowerShell window, paste hello script from hello text editor into your PowerShell session toorun it.</span></span> <span data-ttu-id="464ca-170">Se ainda mostrará o prompt Olá  **>>** , pressione Enter novamente toomake-se de que o script hello inicia em execução.</span><span class="sxs-lookup"><span data-stu-id="464ca-170">If hello prompt still shows **>>**, Press Enter again toomake sure that hello script starts running.</span></span>

4. <span data-ttu-id="464ca-171">Repita Olá etapas anteriores para cada VM.</span><span class="sxs-lookup"><span data-stu-id="464ca-171">Repeat hello preceding steps for each VM.</span></span>  
    <span data-ttu-id="464ca-172">Esse script configura o recurso de endereço IP hello com o endereço IP Olá Olá do serviço de nuvem e define outros parâmetros, como a porta de investigação de saudação.</span><span class="sxs-lookup"><span data-stu-id="464ca-172">This script configures hello IP address resource with hello IP address of hello cloud service and sets other parameters, such as hello probe port.</span></span> <span data-ttu-id="464ca-173">Quando o recurso de endereço IP hello é colocado online, ele pode responder toohello sondagem na porta de investigação de saudação do ponto de extremidade com balanceamento de carga Olá que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="464ca-173">When hello IP address resource is brought online, it can respond toohello polling on hello probe port from hello load-balanced endpoint that you created earlier.</span></span>

## <a name="bring-hello-listener-online"></a><span data-ttu-id="464ca-174">Coloque o ouvinte Olá online</span><span class="sxs-lookup"><span data-stu-id="464ca-174">Bring hello listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="464ca-175">Itens de acompanhamento</span><span class="sxs-lookup"><span data-stu-id="464ca-175">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a><span data-ttu-id="464ca-176">Ouvinte de grupo de disponibilidade do teste hello (Olá na mesma rede virtual)</span><span class="sxs-lookup"><span data-stu-id="464ca-176">Test hello availability group listener (within hello same virtual network)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a><span data-ttu-id="464ca-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="464ca-177">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
