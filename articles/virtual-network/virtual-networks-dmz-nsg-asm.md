---
title: "Exemplo de DMZ do Azure ‑ Criar um DMZ simples com NSGs | Microsoft Docs"
description: "Criar uma DMZ com grupos de segurança de rede (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: ed172d552e1e4c9ee27c58abcd7ad2d98df21579
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a><span data-ttu-id="7122a-103">Exemplo 1 – Criar uma DMZ simples usando NSGs com o PowerShell clássico</span><span class="sxs-lookup"><span data-stu-id="7122a-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span></span>
<span data-ttu-id="7122a-104">[Voltar à página Práticas recomendadas de limite de segurança][HOME]</span><span class="sxs-lookup"><span data-stu-id="7122a-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7122a-105">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7122a-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="7122a-106">Clássico - PowerShell</span><span class="sxs-lookup"><span data-stu-id="7122a-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="7122a-107">Este exemplo criará uma DMZ simples com quatro servidores Windows e Grupos de Segurança de Rede.</span><span class="sxs-lookup"><span data-stu-id="7122a-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="7122a-108">Este exemplo descreve cada um dos comandos relevantes do PowerShell para fornecer uma compreensão mais profunda de cada etapa.</span><span class="sxs-lookup"><span data-stu-id="7122a-108">This example describes each of the relevant PowerShell commands to provide a deeper understanding of each step.</span></span> <span data-ttu-id="7122a-109">Também há uma seção Cenário de Tráfego para fornecer um passo a passo detalhado sobre como o tráfego passa pelas camadas de defesa da rede de perímetro.</span><span class="sxs-lookup"><span data-stu-id="7122a-109">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="7122a-110">Por fim, na seção de referências, há o código e as instruções completas para criar este ambiente para testar e experimentar diversos cenários.</span><span class="sxs-lookup"><span data-stu-id="7122a-110">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span></span> 

<span data-ttu-id="7122a-111">![DMZ de entrada com NSG][1]</span><span class="sxs-lookup"><span data-stu-id="7122a-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="7122a-112">Descrição do ambiente</span><span class="sxs-lookup"><span data-stu-id="7122a-112">Environment description</span></span>
<span data-ttu-id="7122a-113">Neste exemplo, uma assinatura contém os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="7122a-113">In this example a subscription contains the following resources:</span></span>

* <span data-ttu-id="7122a-114">Dois serviços de nuvem: "FrontEnd001" e "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="7122a-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="7122a-115">Uma rede virtual, “CorpNetwork”, com duas sub-redes, “FrontEnd” e “BackEnd”</span><span class="sxs-lookup"><span data-stu-id="7122a-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="7122a-116">Um grupo de segurança de rede que é aplicado a ambas as sub-redes</span><span class="sxs-lookup"><span data-stu-id="7122a-116">A Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="7122a-117">Um Windows Server que representa um servidor Web de aplicativos ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="7122a-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="7122a-118">Dois servidores Windows que representam servidores de back-end de aplicativos (“AppVM01”, “AppVM02”)</span><span class="sxs-lookup"><span data-stu-id="7122a-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="7122a-119">Um servidor Windows que representa um servidor DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="7122a-119">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="7122a-120">Na seção de referências, há um script do PowerShell que cria a maior parte do ambiente descrito no exemplo.</span><span class="sxs-lookup"><span data-stu-id="7122a-120">In the references section, there is a PowerShell script that builds most of the environment described in this example.</span></span> <span data-ttu-id="7122a-121">A criação das VMs e das Redes Virtuais, embora seja feita por script de exemplo, não será descrita em detalhes neste documento.</span><span class="sxs-lookup"><span data-stu-id="7122a-121">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span></span> 

<span data-ttu-id="7122a-122">Para criar o ambiente;</span><span class="sxs-lookup"><span data-stu-id="7122a-122">To build the environment;</span></span>

1. <span data-ttu-id="7122a-123">Salve o arquivo xml de configuração de rede incluído na seção de referências (atualizado com nomes, localização e endereços IP que correspondam ao cenário determinado)</span><span class="sxs-lookup"><span data-stu-id="7122a-123">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span></span>
2. <span data-ttu-id="7122a-124">Atualize as variáveis do usuário no script para fazer a correspondência do ambiente em que o script deve ser executado (assinaturas, nomes de serviço, etc.)</span><span class="sxs-lookup"><span data-stu-id="7122a-124">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc.)</span></span>
3. <span data-ttu-id="7122a-125">Execute o script no PowerShell</span><span class="sxs-lookup"><span data-stu-id="7122a-125">Execute the script in PowerShell</span></span>

>[!Note]
><span data-ttu-id="7122a-126">A região representada no script do PowerShell deve corresponder à região representada no arquivo xml de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="7122a-126">The region signified in the PowerShell script must match the region signified in the network configuration xml file.</span></span>
>
>

<span data-ttu-id="7122a-127">Depois que o script é executado com sucesso, etapas adicionais podem ser seguidas; na seção de referências, há dois scripts para configurar o servidor Web e um servidor de aplicativos com um aplicativo Web simples para testar a configuração desta DMZ.</span><span class="sxs-lookup"><span data-stu-id="7122a-127">Once the script runs successfully additional optional steps may be taken, in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span>

