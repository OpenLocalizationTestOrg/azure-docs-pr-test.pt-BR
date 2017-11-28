---
title: "aaaPlan de rede para replicação do Hyper-V (sem o System Center VMM) tooAzure com o Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve o planejamento da rede necessários ao replicar tooAzure de VMs Hyper-V (sem VMM)"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5ca12254-975d-48e8-a84d-422825dac9b2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: a35de72b53ca921a7b9bfca00a0edcb9416d5aa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-hyper-v-tooazure-replication"></a><span data-ttu-id="d420e-103">Etapa 4: Planejar a rede para replicação do Hyper-V tooAzure</span><span class="sxs-lookup"><span data-stu-id="d420e-103">Step 4: Plan networking for Hyper-V tooAzure replication</span></span>

<span data-ttu-id="d420e-104">Este artigo resume rede considerações de planejamento, quando a replicação local tooAzure de VMs Hyper-V (sem o System Center VMM) usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.</span><span class="sxs-lookup"><span data-stu-id="d420e-104">This article summarizes network planning considerations when replicating on-premises Hyper-V VMs (without System Center VMM) tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="d420e-105">Lançar os comentários na parte inferior da saudação deste artigo, ou fazer perguntas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="d420e-105">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connecting-tooreplica-vms-after-failover"></a><span data-ttu-id="d420e-106">Conectando VMs tooreplica após o failover</span><span class="sxs-lookup"><span data-stu-id="d420e-106">Connecting tooreplica VMs after failover</span></span>

<span data-ttu-id="d420e-107">Ao planejar sua estratégia de failover e replicação, uma das perguntas mais importantes Olá é como tooconnect toohello VM do Azure após o failover.</span><span class="sxs-lookup"><span data-stu-id="d420e-107">When planning your replication and failover strategy, one of hello key questions is how tooconnect toohello Azure VM after failover.</span></span> <span data-ttu-id="d420e-108">Há algumas opções ao criar sua estratégia de rede para VMs de réplica do Azure:</span><span class="sxs-lookup"><span data-stu-id="d420e-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="d420e-109">**Endereço IP diferente**: você pode selecionar toouse um intervalo de endereço IP diferente para Olá replicadas a rede VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="d420e-109">**Different IP address**: You can select toouse a different IP address range for hello replicated Azure VM network.</span></span> <span data-ttu-id="d420e-110">No hello cenário VM obtém um novo endereço IP após o failover, e é necessária uma atualização DNS.</span><span class="sxs-lookup"><span data-stu-id="d420e-110">In this scenario hello VM gets a new IP address after failover, and a DNS update is required.</span></span> [<span data-ttu-id="d420e-111">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="d420e-111">Learn more</span></span>](site-recovery-test-failover-vmm-to-vmm.md#prepare-the-infrastructure-for-test-failover)
- <span data-ttu-id="d420e-112">**Mesmo endereço IP**: talvez você queira toouse Olá mesmo intervalo de endereços IP, como no local primário de rede, para Olá rede Azure após o failover.</span><span class="sxs-lookup"><span data-stu-id="d420e-112">**Same IP address**: You might want toouse hello same IP address range as that in your primary on-premises network, for hello Azure network after failover.</span></span>  <span data-ttu-id="d420e-113">Olá mantendo mesmos endereços IP simplifica recuperação hello, reduzindo problemas relacionados à rede após o failover.</span><span class="sxs-lookup"><span data-stu-id="d420e-113">Keeping hello same IP addresses simplifies hello recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="d420e-114">No entanto, quando você estiver replicando tooAzure, você precisará tooupdate rotas com o novo local Olá endereços IP hello após o failover.</span><span class="sxs-lookup"><span data-stu-id="d420e-114">However, when you're replicating tooAzure, you will need tooupdate routes with hello new location of hello IP addresses after failover.</span></span>


## <a name="retain-ip-addresses"></a><span data-ttu-id="d420e-115">Reter os endereços IP</span><span class="sxs-lookup"><span data-stu-id="d420e-115">Retain IP addresses</span></span>

<span data-ttu-id="d420e-116">Recuperação de site fornece endereços IP hello recurso tooretain fixo durante o failover tooAzure, com um failover de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="d420e-116">Site Recovery provides hello capability tooretain fixed IP addresses when failing over tooAzure, with a subnet failover.</span></span>

