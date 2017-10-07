---
title: "aaaAzure exemplo DMZ – criar uma rede de Perímetro simples com NSGs | Microsoft Docs"
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
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a><span data-ttu-id="467be-103">Exemplo 1 – Criar uma DMZ simples usando NSGs com o PowerShell clássico</span><span class="sxs-lookup"><span data-stu-id="467be-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span></span>
<span data-ttu-id="467be-104">[Retornar toohello página segurança limite de melhores práticas][HOME]</span><span class="sxs-lookup"><span data-stu-id="467be-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="467be-105">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="467be-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="467be-106">Clássico - PowerShell</span><span class="sxs-lookup"><span data-stu-id="467be-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="467be-107">Este exemplo criará uma DMZ simples com quatro servidores Windows e Grupos de Segurança de Rede.</span><span class="sxs-lookup"><span data-stu-id="467be-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="467be-108">Este exemplo descreve cada Olá relevantes PowerShell comandos tooprovide uma compreensão mais profunda de cada etapa.</span><span class="sxs-lookup"><span data-stu-id="467be-108">This example describes each of hello relevant PowerShell commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="467be-109">Também há um cenário de tráfego seção tooprovide um detalhadas passo a passo sobre como o tráfego passa as camadas de saudação de defesa Olá DMZ.</span><span class="sxs-lookup"><span data-stu-id="467be-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="467be-110">Por fim, na seção de referências de saudação é código completo hello e instrução toobuild este ambiente tootest e experiência com vários cenários.</span><span class="sxs-lookup"><span data-stu-id="467be-110">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="467be-111">![DMZ de entrada com NSG][1]</span><span class="sxs-lookup"><span data-stu-id="467be-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="467be-112">Descrição do ambiente</span><span class="sxs-lookup"><span data-stu-id="467be-112">Environment description</span></span>
<span data-ttu-id="467be-113">Neste exemplo, uma assinatura contém Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="467be-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="467be-114">Dois serviços de nuvem: "FrontEnd001" e "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="467be-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="467be-115">Uma rede virtual, “CorpNetwork”, com duas sub-redes, “FrontEnd” e “BackEnd”</span><span class="sxs-lookup"><span data-stu-id="467be-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="467be-116">Um grupo de segurança de rede que é aplicada tooboth sub-redes</span><span class="sxs-lookup"><span data-stu-id="467be-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="467be-117">Um Windows Server que representa um servidor Web de aplicativos ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="467be-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="467be-118">Dois servidores Windows que representam servidores de back-end de aplicativos (“AppVM01”, “AppVM02”)</span><span class="sxs-lookup"><span data-stu-id="467be-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="467be-119">Um servidor Windows que representa um servidor DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="467be-119">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="467be-120">Na seção de referências de hello, há um script do PowerShell que cria a maior parte do ambiente de saudação descrito neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="467be-120">In hello references section, there is a PowerShell script that builds most of hello environment described in this example.</span></span> <span data-ttu-id="467be-121">Criando Olá VMs e redes virtuais, embora são feitos pelo script de exemplo hello, não são descritas em detalhes neste documento.</span><span class="sxs-lookup"><span data-stu-id="467be-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span> 

<span data-ttu-id="467be-122">ambiente de saudação toobuild;</span><span class="sxs-lookup"><span data-stu-id="467be-122">toobuild hello environment;</span></span>

1. <span data-ttu-id="467be-123">Salvar arquivo hello rede config xml incluído na seção de referências de saudação (atualizada com nomes, o local e o cenário de saudação fornecido de toomatch de endereços IP)</span><span class="sxs-lookup"><span data-stu-id="467be-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="467be-124">Atualização Olá variáveis no script de Olá Olá script toomatch Olá ambiente é toobe executar (assinaturas, nomes de serviço, etc.)</span><span class="sxs-lookup"><span data-stu-id="467be-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc.)</span></span>
3. <span data-ttu-id="467be-125">Execute o script hello no PowerShell</span><span class="sxs-lookup"><span data-stu-id="467be-125">Execute hello script in PowerShell</span></span>

>[!Note]
><span data-ttu-id="467be-126">região Olá representado em Olá script do PowerShell deve corresponder região Olá representada no arquivo de xml de configuração de rede hello.</span><span class="sxs-lookup"><span data-stu-id="467be-126">hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>
>
>