<span data-ttu-id="7122a-128">As seções a seguir fornecem uma descrição detalhada dos Grupos de Segurança de Rede e como eles funcionam neste exemplo, percorrendo as principais linhas do script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7122a-128">The following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of the PowerShell script.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="7122a-129">Grupos de segurança de rede (NSG)</span><span class="sxs-lookup"><span data-stu-id="7122a-129">Network Security Groups (NSG)</span></span>
<span data-ttu-id="7122a-130">Neste exemplo, um grupo NSG é criado e então carregado com seis regras.</span><span class="sxs-lookup"><span data-stu-id="7122a-130">For this example, an NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="7122a-131">Em geral, você deve criar suas regras específicas "Permitir" primeiro e então as regras “Negar” mais genéricas por último.</span><span class="sxs-lookup"><span data-stu-id="7122a-131">Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last.</span></span> <span data-ttu-id="7122a-132">A prioridade atribuída ditará quais regras serão avaliadas primeiro.</span><span class="sxs-lookup"><span data-stu-id="7122a-132">The assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="7122a-133">Quando o tráfego se aplicar a uma regra específica, nenhuma regra adicional será avaliada.</span><span class="sxs-lookup"><span data-stu-id="7122a-133">Once traffic is found to apply to a specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="7122a-134">As regras NSG podem se aplicar na direção de entrada ou de saída (na perspectiva da sub-rede).</span><span class="sxs-lookup"><span data-stu-id="7122a-134">NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).</span></span>
> 
> 

<span data-ttu-id="7122a-135">Declarativamente, as regras a seguir estão sendo criadas para tráfego de entrada:</span><span class="sxs-lookup"><span data-stu-id="7122a-135">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="7122a-136">O tráfego interno de DNS (porta 53) é permitido</span><span class="sxs-lookup"><span data-stu-id="7122a-136">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="7122a-137">O tráfego de RDP (porta 3389) da Internet para qualquer VM é permitido</span><span class="sxs-lookup"><span data-stu-id="7122a-137">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="7122a-138">O tráfego HTTP (porta 80) da Internet ao servidor Web (IIS01) é permitido</span><span class="sxs-lookup"><span data-stu-id="7122a-138">HTTP traffic (port 80) from the Internet to web server (IIS01) is allowed</span></span>
4. <span data-ttu-id="7122a-139">Todo tráfego (todas as portas) de IIS01 para AppVM1 é permitido</span><span class="sxs-lookup"><span data-stu-id="7122a-139">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="7122a-140">Todo o tráfego (todas as portas) da Internet para a Rede Virtual inteira (todas as sub-redes) é Negado</span><span class="sxs-lookup"><span data-stu-id="7122a-140">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="7122a-141">Todo tráfego (todas as portas) da sub-rede Frontend para a sub-rede Backend é negado</span><span class="sxs-lookup"><span data-stu-id="7122a-141">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="7122a-142">Com essas regras associadas a cada sub-rede, se uma solicitação HTTP tiver entrado da Internet para o servidor Web, ambas as regras 3 (permitir) e 5 (negar) se aplicariam, mas já que a regra 3 tem uma prioridade maior, somente ela se aplicaria e a regra 5 não seria utilizada.</span><span class="sxs-lookup"><span data-stu-id="7122a-142">With these rules bound to each subnet, if an HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="7122a-143">Portanto, a solicitação HTTP seria permitida para o servidor Web.</span><span class="sxs-lookup"><span data-stu-id="7122a-143">Thus the HTTP request would be allowed to the web server.</span></span> <span data-ttu-id="7122a-144">Se esse mesmo tráfego estivesse tentando acessar o servidor DNS01, a regra 5 (Negar) seria a primeira a ser aplicada e o tráfego não teria permissão para passar para o servidor.</span><span class="sxs-lookup"><span data-stu-id="7122a-144">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="7122a-145">A regra 6 (Negar) impede que a sub-rede Frontend converse com a sub-rede Backend (exceto pelo tráfego permitido nas regras 1 e 4); esse conjunto de regras protege a rede Backend caso um invasor comprometa o aplicativo Web na rede Frontend, pois ele teria acesso limitado à rede Backend “protegida” (somente para recursos expostos no servidor AppVM01).</span><span class="sxs-lookup"><span data-stu-id="7122a-145">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="7122a-146">Há uma regra de saída padrão que permite o tráfego de saída para a Internet.</span><span class="sxs-lookup"><span data-stu-id="7122a-146">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="7122a-147">Neste exemplo, permitiremos o tráfego de saída e não modificaremos quaisquer regras de saída.</span><span class="sxs-lookup"><span data-stu-id="7122a-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="7122a-148">Para bloquear o tráfego em ambos os sentidos, o Roteamento Definido pelo Usuário é necessário e explorado no “Exemplo 3”, na [Página de práticas recomendadas dos limites de segurança][HOME].</span><span class="sxs-lookup"><span data-stu-id="7122a-148">To lock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on the [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="7122a-149">Cada regra é discutida em mais detalhes da seguinte maneira (**Observação**: qualquer item na lista a seguir que comece com um sinal de cifrão (por exemplo, $NSGName) é uma variável definida pelo usuário do script na seção de referência deste documento):</span><span class="sxs-lookup"><span data-stu-id="7122a-149">Each rule is discussed in more detail as follows (**Note**: any item in the following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from the script in the reference section of this document):</span></span>