<span data-ttu-id="d420e-117">Com o failover de sub-rede, uma sub-rede específica está presente no Site 1 ou Site 2, mas nunca em ambos os sites ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="d420e-117">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="d420e-118">Em ordem toomaintain Olá espaço de endereço IP no evento de saudação de um failover, você organiza programaticamente para Olá roteador infraestrutura toomove Olá subredes de tooanother de um site.</span><span class="sxs-lookup"><span data-stu-id="d420e-118">In order toomaintain hello IP address space in hello event of a failover, you programmatically arrange for hello router infrastructure toomove hello subnets from one site tooanother.</span></span> <span data-ttu-id="d420e-119">Durante o failover, Olá sub-redes mover com hello associados VMs protegidas.</span><span class="sxs-lookup"><span data-stu-id="d420e-119">During failover, hello subnets move with hello associated protected VMs.</span></span> <span data-ttu-id="d420e-120">Olá principal desvantagem é na saudação de uma falha, você tem subrede inteira toomove hello.</span><span class="sxs-lookup"><span data-stu-id="d420e-120">hello main drawback is that in hello event of a failure, you have toomove hello whole subnet.</span></span>


### <a name="failover-example"></a><span data-ttu-id="d420e-121">Exemplo de failover</span><span class="sxs-lookup"><span data-stu-id="d420e-121">Failover example</span></span>

<span data-ttu-id="d420e-122">Vejamos um exemplo de tooAzure de failover.</span><span class="sxs-lookup"><span data-stu-id="d420e-122">Let's look at an example for failover tooAzure.</span></span>

- <span data-ttu-id="d420e-123">Uma organização fictícia, o Woodgrove Bank, tem uma infraestrutura local que hospeda seus aplicativos de negócios.</span><span class="sxs-lookup"><span data-stu-id="d420e-123">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="d420e-124">Seus aplicativos móveis são hospedados no Azure.</span><span class="sxs-lookup"><span data-stu-id="d420e-124">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="d420e-125">Conectividade entre VMs do Woodgrove Bank em servidores locais e do Azure é fornecida por uma conexão de (VPN) site a site entre a rede de borda de local de saudação e Olá rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="d420e-125">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between hello on-premises edge network and hello Azure virtual network.</span></span>
- <span data-ttu-id="d420e-126">Isso significa VPN que Olá da rede virtual no Azure da empresa é exibido como uma extensão da sua rede local.</span><span class="sxs-lookup"><span data-stu-id="d420e-126">This VPN means that hello company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="d420e-127">O Woodgrove deseja toouse recuperação de Site tooreplicate local cargas de trabalho tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d420e-127">Woodgrove wants toouse Site Recovery tooreplicate on-premises workloads tooAzure.</span></span>
 - <span data-ttu-id="d420e-128">O Woodgrove tem toodeal com aplicativos e configurações que dependem embutido endereços IP e, portanto, precisam tooretain endereços IP para seus aplicativos depois tooAzure de failover.</span><span class="sxs-lookup"><span data-stu-id="d420e-128">Woodgrove has toodeal with applications and configurations which depend on hard-coded IP addresses, and thus need tooretain IP addresses for their applications after failover tooAzure.</span></span>
 - <span data-ttu-id="d420e-129">O Woodgrove tem endereços IP do intervalo 172.16.1.0/24, 172.16.2.0/24 tooits recursos atribuídos em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="d420e-129">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 tooits resources running in Azure.</span></span>


<span data-ttu-id="d420e-130">Para Woodgrove toobe capaz de tooreplicate tooAzure suas VMs, enquanto retendo Olá IP endereços, é aqui que empresa Olá precisa toodo:</span><span class="sxs-lookup"><span data-stu-id="d420e-130">For Woodgrove toobe able tooreplicate its VMs tooAzure while retaining hello IP addresses, here's what hello company needs toodo:</span></span>

1. <span data-ttu-id="d420e-131">Crie uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="d420e-131">Create an Azure virtual network.</span></span> <span data-ttu-id="d420e-132">Ele deve ser uma extensão da saudação de rede, no local para que os aplicativos podem fazer failover perfeitamente.</span><span class="sxs-lookup"><span data-stu-id="d420e-132">It should be an extension of hello on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="d420e-133">Azure permite que você tooadd site a site conectividade VPN, além de conectividade de site a toopoint toohello as redes virtuais criadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="d420e-133">Azure allows you tooadd site-to-site VPN connectivity, in addition toopoint-to-site connectivity toohello virtual networks created in Azure.</span></span>
3. <span data-ttu-id="d420e-134">Ao configurar a conexão de site a site Olá, em hello Azure de rede, você pode rotear o tráfego toohello local (rede local) somente se o intervalo de endereços IP hello é diferente do intervalo de endereços IP hello local.</span><span class="sxs-lookup"><span data-stu-id="d420e-134">When setting up hello site-to-site connection, in hello Azure network, you can route traffic toohello on-premises location (local-network) only if hello IP address range is different from hello on-premises IP address range.</span></span>
    - <span data-ttu-id="d420e-135">Isso ocorre porque o Azure não dá suporte a sub-redes ampliadas.</span><span class="sxs-lookup"><span data-stu-id="d420e-135">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="d420e-136">Então se você tiver sub-redes 192.168.1.0/24 local, não é possível adicionar 192.168.1.0/24 um local de rede na rede do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="d420e-136">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in hello Azure network.</span></span>
    - <span data-ttu-id="d420e-137">Isso é esperado, pois o Azure não sabe que não há nenhuma VM active na sub-rede hello e sub-rede hello está sendo criado para a recuperação de desastres.</span><span class="sxs-lookup"><span data-stu-id="d420e-137">This is expected because Azure doesn’t know that there are no active VMs in hello subnet, and that hello subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="d420e-138">toobe toocorrectly capaz de rotear o tráfego de rede fora de um Azure Olá sub-redes na rede de saudação e saudação da rede local não deve estar em conflito.</span><span class="sxs-lookup"><span data-stu-id="d420e-138">toobe able toocorrectly route network traffic out of an Azure network hello subnets in hello network and hello local-network mustn't conflict.</span></span>