<span data-ttu-id="467be-127">Depois que o script hello é executado com êxito adicional etapas opcionais que podem ser tomadas, na seção de referências de saudação dois tooset de scripts, o servidor de web hello e servidor de aplicativos com um tooallow de aplicativo da web simples teste com essa configuração de rede de Perímetro.</span><span class="sxs-lookup"><span data-stu-id="467be-127">Once hello script runs successfully additional optional steps may be taken, in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="467be-128">Olá seções a seguir fornecem uma descrição detalhada dos grupos de segurança de rede e como eles funcionam para este exemplo, acompanhando a linhas de chave de script do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="467be-128">hello following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of hello PowerShell script.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="467be-129">Grupos de segurança de rede (NSG)</span><span class="sxs-lookup"><span data-stu-id="467be-129">Network Security Groups (NSG)</span></span>
<span data-ttu-id="467be-130">Neste exemplo, um grupo NSG é criado e então carregado com seis regras.</span><span class="sxs-lookup"><span data-stu-id="467be-130">For this example, an NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="467be-131">Em geral, você deve primeiro criar suas regras específicas de "Permitir" e Olá a regras mais genéricas de "Negar" última.</span><span class="sxs-lookup"><span data-stu-id="467be-131">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="467be-132">Olá prioridade determina quais regras são avaliadas primeiro.</span><span class="sxs-lookup"><span data-stu-id="467be-132">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="467be-133">Depois que o tráfego for encontrado uma regra específica de tooa tooapply, nenhuma regra adicional será avaliada.</span><span class="sxs-lookup"><span data-stu-id="467be-133">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="467be-134">Regras NSG podem ser aplicados em Olá direção de entrada ou saída (da perspectiva de saudação da sub-rede Olá).</span><span class="sxs-lookup"><span data-stu-id="467be-134">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="467be-135">Declarativamente, Olá regras a seguir está sendo compilado para o tráfego de entrada:</span><span class="sxs-lookup"><span data-stu-id="467be-135">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="467be-136">O tráfego interno de DNS (porta 53) é permitido</span><span class="sxs-lookup"><span data-stu-id="467be-136">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="467be-137">O tráfego de RDP (porta 3389) do hello Internet tooany VM é permitido</span><span class="sxs-lookup"><span data-stu-id="467be-137">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="467be-138">O tráfego HTTP (porta 80) Olá tooweb do servidor de Internet (IIS01) é permitido</span><span class="sxs-lookup"><span data-stu-id="467be-138">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="467be-139">Qualquer tráfego (todas as portas) do IIS01 tooAppVM1 é permitido</span><span class="sxs-lookup"><span data-stu-id="467be-139">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="467be-140">Qualquer tráfego (todas as portas) do hello Internet toohello VNet inteira (ambas as sub-redes) foi negado</span><span class="sxs-lookup"><span data-stu-id="467be-140">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="467be-141">Qualquer tráfego (todas as portas) da sub-rede de back-end do hello front-end subrede toohello foi negado</span><span class="sxs-lookup"><span data-stu-id="467be-141">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="467be-142">A sub-rede de tooeach associada essas regras, se uma solicitação HTTP foi entrada do servidor web do hello Internet toohello, ambos regras 3 (Permitir) e 5 (Negar) seria aplicado, mas como a regra 3 tem uma prioridade mais alta somente seria aplicada e regra 5 não seria entram em ação.</span><span class="sxs-lookup"><span data-stu-id="467be-142">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="467be-143">Assim você seria permitido a solicitação HTTP Olá toohello servidor de web.</span><span class="sxs-lookup"><span data-stu-id="467be-143">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="467be-144">Se o mesmo que o tráfego foi a tentativa de servidor de DNS01 tooreach hello, regra 5 (Negar) seria Olá primeiro tooapply e hello tráfego não será permitido toopass toohello server.</span><span class="sxs-lookup"><span data-stu-id="467be-144">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="467be-145">Regra 6 (Negar) bloqueia a sub-rede de front-end de saudação do falando toohello sub-rede de back-end (com exceção de tráfego permitido nas regras 1 e 4), esse conjunto de regras protege a rede de back-end Olá no caso de um invasor comprometer Olá aplicativo da web em Olá front-end, invasor Olá seria limitado toohello de acesso (somente tooresources exposto no servidor de AppVM01 Olá) de rede back-end "protegido".</span><span class="sxs-lookup"><span data-stu-id="467be-145">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="467be-146">Há uma regra de saída padrão que permite que o tráfego de saída toohello internet.</span><span class="sxs-lookup"><span data-stu-id="467be-146">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="467be-147">Neste exemplo, permitiremos o tráfego de saída e não modificaremos quaisquer regras de saída.</span><span class="sxs-lookup"><span data-stu-id="467be-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="467be-148">toolock tráfego em ambas as direções, roteamento de definido pelo usuário é necessário e explorado no "Exemplo 3" no hello [página segurança limite de melhores práticas][HOME].</span><span class="sxs-lookup"><span data-stu-id="467be-148">toolock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="467be-149">Cada regra é discutida mais detalhadamente como segue (**Observação**: qualquer item na Olá a seguir lista começando com um sinal de cifrão (por exemplo: $NSGName) é uma variável definida pelo usuário do script hello na seção de referência Olá deste documento):</span><span class="sxs-lookup"><span data-stu-id="467be-149">Each rule is discussed in more detail as follows (**Note**: any item in hello following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="467be-150">Primeiro um grupo de segurança de rede devem ser compilado regras de saudação toohold:</span><span class="sxs-lookup"><span data-stu-id="467be-150">First a Network Security Group must be built toohold hello rules:</span></span>

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. <span data-ttu-id="467be-151">a primeira regra Olá neste exemplo permite que o tráfego DNS entre todos os servidores DNS toohello redes internas na sub-rede de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="467be-151">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="467be-152">regra de saudação tem alguns parâmetros importantes:</span><span class="sxs-lookup"><span data-stu-id="467be-152">hello rule has some important parameters:</span></span>
   
   * <span data-ttu-id="467be-153">“Type” (Tipo) indica em qual direção do fluxo de tráfego esta regra entra em vigor.</span><span class="sxs-lookup"><span data-stu-id="467be-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="467be-154">direção de saudação é da perspectiva de saudação de sub-rede hello ou máquina Virtual (dependendo de onde essa NSG está associado).</span><span class="sxs-lookup"><span data-stu-id="467be-154">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="467be-155">Portanto, se o tipo é "Entrada" e tráfego está inserindo a sub-rede de saudação, Olá regra se aplica e tráfego deixando sub-rede Olá não é afetado por essa regra.</span><span class="sxs-lookup"><span data-stu-id="467be-155">Thus if Type is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
   * <span data-ttu-id="467be-156">"Priority" define a ordem de saudação no qual um fluxo de tráfego é avaliado.</span><span class="sxs-lookup"><span data-stu-id="467be-156">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="467be-157">Olá inferior Olá número Olá Olá prioridade.</span><span class="sxs-lookup"><span data-stu-id="467be-157">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="467be-158">Quando uma regra se aplica o fluxo de tráfego específico tooa, nenhuma regra adicional é processada.</span><span class="sxs-lookup"><span data-stu-id="467be-158">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="467be-159">Portanto, se uma regra com prioridade 1 permite o tráfego e uma regra com prioridade 2 nega o tráfego e ambas as regras se aplicam a tootraffic então Olá tráfego será permitido tooflow (desde que a regra 1 tinha uma prioridade mais alta que levou o efeito e nenhuma regra adicional foram aplicada).</span><span class="sxs-lookup"><span data-stu-id="467be-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
   * <span data-ttu-id="467be-160">"Action" significa se um tráfego afetado por essa regra é bloqueado ou permitido.</span><span class="sxs-lookup"><span data-stu-id="467be-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span></span>

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. <span data-ttu-id="467be-161">Essa regra permite tooflow de tráfego RDP de porta do RDP Olá internet toohello em qualquer servidor Olá associado a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="467be-161">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> <span data-ttu-id="467be-162">Essa regra usa dois tipos especiais de prefixos de endereço; “VIRTUAL_NETWORK” e “INTERNET”.</span><span class="sxs-lookup"><span data-stu-id="467be-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span></span> <span data-ttu-id="467be-163">Essas marcas são uma maneira fácil de tooaddress uma categoria de maior de prefixos de endereço.</span><span class="sxs-lookup"><span data-stu-id="467be-163">These tags are an easy way tooaddress a larger category of address prefixes.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. <span data-ttu-id="467be-164">Essa regra permite que o servidor de web do entrada da internet tráfego toohit hello.</span><span class="sxs-lookup"><span data-stu-id="467be-164">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="467be-165">Essa regra não altera o comportamento de roteamento hello.</span><span class="sxs-lookup"><span data-stu-id="467be-165">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="467be-166">regra de saudação permite apenas o tráfego destinado a IIS01 toopass.</span><span class="sxs-lookup"><span data-stu-id="467be-166">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="467be-167">Portanto, se o tráfego de Internet de saudação tivesse servidor de web hello como seu destino essa regra deve permitir que ele e parar o processamento mais regras.</span><span class="sxs-lookup"><span data-stu-id="467be-167">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="467be-168">(Regra Olá em prioridade 140 todos os outros tráfego da internet é bloqueado).</span><span class="sxs-lookup"><span data-stu-id="467be-168">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="467be-169">Se você só estiver processando o tráfego de HTTP, essa regra pode ser mais restrito tooonly permitir destino porta 80.</span><span class="sxs-lookup"><span data-stu-id="467be-169">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. <span data-ttu-id="467be-170">Essa regra permite toopass de tráfego do servidor de IIS01 Olá toohello AppVM01 server, uma regra posterior bloqueia todos os outros tráfegos de tooBackend de front-end.</span><span class="sxs-lookup"><span data-stu-id="467be-170">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="467be-171">tooimprove esta regra, se a porta de saudação é conhecida que deve ser adicionada.</span><span class="sxs-lookup"><span data-stu-id="467be-171">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="467be-172">Por exemplo, se servidor IIS hello está atingindo somente SQL Server no AppVM01, Olá intervalo de portas de destino deverá ser alterado de "*" (qualquer) too1433 (Olá porta do SQL), permitindo uma menor superfície de ataque de entrada em AppVM01 deve aplicativo da web hello comprometido.</span><span class="sxs-lookup"><span data-stu-id="467be-172">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. <span data-ttu-id="467be-173">Esta regra nega o tráfego de servidores na rede Olá tooany da internet hello.</span><span class="sxs-lookup"><span data-stu-id="467be-173">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="467be-174">Com as regras de saudação em prioridade 110 e 120, o efeito de saudação é tooallow somente internet tráfego toohello firewall de entrada e as portas do RDP em servidores e bloqueia todo o resto.</span><span class="sxs-lookup"><span data-stu-id="467be-174">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="467be-175">Essa regra é "à prova de falhas" regra tooblock todos os fluxos inesperados.</span><span class="sxs-lookup"><span data-stu-id="467be-175">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. <span data-ttu-id="467be-176">regra final Olá nega o tráfego de sub-rede de back-end do hello front-end subrede toohello.</span><span class="sxs-lookup"><span data-stu-id="467be-176">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="467be-177">Como essa regra é uma regra de entrada única, inversa de tráfego é permitida (de back-end de saudação toohello front-end).</span><span class="sxs-lookup"><span data-stu-id="467be-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="467be-178">Cenários de tráfego</span><span class="sxs-lookup"><span data-stu-id="467be-178">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="467be-179">(*Permitidos*) servidor tooweb da Internet</span><span class="sxs-lookup"><span data-stu-id="467be-179">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="467be-180">Um usuário da Internet solicita uma página HTTP de FrontEnd001.CloudApp.Net (Serviço de Nuvem Voltado para Internet)</span><span class="sxs-lookup"><span data-stu-id="467be-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="467be-181">Nuvem tráfego passa do serviço por meio de um ponto de extremidade aberto na porta 80 para IIS01 (servidor de web hello)</span><span class="sxs-lookup"><span data-stu-id="467be-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="467be-182">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="467be-182">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="467be-183">Não se aplica a regra 1 (DNS), NSG, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="467be-183">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="467be-184">2 de regra NSG (RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="467be-184">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="467be-185">Aplicar NSG regra 3 (Internet tooIIS01), o tráfego é o processamento de regras permitido, interrompa</span><span class="sxs-lookup"><span data-stu-id="467be-185">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="467be-186">Tráfego atinge o endereço IP interno do servidor de web hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="467be-186">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="467be-187">IIS01 está escutando o tráfego da web, recebe essa solicitação e inicia o processamento de solicitação de saudação</span><span class="sxs-lookup"><span data-stu-id="467be-187">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="467be-188">IIS01 solicita saudação do SQL Server em AppVM01 informações</span><span class="sxs-lookup"><span data-stu-id="467be-188">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="467be-189">Como não há regras de saída na sub-rede Frontend, o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="467be-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="467be-190">subrede back-end Olá começa o processamento de regras de entrada:</span><span class="sxs-lookup"><span data-stu-id="467be-190">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="467be-191">Não se aplica a regra 1 (DNS), NSG, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="467be-191">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="467be-192">2 de regra NSG (RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="467be-192">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="467be-193">NSG regra 3 (tooFirewall da Internet) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="467be-193">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="467be-194">4 de regra NSG (IIS01 tooAppVM01) se aplicam, o tráfego é o processamento de regras permitido, interrompa</span><span class="sxs-lookup"><span data-stu-id="467be-194">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="467be-195">AppVM01 recebe Olá consulta SQL e responde</span><span class="sxs-lookup"><span data-stu-id="467be-195">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="467be-196">Como não há nenhuma regra de saída na sub-rede de back-end hello, resposta Olá é permitida</span><span class="sxs-lookup"><span data-stu-id="467be-196">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="467be-197">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="467be-197">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="467be-198">Não há nenhuma regra NSG que aplica tooInbound tráfego da sub-rede de front-end do toohello de sub-rede de back-end Olá, para que nenhuma das regras do NSG Olá aplicar</span><span class="sxs-lookup"><span data-stu-id="467be-198">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="467be-199">regra do sistema padrão Olá permitindo o tráfego entre as sub-redes permitiria que esse tráfego para que o tráfego de saudação é permitido.</span><span class="sxs-lookup"><span data-stu-id="467be-199">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="467be-200">servidor do IIS Olá recebe a resposta SQL hello e conclui a resposta HTTP hello e envia toohello solicitante</span><span class="sxs-lookup"><span data-stu-id="467be-200">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
13. <span data-ttu-id="467be-201">Como não há nenhuma regra de saída na sub-rede de front-end Olá Olá resposta seja permitida, e hello internet usuário recebe Olá web página solicitada.</span><span class="sxs-lookup"><span data-stu-id="467be-201">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="467be-202">(*Permitidos*) toobackend RDP</span><span class="sxs-lookup"><span data-stu-id="467be-202">(*Allowed*) RDP toobackend</span></span>
1. <span data-ttu-id="467be-203">Administrador do servidor na internet solicitações tooAppVM01 de sessão RDP no BackEnd001.CloudApp.Net:xxxxx onde xxxxx é o número da porta Olá atribuído aleatoriamente para RDP tooAppVM01 (porta Olá atribuído pode ser encontrada em Olá portal do Azure ou por meio do PowerShell)</span><span class="sxs-lookup"><span data-stu-id="467be-203">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure portal or via PowerShell)</span></span>
2. <span data-ttu-id="467be-204">A sub-rede Backend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="467be-204">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="467be-205">Não se aplica a regra 1 (DNS), NSG, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="467be-205">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="467be-206">A regra NSG 2 (RDP) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="467be-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
3. <span data-ttu-id="467be-207">Sem regras de saída, as regras padrão serão aplicadas e o tráfego de retorno será permitido</span><span class="sxs-lookup"><span data-stu-id="467be-207">With no outbound rules, default rules apply and return traffic is allowed</span></span>
4. <span data-ttu-id="467be-208">A sessão RDP está habilitada</span><span class="sxs-lookup"><span data-stu-id="467be-208">RDP session is enabled</span></span>
5. <span data-ttu-id="467be-209">Prompts de AppVM01 Olá nome de usuário e senha</span><span class="sxs-lookup"><span data-stu-id="467be-209">AppVM01 prompts for hello user name and password</span></span>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="467be-210">(*Permitido*) Pesquisa de DNS do servidor Web no servidor DNS</span><span class="sxs-lookup"><span data-stu-id="467be-210">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="467be-211">Web necessidades de servidor, IIS01, um feed de dados em www.data.gov, mas precisa tooresolve Olá endereço.</span><span class="sxs-lookup"><span data-stu-id="467be-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="467be-212">Olá configuração de rede para listas de rede virtual Olá DNS01 (10.0.2.4 na sub-rede de back-end Olá) como o servidor DNS primário de hello, IIS01 envia Olá tooDNS01 de solicitação DNS</span><span class="sxs-lookup"><span data-stu-id="467be-212">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="467be-213">Não há regras de saída na sub-rede Frontend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="467be-213">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="467be-214">A sub-rede Backend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="467be-214">Backend subnet begins inbound rule processing:</span></span>
   * <span data-ttu-id="467be-215">A regra NSG 1 (DNS) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="467be-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="467be-216">Servidor DNS recebe a solicitação de saudação</span><span class="sxs-lookup"><span data-stu-id="467be-216">DNS server receives hello request</span></span>