1. <span data-ttu-id="7122a-150">Primeiro, um grupo de segurança de rede deve ser criado para conter as regras:</span><span class="sxs-lookup"><span data-stu-id="7122a-150">First a Network Security Group must be built to hold the rules:</span></span>

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. <span data-ttu-id="7122a-151">A primeira regra neste exemplo habilita o tráfego DNS entre todas as redes internas para o servidor DNS na sub-rede de back-end.</span><span class="sxs-lookup"><span data-stu-id="7122a-151">The first rule in this example allows DNS traffic between all internal networks to the DNS server on the backend subnet.</span></span> <span data-ttu-id="7122a-152">A regra tem alguns parâmetros importantes:</span><span class="sxs-lookup"><span data-stu-id="7122a-152">The rule has some important parameters:</span></span>
   
   * <span data-ttu-id="7122a-153">“Type” (Tipo) indica em qual direção do fluxo de tráfego esta regra entra em vigor.</span><span class="sxs-lookup"><span data-stu-id="7122a-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="7122a-154">Esta é a direção da perspectiva da sub-rede ou da máquina virtual (dependendo da associação desse NSG).</span><span class="sxs-lookup"><span data-stu-id="7122a-154">The direction is from the perspective of the subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="7122a-155">Portanto, se o tipo é "Inbound" e tráfego está entrando na sub-rede, a regra se aplica e o tráfego que sai da sub-rede não é afetado por essa regra.</span><span class="sxs-lookup"><span data-stu-id="7122a-155">Thus if Type is “Inbound” and traffic is entering the subnet, the rule would apply and traffic leaving the subnet would not be affected by this rule.</span></span>
   * <span data-ttu-id="7122a-156">“Priority” (Prioridade) define a ordem na qual um fluxo de tráfego é avaliado.</span><span class="sxs-lookup"><span data-stu-id="7122a-156">“Priority” sets the order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="7122a-157">Quanto menor o número, maior a prioridade.</span><span class="sxs-lookup"><span data-stu-id="7122a-157">The lower the number the higher the priority.</span></span> <span data-ttu-id="7122a-158">Assim que uma regra se aplicar a um fluxo de tráfego específico, nenhuma regra adicional será processada.</span><span class="sxs-lookup"><span data-stu-id="7122a-158">When a rule applies to a specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="7122a-159">Portanto, se uma regra com prioridade 1 permite o tráfego e uma regra com prioridade 2 impede o tráfego e ambas as regras se aplicam ao tráfego, ele teria o fluxo permitido (já que a regra 1 tinha uma prioridade mais alta, ela vigorou e nenhuma regra adicional foi aplicada).</span><span class="sxs-lookup"><span data-stu-id="7122a-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply to traffic then the traffic would be allowed to flow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
   * <span data-ttu-id="7122a-160">"Action" significa se um tráfego afetado por essa regra é bloqueado ou permitido.</span><span class="sxs-lookup"><span data-stu-id="7122a-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span></span>

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. <span data-ttu-id="7122a-161">Essa regra permite que o tráfego de RDP flua da Internet para a porta RDP em qualquer servidor na sub-rede associada.</span><span class="sxs-lookup"><span data-stu-id="7122a-161">This rule allows RDP traffic to flow from the internet to the RDP port on any server on the bound subnet.</span></span> <span data-ttu-id="7122a-162">Essa regra usa dois tipos especiais de prefixos de endereço; “VIRTUAL_NETWORK” e “INTERNET”.</span><span class="sxs-lookup"><span data-stu-id="7122a-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span></span> <span data-ttu-id="7122a-163">Essas marcações são uma maneira fácil de resolver uma categoria maior de prefixos de endereço.</span><span class="sxs-lookup"><span data-stu-id="7122a-163">These tags are an easy way to address a larger category of address prefixes.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. <span data-ttu-id="7122a-164">Essa regra permite que o tráfego da internet alcance o servidor Web.</span><span class="sxs-lookup"><span data-stu-id="7122a-164">This rule allows inbound internet traffic to hit the web server.</span></span> <span data-ttu-id="7122a-165">Essa regra não altera o comportamento de roteamento.</span><span class="sxs-lookup"><span data-stu-id="7122a-165">This rule does not change the routing behavior.</span></span> <span data-ttu-id="7122a-166">A regra permite a passagem somente de tráfego destinado a IIS01.</span><span class="sxs-lookup"><span data-stu-id="7122a-166">The rule only allows traffic destined for IIS01 to pass.</span></span> <span data-ttu-id="7122a-167">Portanto, se o tráfego da Internet tinha o servidor Web como seu destino, essa regra deve permiti-lo e deve parar de processar outras regras.</span><span class="sxs-lookup"><span data-stu-id="7122a-167">Thus if traffic from the Internet had the web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="7122a-168">(Na regra com prioridade 140, todos os outros tráfegos de entrada da Internet estão bloqueados.)</span><span class="sxs-lookup"><span data-stu-id="7122a-168">(In the rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="7122a-169">Se você estiver processando somente tráfego HTTP, essa regra poderá ser mais restrita para permitir somente a porta de destino 80.</span><span class="sxs-lookup"><span data-stu-id="7122a-169">If you're only processing HTTP traffic, this rule could be further restricted to only allow Destination Port 80.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet to $VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. <span data-ttu-id="7122a-170">Essa regra permite que o tráfego passe do servidor IIS01 para o servidor AppVM01; uma regra posterior bloqueia todo o tráfego de Frontend para Backend.</span><span class="sxs-lookup"><span data-stu-id="7122a-170">This rule allows traffic to pass from the IIS01 server to the AppVM01 server, a later rule blocks all other Frontend to Backend traffic.</span></span> <span data-ttu-id="7122a-171">Para melhorar essa regra, se a porta for conhecida, ela deve ser adicionada.</span><span class="sxs-lookup"><span data-stu-id="7122a-171">To improve this rule, if the port is known that should be added.</span></span> <span data-ttu-id="7122a-172">Por exemplo, se o servidor IIS está atingindo somente o SQL Server no AppVM01, o intervalo de porta de destino deve ser alterado de "*" (qualquer) para 1433 (a porta do SQL), permitindo uma menor superfície de ataque de entrada em AppVM01 se o aplicativo Web for comprometido.</span><span class="sxs-lookup"><span data-stu-id="7122a-172">For example, if the IIS server is hitting only SQL Server on AppVM01, the Destination Port Range should be changed from “*” (Any) to 1433 (the SQL port) thus allowing a smaller inbound attack surface on AppVM01 should the web application ever be compromised.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] to $VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. <span data-ttu-id="7122a-173">Essa regra nega o tráfego da Internet para todos os servidores na rede.</span><span class="sxs-lookup"><span data-stu-id="7122a-173">This rule denies traffic from the internet to any servers on the network.</span></span> <span data-ttu-id="7122a-174">Com a regra em prioridades 110 e 120, o efeito é que ela permite somente tráfego de entrada da Internet para o firewall e portas RDP nos servidores e bloqueia todo o resto.</span><span class="sxs-lookup"><span data-stu-id="7122a-174">With the rules at priority 110 and 120, the effect is to allow only inbound internet traffic to the firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="7122a-175">Essa é uma regra “à prova de falhas” para bloquear todos os fluxos inesperados.</span><span class="sxs-lookup"><span data-stu-id="7122a-175">This rule is a "fail-safe" rule to block all unexpected flows.</span></span>
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate the $VNetName VNet from the Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. <span data-ttu-id="7122a-176">A regra final nega odo o tráfego (todas as portas) da sub-rede Frontend para a sub-rede Backend.</span><span class="sxs-lookup"><span data-stu-id="7122a-176">The final rule denies traffic from the Frontend subnet to the Backend subnet.</span></span> <span data-ttu-id="7122a-177">Como essa é uma regra somente de Entrada, o tráfego invertido é permitido (de Backend para Frontend).</span><span class="sxs-lookup"><span data-stu-id="7122a-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from the Backend to the Frontend).</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate the $FESubnet subnet from the $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="7122a-178">Cenários de tráfego</span><span class="sxs-lookup"><span data-stu-id="7122a-178">Traffic scenarios</span></span>
#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="7122a-179">(*Permitido*) Internet para servidor Web</span><span class="sxs-lookup"><span data-stu-id="7122a-179">(*Allowed*) Internet to web server</span></span>
1. <span data-ttu-id="7122a-180">Um usuário da Internet solicita uma página HTTP de FrontEnd001.CloudApp.Net (Serviço de Nuvem Voltado para Internet)</span><span class="sxs-lookup"><span data-stu-id="7122a-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="7122a-181">O serviço de nuvem passa o tráfego pelo ponto de extremidade aberto na porta 80 para o IIS01 (o servidor Web)</span><span class="sxs-lookup"><span data-stu-id="7122a-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="7122a-182">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="7122a-182">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7122a-183">A Regra NSG 1 (DNS) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="7122a-183">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="7122a-184">A Regra NSG 2 (RDP) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="7122a-184">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="7122a-185">A Regra NSG 3 (Internet para IIS01) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="7122a-185">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="7122a-186">O tráfego atinge o endereço IP interno do servidor Web IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="7122a-186">Traffic hits internal IP address of the web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="7122a-187">O IIS01 está escutando o tráfego da Web, recebe essa solicitação e começa a processar a solicitação</span><span class="sxs-lookup"><span data-stu-id="7122a-187">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
6. <span data-ttu-id="7122a-188">O IIS01 solicita informações do SQL Server na AppVM01</span><span class="sxs-lookup"><span data-stu-id="7122a-188">IIS01 asks the SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="7122a-189">Como não há regras de saída na sub-rede Frontend, o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="7122a-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="7122a-190">A sub-rede Backend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="7122a-190">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7122a-191">A Regra NSG 1 (DNS) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="7122a-191">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="7122a-192">A Regra NSG 2 (RDP) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="7122a-192">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="7122a-193">A Regra NSG 3 (Internet para Firewall) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="7122a-193">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="7122a-194">A regra NSG 4 (IIS01 para AppVM01) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="7122a-194">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="7122a-195">AppVM01 recebe a consulta SQL e responde</span><span class="sxs-lookup"><span data-stu-id="7122a-195">AppVM01 receives the SQL Query and responds</span></span>
10. <span data-ttu-id="7122a-196">Como não há nenhuma regra de saída na sub-rede de Back-end, a resposta é permitida</span><span class="sxs-lookup"><span data-stu-id="7122a-196">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
11. <span data-ttu-id="7122a-197">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="7122a-197">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="7122a-198">Não há nenhuma regra NSG que se aplique ao tráfego de Entrada da sub-rede Backend para a sub-rede Frontend e, portanto, nenhuma das regras NSG se aplica</span><span class="sxs-lookup"><span data-stu-id="7122a-198">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="7122a-199">A regra do sistema padrão que permite o tráfego entre sub-redes permitiria esse tráfego e, portanto, o tráfego é permitido.</span><span class="sxs-lookup"><span data-stu-id="7122a-199">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
12. <span data-ttu-id="7122a-200">O servidor IIS recebe a resposta SQL e conclui a resposta HTTP e envia ao solicitante</span><span class="sxs-lookup"><span data-stu-id="7122a-200">The IIS server receives the SQL response and completes the HTTP response and sends to the requestor</span></span>
13. <span data-ttu-id="7122a-201">Como não há nenhuma regra de saída na sub-rede Frontend, a resposta é permitida e o Usuário da Internet recebe a página da Web solicitada.</span><span class="sxs-lookup"><span data-stu-id="7122a-201">Since there are no outbound rules on the Frontend subnet the response is allowed, and the internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-backend"></a><span data-ttu-id="7122a-202">(*Permitido*) RDP para back-end</span><span class="sxs-lookup"><span data-stu-id="7122a-202">(*Allowed*) RDP to backend</span></span>
1. <span data-ttu-id="7122a-203">O Administrador do servidor na Internet solicita a sessão RDP para AppVM01 em BackEnd001.CloudApp.Net:xxxxx, em que xxxxx é o número da porta atribuído aleatoriamente para RDP para AppVM01 (a porta atribuída pode ser encontrada no Portal do Azure ou através do PowerShell)</span><span class="sxs-lookup"><span data-stu-id="7122a-203">Server Admin on internet requests RDP session to AppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is the randomly assigned port number for RDP to AppVM01 (the assigned port can be found on the Azure portal or via PowerShell)</span></span>
2. <span data-ttu-id="7122a-204">A sub-rede Backend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="7122a-204">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7122a-205">A Regra NSG 1 (DNS) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="7122a-205">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="7122a-206">A regra NSG 2 (RDP) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="7122a-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
3. <span data-ttu-id="7122a-207">Sem regras de saída, as regras padrão serão aplicadas e o tráfego de retorno será permitido</span><span class="sxs-lookup"><span data-stu-id="7122a-207">With no outbound rules, default rules apply and return traffic is allowed</span></span>
4. <span data-ttu-id="7122a-208">A sessão RDP está habilitada</span><span class="sxs-lookup"><span data-stu-id="7122a-208">RDP session is enabled</span></span>
5. <span data-ttu-id="7122a-209">O AppVM01 solicita o nome de usuário e senha</span><span class="sxs-lookup"><span data-stu-id="7122a-209">AppVM01 prompts for the user name and password</span></span>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="7122a-210">(*Permitido*) Pesquisa de DNS do servidor Web no servidor DNS</span><span class="sxs-lookup"><span data-stu-id="7122a-210">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="7122a-211">O Servidor Web, IIS01, necessita de um feed de dados em www.data.gov, mas precisa resolver o endereço.</span><span class="sxs-lookup"><span data-stu-id="7122a-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="7122a-212">A configuração de rede para a Rede Virtual lista DNS01 (10.0.2.4 na sub-rede Backend), já que o servidor DNS primário, IIS01, envia a solicitação DNS para DNS01</span><span class="sxs-lookup"><span data-stu-id="7122a-212">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="7122a-213">Não há regras de saída na sub-rede Frontend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="7122a-213">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="7122a-214">A sub-rede Backend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="7122a-214">Backend subnet begins inbound rule processing:</span></span>
   * <span data-ttu-id="7122a-215">A regra NSG 1 (DNS) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="7122a-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="7122a-216">O servidor DNS recebe a solicitação</span><span class="sxs-lookup"><span data-stu-id="7122a-216">DNS server receives the request</span></span>
