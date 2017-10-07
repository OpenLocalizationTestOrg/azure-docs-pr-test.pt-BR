---
title: "aaaTroubleshoot grupos de segurança de rede - PowerShell | Microsoft Docs"
description: "Saiba como grupos de segurança de rede tootroubleshoot na implantação do Azure Resource Manager Olá modelo usando o PowerShell do Azure."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a><span data-ttu-id="581f4-103">Solucionar problemas de grupos de segurança de rede usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="581f4-103">Troubleshoot Network Security Groups using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="581f4-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="581f4-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="581f4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="581f4-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="581f4-106">Se configurado os grupos de segurança de rede (NSGs) em sua máquina virtual (VM) e estão com problemas de conectividade VM, este artigo fornece uma visão geral dos recursos de diagnóstico para os NSGs toohelp solucionar outros problemas.</span><span class="sxs-lookup"><span data-stu-id="581f4-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs toohelp troubleshoot further.</span></span>

<span data-ttu-id="581f4-107">Os NSGs permitem que você toocontrol tipos de saudação do tráfego de fluxo para dentro e fora de suas máquinas virtuais (VMs).</span><span class="sxs-lookup"><span data-stu-id="581f4-107">NSGs enable you toocontrol hello types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="581f4-108">Os NSGs podem ser aplicadas toosubnets em uma rede Virtual do Azure (VNet), interfaces de rede (NIC) ou ambos.</span><span class="sxs-lookup"><span data-stu-id="581f4-108">NSGs can be applied toosubnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="581f4-109">Olá efetivo regras aplicadas tooa NIC são uma agregação das regras de saudação que existem no hello NSGs aplicados tooa NIC e hello sub-rede está conectado ao.</span><span class="sxs-lookup"><span data-stu-id="581f4-109">hello effective rules applied tooa NIC are an aggregation of hello rules that exist in hello NSGs applied tooa NIC and hello subnet it is connected to.</span></span> <span data-ttu-id="581f4-110">As regras nesses NSGs podem, às vezes, entrar em conflito umas com as outras e afetar a conectividade de rede de uma VM.</span><span class="sxs-lookup"><span data-stu-id="581f4-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="581f4-111">Você pode exibir todas as regras de segurança efetiva de saudação do seus NSGs aplicados ao NICs da VM.</span><span class="sxs-lookup"><span data-stu-id="581f4-111">You can view all hello effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="581f4-112">Este artigo mostra como problemas de conectividade VM tootroubleshoot usando essas regras em Olá modelo de implantação do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="581f4-112">This article shows how tootroubleshoot VM connectivity issues using these rules in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="581f4-113">Se você não estiver familiarizado com conceitos de rede virtual e NSG, leia Olá [rede Virtual](virtual-networks-overview.md) e [grupos de segurança de rede](virtual-networks-nsg.md) artigos de visão geral.</span><span class="sxs-lookup"><span data-stu-id="581f4-113">If you're not familiar with VNet and NSG concepts, read hello [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="581f4-114">Usando o fluxo de tráfego VM de tootroubleshoot de regras de segurança efetiva</span><span class="sxs-lookup"><span data-stu-id="581f4-114">Using Effective Security Rules tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="581f4-115">cenário de saudação que segue é um exemplo de um problema de conexão comum:</span><span class="sxs-lookup"><span data-stu-id="581f4-115">hello scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="581f4-116">Uma VM denominada *VM1* faz parte de uma sub-rede denominada *Subnet1* em uma VNet denominada *WestUS-VNet1*.</span><span class="sxs-lookup"><span data-stu-id="581f4-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="581f4-117">Toohello de tooconnect uma tentativa de VM usando o RDP usando a porta TCP 3389 falhará.</span><span class="sxs-lookup"><span data-stu-id="581f4-117">An attempt tooconnect toohello VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="581f4-118">Os NSGs são aplicados em ambos os Olá NIC *VM1 NIC1* e Olá sub-rede *Subnet1*.</span><span class="sxs-lookup"><span data-stu-id="581f4-118">NSGs are applied at both hello NIC *VM1-NIC1* and hello subnet *Subnet1*.</span></span> <span data-ttu-id="581f4-119">TooTCP porta 3389 do tráfego é permitida em Olá associado à interface de rede de saudação do NSG *VM1 NIC1*, no entanto, porta 3389 ocorre uma falha da tooVM1 ping do TCP.</span><span class="sxs-lookup"><span data-stu-id="581f4-119">Traffic tooTCP port 3389 is allowed in hello NSG associated with hello network interface *VM1-NIC1*, however TCP ping tooVM1's port 3389 fails.</span></span>