6. <span data-ttu-id="467be-217">Servidor DNS não tem endereço Olá armazenado em cache e solicita que um servidor DNS raiz em Olá internet</span><span class="sxs-lookup"><span data-stu-id="467be-217">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="467be-218">Nenhuma regra de saída na sub-rede Backend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="467be-218">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="467be-219">Resposta de saudação responde do servidor DNS da Internet, desde que esta sessão foi iniciada internamente, é permitida</span><span class="sxs-lookup"><span data-stu-id="467be-219">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="467be-220">Servidor DNS armazena em cache a resposta hello e responde toohello solicitação inicial back tooIIS01</span><span class="sxs-lookup"><span data-stu-id="467be-220">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="467be-221">Nenhuma regra de saída na sub-rede Backend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="467be-221">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="467be-222">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="467be-222">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="467be-223">Não há nenhuma regra NSG que aplica tooInbound tráfego da sub-rede de front-end do toohello de sub-rede de back-end Olá, para que nenhuma das regras do NSG Olá aplicar</span><span class="sxs-lookup"><span data-stu-id="467be-223">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="467be-224">regra do sistema padrão Olá permitindo o tráfego entre as sub-redes permitiria que esse tráfego para que Olá tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="467be-224">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="467be-225">IIS01 recebe a resposta de saudação do DNS01</span><span class="sxs-lookup"><span data-stu-id="467be-225">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="467be-226">(*Permitido*) Arquivo de acesso do servidor Web em AppVM01</span><span class="sxs-lookup"><span data-stu-id="467be-226">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="467be-227">IIS01 solicita um arquivo em AppVM01</span><span class="sxs-lookup"><span data-stu-id="467be-227">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="467be-228">Não há regras de saída na sub-rede Frontend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="467be-228">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="467be-229">subrede back-end Olá começa o processamento de regras de entrada:</span><span class="sxs-lookup"><span data-stu-id="467be-229">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="467be-230">Não se aplica a regra 1 (DNS), NSG, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="467be-230">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="467be-231">2 de regra NSG (RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="467be-231">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="467be-232">NSG regra 3 (tooIIS01 da Internet) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="467be-232">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="467be-233">4 de regra NSG (IIS01 tooAppVM01) se aplicam, o tráfego é o processamento de regras permitido, interrompa</span><span class="sxs-lookup"><span data-stu-id="467be-233">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="467be-234">AppVM01 recebe a solicitação de saudação e responde com o arquivo (supondo que o acesso é autorizado)</span><span class="sxs-lookup"><span data-stu-id="467be-234">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="467be-235">Como não há nenhuma regra de saída na sub-rede de back-end hello, resposta Olá é permitida</span><span class="sxs-lookup"><span data-stu-id="467be-235">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="467be-236">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="467be-236">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="467be-237">Não há nenhuma regra NSG que aplica tooInbound tráfego da sub-rede de front-end do toohello de sub-rede de back-end Olá, para que nenhuma das regras do NSG Olá aplicar</span><span class="sxs-lookup"><span data-stu-id="467be-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="467be-238">regra do sistema padrão Olá permitindo o tráfego entre as sub-redes permitiria que esse tráfego para que o tráfego de saudação é permitido.</span><span class="sxs-lookup"><span data-stu-id="467be-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="467be-239">servidor do IIS Olá recebe arquivo hello</span><span class="sxs-lookup"><span data-stu-id="467be-239">hello IIS server receives hello file</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="467be-240">(*Negado*) servidor do Web toobackend</span><span class="sxs-lookup"><span data-stu-id="467be-240">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="467be-241">Um usuário de internet tenta tooaccess um arquivo em AppVM01 por meio de saudação BackEnd001.CloudApp.Net serviço</span><span class="sxs-lookup"><span data-stu-id="467be-241">An internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="467be-242">Como não há nenhum ponto de extremidade aberto para compartilhamento de arquivos, esse tráfego não passaria Olá serviço de nuvem e não alcançar o servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="467be-242">Since there are no endpoints open for file share, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="467be-243">Se o ponto de extremidade de saudação estava aberto por algum motivo, a regra NSG 5 (Internet tooVNet) bloqueia esse tráfego</span><span class="sxs-lookup"><span data-stu-id="467be-243">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="467be-244">(*Negado*) Pesquisa de DNS na Web no servidor DNS</span><span class="sxs-lookup"><span data-stu-id="467be-244">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="467be-245">Um usuário de internet tenta toolook um registro de DNS interno em DNS01 por meio de saudação BackEnd001.CloudApp.Net serviço</span><span class="sxs-lookup"><span data-stu-id="467be-245">An internet user tries toolook up an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="467be-246">Como não há nenhum ponto de extremidade aberto para DNS, esse tráfego não passaria Olá serviço de nuvem e não alcançar o servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="467be-246">Since there are no endpoints open for DNS, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="467be-247">Se o ponto de extremidade de saudação estava aberto por algum motivo, a regra NSG 5 (Internet tooVNet) bloqueia esse tráfego (Observação: essa regra 1 (DNS) não se aplicariam por dois motivos, primeiro endereço de origem de saudação é Olá da internet, esta regra só se aplica a toohello redes locais como saudação de origem, também Essa regra é uma regra de permissão, portanto ele nunca seria negar o tráfego)</span><span class="sxs-lookup"><span data-stu-id="467be-247">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this rule is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="467be-248">(*Negado*) Web tooSQL acesso através do firewall</span><span class="sxs-lookup"><span data-stu-id="467be-248">(*Denied*) Web tooSQL access through firewall</span></span>
1. <span data-ttu-id="467be-249">Um usuário da Internet solicita dados SQL de FrontEnd001.CloudApp.Net (Serviço de Nuvem Voltado para a Internet)</span><span class="sxs-lookup"><span data-stu-id="467be-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="467be-250">Como não há nenhum ponto de extremidade aberto para SQL, esse tráfego não passaria Olá serviço de nuvem e não alcançar o firewall Olá</span><span class="sxs-lookup"><span data-stu-id="467be-250">Since there are no endpoints open for SQL, this traffic would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="467be-251">Se o ponto de extremidade estava aberto por algum motivo, sub-rede front-end de saudação começa o processamento de regras de entrada:</span><span class="sxs-lookup"><span data-stu-id="467be-251">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="467be-252">Não se aplica a regra 1 (DNS), NSG, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="467be-252">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="467be-253">2 de regra NSG (RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="467be-253">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="467be-254">Aplicar NSG regra 3 (Internet tooIIS01), o tráfego é o processamento de regras permitido, interrompa</span><span class="sxs-lookup"><span data-stu-id="467be-254">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="467be-255">Tráfego atinge o endereço IP interno do hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="467be-255">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="467be-256">IIS01 não está escutando na porta 1433, assim nenhuma solicitação de toohello de resposta</span><span class="sxs-lookup"><span data-stu-id="467be-256">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="467be-257">Conclusão</span><span class="sxs-lookup"><span data-stu-id="467be-257">Conclusion</span></span>
<span data-ttu-id="467be-258">Este exemplo é uma maneira relativamente simple e direta de isolamento de sub-rede de back-end de saudação do tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="467be-258">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="467be-259">Mais exemplos e uma visão geral dos limites de segurança de rede podem ser encontrados [aqui][HOME].</span><span class="sxs-lookup"><span data-stu-id="467be-259">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="467be-260">Referências</span><span class="sxs-lookup"><span data-stu-id="467be-260">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="467be-261">Script principal e configuração de rede</span><span class="sxs-lookup"><span data-stu-id="467be-261">Main script and network config</span></span>
<span data-ttu-id="467be-262">Salve Olá Script completo em um arquivo de script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="467be-262">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="467be-263">Salvar Olá configuração de rede em um arquivo denominado "NetworkConf1.xml".</span><span class="sxs-lookup"><span data-stu-id="467be-263">Save hello Network Config into a file named “NetworkConf1.xml.”</span></span>
<span data-ttu-id="467be-264">Modificar Olá variáveis definidas pelo usuário como script hello necessários e execução.</span><span class="sxs-lookup"><span data-stu-id="467be-264">Modify hello user-defined variables as needed and run hello script.</span></span>

#### <a name="full-script"></a><span data-ttu-id="467be-265">Script completo</span><span class="sxs-lookup"><span data-stu-id="467be-265">Full script</span></span>
<span data-ttu-id="467be-266">Esse script será, com base em variáveis definidas pelo usuário Olá;</span><span class="sxs-lookup"><span data-stu-id="467be-266">This script will, based on hello user-defined variables;</span></span>

1. <span data-ttu-id="467be-267">Conecte-se tooan assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="467be-267">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="467be-268">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="467be-268">Create a storage account</span></span>
3. <span data-ttu-id="467be-269">Criar uma rede virtual e duas sub-redes, conforme definido no arquivo de configuração de rede de saudação</span><span class="sxs-lookup"><span data-stu-id="467be-269">Create a VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="467be-270">Crie quatro VMs do Windows Server</span><span class="sxs-lookup"><span data-stu-id="467be-270">Build four windows server VMs</span></span>
5. <span data-ttu-id="467be-271">Configure o NSG, incluindo:</span><span class="sxs-lookup"><span data-stu-id="467be-271">Configure NSG including:</span></span>
   * <span data-ttu-id="467be-272">Criando um NSG</span><span class="sxs-lookup"><span data-stu-id="467be-272">Creating an NSG</span></span>
   * <span data-ttu-id="467be-273">Preenchendo-o com regras</span><span class="sxs-lookup"><span data-stu-id="467be-273">Populating it with rules</span></span>
   * <span data-ttu-id="467be-274">Associação de sub-redes apropriados da saudação NSG toohello</span><span class="sxs-lookup"><span data-stu-id="467be-274">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="467be-275">Este script do PowerShell deve ser executado localmente em um computador ou servidor conectado à Internet.</span><span class="sxs-lookup"><span data-stu-id="467be-275">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="467be-276">Quando esse script for executado, poderá haver avisos ou outras mensagens informativas que aparecerão no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="467be-276">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="467be-277">Somente as mensagens de erro em vermelho são motivo de preocupação.</span><span class="sxs-lookup"><span data-stu-id="467be-277">Only error messages in red are cause for concern.</span></span>
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
   - One server on hello FrontEnd Subnet
   - Three Servers on hello BackEnd Subnet
   - Network Security Groups tooallow/deny traffic patterns as declared

  Before running script, ensure hello network configuration file is created in
  hello directory referenced by $NetworkConfigFile variable (or update the
  variable tooreflect hello path and file name of hello config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  hello appropriate layer(s) of protection. This script serves as an example of some
  of hello techniques that can be used, but should not be used for all scenarios. You
  are responsible tooassess your security needs and hello appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

  BackEnd Service (BackEnd subnet 10.0.2.0/24)
   DNS01      - 10.0.2.4
   AppVM01    - 10.0.2.5
   AppVM02    - 10.0.2.6

#>

# Fixed Variables
    $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
    $VMName = @()
    $ServiceName = @()
    $VMFamily = @()
    $img = @()
    $size = @()
    $SubnetName = @()
    $VMIP = @()

# User-Defined Global Variables
  # These should be changes tooreflect your subscription and services
  # Invalid options will fail in hello validation section

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
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
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

  # Update Subscription Pointer tooNew Storage Account
    Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
    Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

# Validation
$FatalError = $false

If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
     Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
     $FatalError = $true}

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

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
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign hello NSG toohello Subnets
        Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a><span data-ttu-id="467be-278">Arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="467be-278">Network config file</span></span>
<span data-ttu-id="467be-279">Salve esse arquivo xml com o local atualizado e adicionar variável de toohello $NetworkConfigFile Olá link toothis arquivo hello precede o script.</span><span class="sxs-lookup"><span data-stu-id="467be-279">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello preceding script.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="467be-280">Scripts de aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="467be-280">Sample application scripts</span></span>
<span data-ttu-id="467be-281">Se você quiser tooinstall um aplicativo de exemplo para este e outros exemplos de rede de Perímetro, foi fornecido no hello link a seguir: [Script de exemplo de aplicativo][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="467be-281">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="467be-282">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="467be-282">Next steps</span></span>
* <span data-ttu-id="467be-283">Atualizar e salvar o arquivo XML</span><span class="sxs-lookup"><span data-stu-id="467be-283">Update and save XML file</span></span>
* <span data-ttu-id="467be-284">Executar o ambiente de saudação do hello PowerShell script toobuild</span><span class="sxs-lookup"><span data-stu-id="467be-284">Run hello PowerShell script toobuild hello environment</span></span>
* <span data-ttu-id="467be-285">Instalar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="467be-285">Install hello sample application</span></span>
* <span data-ttu-id="467be-286">Testar diferentes fluxos de tráfego por meio dessa DMZ</span><span class="sxs-lookup"><span data-stu-id="467be-286">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "DMZ de entrada com NSG"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