6. <span data-ttu-id="7122a-217">O servidor DNS não tem o endereço armazenado em cache e consulta um servidor DNS raiz na Internet</span><span class="sxs-lookup"><span data-stu-id="7122a-217">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="7122a-218">Nenhuma regra de saída na sub-rede Backend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="7122a-218">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="7122a-219">O servidor DNS da Internet responde e, desde que esta sessão tenha sido iniciada internamente, a resposta será permitida</span><span class="sxs-lookup"><span data-stu-id="7122a-219">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="7122a-220">O servidor DNS armazena em cache a resposta e responde à solicitação inicial para IIS01</span><span class="sxs-lookup"><span data-stu-id="7122a-220">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="7122a-221">Nenhuma regra de saída na sub-rede Backend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="7122a-221">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="7122a-222">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="7122a-222">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="7122a-223">Não há nenhuma regra NSG que se aplique ao tráfego de Entrada da sub-rede Backend para a sub-rede Frontend e, portanto, nenhuma das regras NSG se aplica</span><span class="sxs-lookup"><span data-stu-id="7122a-223">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="7122a-224">A regra do sistema padrão que permite o tráfego entre sub-redes permitiria esse tráfego e, portanto, o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="7122a-224">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="7122a-225">O IIS01 recebe a resposta do DNS01</span><span class="sxs-lookup"><span data-stu-id="7122a-225">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="7122a-226">(*Permitido*) Arquivo de acesso do servidor Web em AppVM01</span><span class="sxs-lookup"><span data-stu-id="7122a-226">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="7122a-227">IIS01 solicita um arquivo em AppVM01</span><span class="sxs-lookup"><span data-stu-id="7122a-227">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="7122a-228">Não há regras de saída na sub-rede Frontend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="7122a-228">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="7122a-229">A sub-rede Backend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="7122a-229">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7122a-230">A Regra NSG 1 (DNS) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="7122a-230">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="7122a-231">A Regra NSG 2 (RDP) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="7122a-231">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="7122a-232">A Regra NSG 3 (Internet para IIS01) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="7122a-232">NSG Rule 3 (Internet to IIS01) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="7122a-233">A regra NSG 4 (IIS01 para AppVM01) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="7122a-233">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="7122a-234">AppVM01 recebe a solicitação e responde com o arquivo (supondo que o acesso é autorizado)</span><span class="sxs-lookup"><span data-stu-id="7122a-234">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="7122a-235">Como não há nenhuma regra de saída na sub-rede de Back-end, a resposta é permitida</span><span class="sxs-lookup"><span data-stu-id="7122a-235">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
6. <span data-ttu-id="7122a-236">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="7122a-236">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7122a-237">Não há nenhuma regra NSG que se aplique ao tráfego de Entrada da sub-rede Backend para a sub-rede Frontend e, portanto, nenhuma das regras NSG se aplica</span><span class="sxs-lookup"><span data-stu-id="7122a-237">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
   2. <span data-ttu-id="7122a-238">A regra do sistema padrão que permite o tráfego entre sub-redes permitiria esse tráfego e, portanto, o tráfego é permitido.</span><span class="sxs-lookup"><span data-stu-id="7122a-238">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="7122a-239">O servidor IIS recebe o arquivo</span><span class="sxs-lookup"><span data-stu-id="7122a-239">The IIS server receives the file</span></span>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="7122a-240">(*Negado*) Web para o servidor de back-end</span><span class="sxs-lookup"><span data-stu-id="7122a-240">(*Denied*) Web to backend server</span></span>
