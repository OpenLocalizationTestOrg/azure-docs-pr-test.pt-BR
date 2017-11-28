---
title: "aaaCreate uma máquina virtual do Azure com rede acelerado | Microsoft Docs"
description: "Saiba como toocreate uma máquina virtual com acelerado de rede."
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
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a><span data-ttu-id="46337-103">Criar uma máquina virtual com Rede Acelerada</span><span class="sxs-lookup"><span data-stu-id="46337-103">Create a virtual machine with Accelerated Networking</span></span>

<span data-ttu-id="46337-104">Neste tutorial, você aprenderá como toocreate uma máquina Virtual (VM) do Azure com acelerado em rede.</span><span class="sxs-lookup"><span data-stu-id="46337-104">In this tutorial, you learn how toocreate an Azure Virtual Machine (VM) with Accelerated Networking.</span></span> <span data-ttu-id="46337-105">A Rede Acelerada é GA para Windows e em uma Visualização Pública para distribuições específicas do Linux.</span><span class="sxs-lookup"><span data-stu-id="46337-105">Accelerated Networking is GA for Windows and in a Public Preview for specific Linux distributions.</span></span> <span data-ttu-id="46337-106">Rede acelerado permite tooa de virtualização (SR-IOV) de e/s de raiz única VM, melhorando o desempenho de rede.</span><span class="sxs-lookup"><span data-stu-id="46337-106">Accelerated networking enables single root I/O virtualization (SR-IOV) tooa VM, greatly improving its networking performance.</span></span> <span data-ttu-id="46337-107">Esse caminho de alto desempenho ignora o host de saudação do caminho de dados Olá reduzindo a latência, a variação e a utilização da CPU, para uso com cargas de trabalho mais exigentes de rede do hello em tipos VM com suporte.</span><span class="sxs-lookup"><span data-stu-id="46337-107">This high-performance path bypasses hello host from hello datapath reducing latency, jitter, and CPU utilization, for use with hello most demanding network workloads on supported VM types.</span></span> <span data-ttu-id="46337-108">Olá a seguir mostra a imagem a comunicação entre duas máquinas virtuais (VM) com e sem conexão de rede rápida:</span><span class="sxs-lookup"><span data-stu-id="46337-108">hello following picture shows communication between two virtual machines (VM) with and without accelerated networking:</span></span>

![Comparação](./media/virtual-network-create-vm-accelerated-networking/image1.png)

