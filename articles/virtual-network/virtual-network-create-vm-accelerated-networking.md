---
title: "Criar uma máquina virtual do Azure com Rede Acelerada | Microsoft Docs"
description: "Saiba como criar uma máquina virtual com Rede Acelerada."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 449425189a3b42dcb2c31316c1c8e38fac69d761
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a><span data-ttu-id="2fd67-103">Criar uma máquina virtual com Rede Acelerada</span><span class="sxs-lookup"><span data-stu-id="2fd67-103">Create a virtual machine with Accelerated Networking</span></span>

<span data-ttu-id="2fd67-104">Neste tutorial, você aprenderá a criar uma VM (máquina Virtual) do Azure com Rede Acelerada.</span><span class="sxs-lookup"><span data-stu-id="2fd67-104">In this tutorial, you learn how to create an Azure Virtual Machine (VM) with Accelerated Networking.</span></span> <span data-ttu-id="2fd67-105">A Rede Acelerada é GA para Windows e em uma Visualização Pública para distribuições específicas do Linux.</span><span class="sxs-lookup"><span data-stu-id="2fd67-105">Accelerated Networking is GA for Windows and in a Public Preview for specific Linux distributions.</span></span> <span data-ttu-id="2fd67-106">Rede acelerada permite SR-IOV (virtualização de E/S de raiz única) para uma VM, melhorando muito seu desempenho de rede.</span><span class="sxs-lookup"><span data-stu-id="2fd67-106">Accelerated networking enables single root I/O virtualization (SR-IOV) to a VM, greatly improving its networking performance.</span></span> <span data-ttu-id="2fd67-107">Esse caminho de alto desempenho ignora o host do caminho de dados, reduzindo a latência, a tremulação e a utilização da CPU para uso com as cargas de trabalho de rede mais exigentes nos tipos de VM com suporte.</span><span class="sxs-lookup"><span data-stu-id="2fd67-107">This high-performance path bypasses the host from the datapath reducing latency, jitter, and CPU utilization, for use with the most demanding network workloads on supported VM types.</span></span> <span data-ttu-id="2fd67-108">A figura abaixo mostra a comunicação entre duas VMs (máquinas virtuais) com e sem rede acelerada:</span><span class="sxs-lookup"><span data-stu-id="2fd67-108">The following picture shows communication between two virtual machines (VM) with and without accelerated networking:</span></span>

![Comparação](./media/virtual-network-create-vm-accelerated-networking/image1.png)