1. <span data-ttu-id="7122a-241">Um usuário da Internet tenta acessar um arquivo em AppVM01 por meio do serviço BackEnd001.CloudApp.Net</span><span class="sxs-lookup"><span data-stu-id="7122a-241">An internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="7122a-242">Como não há nenhum ponto de extremidade aberto para compartilhamento de arquivos, esse tráfego não passaria no Serviço de Nuvem e não alcançaria o servidor</span><span class="sxs-lookup"><span data-stu-id="7122a-242">Since there are no endpoints open for file share, this traffic would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="7122a-243">Se os pontos de extremidade estiverem abertos por algum motivo, a regra NSG 5 (Internet para Rede Virtual) bloquearia esse tráfego</span><span class="sxs-lookup"><span data-stu-id="7122a-243">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="7122a-244">(*Negado*) Pesquisa de DNS na Web no servidor DNS</span><span class="sxs-lookup"><span data-stu-id="7122a-244">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="7122a-245">Um usuário da Internet tenta procurar um registro DNS interno em DNS01 por meio do serviço BackEnd001.CloudApp.Net</span><span class="sxs-lookup"><span data-stu-id="7122a-245">An internet user tries to look up an internal DNS record on DNS01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="7122a-246">Como não há nenhum ponto de extremidade aberto para DNS, esse tráfego não passaria no Serviço de Nuvem e não alcançaria o servidor</span><span class="sxs-lookup"><span data-stu-id="7122a-246">Since there are no endpoints open for DNS, this traffic would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="7122a-247">Se os pontos de extremidade tiverem sido abertos por algum motivo, a regra NSG 5 (Internet para Rede Virtual) bloquearia esse tráfego (observação: essa Regra 1 (DNS) não se aplicariam por dois motivos, primeiro o endereço de origem será a Internet, essa regra só se aplicará à VNet local como a origem e, como esta também é uma regra Permitir, nunca negaria o tráfego)</span><span class="sxs-lookup"><span data-stu-id="7122a-247">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first the source address is the internet, this rule only applies to the local VNet as the source, also this rule is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-to-sql-access-through-firewall"></a><span data-ttu-id="7122a-248">(*Negado*) Acesso Web ao SQL por meio do firewall</span><span class="sxs-lookup"><span data-stu-id="7122a-248">(*Denied*) Web to SQL access through firewall</span></span>
1. <span data-ttu-id="7122a-249">Um usuário da Internet solicita dados SQL de FrontEnd001.CloudApp.Net (Serviço de Nuvem Voltado para a Internet)</span><span class="sxs-lookup"><span data-stu-id="7122a-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="7122a-250">Como não há nenhum ponto de extremidade aberto para SQL, esse tráfego não passaria no Serviço de Nuvem e não alcançaria o firewall</span><span class="sxs-lookup"><span data-stu-id="7122a-250">Since there are no endpoints open for SQL, this traffic would not pass the Cloud Service and wouldn’t reach the firewall</span></span>
3. <span data-ttu-id="7122a-251">Se os pontos de extremidade estiverem abertos por algum motivo, a sub-rede Frontend inicia o processamento de regras de entrada:</span><span class="sxs-lookup"><span data-stu-id="7122a-251">If endpoints were open for some reason, the Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7122a-252">A Regra NSG 1 (DNS) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="7122a-252">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="7122a-253">A Regra NSG 2 (RDP) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="7122a-253">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="7122a-254">A Regra NSG 3 (Internet para IIS01) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="7122a-254">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="7122a-255">O tráfego atinge o endereço IP interno do IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="7122a-255">Traffic hits internal IP address of the IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="7122a-256">O IIS01 não está escutando na porta 1433; portanto, não há resposta para a solicitação</span><span class="sxs-lookup"><span data-stu-id="7122a-256">IIS01 isn't listening on port 1433, so no response to the request</span></span>