<span data-ttu-id="46337-110">Sem conexão de rede rápida, todo o tráfego de rede dentro e fora de saudação VM deve ignorar host hello e comutador hello.</span><span class="sxs-lookup"><span data-stu-id="46337-110">Without accelerated networking, all networking traffic in and out of hello VM must traverse hello host and hello virtual switch.</span></span> <span data-ttu-id="46337-111">Olá ele proporciona imposição de política de todos os, tais como grupos de segurança de rede acessar listas de controle, isolamento e outro tráfego de toonetwork de serviços de rede virtualizado.</span><span class="sxs-lookup"><span data-stu-id="46337-111">hello virtual switch provides all policy enforcement, such as network security groups, access control lists, isolation, and other network virtualized services toonetwork traffic.</span></span> <span data-ttu-id="46337-112">toolearn mais sobre os comutadores virtuais, ler Olá [virtualização de rede do Hyper-V e o comutador virtual](https://technet.microsoft.com/library/jj945275.aspx) artigo.</span><span class="sxs-lookup"><span data-stu-id="46337-112">toolearn more about virtual switches, read hello [Hyper-V network virtualization and virtual switch](https://technet.microsoft.com/library/jj945275.aspx) article.</span></span>

<span data-ttu-id="46337-113">Com a rede acelerada, tráfego de rede chega na interface de rede da VM hello (NIC) e é então encaminhado toohello VM.</span><span class="sxs-lookup"><span data-stu-id="46337-113">With accelerated networking, network traffic arrives at hello VM's network interface (NIC), and is then forwarded toohello VM.</span></span> <span data-ttu-id="46337-114">Aplica-se todas as políticas de rede que Olá comutador virtual sem rede acelerado são descarregados e aplicadas em hardware.</span><span class="sxs-lookup"><span data-stu-id="46337-114">All network policies that hello virtual switch applies without accelerated networking are offloaded and applied in hardware.</span></span> <span data-ttu-id="46337-115">Aplicação de política no hardware habilita Olá NIC tooforward tráfego de rede diretamente toohello VM, ignorando host hello e comutador hello, mantendo todas as política Olá ele aplicado no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="46337-115">Applying policy in hardware enables hello NIC tooforward network traffic directly toohello VM, bypassing hello host and hello virtual switch, while maintaining all hello policy it applied in hello host.</span></span>

<span data-ttu-id="46337-116">Olá benefícios da rede acelerado se aplicam somente toohello que ele é habilitado na VM.</span><span class="sxs-lookup"><span data-stu-id="46337-116">hello benefits of accelerated networking only apply toohello VM that it is enabled on.</span></span> <span data-ttu-id="46337-117">Para obter melhores resultados de Olá, é ideal tooenable esse recurso em pelo menos duas VMs conectado toohello mesma rede Virtual do Azure (VNet).</span><span class="sxs-lookup"><span data-stu-id="46337-117">For hello best results, it is ideal tooenable this feature on at least two VMs connected toohello same Azure Virtual Network (VNet).</span></span> <span data-ttu-id="46337-118">Ao se comunicar em VNets ou a conexão local, esse recurso tem uma latência de toooverall impacto mínimo.</span><span class="sxs-lookup"><span data-stu-id="46337-118">When communicating across VNets or connecting on-premises, this feature has minimal impact toooverall latency.</span></span>

> [!WARNING]
> <span data-ttu-id="46337-119">Este Linux visualização pública pode não ter Olá são do mesmo nível de disponibilidade e confiabilidade como recursos em geral versão de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="46337-119">This Linux Public Preview may not have hello same level of availability and reliability as features that are in general availability release.</span></span> <span data-ttu-id="46337-120">Olá recurso não tem suporte, pode ter restringido recursos e pode não estar disponível em todos os locais do Azure.</span><span class="sxs-lookup"><span data-stu-id="46337-120">hello feature is not supported, may have constrained capabilities, and may not be available in all Azure locations.</span></span> <span data-ttu-id="46337-121">Para notificações mais recentes de Olá em disponibilidade e o status desse recurso, verifique Olá página de atualizações de rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="46337-121">For hello most up-to-date notifications on availability and status of this feature, check hello Azure Virtual Network updates page.</span></span>

## <a name="benefits"></a><span data-ttu-id="46337-122">Benefícios</span><span class="sxs-lookup"><span data-stu-id="46337-122">Benefits</span></span>
* <span data-ttu-id="46337-123">**Reduzir a latência / superior pacotes por segundo (pps):** removendo Olá comutador do caminho de dados de saudação remove tempo de saudação pacotes gastam no host Olá para processamento de política e aumenta Olá número de pacotes que podem ser processadas em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="46337-123">**Lower Latency / Higher packets per second (pps):** Removing hello virtual switch from hello datapath removes hello time packets spend in hello host for policy processing and increases hello number of packets that can be processed inside hello VM.</span></span>
* <span data-ttu-id="46337-124">**Redução de tremulação:** switch Virtual processamento depende de quantidade de saudação de política que precisa toobe aplicado e Olá carga de trabalho de saudação da CPU que está fazendo o processamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="46337-124">**Reduced jitter:** Virtual switch processing depends on hello amount of policy that needs toobe applied and hello workload of hello CPU that is doing hello processing.</span></span> <span data-ttu-id="46337-125">O descarregamento de hardware de toohello de imposição de política de saudação remove essa variação, oferecendo pacotes diretamente alterna toohello VM, removendo a comunicação Olá host tooVM e todas as interrupções de software e contexto.</span><span class="sxs-lookup"><span data-stu-id="46337-125">Offloading hello policy enforcement toohello hardware removes that variability by delivering packets directly toohello VM, removing hello host tooVM communication and all software interrupts and context switches.</span></span>
* <span data-ttu-id="46337-126">**Diminuir a utilização da CPU:** Bypassing Olá comutador no host Olá leva a utilização de CPU tooless para processamento do tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="46337-126">**Decreased CPU utilization:** Bypassing hello virtual switch in hello host leads tooless CPU utilization for processing network traffic.</span></span>

## <span data-ttu-id="46337-127"><a name="Limitations"></a>Limitações</span><span class="sxs-lookup"><span data-stu-id="46337-127"><a name="Limitations"></a>Limitations</span></span>
<span data-ttu-id="46337-128">Olá limitações a seguir existe ao usar esse recurso:</span><span class="sxs-lookup"><span data-stu-id="46337-128">hello following limitations exist when using this capability:</span></span>

* <span data-ttu-id="46337-129">**Criação de interface de rede:** rede acelerada só pode ser habilitada para uma NIC nova.</span><span class="sxs-lookup"><span data-stu-id="46337-129">**Network interface creation:** Accelerated networking can only be enabled for a new NIC.</span></span> <span data-ttu-id="46337-130">Não pode ser habilitada para uma NIC existente.</span><span class="sxs-lookup"><span data-stu-id="46337-130">It cannot be enabled for an existing NIC.</span></span>
* <span data-ttu-id="46337-131">**Criação de VM:** A NIC com a rede acelerado habilitada pode somente ser anexado tooa VM quando hello VM é criada.</span><span class="sxs-lookup"><span data-stu-id="46337-131">**VM creation:** A NIC with accelerated networking enabled can only be attached tooa VM when hello VM is created.</span></span> <span data-ttu-id="46337-132">Olá NIC não pode ser anexado tooan existente de VM.</span><span class="sxs-lookup"><span data-stu-id="46337-132">hello NIC cannot be attached tooan existing VM.</span></span>
* <span data-ttu-id="46337-133">**Regiões:** VMs do Windows com rede acelerada são oferecidas na maioria das regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="46337-133">**Regions:** Windows VMs with accelerated networking are offered in most Azure regions.</span></span> <span data-ttu-id="46337-134">VMs do Linux com rede acelerada são oferecidas em várias regiões.</span><span class="sxs-lookup"><span data-stu-id="46337-134">Linux VMs with accelerated networking are offered in multiple regions.</span></span> <span data-ttu-id="46337-135">regiões Olá esse recurso está disponível em expansão.</span><span class="sxs-lookup"><span data-stu-id="46337-135">hello regions this capability is available in is expanding.</span></span> <span data-ttu-id="46337-136">Consulte o blog de atualizações de sistema de rede Virtual do Azure Olá abaixo para obter informações mais recentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="46337-136">Please see hello Azure Virtual Networking Updates blog below for hello latest information.</span></span>   
* <span data-ttu-id="46337-137">**Sistemas operacionais com suporte:** Windows: Microsoft Windows Server 2012 R2 Datacenter e Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="46337-137">**Supported operating systems:** Windows: Microsoft Windows Server 2012 R2 Datacenter and Windows Server 2016.</span></span> <span data-ttu-id="46337-138">Linux: Ubuntu Server 16.04 LTS com kernel 4.4.0-77 ou superior, SLES 12 SP2, RHEL 7.3 e CentOS 7.3 (publicado por "Rogue Wave Software").</span><span class="sxs-lookup"><span data-stu-id="46337-138">Linux: Ubuntu Server 16.04 LTS with kernel 4.4.0-77 or higher, SLES 12 SP2, RHEL 7.3 and CentOS 7.3 (Published by “Rogue Wave Software”).</span></span>
* <span data-ttu-id="46337-139">**Tamanho da VM:** tamanhos de instância com computação otimizada e de finalidade geral com oito ou mais núcleos.</span><span class="sxs-lookup"><span data-stu-id="46337-139">**VM Size:** General purpose and compute-optimized instance sizes with eight or more cores.</span></span> <span data-ttu-id="46337-140">Para obter mais informações, consulte Olá [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) e [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigos de tamanhos de VM.</span><span class="sxs-lookup"><span data-stu-id="46337-140">For more information, see hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM sizes articles.</span></span> <span data-ttu-id="46337-141">Olá conjunto de tamanhos de instância VM com suporte será expandida em Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="46337-141">hello set of supported VM instance sizes will expand in hello future.</span></span>
* <span data-ttu-id="46337-142">**Implantação somente por meio do ARM (Azure Resource Manager):** a Rede Acelerada não está disponível para implantação por meio do ASM/RDFE.</span><span class="sxs-lookup"><span data-stu-id="46337-142">**Deployment through Azure Resource Manager (ARM) only:** Accelerated Networking is not available for deployment through ASM/RDFE.</span></span>

<span data-ttu-id="46337-143">Alterações toothese limitações são anunciadas pelo Olá [rede Virtual do Azure atualiza](https://azure.microsoft.com/updates/accelerated-networking-in-preview) página.</span><span class="sxs-lookup"><span data-stu-id="46337-143">Changes toothese limitations are announced through hello [Azure Virtual Networking updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="46337-144">Criar uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="46337-144">Create a Windows VM</span></span>
<span data-ttu-id="46337-145">Você pode usar o hello portal do Azure ou Azure [PowerShell](#windows-powershell) toocreate Olá VM.</span><span class="sxs-lookup"><span data-stu-id="46337-145">You can use hello Azure portal or Azure [PowerShell](#windows-powershell) toocreate hello VM.</span></span>

### <span data-ttu-id="46337-146"><a name="windows-portal"></a>Portal</span><span class="sxs-lookup"><span data-stu-id="46337-146"><a name="windows-portal"></a>Portal</span></span>

1. <span data-ttu-id="46337-147">Em um navegador da Internet, abra hello Azure [portal](https://portal.azure.com) e entre com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="46337-147">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="46337-148">Caso ainda não tenha uma conta, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="46337-148">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="46337-149">No portal de saudação, clique em **+ novo** > **de computação** > **Datacenter do Windows Server 2016**.</span><span class="sxs-lookup"><span data-stu-id="46337-149">In hello portal, click **+ New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
3. <span data-ttu-id="46337-150">Em Olá **Datacenter do Windows Server 2016** folha exibida, deixe *Gerenciador de recursos de* selecionado em **selecionar um modelo de implantação**e clique em **criar** .</span><span class="sxs-lookup"><span data-stu-id="46337-150">In hello **Windows Server 2016 Datacenter** blade that appears, leave *Resource Manager* selected under **Select a deployment model**, and click **Create**.</span></span>
4. <span data-ttu-id="46337-151">Em Olá **Noções básicas de** folha que aparece, digite Olá valores a seguir, deixe Olá restantes opções padrão ou selecione ou insira seus próprios valores e clique em Olá **Okey** botão:</span><span class="sxs-lookup"><span data-stu-id="46337-151">In hello **Basics** blade that appears, enter hello following values, leave hello remaining default options or select or enter your own values, and click hello **OK** button:</span></span>

    |<span data-ttu-id="46337-152">Configuração</span><span class="sxs-lookup"><span data-stu-id="46337-152">Setting</span></span>|<span data-ttu-id="46337-153">Valor</span><span class="sxs-lookup"><span data-stu-id="46337-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="46337-154">Nome</span><span class="sxs-lookup"><span data-stu-id="46337-154">Name</span></span>|<span data-ttu-id="46337-155">MyVm</span><span class="sxs-lookup"><span data-stu-id="46337-155">MyVm</span></span>|
    |<span data-ttu-id="46337-156">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="46337-156">Resource group</span></span>|<span data-ttu-id="46337-157">Deixe **Criar novo** selecionado e digite *MyResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="46337-157">Leave **Create new** selected and enter *MyResourceGroup*</span></span>|
    |<span data-ttu-id="46337-158">Local</span><span class="sxs-lookup"><span data-stu-id="46337-158">Location</span></span>|<span data-ttu-id="46337-159">Oeste dos EUA 2</span><span class="sxs-lookup"><span data-stu-id="46337-159">West US 2</span></span>|

    <span data-ttu-id="46337-160">Se você for novo tooAzure, saiba mais sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [assinaturas](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), e [locais](https://azure.microsoft.com/regions) (que também são chamadas de regiões tooas).</span><span class="sxs-lookup"><span data-stu-id="46337-160">If you're new tooAzure, learn more about [Resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (which are also referred tooas regions).</span></span>
5. <span data-ttu-id="46337-161">Em Olá **escolher um tamanho de** folha que aparece, digite *8* em Olá **mínimo de núcleos** caixa e, em seguida, clique em **exibir todos os**.</span><span class="sxs-lookup"><span data-stu-id="46337-161">In hello **Choose a size** blade that appears, enter *8* in hello **Minimum cores** box, then click **View all**.</span></span>
6. <span data-ttu-id="46337-162">Clique em **DS4_V2 padrão**, ou qualquer suporte a VM, e clique em Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="46337-162">Click **DS4_V2 Standard**, or any supported VM, then click hello **Select** button.</span></span>
7. <span data-ttu-id="46337-163">Em hello **configurações** folha exibida, deixe todas as configurações como-é, exceto clique **habilitado** em **acelerado por rede**, clique Olá **Okey** botão.</span><span class="sxs-lookup"><span data-stu-id="46337-163">In hello **Settings** blade that appears, leave all settings as-is, except click **Enabled** under **Accelerated networking**, then click hello **OK** button.</span></span> <span data-ttu-id="46337-164">**Observação:** se, nas etapas anteriores, você selecionou valores de tamanho VM, o sistema operacional ou local que não estão listados na Olá [limitações](#Limitations) deste artigo, **Accelerated rede**não estiver visível.</span><span class="sxs-lookup"><span data-stu-id="46337-164">**Note:** If, in previous steps, you selected values for VM size, operating system, or location that aren't listed in hello [Limitations](#Limitations) section of this article, **Accelerated networking** isn't visible.</span></span>
8. <span data-ttu-id="46337-165">Em Olá **resumo** folha que aparece, clique em Olá **Okey** botão.</span><span class="sxs-lookup"><span data-stu-id="46337-165">In hello **Summary** blade that appears, click hello **OK** button.</span></span> <span data-ttu-id="46337-166">Criando Olá VM a partir do Azure.</span><span class="sxs-lookup"><span data-stu-id="46337-166">Azure starts creating hello VM.</span></span> <span data-ttu-id="46337-167">A criação da VM leva alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="46337-167">VM creation takes a few minutes.</span></span>
9. <span data-ttu-id="46337-168">Olá tooinstall acelerado driver de rede para Windows, Olá concluir as etapas em Olá [configurar o Windows](#configure-windows) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="46337-168">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="46337-169"><a name="windows-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="46337-169"><a name="windows-powershell"></a>PowerShell</span></span>
1. <span data-ttu-id="46337-170">Instale a versão mais recente Olá de saudação do Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo.</span><span class="sxs-lookup"><span data-stu-id="46337-170">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="46337-171">Se você for novo tooAzure PowerShell, ler Olá [visão geral do Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.</span><span class="sxs-lookup"><span data-stu-id="46337-171">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="46337-172">Iniciar uma sessão do PowerShell clicando o botão Iniciar do Windows hello, digitando **powershell**, em seguida, clicando em **PowerShell** Olá dos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="46337-172">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="46337-173">Na janela do PowerShell, digite Olá `login-azurermaccount` toosign de comando com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="46337-173">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="46337-174">Caso ainda não tenha uma conta, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="46337-174">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="46337-175">No navegador, copie Olá script a seguir:</span><span class="sxs-lookup"><span data-stu-id="46337-175">In your browser, copy hello following script:</span></span>
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

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
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

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. <span data-ttu-id="46337-176">Na janela do PowerShell, clique toopaste script de saudação e começar a executá-lo.</span><span class="sxs-lookup"><span data-stu-id="46337-176">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="46337-177">Você será solicitado a informar um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="46337-177">You are prompted for a username and password.</span></span> <span data-ttu-id="46337-178">Use essas credenciais toolog no toohello VM ao conectar-se tooit na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="46337-178">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="46337-179">Se o script hello falha e você alterou os valores no script hello antes da execução, confirme valores hello usado para o tamanho da VM, sistema operacional, e local são listados no hello [limitações](#Limitations) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="46337-179">If hello script fails, and you changed values in hello script before executing it, confirm hello values you used for VM size, operating system, and location are listed in hello [Limitations](#Limitations) section of this article.</span></span>
6. <span data-ttu-id="46337-180">Olá tooinstall acelerado driver de rede para Windows, Olá concluir as etapas em Olá [configurar o Windows](#configure-windows) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="46337-180">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="46337-181"><a name="configure-windows"></a>Configurar Windows</span><span class="sxs-lookup"><span data-stu-id="46337-181"><a name="configure-windows"></a>Configure Windows</span></span>
<span data-ttu-id="46337-182">Quando você criar hello VM no Azure, você deve instalar o driver de rede acelerado Olá para Windows.</span><span class="sxs-lookup"><span data-stu-id="46337-182">Once you create hello VM in Azure, you must install hello accelerated networking driver for Windows.</span></span> <span data-ttu-id="46337-183">Antes de concluir Olá etapas a seguir, você deve ter uma VM do Windows criado com a rede acelerado usando qualquer Olá [portal](#windows-portal) ou [PowerShell](#windows-powershell) as etapas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="46337-183">Before completing hello following steps, you must have created a Windows VM with accelerated networking using either hello [portal](#windows-portal) or [PowerShell](#windows-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="46337-184">Em um navegador da Internet, abra hello Azure [portal](https://portal.azure.com) e entre com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="46337-184">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="46337-185">Caso ainda não tenha uma conta, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="46337-185">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="46337-186">Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="46337-186">In hello box that contains hello text *Search resources* at hello top of hello Azure portal, type *MyVm*.</span></span> <span data-ttu-id="46337-187">Quando **MyVm** aparece nos resultados da pesquisa hello, clique nele.</span><span class="sxs-lookup"><span data-stu-id="46337-187">When **MyVm** appears in hello search results, click it.</span></span>
3. <span data-ttu-id="46337-188">Em Olá **MyVm** folha que aparece, clique em Olá **conectar** botão no canto superior esquerdo de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="46337-188">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="46337-189">**Observação:** se **criando** for visível sob Olá **conectar** botão Azure ainda não foi concluída criando Olá VM.</span><span class="sxs-lookup"><span data-stu-id="46337-189">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="46337-190">Clique em **conectar** somente depois que você não verá mais **criando** em Olá **conectar** botão.</span><span class="sxs-lookup"><span data-stu-id="46337-190">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
4. <span data-ttu-id="46337-191">Permitir Olá de toodownload seu navegador **MyVm.rdp** arquivo.</span><span class="sxs-lookup"><span data-stu-id="46337-191">Allow your browser toodownload hello **MyVm.rdp** file.</span></span>  <span data-ttu-id="46337-192">Após o download, clique em Olá arquivo tooopen-lo.</span><span class="sxs-lookup"><span data-stu-id="46337-192">Once downloaded, click hello file tooopen it.</span></span> 
5. <span data-ttu-id="46337-193">Clique em Olá **conectar** botão Olá **Conexão de área de trabalho remota** caixa que aparece, informando que Olá Editor de conexão remota Olá não pode ser identificado.</span><span class="sxs-lookup"><span data-stu-id="46337-193">Click hello **Connect** button in hello **Remote Desktop Connection** box that appears, notifying you that hello publisher of hello remote connection can't be identified.</span></span>
6. <span data-ttu-id="46337-194">Em Olá **a segurança do Windows** caixa que aparece, clique em **mais opções**, em seguida, clique em **usar uma conta diferente**.</span><span class="sxs-lookup"><span data-stu-id="46337-194">In hello **Windows Security** box that appears, click **More choices**, then click **Use a different account**.</span></span> <span data-ttu-id="46337-195">Digite hello nome de usuário e senha que você digitou na etapa 4, clique em Olá **Okey** botão.</span><span class="sxs-lookup"><span data-stu-id="46337-195">Enter hello username and password you entered in step 4, then click hello **OK** button.</span></span>
7. <span data-ttu-id="46337-196">Clique em Olá **Sim** botão na caixa de Conexão de área de trabalho remota Olá que aparece, informando que a identidade de saudação do computador remoto Olá não pode ser verificada.</span><span class="sxs-lookup"><span data-stu-id="46337-196">Click hello **Yes** button in hello Remote Desktop Connection box that appears, notifying you that hello identity of hello remote computer cannot be verified.</span></span>
8. <span data-ttu-id="46337-197">Clique o botão Iniciar do Windows do hello e clique em **Gerenciador de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="46337-197">Right-click hello Windows Start button and click **Device Manager**.</span></span> <span data-ttu-id="46337-198">Expanda Olá **adaptadores de rede** nó.</span><span class="sxs-lookup"><span data-stu-id="46337-198">Expand hello **Network adapters** node.</span></span> <span data-ttu-id="46337-199">Confirme que Olá **adaptador de Ethernet de função Virtual Mellanox ConnectX-3** aparece, como mostrado na figura abaixo de saudação:</span><span class="sxs-lookup"><span data-stu-id="46337-199">Confirm that hello **Mellanox ConnectX-3 Virtual Function Ethernet Adapter** appears, as shown in hello following picture:</span></span>
   
    ![Gerenciador de Dispositivos](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. <span data-ttu-id="46337-201">A Rede Acelerada agora está habilitada para sua VM.</span><span class="sxs-lookup"><span data-stu-id="46337-201">Accelerated Networking is now enabled for your VM.</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="46337-202">Criar uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="46337-202">Create a Linux VM</span></span>
<span data-ttu-id="46337-203">Você pode usar o hello portal do Azure ou Azure [PowerShell](#linux-powershell) toocreate um Ubuntu ou SLES VM.</span><span class="sxs-lookup"><span data-stu-id="46337-203">You can use hello Azure portal or Azure [PowerShell](#linux-powershell) toocreate an Ubuntu or SLES VM.</span></span> <span data-ttu-id="46337-204">Para VMs RHEL e CentOS, há um fluxo de trabalho diferente.</span><span class="sxs-lookup"><span data-stu-id="46337-204">For RHEL and CentOS VMs there is a different workflow.</span></span>  <span data-ttu-id="46337-205">Consulte as instruções de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="46337-205">Please see hello instructions below.</span></span>

### <span data-ttu-id="46337-206"><a name="linux-portal"></a>Portal</span><span class="sxs-lookup"><span data-stu-id="46337-206"><a name="linux-portal"></a>Portal</span></span>
1. <span data-ttu-id="46337-207">Registre-se para Olá acelerado de rede para a visualização de Linux completando as etapas 1 a 5 de saudação [criar uma VM do Linux - PowerShell](#linux-powershell) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="46337-207">Register for hello accelerated networking for Linux preview by completing steps 1-5 of hello [Create a Linux VM - PowerShell](#linux-powershell) section of this article.</span></span>  <span data-ttu-id="46337-208">Você não pode registrar para visualização de saudação no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="46337-208">You cannot register for hello preview in hello portal.</span></span>
2. <span data-ttu-id="46337-209">Concluir as etapas Olá em 1 a 8 [criar uma VM do Windows - portal](#windows-portal) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="46337-209">Complete steps 1-8 in hello [Create a Windows VM - portal](#windows-portal) section of this article.</span></span> <span data-ttu-id="46337-210">Na etapa 2, clique em **Ubuntu Server 16.04 LTS**, em vez de **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="46337-210">In step 2, click **Ubuntu Server 16.04 LTS** instead of **Windows Server 2016 Datacenter**.</span></span> <span data-ttu-id="46337-211">Para este tutorial, escolha toouse uma senha, em vez de uma chave SSH, embora para implantações de produção, você pode usar.</span><span class="sxs-lookup"><span data-stu-id="46337-211">For this tutorial, choose toouse a password, rather than an SSH key, though for production deployments, you can use either.</span></span> <span data-ttu-id="46337-212">Se **acelerado por rede** não aparece quando você concluir a etapa 7 da saudação [criar uma VM do Windows - portal](#windows-portal) seção deste artigo, é provável que uma saudação motivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="46337-212">If **Accelerated networking** does not appear when you complete step 7 of hello [Create a Windows VM - portal](#windows-portal) section of this article, it's likely for one of hello following reasons:</span></span>
    - <span data-ttu-id="46337-213">Você não ainda foram registradas para a visualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="46337-213">You are not yet registered for hello preview.</span></span> <span data-ttu-id="46337-214">Confirme se o estado do registro é **registrado**, conforme explicado na etapa 4 do hello [criar uma VM do Linux - Powershell](#linux-powershell) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="46337-214">Confirm that your registration state is **Registered**, as explained in step 4 of hello [Create a Linux VM - Powershell](#linux-powershell) section of this article.</span></span> <span data-ttu-id="46337-215">**Observação:** se você participou da saudação acelerada de rede para a visualização de máquinas virtuais do Windows (seu nenhum toouse tooregister necessário mais acelerado de rede para máquinas virtuais do Windows), você não é registrados automaticamente para Olá Accelerated rede para Visualização de VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="46337-215">**Note:** If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="46337-216">Você deve registrar para a rede de Accelerated Olá para VMs do Linux visualizar tooparticipate nele.</span><span class="sxs-lookup"><span data-stu-id="46337-216">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
    - <span data-ttu-id="46337-217">Você não selecionou um tamanho VM, o sistema operacional ou o local listado na Olá [limitações](#limitations) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="46337-217">You have not selected a VM size, operating system, or location listed in hello [Limitations](#limitations) section of this article.</span></span>
3. <span data-ttu-id="46337-218">Olá tooinstall acelerado driver de rede para Linux, Olá concluir as etapas em Olá [configurar Linux](#configure-linux) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="46337-218">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="46337-219"><a name="linux-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="46337-219"><a name="linux-powershell"></a>PowerShell</span></span>

>[!WARNING]
><span data-ttu-id="46337-220">Se você criar VMs do Linux com redes acelerado em uma assinatura e, em seguida, tente toocreate uma VM do Windows com a rede acelerada em Olá mesma assinatura, Olá criação de VM do Windows pode falhar.</span><span class="sxs-lookup"><span data-stu-id="46337-220">If you create Linux VMs with accelerated networking in a subscription, and then attempt toocreate a Windows VM with accelerated networking in hello same subscription, hello Windows VM creation may fail.</span></span> <span data-ttu-id="46337-221">Durante essa versão prévia, é recomendável testar VMs do Linux e do Windows com rede acelerada em assinaturas diferentes.</span><span class="sxs-lookup"><span data-stu-id="46337-221">During this preview, it's recommended that you test Linux and Windows VMs with accelerated networking in separate subscriptions.</span></span>
>

1. <span data-ttu-id="46337-222">Instale a versão mais recente Olá de saudação do Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo.</span><span class="sxs-lookup"><span data-stu-id="46337-222">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="46337-223">Se você for novo tooAzure PowerShell, ler Olá [visão geral do Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.</span><span class="sxs-lookup"><span data-stu-id="46337-223">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="46337-224">Iniciar uma sessão do PowerShell clicando o botão Iniciar do Windows hello, digitando **powershell**, em seguida, clicando em **PowerShell** Olá dos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="46337-224">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="46337-225">Na janela do PowerShell, digite Olá `login-azurermaccount` toosign de comando com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="46337-225">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="46337-226">Caso ainda não tenha uma conta, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="46337-226">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="46337-227">Registre-se para Olá acelerado de rede para o Azure preview Concluindo Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="46337-227">Register for hello accelerated networking for Azure preview by completing hello following steps:</span></span>
    - <span data-ttu-id="46337-228">Enviar um email muito[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) com sua ID de assinatura do Azure e o uso pretendido.</span><span class="sxs-lookup"><span data-stu-id="46337-228">Send an email too[axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) with your Azure subscription ID and intended use.</span></span> <span data-ttu-id="46337-229">Aguarde um email de confirmação da Microsoft sobre sua assinatura ser habilitada.</span><span class="sxs-lookup"><span data-stu-id="46337-229">Please wait for an email confirmation from Microsoft about your subscription being enabled.</span></span>
    - <span data-ttu-id="46337-230">Digite hello tooconfirm de comando que você está registrado para a visualização de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="46337-230">Enter hello following command tooconfirm you are registered for hello preview:</span></span>
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        <span data-ttu-id="46337-231">Não continue com a etapa 5 até **registrado** aparece no hello depois de inserir o comando anterior Olá de saída.</span><span class="sxs-lookup"><span data-stu-id="46337-231">Do not continue with step 5 until **Registered** appears in hello output after you enter hello previous command.</span></span> <span data-ttu-id="46337-232">A saída deve ter a aparência Olá seguir saída antes de continuar:</span><span class="sxs-lookup"><span data-stu-id="46337-232">Your output must look like hello following output before continuing:</span></span>
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      ><span data-ttu-id="46337-233">Se você participou da saudação acelerada de rede para a visualização de máquinas virtuais do Windows (seu nenhum toouse tooregister necessário mais acelerado de rede para máquinas virtuais do Windows), você não é registrados automaticamente para Olá acelerada de rede para a visualização de VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="46337-233">If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="46337-234">Você deve registrar para a rede de Accelerated Olá para VMs do Linux visualizar tooparticipate nele.</span><span class="sxs-lookup"><span data-stu-id="46337-234">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
      >
5. <span data-ttu-id="46337-235">No navegador, cópia Olá script a seguir substituindo Ubuntu ou SLES conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="46337-235">In your browser, copy hello following script substituting Ubuntu or SLES as desired.</span></span>  <span data-ttu-id="46337-236">Novamente, o Redhat e o CentOS têm um fluxo de trabalho diferente, descrito abaixo:</span><span class="sxs-lookup"><span data-stu-id="46337-236">Again, Redhat and CentOS have a different workflow outlined below:</span></span>

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

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
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

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. <span data-ttu-id="46337-237">Na janela do PowerShell, clique toopaste script de saudação e começar a executá-lo.</span><span class="sxs-lookup"><span data-stu-id="46337-237">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="46337-238">Você será solicitado a informar um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="46337-238">You are prompted for a username and password.</span></span> <span data-ttu-id="46337-239">Use essas credenciais toolog no toohello VM ao conectar-se tooit na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="46337-239">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="46337-240">Se o script hello falhar, confirme se:</span><span class="sxs-lookup"><span data-stu-id="46337-240">If hello script fails, confirm that:</span></span>
    - <span data-ttu-id="46337-241">Você está registrado para a visualização de hello, conforme explicado na etapa 4</span><span class="sxs-lookup"><span data-stu-id="46337-241">You are registered for hello preview, as explained in step 4</span></span>
    - <span data-ttu-id="46337-242">Se você alterou o tamanho, tipo de sistema operacional ou valores do local no script hello VM antes da execução, que os valores hello estão listados na Olá [limitações](#Limitations) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="46337-242">If you changed VM size, operating system type, or location values in hello script before executing it, that hello values are listed in hello [Limitations](#Limitations) section of this article.</span></span>
7. <span data-ttu-id="46337-243">Olá tooinstall acelerado driver de rede para Linux, Olá concluir as etapas em Olá [configurar Linux](#configure-linux) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="46337-243">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="46337-244"><a name="configure-linux"></a>Configurar Linux</span><span class="sxs-lookup"><span data-stu-id="46337-244"><a name="configure-linux"></a>Configure Linux</span></span>

<span data-ttu-id="46337-245">Quando você criar hello VM no Azure, você deve instalar o driver de rede acelerado Olá para Linux.</span><span class="sxs-lookup"><span data-stu-id="46337-245">Once you create hello VM in Azure, you must install hello accelerated networking driver for Linux.</span></span> <span data-ttu-id="46337-246">Antes de concluir Olá etapas a seguir, você deve ter uma VM do Linux criado com a rede acelerado usando qualquer Olá [portal](#linux-portal) ou [PowerShell](#linux-powershell) as etapas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="46337-246">Before completing hello following steps, you must have created a Linux VM with accelerated networking using either hello [portal](#linux-portal) or [PowerShell](#linux-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="46337-247">Em um navegador da Internet, abra hello Azure [portal](https://portal.azure.com) e entre com o Azure [conta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="46337-247">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="46337-248">Caso ainda não tenha uma conta, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="46337-248">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="46337-249">Na parte superior de saudação do direito de toohello portal, Olá de saudação *pesquisar recursos* barra, clique em Olá **> _** ícone toostart um shell de nuvem Bash (visualização).</span><span class="sxs-lookup"><span data-stu-id="46337-249">At hello top of hello portal, toohello right of hello *Search resources* bar, click hello **>_** icon toostart a Bash cloud shell (Preview).</span></span> <span data-ttu-id="46337-250">Olá Bash nuvem shell painel aparece na parte inferior de saudação do portal hello e após alguns segundos, apresenta um  **username@Azure:~ $** prompt.</span><span class="sxs-lookup"><span data-stu-id="46337-250">hello Bash cloud shell pane appears at hello bottom of hello portal and after a few seconds, presents a **username@Azure:~$** prompt.</span></span> <span data-ttu-id="46337-251">Embora seja possível SSH toohello VM do seu computador, em vez do shell de nuvem Olá, instruções de saudação neste tutorial presumem que você está usando o shell de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="46337-251">Though you can SSH toohello VM from your computer, rather than hello cloud shell, hello instructions in this tutorial assume you're using hello cloud shell.</span></span>
3. <span data-ttu-id="46337-252">Na parte superior de saudação do portal hello, na caixa de saudação que contém o texto de saudação *pesquisar recursos*, tipo *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="46337-252">At hello top of hello portal, in hello box that contains hello text *Search resources*, type *MyVm*.</span></span> <span data-ttu-id="46337-253">Quando **MyVm** aparece nos resultados da pesquisa hello, clique nele.</span><span class="sxs-lookup"><span data-stu-id="46337-253">When **MyVm** appears in hello search results, click it.</span></span>
4. <span data-ttu-id="46337-254">Em Olá **MyVm** folha que aparece, clique em Olá **conectar** botão no canto superior esquerdo de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="46337-254">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="46337-255">**Observação:** se **criando** for visível sob Olá **conectar** botão Azure ainda não foi concluída criando Olá VM.</span><span class="sxs-lookup"><span data-stu-id="46337-255">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="46337-256">Clique em **conectar** somente depois que você não verá mais **criando** em Olá **conectar** botão.</span><span class="sxs-lookup"><span data-stu-id="46337-256">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
5. <span data-ttu-id="46337-257">Azure abre uma caixa informando Olá tooenter `ssh adminuser@<ipaddress>`.</span><span class="sxs-lookup"><span data-stu-id="46337-257">Azure opens a box telling you tooenter hello `ssh adminuser@<ipaddress>`.</span></span> <span data-ttu-id="46337-258">Digite este comando no hello nuvem shell (ou cópia de caixa de saudação apareceu na etapa 4 e cole-o no shell de nuvem toohello), em seguida, pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="46337-258">Enter this command in hello cloud shell (or copy it from hello box that appeared in step 4 and paste it in toohello cloud shell), then press Enter.</span></span>
6. <span data-ttu-id="46337-259">Insira **Sim** toohello pergunta solicitando que você se você quiser se conectar toocontinue, em seguida, pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="46337-259">Enter **yes** toohello question asking you if you want toocontinue connecting, then press Enter.</span></span>
7. <span data-ttu-id="46337-260">Digite a senha de saudação inserido durante a criação de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="46337-260">Enter hello password you entered when creating hello VM.</span></span> <span data-ttu-id="46337-261">Uma vez fez logon com êxito no toohello VM, você verá um adminuser@MyVm:~ prompt$.</span><span class="sxs-lookup"><span data-stu-id="46337-261">Once successfully logged in toohello VM, you see an adminuser@MyVm:~$ prompt.</span></span> <span data-ttu-id="46337-262">Agora você está logado toohello VM por meio da sessão do shell de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="46337-262">You are now logged in toohello VM through hello cloud shell session.</span></span> <span data-ttu-id="46337-263">**Observação:** as sessões de cloud shell atingem o tempo limite depois de 10 minutos de inatividade.</span><span class="sxs-lookup"><span data-stu-id="46337-263">**Note:** Cloud shell sessions time out after 10 minutes of inactivity.</span></span>

<span data-ttu-id="46337-264">Neste ponto, instruções de saudação variam de acordo com distribuição Olá que você está usando.</span><span class="sxs-lookup"><span data-stu-id="46337-264">At this point, hello instructions vary based on hello distribution you are using.</span></span> 

#### <a name="ubuntusles"></a><span data-ttu-id="46337-265">Ubuntu/SLES</span><span class="sxs-lookup"><span data-stu-id="46337-265">Ubuntu/SLES</span></span>

1. <span data-ttu-id="46337-266">No prompt de hello, digite `uname -r` e confirmar versão Olá para:</span><span class="sxs-lookup"><span data-stu-id="46337-266">At hello prompt, enter `uname -r` and confirm hello version for:</span></span>

    * <span data-ttu-id="46337-267">O Ubuntu é "4.4.0-77-generic" ou superior</span><span class="sxs-lookup"><span data-stu-id="46337-267">Ubuntu is "4.4.0-77-generic," or greater</span></span>
    * <span data-ttu-id="46337-268">O SLES é "4.4.59-92.20-default" ou superior</span><span class="sxs-lookup"><span data-stu-id="46337-268">SLES is "4.4.59-92.20-default" or greater</span></span>

2. <span data-ttu-id="46337-269">Crie um vínculo entre o hello vNIC de rede padrão e vNIC rede Olá acelerado por execução de comandos Olá que seguem.</span><span class="sxs-lookup"><span data-stu-id="46337-269">Create a bond between hello standard networking vNIC and hello accelerated networking vNIC by running hello commands that follow.</span></span> <span data-ttu-id="46337-270">Tráfego de rede usa Olá maior desempenho acelerada vNIC de rede, enquanto o título Olá garante que o tráfego de rede não seja interrompido em determinadas alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="46337-270">Network traffic uses hello higher performing accelerated networking vNIC, while hello bond ensures that networking traffic is not interrupted across certain configuration changes.</span></span>
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. <span data-ttu-id="46337-271">Após executando o script hello, Olá VM será reiniciado depois de pausar a 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="46337-271">After running hello script, hello VM will restart after a 60 second pause.</span></span>
4. <span data-ttu-id="46337-272">Uma vez Olá VM é reiniciada, reconecte tooit completando as etapas 5 a 7 novamente.</span><span class="sxs-lookup"><span data-stu-id="46337-272">Once hello VM is restarted, reconnect tooit by completing steps 5-7 again.</span></span>
5. <span data-ttu-id="46337-273">Executar Olá `ifconfig` comando e confirme que ficou bond0 e interface hello está mostrando como backup.</span><span class="sxs-lookup"><span data-stu-id="46337-273">Run hello `ifconfig` command and confirm that bond0 has come up and hello interface is showing as UP.</span></span> 
 
 >[!NOTE]
      ><span data-ttu-id="46337-274">Aplicativos que usam a rede acelerado devem se comunicar através de saudação *bond0* interface não *eth0*.</span><span class="sxs-lookup"><span data-stu-id="46337-274">Applications using accelerated networking must communicate over hello *bond0* interface, not *eth0*.</span></span>  <span data-ttu-id="46337-275">nome da interface Olá pode alterar antes de rede acelerado alcança disponibilidade geral.</span><span class="sxs-lookup"><span data-stu-id="46337-275">hello interface name may change before accelerated networking reaches general availability.</span></span>

#### <a name="rhelcentos"></a><span data-ttu-id="46337-276">RHEL/CentOS</span><span class="sxs-lookup"><span data-stu-id="46337-276">RHEL/CentOS</span></span>

<span data-ttu-id="46337-277">Criando um Red Hat Enterprise Linux ou CentOS 7.3 VM requer alguns extra etapas tooload hello mais recentes drivers necessários para a SR-IOV e hello driver VF (função Virtual) para a placa de rede hello.</span><span class="sxs-lookup"><span data-stu-id="46337-277">Creating a Red Hat Enterprise Linux or CentOS 7.3 VM requires some extra steps tooload hello latest drivers needed for SR-IOV and hello Virtual Function (VF) driver for hello network card.</span></span> <span data-ttu-id="46337-278">Olá primeira fase de instruções Olá prepara a uma imagem que pode ser usado toomake um ou mais máquinas virtuais com drivers Olá pré-carregado.</span><span class="sxs-lookup"><span data-stu-id="46337-278">hello first phase of hello instructions prepares an image that can be used toomake one or more virtual machines that have hello drivers pre-loaded.</span></span>

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a><span data-ttu-id="46337-279">Fase um: preparar uma imagem base do Red Hat Enterprise Linux ou CentOS 7.3.</span><span class="sxs-lookup"><span data-stu-id="46337-279">Phase one: prepare a Red Hat Enterprise Linux or CentOS 7.3 base image.</span></span> 

1.  <span data-ttu-id="46337-280">Provisione uma VM CentOS 7.3 não SRIOV no Azure</span><span class="sxs-lookup"><span data-stu-id="46337-280">Provision a non-SRIOV CentOS 7.3 VM on Azure</span></span>

2.  <span data-ttu-id="46337-281">Instale o LIS 4.2.2:</span><span class="sxs-lookup"><span data-stu-id="46337-281">Install LIS 4.2.2:</span></span>
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  <span data-ttu-id="46337-282">Baixe os arquivos de configuração</span><span class="sxs-lookup"><span data-stu-id="46337-282">Download config files</span></span>
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  <span data-ttu-id="46337-283">Desprovisione essa VM</span><span class="sxs-lookup"><span data-stu-id="46337-283">Deprovision this VM</span></span>

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  <span data-ttu-id="46337-284">No portal do Azure, parar essa VM; e ir "Discos" do tooVM, captura o URI do VHD do hello OSDisk.</span><span class="sxs-lookup"><span data-stu-id="46337-284">From Azure portal, stop this VM; and go tooVM’s "Disks", capture hello OSDisk’s VHD URI.</span></span> <span data-ttu-id="46337-285">Esse URI contém o nome do VHD da imagem base hello e sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="46337-285">This URI contains hello base image’s VHD name and its storage account.</span></span> 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a><span data-ttu-id="46337-286">Fase dois: provisionar novas VMs no Azure</span><span class="sxs-lookup"><span data-stu-id="46337-286">Phase two: Provision new VMs on Azure</span></span>

1.  <span data-ttu-id="46337-287">Provisionar novas VMs com base em com New-AzureRMVMConfig usando Olá a imagem base do VHD capturado na fase 1, com AcceleratedNetworking ativado vNIC hello:</span><span class="sxs-lookup"><span data-stu-id="46337-287">Provision new VMs based with New-AzureRMVMConfig using hello base image VHD captured in phase one, with AcceleratedNetworking enabled on hello vNIC:</span></span>

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
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
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
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  <span data-ttu-id="46337-288">Depois de inicializam as VMs, verifique o dispositivo de FV hello, "lspci" e verifique Olá Mellanox entrada.</span><span class="sxs-lookup"><span data-stu-id="46337-288">After VMs boot up, check hello VF device by "lspci" and check hello Mellanox entry.</span></span> <span data-ttu-id="46337-289">Por exemplo, podemos deve ver este item na saída de lspci Olá:</span><span class="sxs-lookup"><span data-stu-id="46337-289">For example, we should see this item in hello lspci output:</span></span>
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  <span data-ttu-id="46337-290">Execute script de acoplamento Olá por:</span><span class="sxs-lookup"><span data-stu-id="46337-290">Run hello bonding script by:</span></span>

    ```bash
    sudo bondvf.sh
    ```

4.  <span data-ttu-id="46337-291">Reinicializar Olá novas VMs:</span><span class="sxs-lookup"><span data-stu-id="46337-291">Reboot hello new VMs:</span></span>

    ```bash
    sudo reboot
    ```

<span data-ttu-id="46337-292">Olá VM deve começar com bond0 configurado e hello caminho acelerado de rede habilitado.</span><span class="sxs-lookup"><span data-stu-id="46337-292">hello VM should start with bond0 configured and hello Accelerated Networking path enabled.</span></span>  <span data-ttu-id="46337-293">Executar `ifconfig` tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="46337-293">Run `ifconfig` tooconfirm.</span></span>