![Antes do failover da sub-rede](./media/hyper-v-site-walkthrough-network/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="d420e-140">Antes do failover</span><span class="sxs-lookup"><span data-stu-id="d420e-140">Before failover</span></span>

1. <span data-ttu-id="d420e-141">Crie uma rede adicional (por exemplo, uma Rede de Recuperação).</span><span class="sxs-lookup"><span data-stu-id="d420e-141">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="d420e-142">Esta é a rede de saudação que passou por failover de máquinas virtuais são criados.</span><span class="sxs-lookup"><span data-stu-id="d420e-142">This is hello network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="d420e-143">tooensure que hello endereço IP para uma máquina virtual é mantido após um failover, nas propriedades VM hello > **configurar**, especifique Olá que Olá VM tem local e clique em de endereços IP mesmo **salvar**.</span><span class="sxs-lookup"><span data-stu-id="d420e-143">tooensure that hello IP address for a VM is retained after a failover, in hello VM properties > **Configure**, specify hello same IP address that hello VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="d420e-144">Quando Olá VM é feito o failover, Azure Site Recovery atribuirá Olá fornecido tooit de endereço IP.</span><span class="sxs-lookup"><span data-stu-id="d420e-144">When hello VM is failed over, Azure Site Recovery will assign hello provided IP address tooit.</span></span>

    ![Propriedades da rede](./media/hyper-v-site-walkthrough-network/network-design8.png)

4. <span data-ttu-id="d420e-146">Depois de failover disparador é acionado e Olá VMs são criadas no Azure com o endereço IP hello necessário, você pode se conectar toohello de rede usando um [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="d420e-146">After failover is trigger is triggered, and hello VMs are created in Azure with hello required IP address, you can connect toohello network using a [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="d420e-147">Essa ação pode ser inserida em um script.</span><span class="sxs-lookup"><span data-stu-id="d420e-147">This action can be scripted.</span></span>
5. <span data-ttu-id="d420e-148">Rotas necessário toobe modificado adequadamente, tooreflect que 192.168.1.0/24 agora foi movido tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d420e-148">Routes need toobe appropriately modified, tooreflect that 192.168.1.0/24 has now moved tooAzure.</span></span>

    ![Após o failover da sub-rede](./media/hyper-v-site-walkthrough-network/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="d420e-150">Após o failover</span><span class="sxs-lookup"><span data-stu-id="d420e-150">After failover</span></span>

<span data-ttu-id="d420e-151">Caso você não tenha uma rede do Azure, conforme ilustrado acima, poderá criar uma conexão VPN site a site entre o site primário e o Azure, após o failover.</span><span class="sxs-lookup"><span data-stu-id="d420e-151">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failvoer.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="d420e-152">Alterar os endereços IP</span><span class="sxs-lookup"><span data-stu-id="d420e-152">Change IP addresses</span></span>

<span data-ttu-id="d420e-153">Isso [postagem de blog](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explica como tooset backup Olá infraestrutura de rede do Azure, quando você não precisar tooretain IP endereços após o failover.</span><span class="sxs-lookup"><span data-stu-id="d420e-153">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how tooset up hello Azure networking infrastructure when you don't need tooretain IP addresses after failover.</span></span> <span data-ttu-id="d420e-154">Começa com uma descrição do aplicativo, procura no como tooset uma rede local e no Azure e termina com as informações sobre como executar failovers.</span><span class="sxs-lookup"><span data-stu-id="d420e-154">It starts with an application description, looks at how tooset up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d420e-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d420e-155">Next steps</span></span>

<span data-ttu-id="d420e-156">Vá muito[etapa 5: preparar o Azure](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="d420e-156">Go too[Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>