## <a name="conclusion"></a><span data-ttu-id="7122a-257">Conclusão</span><span class="sxs-lookup"><span data-stu-id="7122a-257">Conclusion</span></span>
<span data-ttu-id="7122a-258">Esse exemplo representa uma maneira relativamente simples e direta de isolar a sub-rede de back-end do tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="7122a-258">This example is a relatively simple and straight forward way of isolating the back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="7122a-259">Mais exemplos e uma visão geral dos limites de segurança de rede podem ser encontrados [aqui][HOME].</span><span class="sxs-lookup"><span data-stu-id="7122a-259">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="7122a-260">Referências</span><span class="sxs-lookup"><span data-stu-id="7122a-260">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="7122a-261">Script principal e configuração de rede</span><span class="sxs-lookup"><span data-stu-id="7122a-261">Main script and network config</span></span>
<span data-ttu-id="7122a-262">Salve o Script Completo em um arquivo de script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7122a-262">Save the Full Script in a PowerShell script file.</span></span> <span data-ttu-id="7122a-263">Salve a Configuração de Rede em um arquivo denominado “NetworkConf1.xml”.</span><span class="sxs-lookup"><span data-stu-id="7122a-263">Save the Network Config into a file named “NetworkConf1.xml.”</span></span>
<span data-ttu-id="7122a-264">Modifique as variáveis definidas pelo usuário como necessárias e execute o script.</span><span class="sxs-lookup"><span data-stu-id="7122a-264">Modify the user-defined variables as needed and run the script.</span></span>

