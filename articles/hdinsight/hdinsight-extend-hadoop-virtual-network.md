---
title: aaaExtend HDInsight com a rede Virtual - Azure | Microsoft Docs
description: Saiba como toouse rede Virtual do Azure tooconnect HDInsight tooother nuvem recursos ou recursos no seu datacenter
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="85aa5-103">Estender o Azure HDInsight usando uma Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="85aa5-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="85aa5-104">Saiba como toouse HDInsight com um [rede Virtual do Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="85aa5-104">Learn how toouse HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="85aa5-105">Usar uma rede Virtual do Azure permite Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="85aa5-105">Using an Azure Virtual Network enables hello following scenarios:</span></span>

* <span data-ttu-id="85aa5-106">Conectando tooHDInsight diretamente de uma rede local.</span><span class="sxs-lookup"><span data-stu-id="85aa5-106">Connecting tooHDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="85aa5-107">Conectar HDInsight toodata armazena em uma rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="85aa5-107">Connecting HDInsight toodata stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="85aa5-108">Diretamente o acesso a serviços Hadoop que não estão disponível publicamente em Olá da internet.</span><span class="sxs-lookup"><span data-stu-id="85aa5-108">Directly accessing Hadoop services that are not available publicly over hello internet.</span></span> <span data-ttu-id="85aa5-109">Por exemplo, as APIs de Kafka ou Olá HBase Java API.</span><span class="sxs-lookup"><span data-stu-id="85aa5-109">For example, Kafka APIs or hello HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="85aa5-110">informações de saudação neste documento requerem uma compreensão de rede TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="85aa5-110">hello information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="85aa5-111">Se você não estiver familiarizado com a rede de TCP/IP, você deve trabalhar junto com alguém que está antes de fazer modificações tooproduction redes.</span><span class="sxs-lookup"><span data-stu-id="85aa5-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications tooproduction networks.</span></span>

## <a name="planning"></a><span data-ttu-id="85aa5-112">Planejamento</span><span class="sxs-lookup"><span data-stu-id="85aa5-112">Planning</span></span>

<span data-ttu-id="85aa5-113">Olá seguem perguntas Olá que você deve responder ao planejar tooinstall HDInsight em uma rede virtual:</span><span class="sxs-lookup"><span data-stu-id="85aa5-113">hello following are hello questions that you must answer when planning tooinstall HDInsight in a virtual network:</span></span>