<span data-ttu-id="581f4-120">Embora este exemplo usa a porta TCP 3389, Olá seguintes etapas pode ser usada toodetermine falhas de conexão de entrada e saída em qualquer porta.</span><span class="sxs-lookup"><span data-stu-id="581f4-120">While this example uses TCP port 3389, hello following steps can be used toodetermine inbound and outbound connection failures over any port.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="581f4-121">Etapas de solução de problemas detalhadas</span><span class="sxs-lookup"><span data-stu-id="581f4-121">Detailed Troubleshooting Steps</span></span>
<span data-ttu-id="581f4-122">Concluir Olá seguindo as etapas tootroubleshoot NSGs para uma VM:</span><span class="sxs-lookup"><span data-stu-id="581f4-122">Complete hello following steps tootroubleshoot NSGs for a VM:</span></span>

1. <span data-ttu-id="581f4-123">Inicie um tooAzure de logon e de sessão do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="581f4-123">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="581f4-124">Se você não estiver familiarizado com o uso do PowerShell do Azure, leia Olá [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.</span><span class="sxs-lookup"><span data-stu-id="581f4-124">If you're not familiar with using Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="581f4-125">Digite hello tooreturn aplicação de todas as regras NSG tooa NIC chamada do comando a seguir *VM1 NIC1* no grupo de recursos de saudação *RG1*:</span><span class="sxs-lookup"><span data-stu-id="581f4-125">Enter hello following command tooreturn all NSG rules applied tooa NIC named *VM1-NIC1* in hello resource group *RG1*:</span></span>
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="581f4-126">Se você não souber o nome de saudação de uma NIC, digite Olá nomes de saudação do comando tooretrieve de todas as NICs de um grupo de recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="581f4-126">If you don't know hello name of a NIC, enter hello following command tooretrieve hello names of all NICs in a resource group:</span></span> 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    <span data-ttu-id="581f4-127">Olá, texto a seguir é um exemplo de saída de regras efetivo hello retornada para Olá *VM1 NIC1* NIC:</span><span class="sxs-lookup"><span data-stu-id="581f4-127">hello following text is a sample of hello effective rules output returned for hello *VM1-NIC1* NIC:</span></span>
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    <span data-ttu-id="581f4-128">Observe Olá informações na saída de hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="581f4-128">Note hello following information in hello output:</span></span>
   
   * <span data-ttu-id="581f4-129">Há duas seções **NetworkSecurityGroup**: uma é associada a uma sub-rede (*Subnet1*) e a outra é associada a uma NIC (*VM1-NIC1*).</span><span class="sxs-lookup"><span data-stu-id="581f4-129">There are two **NetworkSecurityGroup** sections: One is associated with a subnet (*Subnet1*) and one is associated with a NIC (*VM1-NIC1*).</span></span> <span data-ttu-id="581f4-130">Neste exemplo, um NSG foi tooeach aplicado.</span><span class="sxs-lookup"><span data-stu-id="581f4-130">In this example, an NSG has been applied tooeach.</span></span>
   * <span data-ttu-id="581f4-131">**Associação** mostra que o recurso de saudação (subrede ou NIC) um determinado NSG está associado.</span><span class="sxs-lookup"><span data-stu-id="581f4-131">**Association** shows hello resource (subnet or NIC) a given NSG is associated with.</span></span> <span data-ttu-id="581f4-132">Se Olá recurso NSG é desassociado/movido imediatamente antes de executar esse comando, você pode precisar toowait alguns segundos para Olá tooreflect de alteração na saída do comando hello.</span><span class="sxs-lookup"><span data-stu-id="581f4-132">If hello NSG resource is moved/disassociated immediately before running this command, you may need toowait a few seconds for hello change tooreflect in hello command output.</span></span> 
   * <span data-ttu-id="581f4-133">Olá nomes de regras que são precedidos de *defaultSecurityRules*: quando um NSG é criado, várias regras de segurança padrão são criadas com ela.</span><span class="sxs-lookup"><span data-stu-id="581f4-133">hello rule names that are prefaced with *defaultSecurityRules*: When an NSG is created, several default security rules are created within it.</span></span> <span data-ttu-id="581f4-134">Regras padrão não podem ser removidas, mas podem ser substituídas por regras com prioridade mais alta.</span><span class="sxs-lookup"><span data-stu-id="581f4-134">Default rules can't be removed, but they can be overridden with higher priority rules.</span></span>
     <span data-ttu-id="581f4-135">Saudação de leitura [visão geral do NSG](virtual-networks-nsg.md#default-rules) artigo toolearn mais sobre o NSG padrão de regras de segurança.</span><span class="sxs-lookup"><span data-stu-id="581f4-135">Read hello [NSG overview](virtual-networks-nsg.md#default-rules) article toolearn more about NSG default security rules.</span></span>
   * <span data-ttu-id="581f4-136">**ExpandedAddressPrefix** expande os prefixos de endereço Olá para marcas de padrão NSG.</span><span class="sxs-lookup"><span data-stu-id="581f4-136">**ExpandedAddressPrefix** expands hello address prefixes for NSG default tags.</span></span> <span data-ttu-id="581f4-137">As marcações representam vários prefixos de endereço.</span><span class="sxs-lookup"><span data-stu-id="581f4-137">Tags represent multiple address prefixes.</span></span> <span data-ttu-id="581f4-138">Expansão de marcas Olá pode ser útil ao solucionar problemas de conectividade VM de prefixos de endereço específico.</span><span class="sxs-lookup"><span data-stu-id="581f4-138">Expansion of hello tags can be useful when troubleshooting VM connectivity to/from specific address prefixes.</span></span> <span data-ttu-id="581f4-139">Por exemplo, com o emparelhamento de rede virtual, a marca VIRTUAL_NETWORK expande tooshow emparelhadas prefixos de rede virtual na saída de saudação anterior.</span><span class="sxs-lookup"><span data-stu-id="581f4-139">For example, with VNET peering, VIRTUAL_NETWORK tag expands tooshow peered VNet prefixes in hello previous output.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="581f4-140">Olá regras efetivo do comando apenas mostra se um NSG está associado uma sub-rede, uma NIC ou ambos.</span><span class="sxs-lookup"><span data-stu-id="581f4-140">hello command only shows effective rules if an NSG is associated with either a subnet, a NIC, or both.</span></span> <span data-ttu-id="581f4-141">Uma VM pode ter várias NICs com diferentes NSGs aplicados.</span><span class="sxs-lookup"><span data-stu-id="581f4-141">A VM may have multiple NICs with different NSGs applied.</span></span> <span data-ttu-id="581f4-142">Ao solucionar o problema, execute o comando de saudação para cada NIC.</span><span class="sxs-lookup"><span data-stu-id="581f4-142">When troubleshooting, run hello command for each NIC.</span></span>
     > 
     > 
3. <span data-ttu-id="581f4-143">tooease filtragem maior número de regras do NSG, digite Olá comandos tootroubleshoot ainda mais a seguir:</span><span class="sxs-lookup"><span data-stu-id="581f4-143">tooease filtering over larger number of NSG rules, enter hello following commands tootroubleshoot further:</span></span> 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    <span data-ttu-id="581f4-144">Um filtro para o tráfego RDP (porta TCP 3389), é aplicada a exibição de grade toohello, conforme mostrado na figura abaixo de saudação:</span><span class="sxs-lookup"><span data-stu-id="581f4-144">A filter for RDP traffic (TCP port 3389), is applied toohello grid view, as shown in hello following picture:</span></span>
   
    ![Lista de regras](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. <span data-ttu-id="581f4-146">Como você pode ver no modo de exibição de grade hello, há dois permitirem e negar regras para RDP.</span><span class="sxs-lookup"><span data-stu-id="581f4-146">As you can see in hello grid view, there are both allow and deny rules for RDP.</span></span> <span data-ttu-id="581f4-147">Olá, saída da etapa 2 mostra que Olá *DenyRDP* a regra está em Olá NSG aplicada toohello sub-rede.</span><span class="sxs-lookup"><span data-stu-id="581f4-147">hello output from step 2 shows that hello *DenyRDP* rule is in hello NSG applied toohello subnet.</span></span> <span data-ttu-id="581f4-148">Para regras de entrada, os NSGs aplicados toohello sub-rede são processadas primeiro.</span><span class="sxs-lookup"><span data-stu-id="581f4-148">For inbound rules, NSGs applied toohello subnet are processed first.</span></span> <span data-ttu-id="581f4-149">Se uma correspondência for encontrada, a interface de rede do hello NSG aplicada toohello não foi processada.</span><span class="sxs-lookup"><span data-stu-id="581f4-149">If a match is found, hello NSG applied toohello network interface is not processed.</span></span> <span data-ttu-id="581f4-150">Nesse caso, Olá *DenyRDP* blocos de regra da sub-rede Olá RDP toohello VM (**VM1**).</span><span class="sxs-lookup"><span data-stu-id="581f4-150">In this case, hello *DenyRDP* rule from hello subnet blocks RDP toohello VM (**VM1**).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="581f4-151">Uma VM pode ter várias NICs e anexado tooit.</span><span class="sxs-lookup"><span data-stu-id="581f4-151">A VM may have multiple NICs attached tooit.</span></span> <span data-ttu-id="581f4-152">Cada um pode ser conectado tooa outra sub-rede.</span><span class="sxs-lookup"><span data-stu-id="581f4-152">Each may be connected tooa different subnet.</span></span> <span data-ttu-id="581f4-153">Como comandos de saudação nas etapas anteriores Olá são executados em relação a uma NIC, é importante tooensure que você especificar Olá NIC estiver com falha de conectividade de saudação em.</span><span class="sxs-lookup"><span data-stu-id="581f4-153">Since hello commands in hello previous steps are run against a NIC, it's important tooensure that you specify hello NIC you're having hello connectivity failure to.</span></span> <span data-ttu-id="581f4-154">Se você não tiver certeza, você também pode executar comandos de saudação em relação a cada toohello NIC conectada VM.</span><span class="sxs-lookup"><span data-stu-id="581f4-154">If you're not sure, you can always run hello commands against each NIC attached toohello VM.</span></span>
   > 
   > 
5. <span data-ttu-id="581f4-155">tooRDP na VM1, alteração Olá *negar RDP (3389)* regra muito*permitir RDP(3389)* em Olá **Subnet1 NSG** NSG.</span><span class="sxs-lookup"><span data-stu-id="581f4-155">tooRDP into VM1, change hello *Deny RDP (3389)* rule too*Allow RDP(3389)* in hello **Subnet1-NSG** NSG.</span></span> <span data-ttu-id="581f4-156">Confirme que a porta TCP 3389 esteja aberta abrindo uma conexão de RDP toohello VM ou usando a ferramenta de PsPing hello.</span><span class="sxs-lookup"><span data-stu-id="581f4-156">Confirm that TCP port 3389 is open by opening an RDP connection toohello VM or using hello PsPing tool.</span></span> <span data-ttu-id="581f4-157">Você pode aprender mais sobre PsPing ao ler Olá [PsPing página de download](https://technet.microsoft.com/sysinternals/psping.aspx)</span><span class="sxs-lookup"><span data-stu-id="581f4-157">You can learn more about PsPing by reading hello [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx)</span></span>
   
    <span data-ttu-id="581f4-158">Você pode ou remove as regras de um NSG usando informações de saudação da saída Olá Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="581f4-158">You can or remove rules from an NSG by using hello information in hello output from hello following command:</span></span>
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a><span data-ttu-id="581f4-159">Considerações</span><span class="sxs-lookup"><span data-stu-id="581f4-159">Considerations</span></span>
<span data-ttu-id="581f4-160">Considere Olá pontos a seguir ao solucionar problemas de conectividade:</span><span class="sxs-lookup"><span data-stu-id="581f4-160">Consider hello following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="581f4-161">As regras NSG padrão bloqueará o acesso de entrada de saudação à internet e permitir VNet o tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="581f4-161">Default NSG rules will block inbound access from hello internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="581f4-162">As regras devem ser adicionadas explicitamente tooallow acesso de entrada da Internet, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="581f4-162">Rules should be explicitly added tooallow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="581f4-163">Se não houver nenhuma regra de segurança NSG causando toofail de conectividade de rede da VM, problema de saudação pode ser devido a:</span><span class="sxs-lookup"><span data-stu-id="581f4-163">If there are no NSG security rules causing a VM’s network connectivity toofail, hello problem may be due to:</span></span>
  * <span data-ttu-id="581f4-164">Software de firewall em execução no sistema operacional da VM Olá</span><span class="sxs-lookup"><span data-stu-id="581f4-164">Firewall software running within hello VM's operating system</span></span>
  * <span data-ttu-id="581f4-165">Rotas configuradas para soluções de virtualização ou tráfego local.</span><span class="sxs-lookup"><span data-stu-id="581f4-165">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="581f4-166">Tráfego de Internet pode ser redirecionado tooon local por meio de túnel forçado.</span><span class="sxs-lookup"><span data-stu-id="581f4-166">Internet traffic can be redirected tooon-premises via forced-tunneling.</span></span> <span data-ttu-id="581f4-167">Uma conexão de RDP/SSH de saudação Internet tooyour VM pode não funcionar com essa configuração, dependendo de como o hardware de rede local Olá lida com esse tráfego.</span><span class="sxs-lookup"><span data-stu-id="581f4-167">An RDP/SSH connection from hello Internet tooyour VM may not work with this setting, depending on how hello on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="581f4-168">Saudação de leitura [rotas de solução de problemas](virtual-network-routes-troubleshoot-powershell.md) artigo toolearn como toodiagnose encaminhar os problemas que podem estar impedindo Olá fluxo do tráfego do hello VM.</span><span class="sxs-lookup"><span data-stu-id="581f4-168">Read hello [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article toolearn how toodiagnose route problems that may be impeding hello flow of traffic in and out of hello VM.</span></span> 
* <span data-ttu-id="581f4-169">Se você tiver emparelhadas VNets, por padrão, Olá marca VIRTUAL_NETWORK expandirá automaticamente tooinclude prefixos para emparelhadas VNets.</span><span class="sxs-lookup"><span data-stu-id="581f4-169">If you have peered VNets, by default, hello VIRTUAL_NETWORK tag will automatically expand tooinclude prefixes for peered VNets.</span></span> <span data-ttu-id="581f4-170">Você pode exibir esses prefixos no hello **ExpandedAddressPrefix** listar, tootroubleshoot qualquer tooVNet relacionados problemas emparelhamento de conectividade.</span><span class="sxs-lookup"><span data-stu-id="581f4-170">You can view these prefixes in hello **ExpandedAddressPrefix** list, tootroubleshoot any issues related tooVNet peering connectivity.</span></span> 
* <span data-ttu-id="581f4-171">Regras de segurança efetiva são mostradas apenas se houver que um NSG associado da VM Olá NIC e ou uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="581f4-171">Effective security rules are only shown if there is an NSG associated with hello VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="581f4-172">Se não há nenhum NSGs associados Olá NIC ou sub-rede e tiver um endereço IP público atribuído tooyour VM, todas as portas será abertas para acesso de entrada e saído.</span><span class="sxs-lookup"><span data-stu-id="581f4-172">If there are no NSGs associated with hello NIC or subnet and you have a public IP address assigned tooyour VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="581f4-173">Se Olá VM tem um endereço IP público, aplicar os NSGs toohello NIC ou sub-rede é recomendável.</span><span class="sxs-lookup"><span data-stu-id="581f4-173">If hello VM has a public IP address, applying NSGs toohello NIC or subnet is strongly recommended.</span></span>  