#### <a name="full-script"></a><span data-ttu-id="7122a-265">Script completo</span><span class="sxs-lookup"><span data-stu-id="7122a-265">Full script</span></span>
<span data-ttu-id="7122a-266">Esse script se baseará nas variáveis definidas pelo usuário;</span><span class="sxs-lookup"><span data-stu-id="7122a-266">This script will, based on the user-defined variables;</span></span>

1. <span data-ttu-id="7122a-267">Conectar-se a uma assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="7122a-267">Connect to an Azure subscription</span></span>
2. <span data-ttu-id="7122a-268">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="7122a-268">Create a storage account</span></span>
3. <span data-ttu-id="7122a-269">Criar uma nova VNet e duas sub-redes, conforme definido no arquivo de Configuração de Rede</span><span class="sxs-lookup"><span data-stu-id="7122a-269">Create a VNet and two subnets as defined in the Network Config file</span></span>
4. <span data-ttu-id="7122a-270">Crie quatro VMs do Windows Server</span><span class="sxs-lookup"><span data-stu-id="7122a-270">Build four windows server VMs</span></span>
5. <span data-ttu-id="7122a-271">Configure o NSG, incluindo:</span><span class="sxs-lookup"><span data-stu-id="7122a-271">Configure NSG including:</span></span>
   * <span data-ttu-id="7122a-272">Criando um NSG</span><span class="sxs-lookup"><span data-stu-id="7122a-272">Creating an NSG</span></span>
   * <span data-ttu-id="7122a-273">Preenchendo-o com regras</span><span class="sxs-lookup"><span data-stu-id="7122a-273">Populating it with rules</span></span>
   * <span data-ttu-id="7122a-274">Associando o NSG às sub-redes apropriadas</span><span class="sxs-lookup"><span data-stu-id="7122a-274">Binding the NSG to the appropriate subnets</span></span>