* <span data-ttu-id="85aa5-114">Você precisa tooinstall HDInsight em uma rede virtual existente?</span><span class="sxs-lookup"><span data-stu-id="85aa5-114">Do you need tooinstall HDInsight into an existing virtual network?</span></span> <span data-ttu-id="85aa5-115">Ou você está criando uma nova rede?</span><span class="sxs-lookup"><span data-stu-id="85aa5-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="85aa5-116">Se você estiver usando uma rede virtual existente, talvez seja necessário toomodify configuração de rede de saudação antes de instalar o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85aa5-116">If you are using an existing virtual network, you may need toomodify hello network configuration before you can install HDInsight.</span></span> <span data-ttu-id="85aa5-117">Para obter mais informações, consulte Olá [adicionar a rede virtual existente do HDInsight tooan](#existingvnet) seção.</span><span class="sxs-lookup"><span data-stu-id="85aa5-117">For more information, see hello [add HDInsight tooan existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="85aa5-118">Você deseja que sua rede local ou rede virtual do hello tooconnect que contém a rede virtual do HDInsight tooanother?</span><span class="sxs-lookup"><span data-stu-id="85aa5-118">Do you want tooconnect hello virtual network containing HDInsight tooanother virtual network or your on-premises network?</span></span>

    <span data-ttu-id="85aa5-119">trabalho de tooeasily com recursos em redes, você pode precisar toocreate um DNS personalizado e configure o encaminhamento de DNS.</span><span class="sxs-lookup"><span data-stu-id="85aa5-119">tooeasily work with resources across networks, you may need toocreate a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="85aa5-120">Para obter mais informações, consulte Olá [conectar várias redes](#multinet) seção.</span><span class="sxs-lookup"><span data-stu-id="85aa5-120">For more information, see hello [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="85aa5-121">Você deseja toorestrict/redirecionar tráfego de entrada ou saída tooHDInsight?</span><span class="sxs-lookup"><span data-stu-id="85aa5-121">Do you want toorestrict/redirect inbound or outbound traffic tooHDInsight?</span></span>

    <span data-ttu-id="85aa5-122">HDInsight deve ter irrestrito a comunicação com endereços IP específicos no hello data center do Azure.</span><span class="sxs-lookup"><span data-stu-id="85aa5-122">HDInsight must have unrestricted communication with specific IP addresses in hello Azure data center.</span></span> <span data-ttu-id="85aa5-123">Também há diversas portas que devem receber permissão por meio de firewalls para a comunicação do cliente.</span><span class="sxs-lookup"><span data-stu-id="85aa5-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="85aa5-124">Para obter mais informações, consulte Olá [controlando o tráfego de rede](#networktraffic) seção.</span><span class="sxs-lookup"><span data-stu-id="85aa5-124">For more information, see hello [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="85aa5-125"><a id="existingvnet"></a>Adicionar a rede virtual existente do HDInsight tooan</span><span class="sxs-lookup"><span data-stu-id="85aa5-125"><a id="existingvnet"></a>Add HDInsight tooan existing virtual network</span></span>

<span data-ttu-id="85aa5-126">Use etapas Olá toodiscover esta seção como tooadd um novo tooan de HDInsight existente da rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="85aa5-126">Use hello steps in this section toodiscover how tooadd a new HDInsight tooan existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="85aa5-127">Não é possível adicionar um cluster HDInsight existente a uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="85aa5-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="85aa5-128">Você está usando um clássico ou modelo de implantação do Gerenciador de recursos de rede virtual Olá?</span><span class="sxs-lookup"><span data-stu-id="85aa5-128">Are you using a classic or Resource Manager deployment model for hello virtual network?</span></span>

    <span data-ttu-id="85aa5-129">O HDInsight 3.4 e posterior exige uma rede virtual do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="85aa5-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="85aa5-130">Versões anteriores do HDInsight exigiam uma rede virtual clássica.</span><span class="sxs-lookup"><span data-stu-id="85aa5-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="85aa5-131">Se sua rede existente é uma rede virtual clássica, crie uma rede virtual do Gerenciador de recursos e, em seguida, conecte-se Olá dois.</span><span class="sxs-lookup"><span data-stu-id="85aa5-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect hello two.</span></span> <span data-ttu-id="85aa5-132">[Conectando clássico VNets toonew VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span><span class="sxs-lookup"><span data-stu-id="85aa5-132">[Connecting classic VNets toonew VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="85aa5-133">Depois de ingressar, HDInsight instalado na rede do Gerenciador de recursos de saudação pode interagir com recursos de rede clássicos hello.</span><span class="sxs-lookup"><span data-stu-id="85aa5-133">Once joined, HDInsight installed in hello Resource Manager network can interact with resources in hello classic network.</span></span>

2. <span data-ttu-id="85aa5-134">Você usa o túnel forçado?</span><span class="sxs-lookup"><span data-stu-id="85aa5-134">Do you use forced tunneling?</span></span> <span data-ttu-id="85aa5-135">O túnel forçado é uma configuração de sub-rede que força a saída dispositivo tooa de tráfego de Internet para inspeção e registro em log.</span><span class="sxs-lookup"><span data-stu-id="85aa5-135">Forced tunneling is a subnet setting that forces outbound Internet traffic tooa device for inspection and logging.</span></span> <span data-ttu-id="85aa5-136">O HDInsight não dá suporte ao túnel forçado.</span><span class="sxs-lookup"><span data-stu-id="85aa5-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="85aa5-137">Remova o túnel forçado antes de instalar o HDInsight em uma sub-rede ou crie uma nova sub-rede para o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85aa5-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="85aa5-138">Você usa grupos de segurança de rede, rotas definidas pelo usuário ou o tráfego de toorestrict de dispositivos de rede Virtual para ou de rede virtual Olá?</span><span class="sxs-lookup"><span data-stu-id="85aa5-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances toorestrict traffic into or out of hello virtual network?</span></span>

    <span data-ttu-id="85aa5-139">Como um serviço gerenciado, o HDInsight requer acesso irrestrito tooseveral endereços IP no hello data center do Azure.</span><span class="sxs-lookup"><span data-stu-id="85aa5-139">As a managed service, HDInsight requires unrestricted access tooseveral IP addresses in hello Azure data center.</span></span> <span data-ttu-id="85aa5-140">comunicação tooallow com esses endereços IP, atualizar todos os grupos de segurança de rede existentes ou rotas definidas pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="85aa5-140">tooallow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="85aa5-141">O HDInsight hospeda vários serviços, que usam uma variedade de portas.</span><span class="sxs-lookup"><span data-stu-id="85aa5-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="85aa5-142">Não bloquear o tráfego de portas toothese.</span><span class="sxs-lookup"><span data-stu-id="85aa5-142">Do not block traffic toothese ports.</span></span> <span data-ttu-id="85aa5-143">Para obter uma lista de portas tooallow através de firewalls de dispositivo virtual, consulte Olá [segurança](#security) seção.</span><span class="sxs-lookup"><span data-stu-id="85aa5-143">For a list of ports tooallow through virtual appliance firewalls, see hello [Security](#security) section.</span></span>

    <span data-ttu-id="85aa5-144">toofind sua configuração de segurança existente, use hello Azure PowerShell ou CLI do Azure comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="85aa5-144">toofind your existing security configuration, use hello following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="85aa5-145">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="85aa5-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="85aa5-146">Para obter mais informações, consulte Olá [solucionar problemas de grupos de segurança de rede](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) documento.</span><span class="sxs-lookup"><span data-stu-id="85aa5-146">For more information, see hello [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="85aa5-147">As regras do grupo de segurança de rede são aplicadas em ordem, com base na prioridade da regra.</span><span class="sxs-lookup"><span data-stu-id="85aa5-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="85aa5-148">Olá primeira regra correspondente padrão de tráfego de saudação é aplicada, e nenhum outro são aplicados para que o tráfego.</span><span class="sxs-lookup"><span data-stu-id="85aa5-148">hello first rule that matches hello traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="85aa5-149">Regras de ordem do mais permissivo tooleast permissivo.</span><span class="sxs-lookup"><span data-stu-id="85aa5-149">Order rules from most permissive tooleast permissive.</span></span> <span data-ttu-id="85aa5-150">Para obter mais informações, consulte Olá [filtrar o tráfego de rede com os grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md) documento.</span><span class="sxs-lookup"><span data-stu-id="85aa5-150">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="85aa5-151">Rotas definidas pelo usuário</span><span class="sxs-lookup"><span data-stu-id="85aa5-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="85aa5-152">Para obter mais informações, consulte Olá [solucionar rotas](../virtual-network/virtual-network-routes-troubleshoot-portal.md) documento.</span><span class="sxs-lookup"><span data-stu-id="85aa5-152">For more information, see hello [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="85aa5-153">Criar um cluster HDInsight e selecione Olá rede Virtual do Azure durante a configuração.</span><span class="sxs-lookup"><span data-stu-id="85aa5-153">Create an HDInsight cluster and select hello Azure Virtual Network during configuration.</span></span> <span data-ttu-id="85aa5-154">Use as etapas de Olá Olá seguindo o processo de criação de cluster do documentos toounderstand hello:</span><span class="sxs-lookup"><span data-stu-id="85aa5-154">Use hello steps in hello following documents toounderstand hello cluster creation process:</span></span>

    * [<span data-ttu-id="85aa5-155">Criar HDInsight usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="85aa5-155">Create HDInsight using hello Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [<span data-ttu-id="85aa5-156">Criar o HDInsight usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="85aa5-156">Create HDInsight using Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [<span data-ttu-id="85aa5-157">Criar o HDInsight usando a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="85aa5-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="85aa5-158">Criar o HDInsight usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="85aa5-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="85aa5-159">Rede virtual tooa adicionando HDInsight é uma etapa de configuração opcional.</span><span class="sxs-lookup"><span data-stu-id="85aa5-159">Adding HDInsight tooa virtual network is an optional configuration step.</span></span> <span data-ttu-id="85aa5-160">Ser-se de rede virtual Olá de tooselect durante a configuração de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="85aa5-160">Be sure tooselect hello virtual network when configuring hello cluster.</span></span>

## <span data-ttu-id="85aa5-161"><a id="multinet"></a>Conectando várias redes</span><span class="sxs-lookup"><span data-stu-id="85aa5-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="85aa5-162">Olá maior desafio com uma configuração de multi-rede de é a resolução de nomes entre redes de saudação.</span><span class="sxs-lookup"><span data-stu-id="85aa5-162">hello biggest challenge with a multi-network configuration is name resolution between hello networks.</span></span>

<span data-ttu-id="85aa5-163">O Azure fornece a resolução de nomes para os serviços do Azure instalados em uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="85aa5-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="85aa5-164">Essa resolução de nome interno permite HDInsight tooconnect toohello a seguir de recursos usando um nome de domínio totalmente qualificado (FQDN):</span><span class="sxs-lookup"><span data-stu-id="85aa5-164">This built-in name resolution allows HDInsight tooconnect toohello following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="85aa5-165">Qualquer recurso que está disponível no hello da internet.</span><span class="sxs-lookup"><span data-stu-id="85aa5-165">Any resource that is available on hello internet.</span></span> <span data-ttu-id="85aa5-166">Por exemplo, microsoft.com, google.com.</span><span class="sxs-lookup"><span data-stu-id="85aa5-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="85aa5-167">Qualquer recurso que está em Olá mesma rede Virtual do Azure, usando Olá __nome DNS interno__ do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="85aa5-167">Any resource that is in hello same Azure Virtual Network, by using hello __internal DNS name__ of hello resource.</span></span> <span data-ttu-id="85aa5-168">Por exemplo, ao usar a resolução de nome padrão hello, Olá seguem exemplo interno DNS nomes atribuídos tooHDInsight nós de trabalho:</span><span class="sxs-lookup"><span data-stu-id="85aa5-168">For example, when using hello default name resolution, hello following are example internal DNS names assigned tooHDInsight worker nodes:</span></span>

    * <span data-ttu-id="85aa5-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="85aa5-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="85aa5-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="85aa5-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="85aa5-171">Esses dois nós podem se comunicar diretamente um com o outro e com outros nós no HDInsight, usando nomes DNS internos.</span><span class="sxs-lookup"><span data-stu-id="85aa5-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="85aa5-172">resolução de nome padrão Olá __não__ permitir HDInsight tooresolve nomes de saudação de recursos em redes de rede virtual toohello unidas.</span><span class="sxs-lookup"><span data-stu-id="85aa5-172">hello default name resolution does __not__ allow HDInsight tooresolve hello names of resources in networks that are joined toohello virtual network.</span></span> <span data-ttu-id="85aa5-173">Por exemplo, é comum toojoin seu local de rede virtual toohello de rede.</span><span class="sxs-lookup"><span data-stu-id="85aa5-173">For example, it is common toojoin your on-premises network toohello virtual network.</span></span> <span data-ttu-id="85aa5-174">Apenas saudação padrão resolução de nomes, HDInsight não pode acessar recursos na rede de local de saudação por nome.</span><span class="sxs-lookup"><span data-stu-id="85aa5-174">With only hello default name resolution, HDInsight cannot access resources in hello on-premises network by name.</span></span> <span data-ttu-id="85aa5-175">Olá oposto também é verdadeiro, recursos em sua rede local não podem acessar recursos na rede virtual Olá por nome.</span><span class="sxs-lookup"><span data-stu-id="85aa5-175">hello opposite is also true, resources in your on-premises network cannot access resources in hello virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="85aa5-176">Você deve criar um servidor DNS personalizado hello e configurar Olá rede virtual toouse-lo antes de criar hello cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85aa5-176">You must create hello custom DNS server and configure hello virtual network toouse it before creating hello HDInsight cluster.</span></span>

<span data-ttu-id="85aa5-177">resolução de nomes de tooenable entre a rede virtual hello e recursos em redes associadas, você deve executar Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="85aa5-177">tooenable name resolution between hello virtual network and resources in joined networks, you must perform hello following actions:</span></span>

1. <span data-ttu-id="85aa5-178">Crie um servidor DNS personalizado no hello rede Virtual do Azure, onde você planeja tooinstall HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85aa5-178">Create a custom DNS server in hello Azure Virtual Network where you plan tooinstall HDInsight.</span></span>

2. <span data-ttu-id="85aa5-179">Configure Olá rede virtual toouse Olá servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="85aa5-179">Configure hello virtual network toouse hello custom DNS server.</span></span>

3. <span data-ttu-id="85aa5-180">Localize hello que Azure atribuiu sufixo DNS para sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="85aa5-180">Find hello Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="85aa5-181">Esse valor é muito semelhante`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="85aa5-181">This value is similar too`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="85aa5-182">Para obter informações sobre como encontrar o sufixo DNS hello, consulte Olá [exemplo: DNS personalizado](#example-dns) seção.</span><span class="sxs-lookup"><span data-stu-id="85aa5-182">For information on finding hello DNS suffix, see hello [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="85aa5-183">Configure o encaminhamento entre os servidores DNS hello.</span><span class="sxs-lookup"><span data-stu-id="85aa5-183">Configure forwarding between hello DNS servers.</span></span> <span data-ttu-id="85aa5-184">configuração Olá depende do tipo hello da rede remota.</span><span class="sxs-lookup"><span data-stu-id="85aa5-184">hello configuration depends on hello type of remote network.</span></span>

    * <span data-ttu-id="85aa5-185">Se a rede remota Olá é uma rede local, configure o DNS da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="85aa5-185">If hello remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="85aa5-186">__DNS personalizado__ (na rede virtual de saudação):</span><span class="sxs-lookup"><span data-stu-id="85aa5-186">__Custom DNS__ (in hello virtual network):</span></span>

            * <span data-ttu-id="85aa5-187">Encaminhar solicitações para o sufixo DNS de saudação do resolvedor do Azure recursiva toohello do hello rede virtual (168.63.129.16).</span><span class="sxs-lookup"><span data-stu-id="85aa5-187">Forward requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="85aa5-188">Azure lida com solicitações de recursos na rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="85aa5-188">Azure handles requests for resources in hello virtual network</span></span>

            * <span data-ttu-id="85aa5-189">Encaminhe todas as outra solicitações toohello no servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="85aa5-189">Forward all other requests toohello on-premises DNS server.</span></span> <span data-ttu-id="85aa5-190">Olá locais DNS manipula todas as outras solicitações de resolução de nome, até mesmo solicitações para recursos de internet, como Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="85aa5-190">hello on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="85aa5-191">__DNS local__: encaminhar solicitações para Olá rede virtual DNS sufixo toohello um servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="85aa5-191">__On-premises DNS__: Forward requests for hello virtual network DNS suffix toohello custom DNS server.</span></span> <span data-ttu-id="85aa5-192">um servidor DNS personalizado Hello, em seguida, encaminha toohello recursiva Azure resolvedor.</span><span class="sxs-lookup"><span data-stu-id="85aa5-192">hello custom DNS server then forwards toohello Azure recursive resolver.</span></span>

        <span data-ttu-id="85aa5-193">Solicitações de rotas essa configuração para totalmente qualificado de nomes de domínio que contêm o sufixo DNS Olá Olá virtual toohello personalizado DNS do servidor de rede.</span><span class="sxs-lookup"><span data-stu-id="85aa5-193">This configuration routes requests for fully qualified domain names that contain hello DNS suffix of hello virtual network toohello custom DNS server.</span></span> <span data-ttu-id="85aa5-194">Todas as outras solicitações (até mesmo para endereços da internet pública) são manipuladas pelo servidor DNS local hello.</span><span class="sxs-lookup"><span data-stu-id="85aa5-194">All other requests (even for public internet addresses) are handled by hello on-premises DNS server.</span></span>

    * <span data-ttu-id="85aa5-195">Se a rede remota Olá é outra rede Virtual do Azure, configure DNS da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="85aa5-195">If hello remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="85aa5-196">__DNS personalizado__ (em cada rede virtual):</span><span class="sxs-lookup"><span data-stu-id="85aa5-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="85aa5-197">As solicitações para o sufixo DNS de saudação de redes virtuais Olá são encaminhadas toohello servidores DNS personalizados.</span><span class="sxs-lookup"><span data-stu-id="85aa5-197">Requests for hello DNS suffix of hello virtual networks are forwarded toohello custom DNS servers.</span></span> <span data-ttu-id="85aa5-198">Olá DNS em cada rede virtual é responsável por resolver recursos em sua rede.</span><span class="sxs-lookup"><span data-stu-id="85aa5-198">hello DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="85aa5-199">Encaminhe todos os outros resolvedor de Azure recursiva de toohello solicitações.</span><span class="sxs-lookup"><span data-stu-id="85aa5-199">Forward all other requests toohello Azure recursive resolver.</span></span> <span data-ttu-id="85aa5-200">resolvedor de recursiva Olá é responsável por resolver o local e os recursos da internet.</span><span class="sxs-lookup"><span data-stu-id="85aa5-200">hello recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="85aa5-201">servidor DNS Olá para cada rede encaminha solicitações toohello outros, com base em sufixo DNS.</span><span class="sxs-lookup"><span data-stu-id="85aa5-201">hello DNS server for each network forwards requests toohello other, based on DNS suffix.</span></span> <span data-ttu-id="85aa5-202">Outras solicitações são resolvidas usando hello Azure recursiva resolvedor.</span><span class="sxs-lookup"><span data-stu-id="85aa5-202">Other requests are resolved using hello Azure recursive resolver.</span></span>

    <span data-ttu-id="85aa5-203">Para obter um exemplo de cada configuração, consulte Olá [exemplo: DNS personalizado](#example-dns) seção.</span><span class="sxs-lookup"><span data-stu-id="85aa5-203">For an example of each configuration, see hello [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="85aa5-204">Para obter mais informações, consulte Olá [resolução de nomes para VMs e instâncias de função](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) documento.</span><span class="sxs-lookup"><span data-stu-id="85aa5-204">For more information, see hello [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-toohadoop-services"></a><span data-ttu-id="85aa5-205">Conectar-se diretamente tooHadoop serviços</span><span class="sxs-lookup"><span data-stu-id="85aa5-205">Directly connect tooHadoop services</span></span>

<span data-ttu-id="85aa5-206">Mais documentação no HDInsight supõe que você tenha o cluster de toohello de acesso sobre Olá internet.</span><span class="sxs-lookup"><span data-stu-id="85aa5-206">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="85aa5-207">Por exemplo, você pode se conectar a cluster toohello em https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="85aa5-207">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="85aa5-208">Esse endereço usa o gateway pública hello, que não está disponível se você tiver usado os NSGs ou UDRs toorestrict acesso Olá da internet.</span><span class="sxs-lookup"><span data-stu-id="85aa5-208">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="85aa5-209">tooconnect tooAmbari e outras páginas da web por meio da rede virtual do hello, use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="85aa5-209">tooconnect tooAmbari and other web pages through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="85aa5-210">toodiscover Olá interno nomes totalmente qualificados (FQDN) de nós de cluster do HDInsight hello, use um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="85aa5-210">toodiscover hello internal fully qualified domain names (FQDN) of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    <span data-ttu-id="85aa5-211">Na lista de saudação de nós retornados, localize Olá FQDN para Olá nós de cabeçalho e use Olá FQDNs tooconnect tooAmbari e outros serviços da web.</span><span class="sxs-lookup"><span data-stu-id="85aa5-211">In hello list of nodes returned, find hello FQDN for hello head nodes and use hello FQDNs tooconnect tooAmbari and other web services.</span></span> <span data-ttu-id="85aa5-212">Por exemplo, use `http://<headnode-fqdn>:8080` tooaccess Ambari.</span><span class="sxs-lookup"><span data-stu-id="85aa5-212">For example, use `http://<headnode-fqdn>:8080` tooaccess Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="85aa5-213">Alguns serviços hospedados em nós de cabeçalho hello serão apenas ativos em um nó por vez.</span><span class="sxs-lookup"><span data-stu-id="85aa5-213">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="85aa5-214">Se você tentar acessar um serviço em um nó de cabeçalho e retorna um erro 404, alterne toohello outro nó principal.</span><span class="sxs-lookup"><span data-stu-id="85aa5-214">If you try accessing a service on one head node and it returns a 404 error, switch toohello other head node.</span></span>

2. <span data-ttu-id="85aa5-215">nó de saudação toodetermine e porta de um serviço estiver disponível, consulte Olá [portas usadas por serviços de Hadoop no HDInsight](./hdinsight-hadoop-port-settings-for-services.md) documento.</span><span class="sxs-lookup"><span data-stu-id="85aa5-215">toodetermine hello node and port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="85aa5-216"><a id="networktraffic"></a> Controlando o tráfego de rede</span><span class="sxs-lookup"><span data-stu-id="85aa5-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="85aa5-217">Tráfego de rede em redes virtuais do Azure pode ser controlado usando Olá métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="85aa5-217">Network traffic in an Azure Virtual Networks can be controlled using hello following methods:</span></span>

* <span data-ttu-id="85aa5-218">**Grupos de segurança de rede** (NSG) permitem o tráfego de entrada e saída de toofilter toohello de rede.</span><span class="sxs-lookup"><span data-stu-id="85aa5-218">**Network security groups** (NSG) allow you toofilter inbound and outbound traffic toohello network.</span></span> <span data-ttu-id="85aa5-219">Para obter mais informações, consulte Olá [filtrar o tráfego de rede com os grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md) documento.</span><span class="sxs-lookup"><span data-stu-id="85aa5-219">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="85aa5-220">O HDInsight não dá suporte à restrição do tráfego de saída.</span><span class="sxs-lookup"><span data-stu-id="85aa5-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="85aa5-221">**Rotas definidas pelo usuário** (UDR) definem como os fluxos de tráfego entre os recursos na rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="85aa5-221">**User-defined routes** (UDR) define how traffic flows between resources in hello network.</span></span> <span data-ttu-id="85aa5-222">Para obter mais informações, consulte Olá [rotas definidas pelo usuário e encaminhamento de IP](../virtual-network/virtual-networks-udr-overview.md) documento.</span><span class="sxs-lookup"><span data-stu-id="85aa5-222">For more information, see hello [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="85aa5-223">**Soluções de virtualização de rede** duplicar a funcionalidade de saudação de dispositivos, como roteadores e firewalls.</span><span class="sxs-lookup"><span data-stu-id="85aa5-223">**Network virtual appliances** replicate hello functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="85aa5-224">Para obter mais informações, consulte Olá [dispositivos de rede](https://azure.microsoft.com/solutions/network-appliances) documento.</span><span class="sxs-lookup"><span data-stu-id="85aa5-224">For more information, see hello [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="85aa5-225">Como um serviço gerenciado, o HDInsight requer acesso irrestrito tooAzure integridade e o gerenciamento de serviços na nuvem do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="85aa5-225">As a managed service, HDInsight requires unrestricted access tooAzure health and management services in hello Azure cloud.</span></span> <span data-ttu-id="85aa5-226">Ao usar NSGs e UDRs, verifique se o HDInsight e esses serviços podem se comunicar com o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85aa5-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="85aa5-227">O HDInsight expõe serviços em várias portas.</span><span class="sxs-lookup"><span data-stu-id="85aa5-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="85aa5-228">Ao usar um firewall de dispositivo virtual, você deve permitir tráfego na Olá portas usadas para esses serviços.</span><span class="sxs-lookup"><span data-stu-id="85aa5-228">When using a virtual appliance firewall, you must allow traffic on hello ports used for these services.</span></span> <span data-ttu-id="85aa5-229">Para obter mais informações, consulte a seção de saudação [portas necessárias].</span><span class="sxs-lookup"><span data-stu-id="85aa5-229">For more information, see hello [Required ports] section.</span></span>

### <span data-ttu-id="85aa5-230"><a id="hdinsight-ip"></a> HDInsight com grupos de segurança de rede e rotas definidas pelo usuário</span><span class="sxs-lookup"><span data-stu-id="85aa5-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="85aa5-231">Se você planeja usar **grupos de segurança de rede** ou **rotas definidas pelo usuário** toocontrol o tráfego de rede, execute Olá ações a seguir antes de instalar o HDInsight:</span><span class="sxs-lookup"><span data-stu-id="85aa5-231">If you plan on using **network security groups** or **user-defined routes** toocontrol network traffic, perform hello following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="85aa5-232">Identifica Olá região do Azure que você planeje toouse para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85aa5-232">Identify hello Azure region that you plan toouse for HDInsight.</span></span>

2. <span data-ttu-id="85aa5-233">Identificar os endereços IP hello exigidos pelo HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85aa5-233">Identify hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="85aa5-234">Para obter mais informações, consulte Olá [endereços IP necessários para HDInsight](#hdinsight-ip) seção.</span><span class="sxs-lookup"><span data-stu-id="85aa5-234">For more information, see hello [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="85aa5-235">Criar ou modificar grupos de segurança de rede hello ou rotas definidas pelo usuário para a sub-rede de saudação que você planeje tooinstall HDInsight em.</span><span class="sxs-lookup"><span data-stu-id="85aa5-235">Create or modify hello network security groups or user-defined routes for hello subnet that you plan tooinstall HDInsight into.</span></span>

    * <span data-ttu-id="85aa5-236">__Grupos de segurança de rede__: permitir __entrada__ o tráfego na porta __443__ de endereços IP de saudação.</span><span class="sxs-lookup"><span data-stu-id="85aa5-236">__Network security groups__: allow __inbound__ traffic on port __443__ from hello IP addresses.</span></span>
    * <span data-ttu-id="85aa5-237">__Rotas definidas pelo usuário__: criar um endereço IP de tooeach de rota e defina Olá __tipo do próximo salto__ too__Internet__.</span><span class="sxs-lookup"><span data-stu-id="85aa5-237">__User-defined routes__: create a route tooeach IP address and set hello __Next hop type__ too__Internet__.</span></span>

<span data-ttu-id="85aa5-238">Para obter mais informações sobre grupos de segurança de rede ou rotas definidas pelo usuário, consulte Olá documentação a seguir:</span><span class="sxs-lookup"><span data-stu-id="85aa5-238">For more information on network security groups or user-defined routes, see hello following documentation:</span></span>

* [<span data-ttu-id="85aa5-239">Grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="85aa5-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="85aa5-240">Rotas definidas pelo usuário</span><span class="sxs-lookup"><span data-stu-id="85aa5-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="85aa5-241">Túnel forçado</span><span class="sxs-lookup"><span data-stu-id="85aa5-241">Forced tunneling</span></span>

<span data-ttu-id="85aa5-242">O túnel forçado é uma configuração de roteamento definido pelo usuário em que todo o tráfego de uma sub-rede é forçado tooa específicos de rede ou local, como sua rede local.</span><span class="sxs-lookup"><span data-stu-id="85aa5-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced tooa specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="85aa5-243">O HDInsight __não__ dá suporte ao túnel forçado.</span><span class="sxs-lookup"><span data-stu-id="85aa5-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="85aa5-244"><a id="hdinsight-ip"></a> Endereços IP obrigatórios</span><span class="sxs-lookup"><span data-stu-id="85aa5-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85aa5-245">Olá integridade do Azure e serviços de gerenciamento devem ser capaz de toocommunicate com HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85aa5-245">hello Azure health and management services must be able toocommunicate with HDInsight.</span></span> <span data-ttu-id="85aa5-246">Se você usar grupos de segurança de rede ou rotas definidas pelo usuário, permita o tráfego da saudação endereços IP para essas tooreach serviços HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85aa5-246">If you use network security groups or user-defined routes, allow traffic from hello IP addresses for these services tooreach HDInsight.</span></span>
>
> <span data-ttu-id="85aa5-247">Se você não usar grupos de segurança de rede ou tráfego de toocontrol rotas definidas pelo usuário, você pode ignorar esta seção.</span><span class="sxs-lookup"><span data-stu-id="85aa5-247">If you do not use network security groups or user-defined routes toocontrol traffic, you can ignore this section.</span></span>

<span data-ttu-id="85aa5-248">Se você usar grupos de segurança de rede ou rotas definidas pelo usuário, você deve permitir tráfego do hello integridade do Azure e serviços de gerenciamento tooreach HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85aa5-248">If you use network security groups or user-defined routes, you must allow traffic from hello Azure health and management services tooreach HDInsight.</span></span> <span data-ttu-id="85aa5-249">Use Olá etapas toofind Olá endereços IP devem ser permitidos a seguir:</span><span class="sxs-lookup"><span data-stu-id="85aa5-249">Use hello following steps toofind hello IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="85aa5-250">Você sempre deve permitir o tráfego de saudação endereços IP a seguir:</span><span class="sxs-lookup"><span data-stu-id="85aa5-250">You must always allow traffic from hello following IP addresses:</span></span>

    | <span data-ttu-id="85aa5-251">Endereço IP</span><span class="sxs-lookup"><span data-stu-id="85aa5-251">IP address</span></span> | <span data-ttu-id="85aa5-252">Porta permitida</span><span class="sxs-lookup"><span data-stu-id="85aa5-252">Allowed port</span></span> | <span data-ttu-id="85aa5-253">Direção</span><span class="sxs-lookup"><span data-stu-id="85aa5-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="85aa5-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="85aa5-254">168.61.49.99</span></span> | <span data-ttu-id="85aa5-255">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-255">443</span></span> | <span data-ttu-id="85aa5-256">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-256">Inbound</span></span> |
    | <span data-ttu-id="85aa5-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="85aa5-257">23.99.5.239</span></span> | <span data-ttu-id="85aa5-258">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-258">443</span></span> | <span data-ttu-id="85aa5-259">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-259">Inbound</span></span> |
    | <span data-ttu-id="85aa5-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="85aa5-260">168.61.48.131</span></span> | <span data-ttu-id="85aa5-261">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-261">443</span></span> | <span data-ttu-id="85aa5-262">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-262">Inbound</span></span> |
    | <span data-ttu-id="85aa5-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="85aa5-263">138.91.141.162</span></span> | <span data-ttu-id="85aa5-264">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-264">443</span></span> | <span data-ttu-id="85aa5-265">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-265">Inbound</span></span> |

2. <span data-ttu-id="85aa5-266">Se seu cluster HDInsight está em uma saudação regiões a seguir, você deve permitir tráfego de endereços IP de saudação listados para região hello:</span><span class="sxs-lookup"><span data-stu-id="85aa5-266">If your HDInsight cluster is in one of hello following regions, then you must allow traffic from hello IP addresses listed for hello region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="85aa5-267">Se Olá região do Azure que você está usando não estiver listado, só use quatro endereços IP hello da etapa 1.</span><span class="sxs-lookup"><span data-stu-id="85aa5-267">If hello Azure region you are using is not listed, then only use hello four IP addresses from step 1.</span></span>

    | <span data-ttu-id="85aa5-268">País</span><span class="sxs-lookup"><span data-stu-id="85aa5-268">Country</span></span> | <span data-ttu-id="85aa5-269">Região</span><span class="sxs-lookup"><span data-stu-id="85aa5-269">Region</span></span> | <span data-ttu-id="85aa5-270">Endereços IP permitidos</span><span class="sxs-lookup"><span data-stu-id="85aa5-270">Allowed IP addresses</span></span> | <span data-ttu-id="85aa5-271">Porta permitida</span><span class="sxs-lookup"><span data-stu-id="85aa5-271">Allowed port</span></span> | <span data-ttu-id="85aa5-272">Direção</span><span class="sxs-lookup"><span data-stu-id="85aa5-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="85aa5-273">Ásia</span><span class="sxs-lookup"><span data-stu-id="85aa5-273">Asia</span></span> | <span data-ttu-id="85aa5-274">Ásia Oriental</span><span class="sxs-lookup"><span data-stu-id="85aa5-274">East Asia</span></span> | <span data-ttu-id="85aa5-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="85aa5-275">23.102.235.122</span></span></br><span data-ttu-id="85aa5-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="85aa5-276">52.175.38.134</span></span> | <span data-ttu-id="85aa5-277">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-277">443</span></span> | <span data-ttu-id="85aa5-278">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="85aa5-279">Sudeste Asiático</span><span class="sxs-lookup"><span data-stu-id="85aa5-279">Southeast Asia</span></span> | <span data-ttu-id="85aa5-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="85aa5-280">13.76.245.160</span></span></br><span data-ttu-id="85aa5-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="85aa5-281">13.76.136.249</span></span> | <span data-ttu-id="85aa5-282">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-282">443</span></span> | <span data-ttu-id="85aa5-283">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-283">Inbound</span></span> |
    | <span data-ttu-id="85aa5-284">Austrália</span><span class="sxs-lookup"><span data-stu-id="85aa5-284">Australia</span></span> | <span data-ttu-id="85aa5-285">Leste da Austrália</span><span class="sxs-lookup"><span data-stu-id="85aa5-285">Australia East</span></span> | <span data-ttu-id="85aa5-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="85aa5-286">104.210.84.115</span></span></br><span data-ttu-id="85aa5-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="85aa5-287">13.75.152.195</span></span> | <span data-ttu-id="85aa5-288">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-288">443</span></span> | <span data-ttu-id="85aa5-289">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="85aa5-290">Sudeste da Austrália</span><span class="sxs-lookup"><span data-stu-id="85aa5-290">Australia Southeast</span></span> | <span data-ttu-id="85aa5-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="85aa5-291">13.77.2.56</span></span></br><span data-ttu-id="85aa5-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="85aa5-292">13.77.2.94</span></span> | <span data-ttu-id="85aa5-293">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-293">443</span></span> | <span data-ttu-id="85aa5-294">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-294">Inbound</span></span> |
    | <span data-ttu-id="85aa5-295">Brasil</span><span class="sxs-lookup"><span data-stu-id="85aa5-295">Brazil</span></span> | <span data-ttu-id="85aa5-296">Sul do Brasil</span><span class="sxs-lookup"><span data-stu-id="85aa5-296">Brazil South</span></span> | <span data-ttu-id="85aa5-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="85aa5-297">191.235.84.104</span></span></br><span data-ttu-id="85aa5-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="85aa5-298">191.235.87.113</span></span> | <span data-ttu-id="85aa5-299">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-299">443</span></span> | <span data-ttu-id="85aa5-300">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-300">Inbound</span></span> |
    | <span data-ttu-id="85aa5-301">Canadá</span><span class="sxs-lookup"><span data-stu-id="85aa5-301">Canada</span></span> | <span data-ttu-id="85aa5-302">Leste do Canadá</span><span class="sxs-lookup"><span data-stu-id="85aa5-302">Canada East</span></span> | <span data-ttu-id="85aa5-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="85aa5-303">52.229.127.96</span></span></br><span data-ttu-id="85aa5-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="85aa5-304">52.229.123.172</span></span> | <span data-ttu-id="85aa5-305">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-305">443</span></span> | <span data-ttu-id="85aa5-306">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="85aa5-307">Canadá Central</span><span class="sxs-lookup"><span data-stu-id="85aa5-307">Canada Central</span></span> | <span data-ttu-id="85aa5-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="85aa5-308">52.228.37.66</span></span></br><span data-ttu-id="85aa5-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="85aa5-309">52.228.45.222</span></span> | <span data-ttu-id="85aa5-310">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-310">443</span></span> | <span data-ttu-id="85aa5-311">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-311">Inbound</span></span> |
    | <span data-ttu-id="85aa5-312">China</span><span class="sxs-lookup"><span data-stu-id="85aa5-312">China</span></span> | <span data-ttu-id="85aa5-313">Norte da China</span><span class="sxs-lookup"><span data-stu-id="85aa5-313">China North</span></span> | <span data-ttu-id="85aa5-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="85aa5-314">42.159.96.170</span></span></br><span data-ttu-id="85aa5-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="85aa5-315">139.217.2.219</span></span> | <span data-ttu-id="85aa5-316">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-316">443</span></span> | <span data-ttu-id="85aa5-317">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="85aa5-318">Leste da China</span><span class="sxs-lookup"><span data-stu-id="85aa5-318">China East</span></span> | <span data-ttu-id="85aa5-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="85aa5-319">42.159.198.178</span></span></br><span data-ttu-id="85aa5-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="85aa5-320">42.159.234.157</span></span> | <span data-ttu-id="85aa5-321">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-321">443</span></span> | <span data-ttu-id="85aa5-322">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-322">Inbound</span></span> |
    | <span data-ttu-id="85aa5-323">Europa</span><span class="sxs-lookup"><span data-stu-id="85aa5-323">Europe</span></span> | <span data-ttu-id="85aa5-324">Norte da Europa</span><span class="sxs-lookup"><span data-stu-id="85aa5-324">North Europe</span></span> | <span data-ttu-id="85aa5-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="85aa5-325">52.164.210.96</span></span></br><span data-ttu-id="85aa5-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="85aa5-326">13.74.153.132</span></span> | <span data-ttu-id="85aa5-327">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-327">443</span></span> | <span data-ttu-id="85aa5-328">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="85aa5-329">Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="85aa5-329">West Europe</span></span>| <span data-ttu-id="85aa5-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="85aa5-330">52.166.243.90</span></span></br><span data-ttu-id="85aa5-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="85aa5-331">52.174.36.244</span></span> | <span data-ttu-id="85aa5-332">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-332">443</span></span> | <span data-ttu-id="85aa5-333">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-333">Inbound</span></span> |
    | <span data-ttu-id="85aa5-334">Alemanha</span><span class="sxs-lookup"><span data-stu-id="85aa5-334">Germany</span></span> | <span data-ttu-id="85aa5-335">Alemanha Central</span><span class="sxs-lookup"><span data-stu-id="85aa5-335">Germany Central</span></span> | <span data-ttu-id="85aa5-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="85aa5-336">51.4.146.68</span></span></br><span data-ttu-id="85aa5-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="85aa5-337">51.4.146.80</span></span> | <span data-ttu-id="85aa5-338">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-338">443</span></span> | <span data-ttu-id="85aa5-339">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="85aa5-340">Nordeste da Alemanha</span><span class="sxs-lookup"><span data-stu-id="85aa5-340">Germany Northeast</span></span> | <span data-ttu-id="85aa5-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="85aa5-341">51.5.150.132</span></span></br><span data-ttu-id="85aa5-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="85aa5-342">51.5.144.101</span></span> | <span data-ttu-id="85aa5-343">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-343">443</span></span> | <span data-ttu-id="85aa5-344">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-344">Inbound</span></span> |
    | <span data-ttu-id="85aa5-345">Índia</span><span class="sxs-lookup"><span data-stu-id="85aa5-345">India</span></span> | <span data-ttu-id="85aa5-346">Índia Central</span><span class="sxs-lookup"><span data-stu-id="85aa5-346">Central India</span></span> | <span data-ttu-id="85aa5-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="85aa5-347">52.172.153.209</span></span></br><span data-ttu-id="85aa5-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="85aa5-348">52.172.152.49</span></span> | <span data-ttu-id="85aa5-349">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-349">443</span></span> | <span data-ttu-id="85aa5-350">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-350">Inbound</span></span> |
    | <span data-ttu-id="85aa5-351">Japão</span><span class="sxs-lookup"><span data-stu-id="85aa5-351">Japan</span></span> | <span data-ttu-id="85aa5-352">Leste do Japão</span><span class="sxs-lookup"><span data-stu-id="85aa5-352">Japan East</span></span> | <span data-ttu-id="85aa5-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="85aa5-353">13.78.125.90</span></span></br><span data-ttu-id="85aa5-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="85aa5-354">13.78.89.60</span></span> | <span data-ttu-id="85aa5-355">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-355">443</span></span> | <span data-ttu-id="85aa5-356">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="85aa5-357">Oeste do Japão</span><span class="sxs-lookup"><span data-stu-id="85aa5-357">Japan West</span></span> | <span data-ttu-id="85aa5-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="85aa5-358">40.74.125.69</span></span></br><span data-ttu-id="85aa5-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="85aa5-359">138.91.29.150</span></span> | <span data-ttu-id="85aa5-360">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-360">443</span></span> | <span data-ttu-id="85aa5-361">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-361">Inbound</span></span> |
    | <span data-ttu-id="85aa5-362">Coreia</span><span class="sxs-lookup"><span data-stu-id="85aa5-362">Korea</span></span> | <span data-ttu-id="85aa5-363">Coreia Central</span><span class="sxs-lookup"><span data-stu-id="85aa5-363">Korea Central</span></span> | <span data-ttu-id="85aa5-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="85aa5-364">52.231.39.142</span></span></br><span data-ttu-id="85aa5-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="85aa5-365">52.231.36.209</span></span> | <span data-ttu-id="85aa5-366">433</span><span class="sxs-lookup"><span data-stu-id="85aa5-366">433</span></span> | <span data-ttu-id="85aa5-367">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="85aa5-368">Sul da Coreia</span><span class="sxs-lookup"><span data-stu-id="85aa5-368">Korea South</span></span> | <span data-ttu-id="85aa5-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="85aa5-369">52.231.203.16</span></span></br><span data-ttu-id="85aa5-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="85aa5-370">52.231.205.214</span></span> | <span data-ttu-id="85aa5-371">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-371">443</span></span> | <span data-ttu-id="85aa5-372">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-372">Inbound</span></span>
    | <span data-ttu-id="85aa5-373">Reino Unido</span><span class="sxs-lookup"><span data-stu-id="85aa5-373">United Kingdom</span></span> | <span data-ttu-id="85aa5-374">Oeste do Reino Unido</span><span class="sxs-lookup"><span data-stu-id="85aa5-374">UK West</span></span> | <span data-ttu-id="85aa5-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="85aa5-375">51.141.13.110</span></span></br><span data-ttu-id="85aa5-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="85aa5-376">51.141.7.20</span></span> | <span data-ttu-id="85aa5-377">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-377">443</span></span> | <span data-ttu-id="85aa5-378">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="85aa5-379">Sul do Reino Unido</span><span class="sxs-lookup"><span data-stu-id="85aa5-379">UK South</span></span> | <span data-ttu-id="85aa5-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="85aa5-380">51.140.47.39</span></span></br><span data-ttu-id="85aa5-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="85aa5-381">51.140.52.16</span></span> | <span data-ttu-id="85aa5-382">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-382">443</span></span> | <span data-ttu-id="85aa5-383">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-383">Inbound</span></span> |
    | <span data-ttu-id="85aa5-384">Estados Unidos</span><span class="sxs-lookup"><span data-stu-id="85aa5-384">United States</span></span> | <span data-ttu-id="85aa5-385">Centro dos EUA</span><span class="sxs-lookup"><span data-stu-id="85aa5-385">Central US</span></span> | <span data-ttu-id="85aa5-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="85aa5-386">13.67.223.215</span></span></br><span data-ttu-id="85aa5-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="85aa5-387">40.86.83.253</span></span> | <span data-ttu-id="85aa5-388">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-388">443</span></span> | <span data-ttu-id="85aa5-389">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="85aa5-390">Centro-Norte dos EUA</span><span class="sxs-lookup"><span data-stu-id="85aa5-390">North Central US</span></span> | <span data-ttu-id="85aa5-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="85aa5-391">157.56.8.38</span></span></br><span data-ttu-id="85aa5-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="85aa5-392">157.55.213.99</span></span> | <span data-ttu-id="85aa5-393">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-393">443</span></span> | <span data-ttu-id="85aa5-394">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="85aa5-395">Centro-Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="85aa5-395">West Central US</span></span> | <span data-ttu-id="85aa5-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="85aa5-396">52.161.23.15</span></span></br><span data-ttu-id="85aa5-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="85aa5-397">52.161.10.167</span></span> | <span data-ttu-id="85aa5-398">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-398">443</span></span> | <span data-ttu-id="85aa5-399">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="85aa5-400">Oeste dos EUA 2</span><span class="sxs-lookup"><span data-stu-id="85aa5-400">West US 2</span></span> | <span data-ttu-id="85aa5-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="85aa5-401">52.175.211.210</span></span></br><span data-ttu-id="85aa5-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="85aa5-402">52.175.222.222</span></span> | <span data-ttu-id="85aa5-403">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-403">443</span></span> | <span data-ttu-id="85aa5-404">Entrada</span><span class="sxs-lookup"><span data-stu-id="85aa5-404">Inbound</span></span> |

    <span data-ttu-id="85aa5-405">Para obter informações sobre IP hello endereços toouse para governo do Azure, consulte Olá [Azure governamental Intelligence + análise](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) documento.</span><span class="sxs-lookup"><span data-stu-id="85aa5-405">For information on hello IP addresses toouse for Azure Government, see hello [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="85aa5-406">Se você usar um servidor DNS personalizado com a rede virtual, também deverá permitir o acesso de __168.63.129.16__.</span><span class="sxs-lookup"><span data-stu-id="85aa5-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="85aa5-407">Esse endereço é o resolvedor recursivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="85aa5-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="85aa5-408">Para obter mais informações, consulte Olá [resolução de nomes para VMs e função instâncias](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) documento.</span><span class="sxs-lookup"><span data-stu-id="85aa5-408">For more information, see hello [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="85aa5-409">Para obter mais informações, consulte Olá [controlando o tráfego de rede](#networktraffic) seção.</span><span class="sxs-lookup"><span data-stu-id="85aa5-409">For more information, see hello [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="85aa5-410"><a id="hdinsight-ports"></a> Portas obrigatórias</span><span class="sxs-lookup"><span data-stu-id="85aa5-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="85aa5-411">Se você planeja usar uma rede **firewall do dispositivo virtual** toosecure Olá rede virtual, e você deve permitir o tráfego de saída no Olá portas a seguir:</span><span class="sxs-lookup"><span data-stu-id="85aa5-411">If you plan on using a network **virtual appliance firewall** toosecure hello virtual network, you must allow outbound traffic on hello following ports:</span></span>

* <span data-ttu-id="85aa5-412">53</span><span class="sxs-lookup"><span data-stu-id="85aa5-412">53</span></span>
* <span data-ttu-id="85aa5-413">443</span><span class="sxs-lookup"><span data-stu-id="85aa5-413">443</span></span>
* <span data-ttu-id="85aa5-414">1433</span><span class="sxs-lookup"><span data-stu-id="85aa5-414">1433</span></span>
* <span data-ttu-id="85aa5-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="85aa5-415">11000-11999</span></span>
* <span data-ttu-id="85aa5-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="85aa5-416">14000-14999</span></span>

<span data-ttu-id="85aa5-417">Para obter uma lista de portas para serviços específicos, consulte Olá [portas usadas por serviços de Hadoop no HDInsight](hdinsight-hadoop-port-settings-for-services.md) documento.</span><span class="sxs-lookup"><span data-stu-id="85aa5-417">For a list of ports for specific services, see hello [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="85aa5-418">Para obter mais informações sobre regras de firewall para dispositivos virtuais, consulte Olá [cenário de dispositivo virtual](../virtual-network/virtual-network-scenario-udr-gw-nva.md) documento.</span><span class="sxs-lookup"><span data-stu-id="85aa5-418">For more information on firewall rules for virtual appliances, see hello [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="85aa5-419"><a id="hdinsight-nsg"></a>Exemplo: grupos de segurança de rede com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="85aa5-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="85aa5-420">Olá os exemplos nesta seção demonstram como o grupo de segurança de rede toocreate regras que permitem o HDInsight toocommunicate com hello serviços de gerenciamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="85aa5-420">hello examples in this section demonstrate how toocreate network security group rules that allow HDInsight toocommunicate with hello Azure management services.</span></span> <span data-ttu-id="85aa5-421">Antes de usar os exemplos de hello, ajuste Olá IP endereços toomatch hello aqueles para Olá região do Azure que você está usando.</span><span class="sxs-lookup"><span data-stu-id="85aa5-421">Before using hello examples, adjust hello IP addresses toomatch hello ones for hello Azure region you are using.</span></span> <span data-ttu-id="85aa5-422">Você pode encontrar essas informações no hello [HDInsight com rotas definidas pelo usuário e grupos de segurança de rede](#hdinsight-ip) seção.</span><span class="sxs-lookup"><span data-stu-id="85aa5-422">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="85aa5-423">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="85aa5-423">Azure Resource Management template</span></span>

<span data-ttu-id="85aa5-424">Hello modelo gerenciamento de recursos a seguir cria uma rede virtual que restringe o tráfego de entrada, mas permite que o tráfego de endereços IP de saudação exigido pelo HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85aa5-424">hello following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="85aa5-425">Esse modelo também cria um cluster HDInsight na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="85aa5-425">This template also creates an HDInsight cluster in hello virtual network.</span></span>

* [<span data-ttu-id="85aa5-426">Implantar uma Rede Virtual protegida do Azure e um cluster HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="85aa5-426">Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> <span data-ttu-id="85aa5-427">Altere os endereços IP hello usados na saudação de toomatch exemplo região do Azure que você está usando.</span><span class="sxs-lookup"><span data-stu-id="85aa5-427">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="85aa5-428">Você pode encontrar essas informações no hello [HDInsight com rotas definidas pelo usuário e grupos de segurança de rede](#hdinsight-ip) seção.</span><span class="sxs-lookup"><span data-stu-id="85aa5-428">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="85aa5-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="85aa5-429">Azure PowerShell</span></span>

<span data-ttu-id="85aa5-430">Use Olá toocreate de script do PowerShell uma rede virtual que restringe o tráfego de entrada e permite o tráfego de saudação endereços IP para a região do Norte da Europa Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="85aa5-430">Use hello following PowerShell script toocreate a virtual network that restricts inbound traffic and allows traffic from hello IP addresses for hello North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85aa5-431">Altere os endereços IP hello usados na saudação de toomatch exemplo região do Azure que você está usando.</span><span class="sxs-lookup"><span data-stu-id="85aa5-431">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="85aa5-432">Você pode encontrar essas informações no hello [HDInsight com rotas definidas pelo usuário e grupos de segurança de rede](#hdinsight-ip) seção.</span><span class="sxs-lookup"><span data-stu-id="85aa5-432">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="85aa5-433">Este exemplo demonstra como o tráfego em endereços IP hello necessário de entrada tooadd tooallow de regras.</span><span class="sxs-lookup"><span data-stu-id="85aa5-433">This example demonstrates how tooadd rules tooallow inbound traffic on hello required IP addresses.</span></span> <span data-ttu-id="85aa5-434">Ele não contém um toorestrict de regra de acesso de outras fontes de entrada.</span><span class="sxs-lookup"><span data-stu-id="85aa5-434">It does not contain a rule toorestrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="85aa5-435">Olá exemplo a seguir demonstra como acessar o tooenable SSH de saudação da Internet:</span><span class="sxs-lookup"><span data-stu-id="85aa5-435">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="85aa5-436">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="85aa5-436">Azure CLI</span></span>

<span data-ttu-id="85aa5-437">Use Olá seguindo as etapas toocreate uma rede virtual que restringe o tráfego de entrada, mas permite que o tráfego de endereços IP de saudação exigido pelo HDInsight.</span><span class="sxs-lookup"><span data-stu-id="85aa5-437">Use hello following steps toocreate a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="85aa5-438">Saudação de uso após o comando toocreate um novo grupo de segurança de rede denominado `hdisecure`.</span><span class="sxs-lookup"><span data-stu-id="85aa5-438">Use hello following command toocreate a new network security group named `hdisecure`.</span></span> <span data-ttu-id="85aa5-439">Substituir **RESOURCEGROUPNAME** com grupo de recursos de saudação que contém Olá rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="85aa5-439">Replace **RESOURCEGROUPNAME** with hello resource group that contains hello Azure Virtual Network.</span></span> <span data-ttu-id="85aa5-440">Substituir **local** local hello (região) grupo Olá foi criado na.</span><span class="sxs-lookup"><span data-stu-id="85aa5-440">Replace **LOCATION** with hello location (region) that hello group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="85aa5-441">Quando o grupo de saudação tiver sido criado, você recebe informações no novo grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="85aa5-441">Once hello group has been created, you receive information on hello new group.</span></span>

2. <span data-ttu-id="85aa5-442">Use Olá tooadd regras toohello nova rede grupo de segurança que permitem a comunicação de entrada na porta 443 de saudação serviço de integridade e o gerenciamento do Azure HDInsight a seguir.</span><span class="sxs-lookup"><span data-stu-id="85aa5-442">Use hello following tooadd rules toohello new network security group that allow inbound communication on port 443 from hello Azure HDInsight health and management service.</span></span> <span data-ttu-id="85aa5-443">Substituir **RESOURCEGROUPNAME** com nome Olá Olá do grupo de recursos que contém Olá rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="85aa5-443">Replace **RESOURCEGROUPNAME** with hello name of hello resource group that contains hello Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="85aa5-444">Altere os endereços IP hello usados na saudação de toomatch exemplo região do Azure que você está usando.</span><span class="sxs-lookup"><span data-stu-id="85aa5-444">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="85aa5-445">Você pode encontrar essas informações no hello [HDInsight com rotas definidas pelo usuário e grupos de segurança de rede](#hdinsight-ip) seção.</span><span class="sxs-lookup"><span data-stu-id="85aa5-445">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="85aa5-446">tooretrieve Olá identificador exclusivo para esse grupo de segurança de rede, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="85aa5-446">tooretrieve hello unique identifier for this network security group, use hello following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="85aa5-447">Este comando retorna um toohello semelhante valor texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="85aa5-447">This command returns a value similar toohello following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="85aa5-448">Use aspas duplas em torno de id no comando Olá se você não obtiver os resultados de saudação esperado.</span><span class="sxs-lookup"><span data-stu-id="85aa5-448">Use double-quotes around id in hello command if you don't get hello expected results.</span></span>

4. <span data-ttu-id="85aa5-449">Use Olá comando tooapply Olá segurança grupo tooa sub-rede a seguir.</span><span class="sxs-lookup"><span data-stu-id="85aa5-449">Use hello following command tooapply hello network security group tooa subnet.</span></span> <span data-ttu-id="85aa5-450">Substituir saudação __GUID__ e __RESOURCEGROUPNAME__ valores com hello aqueles retornados da etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="85aa5-450">Replace hello __GUID__ and __RESOURCEGROUPNAME__ values with hello ones returned from hello previous step.</span></span> <span data-ttu-id="85aa5-451">Substituir __VNETNAME__ e __SUBNETNAME__ com o nome de rede virtual hello e nome da sub-rede que você deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="85aa5-451">Replace __VNETNAME__ and __SUBNETNAME__ with hello virtual network name and subnet name that you want toocreate.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="85aa5-452">Depois que esse comando for concluído, você pode instalar o HDInsight em Olá rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="85aa5-452">Once this command completes, you can install HDInsight into hello Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85aa5-453">Estas etapas só abra toohello HDInsight integridade e o gerenciamento de serviço de acesso no hello nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="85aa5-453">These steps only open access toohello HDInsight health and management service on hello Azure cloud.</span></span> <span data-ttu-id="85aa5-454">Qualquer outro acesso toohello cluster HDInsight da saudação fora rede Virtual está bloqueada.</span><span class="sxs-lookup"><span data-stu-id="85aa5-454">Any other access toohello HDInsight cluster from outside hello Virtual Network is blocked.</span></span> <span data-ttu-id="85aa5-455">tooenable acesso de rede virtual Olá externa, você deve adicionar regras de grupo de segurança de rede adicionais.</span><span class="sxs-lookup"><span data-stu-id="85aa5-455">tooenable access from outside hello virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="85aa5-456">Olá exemplo a seguir demonstra como acessar o tooenable SSH de saudação da Internet:</span><span class="sxs-lookup"><span data-stu-id="85aa5-456">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="85aa5-457"><a id="example-dns"></a> Exemplo: configuração de DNS</span><span class="sxs-lookup"><span data-stu-id="85aa5-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="85aa5-458">Resolução de nomes entre uma rede virtual e uma rede local conectada</span><span class="sxs-lookup"><span data-stu-id="85aa5-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="85aa5-459">Este exemplo faz Olá seguintes suposições:</span><span class="sxs-lookup"><span data-stu-id="85aa5-459">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="85aa5-460">Você tem uma rede Virtual do Azure que é a rede de local de tooan conectado usando um gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="85aa5-460">You have an Azure Virtual Network that is connected tooan on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="85aa5-461">um servidor DNS personalizado Olá na rede virtual Olá está executando Linux ou Unix como sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="85aa5-461">hello custom DNS server in hello virtual network is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="85aa5-462">[Associar](https://www.isc.org/downloads/bind/) está instalado em um servidor DNS personalizado hello.</span><span class="sxs-lookup"><span data-stu-id="85aa5-462">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS server.</span></span>

<span data-ttu-id="85aa5-463">No servidor DNS de personalizado hello, na rede virtual hello:</span><span class="sxs-lookup"><span data-stu-id="85aa5-463">On hello custom DNS server in hello virtual network:</span></span>

1. <span data-ttu-id="85aa5-464">Use o Azure PowerShell ou CLI do Azure toofind Olá sufixo DNS da rede virtual hello:</span><span class="sxs-lookup"><span data-stu-id="85aa5-464">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of hello virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="85aa5-465">No hello um servidor DNS personalizado para a rede virtual hello, use Olá depois do texto como conteúdo de saudação do hello `/etc/bind/named.conf.local` arquivo:</span><span class="sxs-lookup"><span data-stu-id="85aa5-465">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="85aa5-466">Substituir saudação `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` valor com o sufixo DNS de saudação da sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="85aa5-466">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="85aa5-467">Essa configuração roteia todas as solicitações DNS para o sufixo DNS de saudação do resolvedor do hello rede virtual toohello recursiva do Azure.</span><span class="sxs-lookup"><span data-stu-id="85aa5-467">This configuration routes all DNS requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver.</span></span>

2. <span data-ttu-id="85aa5-468">No hello um servidor DNS personalizado para a rede virtual hello, use Olá depois do texto como conteúdo de saudação do hello `/etc/bind/named.conf.options` arquivo:</span><span class="sxs-lookup"><span data-stu-id="85aa5-468">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="85aa5-469">Substituir saudação `10.0.0.0/16` valor com o intervalo de endereços IP hello da sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="85aa5-469">Replace hello `10.0.0.0/16` value with hello IP address range of your virtual network.</span></span> <span data-ttu-id="85aa5-470">Essa entrada permite endereços de solicitações de resolução de nomes dentro desse intervalo.</span><span class="sxs-lookup"><span data-stu-id="85aa5-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="85aa5-471">Adicionar intervalo de endereços IP hello de saudação local rede toohello `acl goodclients { ... }` seção.</span><span class="sxs-lookup"><span data-stu-id="85aa5-471">Add hello IP address range of hello on-premises network toohello `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="85aa5-472">entrada permite solicitações de resolução de nomes de recursos na rede de local de saudação.</span><span class="sxs-lookup"><span data-stu-id="85aa5-472">entry allows name resolution requests from resources in hello on-premises network.</span></span>
    
    * <span data-ttu-id="85aa5-473">Substituir valor Olá `192.168.0.1` com o endereço IP de saudação do servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="85aa5-473">Replace hello value `192.168.0.1` with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="85aa5-474">Essa entrada encaminha todos os outros DNS solicitações toohello no servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="85aa5-474">This entry routes all other DNS requests toohello on-premises DNS server.</span></span>

3. <span data-ttu-id="85aa5-475">configuração de saudação toouse, reinicie a ligação.</span><span class="sxs-lookup"><span data-stu-id="85aa5-475">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="85aa5-476">Por exemplo: `sudo service bind9 restart`.</span><span class="sxs-lookup"><span data-stu-id="85aa5-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="85aa5-477">Adicione um servidor DNS do encaminhador condicional toohello no local.</span><span class="sxs-lookup"><span data-stu-id="85aa5-477">Add a conditional forwarder toohello on-premises DNS server.</span></span> <span data-ttu-id="85aa5-478">Configure solicitações de toosend Olá encaminhador condicional para o sufixo DNS de saudação da etapa 1 toohello um servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="85aa5-478">Configure hello conditional forwarder toosend requests for hello DNS suffix from step 1 toohello custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="85aa5-479">Consulte a documentação de saudação do seu software DNS para obter informações específicas sobre como tooadd um encaminhador condicional.</span><span class="sxs-lookup"><span data-stu-id="85aa5-479">Consult hello documentation for your DNS software for specifics on how tooadd a conditional forwarder.</span></span>

<span data-ttu-id="85aa5-480">Depois de concluir essas etapas, você pode conectar tooresources na rede usando nomes de domínio totalmente qualificado (FQDN).</span><span class="sxs-lookup"><span data-stu-id="85aa5-480">After completing these steps, you can connect tooresources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="85aa5-481">Agora você pode instalar o HDInsight em rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="85aa5-481">You can now install HDInsight into hello virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="85aa5-482">Resolução de nomes entre duas redes virtuais conectadas</span><span class="sxs-lookup"><span data-stu-id="85aa5-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="85aa5-483">Este exemplo faz Olá seguintes suposições:</span><span class="sxs-lookup"><span data-stu-id="85aa5-483">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="85aa5-484">Você tem duas Redes Virtuais do Azure conectadas usando um gateway de VPN ou um emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="85aa5-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="85aa5-485">um servidor DNS personalizado Olá em ambas as redes está executando o Linux ou Unix como sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="85aa5-485">hello custom DNS server in both networks is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="85aa5-486">[Associar](https://www.isc.org/downloads/bind/) é instalado em servidores DNS personalizados hello.</span><span class="sxs-lookup"><span data-stu-id="85aa5-486">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS servers.</span></span>

1. <span data-ttu-id="85aa5-487">Use o Azure PowerShell ou CLI do Azure toofind Olá sufixo DNS de ambas as redes virtuais:</span><span class="sxs-lookup"><span data-stu-id="85aa5-487">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="85aa5-488">Saudação de uso após o texto como conteúdo de saudação do hello `/etc/bind/named.config.local` arquivo em um servidor DNS personalizado hello.</span><span class="sxs-lookup"><span data-stu-id="85aa5-488">Use hello following text as hello contents of hello `/etc/bind/named.config.local` file on hello custom DNS server.</span></span> <span data-ttu-id="85aa5-489">Fazer essa alteração em um servidor DNS personalizado Olá em ambas as redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="85aa5-489">Make this change on hello custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    <span data-ttu-id="85aa5-490">Substituir saudação `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` valor com o sufixo DNS Olá Olá __outros__ rede virtual.</span><span class="sxs-lookup"><span data-stu-id="85aa5-490">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of hello __other__ virtual network.</span></span> <span data-ttu-id="85aa5-491">Essa entrada encaminha solicitações para o sufixo DNS Olá Olá rede remota toohello personalizado DNS nessa rede.</span><span class="sxs-lookup"><span data-stu-id="85aa5-491">This entry routes requests for hello DNS suffix of hello remote network toohello custom DNS in that network.</span></span>

3. <span data-ttu-id="85aa5-492">Em servidores DNS de personalizado hello, em ambas as redes virtuais, use Olá depois do texto como conteúdo de saudação do hello `/etc/bind/named.conf.options` arquivo:</span><span class="sxs-lookup"><span data-stu-id="85aa5-492">On hello custom DNS servers in both virtual networks, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="85aa5-493">Substituir saudação `10.0.0.0/16` e `10.1.0.0/16` valores com hello IP endereço intervalos de suas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="85aa5-493">Replace hello `10.0.0.0/16` and `10.1.0.0/16` values with hello IP address ranges of your virtual networks.</span></span> <span data-ttu-id="85aa5-494">Essa entrada permite que os recursos em cada rede toomake solicitações de servidores DNS a saudação.</span><span class="sxs-lookup"><span data-stu-id="85aa5-494">This entry allows resources in each network toomake requests of hello DNS servers.</span></span>

    <span data-ttu-id="85aa5-495">Todas as solicitações que não são de sufixos DNS de saudação de redes virtuais da saudação (por exemplo, microsoft.com) é manipulados pelo resolvedor de Azure recursiva de saudação.</span><span class="sxs-lookup"><span data-stu-id="85aa5-495">Any requests that are not for hello DNS suffixes of hello virtual networks (for example, microsoft.com) is handled by hello Azure recursive resolver.</span></span>

4. <span data-ttu-id="85aa5-496">configuração de saudação toouse, reinicie a ligação.</span><span class="sxs-lookup"><span data-stu-id="85aa5-496">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="85aa5-497">Por exemplo, `sudo service bind9 restart` em ambos os servidores DNS.</span><span class="sxs-lookup"><span data-stu-id="85aa5-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="85aa5-498">Depois de concluir essas etapas, você pode conectar tooresources na rede virtual do hello usando nomes de domínio totalmente qualificado (FQDN).</span><span class="sxs-lookup"><span data-stu-id="85aa5-498">After completing these steps, you can connect tooresources in hello virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="85aa5-499">Agora você pode instalar o HDInsight em rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="85aa5-499">You can now install HDInsight into hello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85aa5-500">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="85aa5-500">Next steps</span></span>

* <span data-ttu-id="85aa5-501">Para obter um exemplo de ponta a ponta de configuração de rede local do HDInsight tooconnect tooan, consulte [HDInsight conectar rede de local de tooan](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="85aa5-501">For an end-to-end example of configuring HDInsight tooconnect tooan on-premises network, see [Connect HDInsight tooan on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="85aa5-502">Para obter mais informações sobre redes virtuais do Azure, consulte Olá [visão geral da rede Virtual do Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="85aa5-502">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="85aa5-503">Para obter mais informações sobre os Grupos de Segurança de Rede, veja [Grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="85aa5-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="85aa5-504">Para saber mais sobre rotas definidas pelo usuário, confira [Rotas definidas pelo usuário e encaminhamento IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="85aa5-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>