<span data-ttu-id="2fd67-110">Sem rede acelerada, todo o tráfego de rede que entra e sai da VM deve cruzar o host e o comutador virtual.</span><span class="sxs-lookup"><span data-stu-id="2fd67-110">Without accelerated networking, all networking traffic in and out of the VM must traverse the host and the virtual switch.</span></span> <span data-ttu-id="2fd67-111">O comutador virtual fornece toda a imposição de política, como grupos de segurança de rede, listas de controle de acesso, isolamento e outros serviços virtualizados de rede para tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="2fd67-111">The virtual switch provides all policy enforcement, such as network security groups, access control lists, isolation, and other network virtualized services to network traffic.</span></span> <span data-ttu-id="2fd67-112">Para saber mais sobre comutadores virtuais, leia o artigo [Virtualização de rede Hyper-V e comutador virtual](https://technet.microsoft.com/library/jj945275.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fd67-112">To learn more about virtual switches, read the [Hyper-V network virtualization and virtual switch](https://technet.microsoft.com/library/jj945275.aspx) article.</span></span>

<span data-ttu-id="2fd67-113">Com Rede Acelerada, o tráfego de rede chega à NIC (interface de rede) da VM e então é encaminhado para a VM.</span><span class="sxs-lookup"><span data-stu-id="2fd67-113">With accelerated networking, network traffic arrives at the VM's network interface (NIC), and is then forwarded to the VM.</span></span> <span data-ttu-id="2fd67-114">Todas as políticas de rede que o comutador virtual aplica sem rede acelerada são descarregadas e aplicadas em hardware.</span><span class="sxs-lookup"><span data-stu-id="2fd67-114">All network policies that the virtual switch applies without accelerated networking are offloaded and applied in hardware.</span></span> <span data-ttu-id="2fd67-115">Aplicar a política de hardware permite que a NIC encaminhe tráfego de rede diretamente à VM, ignorando o host e o comutador virtual, mantendo toda a política que aplicou no host.</span><span class="sxs-lookup"><span data-stu-id="2fd67-115">Applying policy in hardware enables the NIC to forward network traffic directly to the VM, bypassing the host and the virtual switch, while maintaining all the policy it applied in the host.</span></span>

<span data-ttu-id="2fd67-116">Os benefícios da rede acelerada aplicam-se somente à VM em que ela está habilitada.</span><span class="sxs-lookup"><span data-stu-id="2fd67-116">The benefits of accelerated networking only apply to the VM that it is enabled on.</span></span> <span data-ttu-id="2fd67-117">Para obter melhores resultados, é ideal habilitar esse recurso em pelo menos duas VMs conectadas à mesma VNet (rede virtual) do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd67-117">For the best results, it is ideal to enable this feature on at least two VMs connected to the same Azure Virtual Network (VNet).</span></span> <span data-ttu-id="2fd67-118">Ao se comunicar entre VNets ou fazer conexão local, esse recurso tem impacto mínimo sobre a latência geral.</span><span class="sxs-lookup"><span data-stu-id="2fd67-118">When communicating across VNets or connecting on-premises, this feature has minimal impact to overall latency.</span></span>

> [!WARNING]
> <span data-ttu-id="2fd67-119">A Visualização Pública do Linux pode não ter o mesmo nível de disponibilidade e confiabilidade que os recursos que estão na versão de disponibilidade geral.</span><span class="sxs-lookup"><span data-stu-id="2fd67-119">This Linux Public Preview may not have the same level of availability and reliability as features that are in general availability release.</span></span> <span data-ttu-id="2fd67-120">Não há suporte para o recurso, o recurso pode ter funcionalidades restritas e ele pode não estar disponível em todas as localizações do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd67-120">The feature is not supported, may have constrained capabilities, and may not be available in all Azure locations.</span></span> <span data-ttu-id="2fd67-121">Para obter as notificações mais atualizadas sobre a disponibilidade e o status desse recurso, confira a página de atualizações da Rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd67-121">For the most up-to-date notifications on availability and status of this feature, check the Azure Virtual Network updates page.</span></span>

## <a name="benefits"></a><span data-ttu-id="2fd67-122">Benefícios</span><span class="sxs-lookup"><span data-stu-id="2fd67-122">Benefits</span></span>
* <span data-ttu-id="2fd67-123">**Latência menor/mais pps (pacotes por segundo):** remover o comutador virtual do caminho de dados elimina o tempo que os pacotes gastam no host para processamento da política e aumenta o número de pacotes que podem ser processados dentro da VM.</span><span class="sxs-lookup"><span data-stu-id="2fd67-123">**Lower Latency / Higher packets per second (pps):** Removing the virtual switch from the datapath removes the time packets spend in the host for policy processing and increases the number of packets that can be processed inside the VM.</span></span>
* <span data-ttu-id="2fd67-124">**Tremulação reduzida:** processamento de comutador virtual depende da quantidade de política que precisa ser aplicada e da carga de trabalho da CPU que está fazendo o processamento.</span><span class="sxs-lookup"><span data-stu-id="2fd67-124">**Reduced jitter:** Virtual switch processing depends on the amount of policy that needs to be applied and the workload of the CPU that is doing the processing.</span></span> <span data-ttu-id="2fd67-125">O descarregamento da imposição de política para o hardware remove essa variabilidade ao entregar pacotes diretamente à VM, removendo a comunicação do host para a VM e todas as interrupções e mudanças de contexto de software.</span><span class="sxs-lookup"><span data-stu-id="2fd67-125">Offloading the policy enforcement to the hardware removes that variability by delivering packets directly to the VM, removing the host to VM communication and all software interrupts and context switches.</span></span>
* <span data-ttu-id="2fd67-126">**Menor utilização da CPU:** ignorar o comutador virtual no host resulta em menor utilização da CPU para processar o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="2fd67-126">**Decreased CPU utilization:** Bypassing the virtual switch in the host leads to less CPU utilization for processing network traffic.</span></span>

## <span data-ttu-id="2fd67-127"><a name="Limitations"></a>Limitações</span><span class="sxs-lookup"><span data-stu-id="2fd67-127"><a name="Limitations"></a>Limitations</span></span>
<span data-ttu-id="2fd67-128">Existem as seguintes limitações ao usar essa funcionalidade:</span><span class="sxs-lookup"><span data-stu-id="2fd67-128">The following limitations exist when using this capability:</span></span>

* <span data-ttu-id="2fd67-129">**Criação de interface de rede:** rede acelerada só pode ser habilitada para uma NIC nova.</span><span class="sxs-lookup"><span data-stu-id="2fd67-129">**Network interface creation:** Accelerated networking can only be enabled for a new NIC.</span></span> <span data-ttu-id="2fd67-130">Não pode ser habilitada para uma NIC existente.</span><span class="sxs-lookup"><span data-stu-id="2fd67-130">It cannot be enabled for an existing NIC.</span></span>
* <span data-ttu-id="2fd67-131">**Criação da VM:** uma NIC com rede acelerada habilitada somente poderá ser conectada a uma VM quando a VM for criada.</span><span class="sxs-lookup"><span data-stu-id="2fd67-131">**VM creation:** A NIC with accelerated networking enabled can only be attached to a VM when the VM is created.</span></span> <span data-ttu-id="2fd67-132">A NIC não pode ser anexada a uma VM existente.</span><span class="sxs-lookup"><span data-stu-id="2fd67-132">The NIC cannot be attached to an existing VM.</span></span>
* <span data-ttu-id="2fd67-133">**Regiões:** VMs do Windows com rede acelerada são oferecidas na maioria das regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd67-133">**Regions:** Windows VMs with accelerated networking are offered in most Azure regions.</span></span> <span data-ttu-id="2fd67-134">VMs do Linux com rede acelerada são oferecidas em várias regiões.</span><span class="sxs-lookup"><span data-stu-id="2fd67-134">Linux VMs with accelerated networking are offered in multiple regions.</span></span> <span data-ttu-id="2fd67-135">As regiões em que essa capacidade está disponível estão em expansão.</span><span class="sxs-lookup"><span data-stu-id="2fd67-135">The regions this capability is available in is expanding.</span></span> <span data-ttu-id="2fd67-136">Consulte o blog de Atualizações de Rede Virtual do Azure abaixo para encontrar as informações mais recentes.</span><span class="sxs-lookup"><span data-stu-id="2fd67-136">Please see the Azure Virtual Networking Updates blog below for the latest information.</span></span>   
* <span data-ttu-id="2fd67-137">**Sistemas operacionais com suporte:** Windows: Microsoft Windows Server 2012 R2 Datacenter e Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="2fd67-137">**Supported operating systems:** Windows: Microsoft Windows Server 2012 R2 Datacenter and Windows Server 2016.</span></span> <span data-ttu-id="2fd67-138">Linux: Ubuntu Server 16.04 LTS com kernel 4.4.0-77 ou superior, SLES 12 SP2, RHEL 7.3 e CentOS 7.3 (publicado por "Rogue Wave Software").</span><span class="sxs-lookup"><span data-stu-id="2fd67-138">Linux: Ubuntu Server 16.04 LTS with kernel 4.4.0-77 or higher, SLES 12 SP2, RHEL 7.3 and CentOS 7.3 (Published by “Rogue Wave Software”).</span></span>
* <span data-ttu-id="2fd67-139">**Tamanho da VM:** tamanhos de instância com computação otimizada e de finalidade geral com oito ou mais núcleos.</span><span class="sxs-lookup"><span data-stu-id="2fd67-139">**VM Size:** General purpose and compute-optimized instance sizes with eight or more cores.</span></span> <span data-ttu-id="2fd67-140">Para obter mais informações, consulte os artigos de tamanhos de VM [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) e [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2fd67-140">For more information, see the [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM sizes articles.</span></span> <span data-ttu-id="2fd67-141">O conjunto de tamanhos de instância VM com suporte será expandido no futuro.</span><span class="sxs-lookup"><span data-stu-id="2fd67-141">The set of supported VM instance sizes will expand in the future.</span></span>
* <span data-ttu-id="2fd67-142">**Implantação somente por meio do ARM (Azure Resource Manager):** a Rede Acelerada não está disponível para implantação por meio do ASM/RDFE.</span><span class="sxs-lookup"><span data-stu-id="2fd67-142">**Deployment through Azure Resource Manager (ARM) only:** Accelerated Networking is not available for deployment through ASM/RDFE.</span></span>

<span data-ttu-id="2fd67-143">Alterações a essas limitações serão anunciadas na página [Atualizações de Rede Virtual do Azure](https://azure.microsoft.com/updates/accelerated-networking-in-preview).</span><span class="sxs-lookup"><span data-stu-id="2fd67-143">Changes to these limitations are announced through the [Azure Virtual Networking updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="2fd67-144">Criar uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="2fd67-144">Create a Windows VM</span></span>
<span data-ttu-id="2fd67-145">Você pode usar o portal do Azure ou o Azure [PowerShell](#windows-powershell) para criar a VM.</span><span class="sxs-lookup"><span data-stu-id="2fd67-145">You can use the Azure portal or Azure [PowerShell](#windows-powershell) to create the VM.</span></span>

### <span data-ttu-id="2fd67-146"><a name="windows-portal"></a>Portal</span><span class="sxs-lookup"><span data-stu-id="2fd67-146"><a name="windows-portal"></a>Portal</span></span>

1. <span data-ttu-id="2fd67-147">Em um navegador da Internet, abra o [portal](https://portal.azure.com) do Azure e entre com a sua [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd67-147">From an Internet browser, open the Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="2fd67-148">Caso ainda não tenha uma conta, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="2fd67-148">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="2fd67-149">No portal, clique em **+ Novo** > **Computação** > **Windows Server Datacenter 2016**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-149">In the portal, click **+ New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
3. <span data-ttu-id="2fd67-150">Na folha do **Windows Server Datacenter 2016** exibida, deixe *Resource Manager* selecionado em **Selecionar um modelo de implantação** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-150">In the **Windows Server 2016 Datacenter** blade that appears, leave *Resource Manager* selected under **Select a deployment model**, and click **Create**.</span></span>
4. <span data-ttu-id="2fd67-151">Na folha **Fundamentos** que aparece, digite os seguintes valores, deixe as opções padrão restantes ou selecione ou insira seus próprios valores e clique no botão **OK**:</span><span class="sxs-lookup"><span data-stu-id="2fd67-151">In the **Basics** blade that appears, enter the following values, leave the remaining default options or select or enter your own values, and click the **OK** button:</span></span>

    |<span data-ttu-id="2fd67-152">Configuração</span><span class="sxs-lookup"><span data-stu-id="2fd67-152">Setting</span></span>|<span data-ttu-id="2fd67-153">Valor</span><span class="sxs-lookup"><span data-stu-id="2fd67-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="2fd67-154">Nome</span><span class="sxs-lookup"><span data-stu-id="2fd67-154">Name</span></span>|<span data-ttu-id="2fd67-155">MyVm</span><span class="sxs-lookup"><span data-stu-id="2fd67-155">MyVm</span></span>|
    |<span data-ttu-id="2fd67-156">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2fd67-156">Resource group</span></span>|<span data-ttu-id="2fd67-157">Deixe **Criar novo** selecionado e digite *MyResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="2fd67-157">Leave **Create new** selected and enter *MyResourceGroup*</span></span>|
    |<span data-ttu-id="2fd67-158">Local</span><span class="sxs-lookup"><span data-stu-id="2fd67-158">Location</span></span>|<span data-ttu-id="2fd67-159">Oeste dos EUA 2</span><span class="sxs-lookup"><span data-stu-id="2fd67-159">West US 2</span></span>|

    <span data-ttu-id="2fd67-160">Se você for novo no Azure, saiba mais sobre [Grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [assinaturas](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) e [locais](https://azure.microsoft.com/regions) (que também são chamados de regiões).</span><span class="sxs-lookup"><span data-stu-id="2fd67-160">If you're new to Azure, learn more about [Resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (which are also referred to as regions).</span></span>
5. <span data-ttu-id="2fd67-161">Na folha **Escolher um tamanho** que aparece, digite *8* na caixa **Mínimo de núcleos** e, em seguida, clique em **Exibir tudo**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-161">In the **Choose a size** blade that appears, enter *8* in the **Minimum cores** box, then click **View all**.</span></span>
6. <span data-ttu-id="2fd67-162">Clique em **DS4_V2 Standard** ou em qualquer VM com suporte e clique no botão **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-162">Click **DS4_V2 Standard**, or any supported VM, then click the **Select** button.</span></span>
7. <span data-ttu-id="2fd67-163">Na folha **Configurações** exibida, deixe todas as configurações como estão, porém, clique em **Habilitado** em **Rede acelerada** e depois clique no botão **OK**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-163">In the **Settings** blade that appears, leave all settings as-is, except click **Enabled** under **Accelerated networking**, then click the **OK** button.</span></span> <span data-ttu-id="2fd67-164">**Observação:** se, nas etapas anteriores, você tiver selecionado valores de tamanho, sistema operacional ou local da VM que não estejam listados na seção [Limitações](#Limitations) deste artigo, **Rede acelerada** não estará visível.</span><span class="sxs-lookup"><span data-stu-id="2fd67-164">**Note:** If, in previous steps, you selected values for VM size, operating system, or location that aren't listed in the [Limitations](#Limitations) section of this article, **Accelerated networking** isn't visible.</span></span>
8. <span data-ttu-id="2fd67-165">Na folha **Resumo** que aparece, clique no botão **OK**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-165">In the **Summary** blade that appears, click the **OK** button.</span></span> <span data-ttu-id="2fd67-166">O Azure começa a criar a VM.</span><span class="sxs-lookup"><span data-stu-id="2fd67-166">Azure starts creating the VM.</span></span> <span data-ttu-id="2fd67-167">A criação da VM leva alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2fd67-167">VM creation takes a few minutes.</span></span>
9. <span data-ttu-id="2fd67-168">Para instalar o driver de rede acelerado para Windows, conclua as etapas na seção [Configurar o Windows](#configure-windows) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2fd67-168">To install the accelerated networking driver for Windows, complete the steps in the [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="2fd67-169"><a name="windows-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd67-169"><a name="windows-powershell"></a>PowerShell</span></span>
1. <span data-ttu-id="2fd67-170">Instale a versão mais recente do módulo [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2fd67-170">Install the latest version of the Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="2fd67-171">Se você for novo no Azure PowerShell, leia o artigo [Visão geral do Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2fd67-171">If you're new to Azure PowerShell, read the [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="2fd67-172">Inicie uma sessão do PowerShell clicando no botão Iniciar do Windows, digitando **powershell** e, em seguida, clicando em **PowerShell** nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="2fd67-172">Start a PowerShell session by clicking the Windows Start button, typing **powershell**, then clicking **PowerShell** from the search results.</span></span>
3. <span data-ttu-id="2fd67-173">Na janela do PowerShell, digite o comando `login-azurermaccount` para entrar na sua [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd67-173">In your PowerShell window, enter the `login-azurermaccount` command to sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="2fd67-174">Caso ainda não tenha uma conta, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="2fd67-174">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="2fd67-175">No navegador, copie o script a seguir:</span><span class="sxs-lookup"><span data-stu-id="2fd67-175">In your browser, copy the following script:</span></span>
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate the public IP address to it
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for the VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create the virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. <span data-ttu-id="2fd67-176">Na janela do PowerShell, clique com o botão direito do mouse para colar o script e começar a executá-lo.</span><span class="sxs-lookup"><span data-stu-id="2fd67-176">In your PowerShell window, right-click to paste the script and start executing it.</span></span> <span data-ttu-id="2fd67-177">Você será solicitado a informar um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="2fd67-177">You are prompted for a username and password.</span></span> <span data-ttu-id="2fd67-178">Use essas credenciais para fazer logon na VM ao conectar-se a ela na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="2fd67-178">Use these credentials to log in to the VM when connecting to it in the next step.</span></span> <span data-ttu-id="2fd67-179">Se o script falhar e você tiver alterado os valores no script antes de executá-lo, verifique se os valores usados para tamanho, sistema operacional e local da VM estão listados na seção [Limitações](#Limitations) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2fd67-179">If the script fails, and you changed values in the script before executing it, confirm the values you used for VM size, operating system, and location are listed in the [Limitations](#Limitations) section of this article.</span></span>
6. <span data-ttu-id="2fd67-180">Para instalar o driver de rede acelerado para Windows, conclua as etapas na seção [Configurar o Windows](#configure-windows) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2fd67-180">To install the accelerated networking driver for Windows, complete the steps in the [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="2fd67-181"><a name="configure-windows"></a>Configurar Windows</span><span class="sxs-lookup"><span data-stu-id="2fd67-181"><a name="configure-windows"></a>Configure Windows</span></span>
<span data-ttu-id="2fd67-182">Depois de criar a VM no Azure, você deve instalar o driver de rede acelerada para Windows.</span><span class="sxs-lookup"><span data-stu-id="2fd67-182">Once you create the VM in Azure, you must install the accelerated networking driver for Windows.</span></span> <span data-ttu-id="2fd67-183">Antes de concluir as etapas a seguir, você deve ter criado uma VM do Windows com rede acelerada usando as etapas do [portal](#windows-portal) ou do [PowerShell](#windows-powershell) neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2fd67-183">Before completing the following steps, you must have created a Windows VM with accelerated networking using either the [portal](#windows-portal) or [PowerShell](#windows-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="2fd67-184">Em um navegador da Internet, abra o [portal](https://portal.azure.com) do Azure e entre com a sua [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd67-184">From an Internet browser, open the Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="2fd67-185">Caso ainda não tenha uma conta, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="2fd67-185">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="2fd67-186">Na caixa que contém o texto *Pesquisar recursos* na parte superior do portal do Azure, digite *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="2fd67-186">In the box that contains the text *Search resources* at the top of the Azure portal, type *MyVm*.</span></span> <span data-ttu-id="2fd67-187">Quando **MyVm** aparecer nos resultados da pesquisa, clique nela.</span><span class="sxs-lookup"><span data-stu-id="2fd67-187">When **MyVm** appears in the search results, click it.</span></span>
3. <span data-ttu-id="2fd67-188">Na folha **MyVm** que é exibida, clique no botão **Conectar** no canto superior esquerdo da folha.</span><span class="sxs-lookup"><span data-stu-id="2fd67-188">In the **MyVm** blade that appears, click the **Connect** button in the top left corner of the blade.</span></span> <span data-ttu-id="2fd67-189">**Observação:** se **Criando** estiver visível sob o botão **Conectar**, o Azure ainda não terminou de criar a VM.</span><span class="sxs-lookup"><span data-stu-id="2fd67-189">**Note:** If **Creating** is visible under the **Connect** button, Azure has not yet finished creating the VM.</span></span> <span data-ttu-id="2fd67-190">Clique em **Conectar** somente depois que **Criando** não for mais exibido sob o botão **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-190">Click **Connect** only after you no longer see **Creating** under the **Connect** button.</span></span>
4. <span data-ttu-id="2fd67-191">Permite ao navegador baixar o arquivo **MyVm.rdp**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-191">Allow your browser to download the **MyVm.rdp** file.</span></span>  <span data-ttu-id="2fd67-192">Após o download, clique no arquivo para abri-lo.</span><span class="sxs-lookup"><span data-stu-id="2fd67-192">Once downloaded, click the file to open it.</span></span> 
5. <span data-ttu-id="2fd67-193">Clique no botão **Conectar** na caixa **Conexão de área de trabalho remota** exibida, informando que o editor da conexão remota não pode ser identificado.</span><span class="sxs-lookup"><span data-stu-id="2fd67-193">Click the **Connect** button in the **Remote Desktop Connection** box that appears, notifying you that the publisher of the remote connection can't be identified.</span></span>
6. <span data-ttu-id="2fd67-194">Na caixa **Segurança do Windows** que aparece, clique em **Mais opções** e, em seguida, clique em **Usar uma conta diferente**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-194">In the **Windows Security** box that appears, click **More choices**, then click **Use a different account**.</span></span> <span data-ttu-id="2fd67-195">Digite o nome de usuário e a senha digitados na etapa 4 e, em seguida, clique no botão **OK**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-195">Enter the username and password you entered in step 4, then click the **OK** button.</span></span>
7. <span data-ttu-id="2fd67-196">Clique no botão **Sim** na caixa de Conexão de Área de Trabalho Remota exibida, informando-o de que não é possível verificar a identidade do computador remoto.</span><span class="sxs-lookup"><span data-stu-id="2fd67-196">Click the **Yes** button in the Remote Desktop Connection box that appears, notifying you that the identity of the remote computer cannot be verified.</span></span>
8. <span data-ttu-id="2fd67-197">Clique com o botão direito do mouse em Iniciar do Windows e clique em **Gerenciador de Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-197">Right-click the Windows Start button and click **Device Manager**.</span></span> <span data-ttu-id="2fd67-198">Expanda o nó **Adaptadores de rede**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-198">Expand the **Network adapters** node.</span></span> <span data-ttu-id="2fd67-199">Verifique se o **Adaptador de Ethernet de Função Virtual Mellanox ConnectX-3** aparece, como mostrado na figura a seguir:</span><span class="sxs-lookup"><span data-stu-id="2fd67-199">Confirm that the **Mellanox ConnectX-3 Virtual Function Ethernet Adapter** appears, as shown in the following picture:</span></span>
   
    ![Gerenciador de Dispositivos](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. <span data-ttu-id="2fd67-201">A Rede Acelerada agora está habilitada para sua VM.</span><span class="sxs-lookup"><span data-stu-id="2fd67-201">Accelerated Networking is now enabled for your VM.</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="2fd67-202">Criar uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="2fd67-202">Create a Linux VM</span></span>
<span data-ttu-id="2fd67-203">Você pode usar o Portal do Azure ou o Azure [PowerShell](#linux-powershell) para criar uma VM Ubuntu ou SLES.</span><span class="sxs-lookup"><span data-stu-id="2fd67-203">You can use the Azure portal or Azure [PowerShell](#linux-powershell) to create an Ubuntu or SLES VM.</span></span> <span data-ttu-id="2fd67-204">Para VMs RHEL e CentOS, há um fluxo de trabalho diferente.</span><span class="sxs-lookup"><span data-stu-id="2fd67-204">For RHEL and CentOS VMs there is a different workflow.</span></span>  <span data-ttu-id="2fd67-205">Veja as instruções abaixo.</span><span class="sxs-lookup"><span data-stu-id="2fd67-205">Please see the instructions below.</span></span>

### <span data-ttu-id="2fd67-206"><a name="linux-portal"></a>Portal</span><span class="sxs-lookup"><span data-stu-id="2fd67-206"><a name="linux-portal"></a>Portal</span></span>
1. <span data-ttu-id="2fd67-207">Registre-se na rede acelerada para a versão prévia do Linux concluindo as etapas 1 a 5 da seção [Criar uma VM do Linux – PowerShell](#linux-powershell) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2fd67-207">Register for the accelerated networking for Linux preview by completing steps 1-5 of the [Create a Linux VM - PowerShell](#linux-powershell) section of this article.</span></span>  <span data-ttu-id="2fd67-208">Você não pode se registrar para a versão prévia no portal.</span><span class="sxs-lookup"><span data-stu-id="2fd67-208">You cannot register for the preview in the portal.</span></span>
2. <span data-ttu-id="2fd67-209">Conclua as etapas 1 a 8 na seção [Criar uma VM do Windows – portal](#windows-portal) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2fd67-209">Complete steps 1-8 in the [Create a Windows VM - portal](#windows-portal) section of this article.</span></span> <span data-ttu-id="2fd67-210">Na etapa 2, clique em **Ubuntu Server 16.04 LTS**, em vez de **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-210">In step 2, click **Ubuntu Server 16.04 LTS** instead of **Windows Server 2016 Datacenter**.</span></span> <span data-ttu-id="2fd67-211">Para este tutorial, opte por usar uma senha, em vez de uma chave SSH, embora você pode usar qualquer uma para implantações de produção.</span><span class="sxs-lookup"><span data-stu-id="2fd67-211">For this tutorial, choose to use a password, rather than an SSH key, though for production deployments, you can use either.</span></span> <span data-ttu-id="2fd67-212">Caso **Rede acelerada** não apareça quando você conclui a etapa 7 da seção [Criar uma VM do Windows – portal](#windows-portal) deste artigo, é provável que isso seja devido a um dos seguintes motivos:</span><span class="sxs-lookup"><span data-stu-id="2fd67-212">If **Accelerated networking** does not appear when you complete step 7 of the [Create a Windows VM - portal](#windows-portal) section of this article, it's likely for one of the following reasons:</span></span>
    - <span data-ttu-id="2fd67-213">Você ainda não está registrado para a versão prévia.</span><span class="sxs-lookup"><span data-stu-id="2fd67-213">You are not yet registered for the preview.</span></span> <span data-ttu-id="2fd67-214">Verifique se o seu estado do registro é **Registrado**, conforme explicado na etapa 4 da seção [Criar uma VM do Linux – Powershell](#linux-powershell) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2fd67-214">Confirm that your registration state is **Registered**, as explained in step 4 of the [Create a Linux VM - Powershell](#linux-powershell) section of this article.</span></span> <span data-ttu-id="2fd67-215">**Observação:** se você tiver participado da rede Acelerada para a versão prévia de VMs do Windows (não é mais necessário registrar-se para usar a rede Acelerada para VMs do Windows), você não estará automaticamente registrado para a rede Acelerada para a versão prévia de VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="2fd67-215">**Note:** If you participated in the Accelerated networking for Windows VMs preview (it's no longer necessary to register to use Accelerated networking for Windows VMs), you are not automatically registered for the Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="2fd67-216">Você deverá registrar-se na rede acelerada para a versão prévia de VMs do Linux para participar delas.</span><span class="sxs-lookup"><span data-stu-id="2fd67-216">You must register for the Accelerated networking for Linux VMs preview to participate in it.</span></span>
    - <span data-ttu-id="2fd67-217">Você não selecionou um tamanho de VM, sistema operacional nem local listado na seção [Limitações](#limitations) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2fd67-217">You have not selected a VM size, operating system, or location listed in the [Limitations](#limitations) section of this article.</span></span>
3. <span data-ttu-id="2fd67-218">Para instalar o driver de rede acelerado para Linux, conclua as etapas na seção [Configurar o Linux](#configure-linux) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2fd67-218">To install the accelerated networking driver for Linux, complete the steps in the [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="2fd67-219"><a name="linux-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd67-219"><a name="linux-powershell"></a>PowerShell</span></span>

>[!WARNING]
><span data-ttu-id="2fd67-220">Se você criar VMs do Linux com rede acelerada em uma assinatura e, em seguida, tentar criar uma VM do Windows com rede acelerada na mesma assinatura, a criação da VM do Windows poderá falhar.</span><span class="sxs-lookup"><span data-stu-id="2fd67-220">If you create Linux VMs with accelerated networking in a subscription, and then attempt to create a Windows VM with accelerated networking in the same subscription, the Windows VM creation may fail.</span></span> <span data-ttu-id="2fd67-221">Durante essa versão prévia, é recomendável testar VMs do Linux e do Windows com rede acelerada em assinaturas diferentes.</span><span class="sxs-lookup"><span data-stu-id="2fd67-221">During this preview, it's recommended that you test Linux and Windows VMs with accelerated networking in separate subscriptions.</span></span>
>

1. <span data-ttu-id="2fd67-222">Instale a versão mais recente do módulo [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2fd67-222">Install the latest version of the Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="2fd67-223">Se você for novo no Azure PowerShell, leia o artigo [Visão geral do Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2fd67-223">If you're new to Azure PowerShell, read the [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="2fd67-224">Inicie uma sessão do PowerShell clicando no botão Iniciar do Windows, digitando **powershell** e, em seguida, clicando em **PowerShell** nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="2fd67-224">Start a PowerShell session by clicking the Windows Start button, typing **powershell**, then clicking **PowerShell** from the search results.</span></span>
3. <span data-ttu-id="2fd67-225">Na janela do PowerShell, digite o comando `login-azurermaccount` para entrar na sua [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd67-225">In your PowerShell window, enter the `login-azurermaccount` command to sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="2fd67-226">Caso ainda não tenha uma conta, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="2fd67-226">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="2fd67-227">Registre-se para rede acelerada para versão prévia do Azure concluindo as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2fd67-227">Register for the accelerated networking for Azure preview by completing the following steps:</span></span>
    - <span data-ttu-id="2fd67-228">Envie um email para [axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) com sua ID de assinatura do Azure e o uso pretendido.</span><span class="sxs-lookup"><span data-stu-id="2fd67-228">Send an email to [axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) with your Azure subscription ID and intended use.</span></span> <span data-ttu-id="2fd67-229">Aguarde um email de confirmação da Microsoft sobre sua assinatura ser habilitada.</span><span class="sxs-lookup"><span data-stu-id="2fd67-229">Please wait for an email confirmation from Microsoft about your subscription being enabled.</span></span>
    - <span data-ttu-id="2fd67-230">Digite o seguinte comando para confirmar que você está registrado para a versão prévia:</span><span class="sxs-lookup"><span data-stu-id="2fd67-230">Enter the following command to confirm you are registered for the preview:</span></span>
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        <span data-ttu-id="2fd67-231">Não continue com a etapa 5 até **Registrado** aparecer na saída após a execução do comando anterior.</span><span class="sxs-lookup"><span data-stu-id="2fd67-231">Do not continue with step 5 until **Registered** appears in the output after you enter the previous command.</span></span> <span data-ttu-id="2fd67-232">A saída deve se parecer com a saída a seguir antes de continuar:</span><span class="sxs-lookup"><span data-stu-id="2fd67-232">Your output must look like the following output before continuing:</span></span>
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      ><span data-ttu-id="2fd67-233">Se você tiver participado da Rede acelerada para versão prévia de VMs do Windows (não é mais necessário registrar-se para usar Rede Acelerada para VMs do Windows), você não estará automaticamente registrado para a Rede acelerada para a versão prévia de VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="2fd67-233">If you participated in the Accelerated networking for Windows VMs preview (it's no longer necessary to register to use Accelerated networking for Windows VMs), you are not automatically registered for the Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="2fd67-234">Você deverá registrar-se na rede acelerada para a versão prévia de VMs do Linux para participar delas.</span><span class="sxs-lookup"><span data-stu-id="2fd67-234">You must register for the Accelerated networking for Linux VMs preview to participate in it.</span></span>
      >
5. <span data-ttu-id="2fd67-235">No navegador, copie o script a seguir substituindo Ubuntu ou SLES conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="2fd67-235">In your browser, copy the following script substituting Ubuntu or SLES as desired.</span></span>  <span data-ttu-id="2fd67-236">Novamente, o Redhat e o CentOS têm um fluxo de trabalho diferente, descrito abaixo:</span><span class="sxs-lookup"><span data-stu-id="2fd67-236">Again, Redhat and CentOS have a different workflow outlined below:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate the public IP address to it
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define the new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for the VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create the virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. <span data-ttu-id="2fd67-237">Na janela do PowerShell, clique com o botão direito do mouse para colar o script e começar a executá-lo.</span><span class="sxs-lookup"><span data-stu-id="2fd67-237">In your PowerShell window, right-click to paste the script and start executing it.</span></span> <span data-ttu-id="2fd67-238">Você será solicitado a informar um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="2fd67-238">You are prompted for a username and password.</span></span> <span data-ttu-id="2fd67-239">Use essas credenciais para fazer logon na VM ao conectar-se a ela na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="2fd67-239">Use these credentials to log in to the VM when connecting to it in the next step.</span></span> <span data-ttu-id="2fd67-240">Se o script falhar, verifique:</span><span class="sxs-lookup"><span data-stu-id="2fd67-240">If the script fails, confirm that:</span></span>
    - <span data-ttu-id="2fd67-241">Se você está registrado para a versão prévia, conforme explicado na etapa 4</span><span class="sxs-lookup"><span data-stu-id="2fd67-241">You are registered for the preview, as explained in step 4</span></span>
    - <span data-ttu-id="2fd67-242">Se você tiver alterado o tamanho, o tipo de sistema operacional ou os valores de local da VM no script antes de executá-lo, se os valores estão listados na seção [Limitações](#Limitations) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2fd67-242">If you changed VM size, operating system type, or location values in the script before executing it, that the values are listed in the [Limitations](#Limitations) section of this article.</span></span>
7. <span data-ttu-id="2fd67-243">Para instalar o driver de rede acelerado para Linux, conclua as etapas na seção [Configurar o Linux](#configure-linux) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2fd67-243">To install the accelerated networking driver for Linux, complete the steps in the [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="2fd67-244"><a name="configure-linux"></a>Configurar Linux</span><span class="sxs-lookup"><span data-stu-id="2fd67-244"><a name="configure-linux"></a>Configure Linux</span></span>

<span data-ttu-id="2fd67-245">Depois de criar a VM no Azure, você deve instalar o driver de rede acelerada para Linux.</span><span class="sxs-lookup"><span data-stu-id="2fd67-245">Once you create the VM in Azure, you must install the accelerated networking driver for Linux.</span></span> <span data-ttu-id="2fd67-246">Antes de concluir as etapas a seguir, você deve ter criado uma VM do Linux com rede acelerada usando as etapas do [portal](#linux-portal) ou do [PowerShell](#linux-powershell) neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2fd67-246">Before completing the following steps, you must have created a Linux VM with accelerated networking using either the [portal](#linux-portal) or [PowerShell](#linux-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="2fd67-247">Em um navegador da Internet, abra o [portal](https://portal.azure.com) do Azure e entre com a sua [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd67-247">From an Internet browser, open the Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="2fd67-248">Caso ainda não tenha uma conta, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="2fd67-248">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="2fd67-249">Na parte superior do portal, à direita da barra *Pesquisar recursos*, clique no ícone **>_** para iniciar um cloud shell de Busca (Versão Prévia).</span><span class="sxs-lookup"><span data-stu-id="2fd67-249">At the top of the portal, to the right of the *Search resources* bar, click the **>_** icon to start a Bash cloud shell (Preview).</span></span> <span data-ttu-id="2fd67-250">O painel do cloud shell de Busca é exibido na parte inferior do portal e, depois de alguns segundos, apresenta um prompt **username@Azure:~$**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-250">The Bash cloud shell pane appears at the bottom of the portal and after a few seconds, presents a **username@Azure:~$** prompt.</span></span> <span data-ttu-id="2fd67-251">Embora você possa usar SSH para a VM do seu computador, em vez do cloud shell, as instruções neste tutorial presumem que você esteja usando o cloud shell.</span><span class="sxs-lookup"><span data-stu-id="2fd67-251">Though you can SSH to the VM from your computer, rather than the cloud shell, the instructions in this tutorial assume you're using the cloud shell.</span></span>
3. <span data-ttu-id="2fd67-252">Na parte superior do portal, na caixa que contém o texto *Pesquisar recursos*, digite *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="2fd67-252">At the top of the portal, in the box that contains the text *Search resources*, type *MyVm*.</span></span> <span data-ttu-id="2fd67-253">Quando **MyVm** aparecer nos resultados da pesquisa, clique nela.</span><span class="sxs-lookup"><span data-stu-id="2fd67-253">When **MyVm** appears in the search results, click it.</span></span>
4. <span data-ttu-id="2fd67-254">Na folha **MyVm** que é exibida, clique no botão **Conectar** no canto superior esquerdo da folha.</span><span class="sxs-lookup"><span data-stu-id="2fd67-254">In the **MyVm** blade that appears, click the **Connect** button in the top left corner of the blade.</span></span> <span data-ttu-id="2fd67-255">**Observação:** se **Criando** estiver visível sob o botão **Conectar**, o Azure ainda não terminou de criar a VM.</span><span class="sxs-lookup"><span data-stu-id="2fd67-255">**Note:** If **Creating** is visible under the **Connect** button, Azure has not yet finished creating the VM.</span></span> <span data-ttu-id="2fd67-256">Clique em **Conectar** somente depois que **Criando** não for mais exibido sob o botão **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="2fd67-256">Click **Connect** only after you no longer see **Creating** under the **Connect** button.</span></span>
5. <span data-ttu-id="2fd67-257">O Azure abre uma caixa pedindo para você inserir o `ssh adminuser@<ipaddress>`.</span><span class="sxs-lookup"><span data-stu-id="2fd67-257">Azure opens a box telling you to enter the `ssh adminuser@<ipaddress>`.</span></span> <span data-ttu-id="2fd67-258">Digite esse comando no cloud shell (ou copie-o da caixa exibida na etapa 4 e cole-o no cloud shell) e, em seguida, pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="2fd67-258">Enter this command in the cloud shell (or copy it from the box that appeared in step 4 and paste it in to the cloud shell), then press Enter.</span></span>
6. <span data-ttu-id="2fd67-259">Insira **Sim** para a pergunta consultando se você deseja continuar a conexão e, em seguida, pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="2fd67-259">Enter **yes** to the question asking you if you want to continue connecting, then press Enter.</span></span>
7. <span data-ttu-id="2fd67-260">Digite a senha inserida ao criar a VM.</span><span class="sxs-lookup"><span data-stu-id="2fd67-260">Enter the password you entered when creating the VM.</span></span> <span data-ttu-id="2fd67-261">Depois de fazer logon com êxito na VM, você verá um prompt adminuser@MyVm:~$.</span><span class="sxs-lookup"><span data-stu-id="2fd67-261">Once successfully logged in to the VM, you see an adminuser@MyVm:~$ prompt.</span></span> <span data-ttu-id="2fd67-262">Agora você está conectado à VM por meio da sessão de cloud shell.</span><span class="sxs-lookup"><span data-stu-id="2fd67-262">You are now logged in to the VM through the cloud shell session.</span></span> <span data-ttu-id="2fd67-263">**Observação:** as sessões de cloud shell atingem o tempo limite depois de 10 minutos de inatividade.</span><span class="sxs-lookup"><span data-stu-id="2fd67-263">**Note:** Cloud shell sessions time out after 10 minutes of inactivity.</span></span>

<span data-ttu-id="2fd67-264">Neste ponto, as instruções variam de acordo com a distribuição que você está usando.</span><span class="sxs-lookup"><span data-stu-id="2fd67-264">At this point, the instructions vary based on the distribution you are using.</span></span> 

#### <a name="ubuntusles"></a><span data-ttu-id="2fd67-265">Ubuntu/SLES</span><span class="sxs-lookup"><span data-stu-id="2fd67-265">Ubuntu/SLES</span></span>

1. <span data-ttu-id="2fd67-266">No prompt, digite `uname -r` e confirme a versão para:</span><span class="sxs-lookup"><span data-stu-id="2fd67-266">At the prompt, enter `uname -r` and confirm the version for:</span></span>

    * <span data-ttu-id="2fd67-267">O Ubuntu é "4.4.0-77-generic" ou superior</span><span class="sxs-lookup"><span data-stu-id="2fd67-267">Ubuntu is "4.4.0-77-generic," or greater</span></span>
    * <span data-ttu-id="2fd67-268">O SLES é "4.4.59-92.20-default" ou superior</span><span class="sxs-lookup"><span data-stu-id="2fd67-268">SLES is "4.4.59-92.20-default" or greater</span></span>

2. <span data-ttu-id="2fd67-269">Crie um vínculo entre a vNIC de rede padrão e a vNIC de rede acelerada executando os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="2fd67-269">Create a bond between the standard networking vNIC and the accelerated networking vNIC by running the commands that follow.</span></span> <span data-ttu-id="2fd67-270">O tráfego de rede usa a vNIC de rede acelerada de maior desempenho, enquanto o vínculo garante que o tráfego de rede não seja interrompido em determinadas alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="2fd67-270">Network traffic uses the higher performing accelerated networking vNIC, while the bond ensures that networking traffic is not interrupted across certain configuration changes.</span></span>
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. <span data-ttu-id="2fd67-271">Depois de executar o script, a VM será reiniciada após uma pausa de 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="2fd67-271">After running the script, the VM will restart after a 60 second pause.</span></span>
4. <span data-ttu-id="2fd67-272">Depois que a VM for reiniciada, reconecte-a ao concluir as etapas 5 a 7 novamente.</span><span class="sxs-lookup"><span data-stu-id="2fd67-272">Once the VM is restarted, reconnect to it by completing steps 5-7 again.</span></span>
5. <span data-ttu-id="2fd67-273">Execute o comando `ifconfig` e confirme se bond0 surgiu e se a interface está aparecendo como UP.</span><span class="sxs-lookup"><span data-stu-id="2fd67-273">Run the `ifconfig` command and confirm that bond0 has come up and the interface is showing as UP.</span></span> 
 
 >[!NOTE]
      ><span data-ttu-id="2fd67-274">Os aplicativos usando a rede acelerada devem se comunicar por meio da interface *bond0*, não *eth0*.</span><span class="sxs-lookup"><span data-stu-id="2fd67-274">Applications using accelerated networking must communicate over the *bond0* interface, not *eth0*.</span></span>  <span data-ttu-id="2fd67-275">O nome da interface pode mudar antes de a rede acelerada atingir disponibilidade geral.</span><span class="sxs-lookup"><span data-stu-id="2fd67-275">The interface name may change before accelerated networking reaches general availability.</span></span>

#### <a name="rhelcentos"></a><span data-ttu-id="2fd67-276">RHEL/CentOS</span><span class="sxs-lookup"><span data-stu-id="2fd67-276">RHEL/CentOS</span></span>

<span data-ttu-id="2fd67-277">Criar uma VM Red Hat Enterprise Linux ou CentOS 7.3 requer algumas etapas adicionais para carregar os drivers mais recentes necessários para SR-IOV e o driver VF (Função Virtual) para a placa de rede.</span><span class="sxs-lookup"><span data-stu-id="2fd67-277">Creating a Red Hat Enterprise Linux or CentOS 7.3 VM requires some extra steps to load the latest drivers needed for SR-IOV and the Virtual Function (VF) driver for the network card.</span></span> <span data-ttu-id="2fd67-278">A primeira fase das instruções prepara uma imagem que pode ser usada para fazer uma ou mais máquinas virtuais com os drivers pré-carregados.</span><span class="sxs-lookup"><span data-stu-id="2fd67-278">The first phase of the instructions prepares an image that can be used to make one or more virtual machines that have the drivers pre-loaded.</span></span>

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a><span data-ttu-id="2fd67-279">Fase um: preparar uma imagem base do Red Hat Enterprise Linux ou CentOS 7.3.</span><span class="sxs-lookup"><span data-stu-id="2fd67-279">Phase one: prepare a Red Hat Enterprise Linux or CentOS 7.3 base image.</span></span> 

1.  <span data-ttu-id="2fd67-280">Provisione uma VM CentOS 7.3 não SRIOV no Azure</span><span class="sxs-lookup"><span data-stu-id="2fd67-280">Provision a non-SRIOV CentOS 7.3 VM on Azure</span></span>

2.  <span data-ttu-id="2fd67-281">Instale o LIS 4.2.2:</span><span class="sxs-lookup"><span data-stu-id="2fd67-281">Install LIS 4.2.2:</span></span>
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  <span data-ttu-id="2fd67-282">Baixe os arquivos de configuração</span><span class="sxs-lookup"><span data-stu-id="2fd67-282">Download config files</span></span>
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  <span data-ttu-id="2fd67-283">Desprovisione essa VM</span><span class="sxs-lookup"><span data-stu-id="2fd67-283">Deprovision this VM</span></span>

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  <span data-ttu-id="2fd67-284">No Portal do Azure, pare essa VM e vá para a captura “Discos” da VM no URI do VHD do OSDisk.</span><span class="sxs-lookup"><span data-stu-id="2fd67-284">From Azure portal, stop this VM; and go to VM’s "Disks", capture the OSDisk’s VHD URI.</span></span> <span data-ttu-id="2fd67-285">Esse URI contém o nome do VHD da imagem base e sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2fd67-285">This URI contains the base image’s VHD name and its storage account.</span></span> 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a><span data-ttu-id="2fd67-286">Fase dois: provisionar novas VMs no Azure</span><span class="sxs-lookup"><span data-stu-id="2fd67-286">Phase two: Provision new VMs on Azure</span></span>

1.  <span data-ttu-id="2fd67-287">Provisione novas VMs com base em New-AzureRMVMConfig usando a imagem base do VHD capturada na fase um, com AcceleratedNetworking habilitado na vNIC:</span><span class="sxs-lookup"><span data-stu-id="2fd67-287">Provision new VMs based with New-AzureRMVMConfig using the base image VHD captured in phase one, with AcceleratedNetworking enabled on the vNIC:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate the public IP address to it
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify the base image's VHD URI (from phase one step 5). 
    # Note: The storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need to replace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for the location from which the new image binary large object (BLOB) is copied to start the virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for the VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create the virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  <span data-ttu-id="2fd67-288">Depois de as VMs inicializarem, verifique o dispositivo VF por “Ispci” e verifique a entrada Mellanox.</span><span class="sxs-lookup"><span data-stu-id="2fd67-288">After VMs boot up, check the VF device by "lspci" and check the Mellanox entry.</span></span> <span data-ttu-id="2fd67-289">Por exemplo, devemos ver esse item na saída de Ispci:</span><span class="sxs-lookup"><span data-stu-id="2fd67-289">For example, we should see this item in the lspci output:</span></span>
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  <span data-ttu-id="2fd67-290">Execute o script de associação por:</span><span class="sxs-lookup"><span data-stu-id="2fd67-290">Run the bonding script by:</span></span>

    ```bash
    sudo bondvf.sh
    ```

4.  <span data-ttu-id="2fd67-291">Reinicialize as novas VMs:</span><span class="sxs-lookup"><span data-stu-id="2fd67-291">Reboot the new VMs:</span></span>

    ```bash
    sudo reboot
    ```

<span data-ttu-id="2fd67-292">A VM deve começar com bond0 configurado e o caminho da Rede Acelerada habilitado.</span><span class="sxs-lookup"><span data-stu-id="2fd67-292">The VM should start with bond0 configured and the Accelerated Networking path enabled.</span></span>  <span data-ttu-id="2fd67-293">Execute `ifconfig` para confirmar.</span><span class="sxs-lookup"><span data-stu-id="2fd67-293">Run `ifconfig` to confirm.</span></span>