<span data-ttu-id="7122a-275">Este script do PowerShell deve ser executado localmente em um computador ou servidor conectado à Internet.</span><span class="sxs-lookup"><span data-stu-id="7122a-275">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7122a-276">Quando esse script for executado, poderá haver avisos ou outras mensagens informativas que aparecerão no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7122a-276">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="7122a-277">Somente as mensagens de erro em vermelho são motivo de preocupação.</span><span class="sxs-lookup"><span data-stu-id="7122a-277">Only error messages in red are cause for concern.</span></span>
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on the FrontEnd Subnet
   - Three Servers on the BackEnd Subnet
   - Network Security Groups to allow/deny traffic patterns as declared

  Before running script, ensure the network configuration file is created in
  the directory referenced by $NetworkConfigFile variable (or update the
  variable to reflect the path and file name of the config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  the appropriate layer(s) of protection. This script serves as an example of some
  of the techniques that can be used, but should not be used for all scenarios. You
  are responsible to assess your security needs and the appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

  BackEnd Service (BackEnd subnet 10.0.2.0/24)
   DNS01      - 10.0.2.4
   AppVM01    - 10.0.2.5
   AppVM02    - 10.0.2.6

#>

# Fixed Variables
    $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password to be used for all VMs"
    $VMName = @()
    $ServiceName = @()
    $VMFamily = @()
    $img = @()
    $size = @()
    $SubnetName = @()
    $VMIP = @()

# User-Defined Global Variables
  # These should be changes to reflect your subscription and services
  # Invalid options will fail in the validation section

  # Subscription Access Details
    $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

  # VM Account, Location, and Storage Details
    $LocalAdmin = "theAdmin"
    $DeploymentLocation = "Central US"
    $StorageAccountName = "vmstore02"

  # Service Details
    $FrontEndService = "FrontEnd001"
    $BackEndService = "BackEnd001"

  # Network Details
    $VNetName = "CorpNetwork"
    $FESubnet = "FrontEnd"
    $FEPrefix = "10.0.1.0/24"
    $BESubnet = "BackEnd"
    $BEPrefix = "10.0.2.0/24"
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: To ensure proper NSG Rule creation later in this script:
    #       - The Web Server must be VM 0
    #       - The AppVM1 Server must be VM 1
    #       - The DNS server must be VM 3
    #
    #       Otherwise the NSG rules in the last section of this
    #       script will need to be changed to match the modified
    #       VM array numbers ($i) so the NSG Rule IP addresses
    #       are aligned to the associated VM IP addresses.

    # VM 0 - The Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - The First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - The Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - The DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
        Return}
    Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
          New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

  # Update Subscription Pointer to New Storage Account
    Write-Host "Updating Subscription Pointer to New Storage Account" -ForegroundColor Cyan 
    Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

# Validation
$FatalError = $false

If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
     Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
     $FatalError = $true}

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "The FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "The BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'The network config file was not found, please update the $NetworkConfigFile variable to point to the network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'The deployment location was not found in the network config file, please check the network config file to ensure the $DeploymentLocation variable is correct and the network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "The deployment location was found in the network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see the above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building the environment." -ForegroundColor Green}

# Create VNET
    Write-Host "Creating VNET" -ForegroundColor Cyan 
    Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

# Create Services
    Write-Host "Creating Services" -ForegroundColor Cyan
    New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
    New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

# Build VMs
    $i=0
    $VMName | Foreach {
        Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

  # Build the NSG
    Write-Host "Building the NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet to $($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) to $($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet from the Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $FESubnet subnet from the $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign the NSG to the Subnets
        Write-Host "Binding the NSG to both subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on the IIS Server)
  # Install Backend resource (Run Post-Build Script on the AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on the IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on the AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a><span data-ttu-id="7122a-278">Arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="7122a-278">Network config file</span></span>
<span data-ttu-id="7122a-279">Salve esse arquivo xml com o local atualizado e adicione o link para esse arquivo à variável $NetworkConfigFile no script anterior.</span><span class="sxs-lookup"><span data-stu-id="7122a-279">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the preceding script.</span></span>

```XML
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="DNS01" IPAddress="10.0.2.4" />
        <DnsServer name="Level3" IPAddress="209.244.0.3" />
      </DnsServers>
    </Dns>
    <VirtualNetworkSites>
      <VirtualNetworkSite name="CorpNetwork" Location="Central US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="FrontEnd">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="BackEnd">
            <AddressPrefix>10.0.2.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
        <DnsServersRef>
          <DnsServerRef name="DNS01" />
          <DnsServerRef name="Level3" />
        </DnsServersRef>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

#### <a name="sample-application-scripts"></a><span data-ttu-id="7122a-280">Scripts de aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="7122a-280">Sample application scripts</span></span>
<span data-ttu-id="7122a-281">Se você desejar instalar um aplicativo de exemplo para esse e outros Exemplos de DMZ, um deles foi fornecido no seguinte link: [Script de aplicativo de exemplo][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="7122a-281">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="7122a-282">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7122a-282">Next steps</span></span>
* <span data-ttu-id="7122a-283">Atualizar e salvar o arquivo XML</span><span class="sxs-lookup"><span data-stu-id="7122a-283">Update and save XML file</span></span>
* <span data-ttu-id="7122a-284">Execute o script do PowerShell para compilar o ambiente</span><span class="sxs-lookup"><span data-stu-id="7122a-284">Run the PowerShell script to build the environment</span></span>
* <span data-ttu-id="7122a-285">Instalar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="7122a-285">Install the sample application</span></span>
* <span data-ttu-id="7122a-286">Testar diferentes fluxos de tráfego por meio dessa DMZ</span><span class="sxs-lookup"><span data-stu-id="7122a-286">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
<span data-ttu-id="7122a-287">[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "DMZ de entrada com NSG"</span><span class="sxs-lookup"><span data-stu-id="7122a-287">[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Inbound DMZ with NSG"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

