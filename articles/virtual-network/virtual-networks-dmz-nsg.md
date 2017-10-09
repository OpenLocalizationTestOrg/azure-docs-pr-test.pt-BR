---
title: "aaaAzure exemplo DMZ – criar uma rede de Perímetro simples com NSGs | Microsoft Docs"
description: "Criar uma DMZ com grupos de segurança de rede (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="40689-103">Exemplo 1 – Criar uma DMZ simples usando NSGs com um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="40689-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="40689-104">[Retornar toohello página segurança limite de melhores práticas][HOME]</span><span class="sxs-lookup"><span data-stu-id="40689-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="40689-105">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="40689-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="40689-106">Clássico - PowerShell</span><span class="sxs-lookup"><span data-stu-id="40689-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="40689-107">Este exemplo criará uma DMZ simples com quatro servidores Windows e Grupos de Segurança de Rede.</span><span class="sxs-lookup"><span data-stu-id="40689-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="40689-108">Este exemplo descreve cada Olá modelo relevante seções tooprovide uma compreensão mais profunda de cada etapa.</span><span class="sxs-lookup"><span data-stu-id="40689-108">This example describes each of hello relevant template sections tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="40689-109">Há também um tooprovide da seção de cenário de tráfego uma Visão aprofundada passo a passo de como o tráfego passa camadas Olá de defesa Olá DMZ.</span><span class="sxs-lookup"><span data-stu-id="40689-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step look at how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="40689-110">Por fim, na seção de referências de saudação é Olá toobuild de código e instruções do modelo completo neste ambiente tootest e experiência com vários cenários.</span><span class="sxs-lookup"><span data-stu-id="40689-110">Finally, in hello references section is hello complete template code and instructions toobuild this environment tootest and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="40689-111">![DMZ de entrada com NSG][1]</span><span class="sxs-lookup"><span data-stu-id="40689-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="40689-112">Descrição do ambiente</span><span class="sxs-lookup"><span data-stu-id="40689-112">Environment description</span></span>
<span data-ttu-id="40689-113">Neste exemplo, uma assinatura contém Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="40689-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="40689-114">Um único grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="40689-114">A single resource group</span></span>
* <span data-ttu-id="40689-115">Uma rede virtual com duas sub-redes: “FrontEnd” e “BackEnd”</span><span class="sxs-lookup"><span data-stu-id="40689-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="40689-116">Um grupo de segurança de rede que é aplicada tooboth sub-redes</span><span class="sxs-lookup"><span data-stu-id="40689-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="40689-117">Um Windows Server que representa um servidor Web de aplicativos ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="40689-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="40689-118">Dois servidores Windows que representam servidores de back-end de aplicativos (“AppVM01”, “AppVM02”)</span><span class="sxs-lookup"><span data-stu-id="40689-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="40689-119">Um servidor Windows que representa um servidor DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="40689-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="40689-120">Um endereço IP público associado Olá aplicativo servidor web</span><span class="sxs-lookup"><span data-stu-id="40689-120">A public IP address associated with hello application web server</span></span>

<span data-ttu-id="40689-121">Na seção de referências de hello, há um modelo do Azure Resource Manager tooan de link que cria um ambiente de saudação descrito neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="40689-121">In hello references section, there is a link tooan Azure Resource Manager template that builds hello environment described in this example.</span></span> <span data-ttu-id="40689-122">Criando Olá VMs e redes virtuais, embora feito pelo modelo de exemplo hello, não são descritas em detalhes neste documento.</span><span class="sxs-lookup"><span data-stu-id="40689-122">Building hello VMs and Virtual Networks, although done by hello example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="40689-123">**toobuild esse ambiente** (são instruções detalhadas na seção de referências de saudação deste documento);</span><span class="sxs-lookup"><span data-stu-id="40689-123">**toobuild this environment** (detailed instructions are in hello references section of this document);</span></span>

1. <span data-ttu-id="40689-124">Implantar Olá modelo do Gerenciador de recursos do Azure em: [modelos de início rápido do Azure][Template]</span><span class="sxs-lookup"><span data-stu-id="40689-124">Deploy hello Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="40689-125">Instalar o aplicativo de exemplo hello em: [Script de exemplo de aplicativo][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="40689-125">Install hello sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
><span data-ttu-id="40689-126">servidores de back-end tooany tooRDP nesta instância, o servidor do IIS Olá é usado como uma "salto caixa".</span><span class="sxs-lookup"><span data-stu-id="40689-126">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="40689-127">Primeiro servidor IIS toohello RDP e, em seguida, do servidor de saudação RDP do servidor IIS toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="40689-127">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span> <span data-ttu-id="40689-128">Como alternativa, um IP público pode ser associado a cada servidor de NIC para realizar RDP mais facilmente.</span><span class="sxs-lookup"><span data-stu-id="40689-128">Alternately a Public IP can be associated with each server NIC for easier RDP.</span></span>
> 
>

<span data-ttu-id="40689-129">Olá seções a seguir fornecem uma descrição detalhada do hello grupo de segurança de rede e como ele funciona para este exemplo, acompanhando a linhas de chave de saudação modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="40689-129">hello following sections provide a detailed description of hello Network Security Group and how it functions for this example by walking through key lines of hello Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="40689-130">Grupos de segurança de rede (NSG)</span><span class="sxs-lookup"><span data-stu-id="40689-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="40689-131">Neste exemplo, um grupo NSG é criado e então carregado com seis regras.</span><span class="sxs-lookup"><span data-stu-id="40689-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
><span data-ttu-id="40689-132">Em geral, você deve primeiro criar suas regras específicas de "Permitir" e Olá a regras mais genéricas de "Negar" última.</span><span class="sxs-lookup"><span data-stu-id="40689-132">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="40689-133">Olá prioridade determina quais regras são avaliadas primeiro.</span><span class="sxs-lookup"><span data-stu-id="40689-133">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="40689-134">Depois que o tráfego for encontrado uma regra específica de tooa tooapply, nenhuma regra adicional será avaliada.</span><span class="sxs-lookup"><span data-stu-id="40689-134">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="40689-135">Regras NSG podem ser aplicados em Olá direção de entrada ou saída (da perspectiva de saudação da sub-rede Olá).</span><span class="sxs-lookup"><span data-stu-id="40689-135">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
>
>

<span data-ttu-id="40689-136">Declarativamente, Olá regras a seguir está sendo compilado para o tráfego de entrada:</span><span class="sxs-lookup"><span data-stu-id="40689-136">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="40689-137">O tráfego interno de DNS (porta 53) é permitido</span><span class="sxs-lookup"><span data-stu-id="40689-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="40689-138">O tráfego de RDP (porta 3389) do hello Internet tooany VM é permitido</span><span class="sxs-lookup"><span data-stu-id="40689-138">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="40689-139">O tráfego HTTP (porta 80) Olá tooweb do servidor de Internet (IIS01) é permitido</span><span class="sxs-lookup"><span data-stu-id="40689-139">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="40689-140">Qualquer tráfego (todas as portas) do IIS01 tooAppVM1 é permitido</span><span class="sxs-lookup"><span data-stu-id="40689-140">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="40689-141">Qualquer tráfego (todas as portas) do hello Internet toohello VNet inteira (ambas as sub-redes) foi negado</span><span class="sxs-lookup"><span data-stu-id="40689-141">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="40689-142">Qualquer tráfego (todas as portas) da sub-rede de back-end do hello front-end subrede toohello foi negado</span><span class="sxs-lookup"><span data-stu-id="40689-142">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="40689-143">A sub-rede de tooeach associada essas regras, se uma solicitação HTTP foi entrada do servidor web do hello Internet toohello, ambos regras 3 (Permitir) e 5 (Negar) seria aplicado, mas como a regra 3 tem uma prioridade mais alta somente seria aplicada e regra 5 não seria entram em ação.</span><span class="sxs-lookup"><span data-stu-id="40689-143">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="40689-144">Assim você seria permitido a solicitação HTTP Olá toohello servidor de web.</span><span class="sxs-lookup"><span data-stu-id="40689-144">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="40689-145">Se o mesmo que o tráfego foi a tentativa de servidor de DNS01 tooreach hello, regra 5 (Negar) seria Olá primeiro tooapply e hello tráfego não será permitido toopass toohello server.</span><span class="sxs-lookup"><span data-stu-id="40689-145">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="40689-146">Regra 6 (Negar) bloqueia a sub-rede de front-end de saudação do falando toohello sub-rede de back-end (com exceção de tráfego permitido nas regras 1 e 4), esse conjunto de regras protege a rede de back-end Olá no caso de um invasor comprometer Olá aplicativo da web em Olá front-end, invasor Olá seria limitado toohello de acesso (somente tooresources exposto no servidor de AppVM01 Olá) de rede back-end "protegido".</span><span class="sxs-lookup"><span data-stu-id="40689-146">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="40689-147">Há uma regra de saída padrão que permite que o tráfego de saída toohello internet.</span><span class="sxs-lookup"><span data-stu-id="40689-147">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="40689-148">Neste exemplo, permitiremos o tráfego de saída e não modificaremos quaisquer regras de saída.</span><span class="sxs-lookup"><span data-stu-id="40689-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="40689-149">tootraffic de política de segurança de tooapply em ambas as direções, roteamento de definido pelo usuário é necessário e explorado no "Exemplo 3" no hello [página segurança limite de melhores práticas][HOME].</span><span class="sxs-lookup"><span data-stu-id="40689-149">tooapply security policy tootraffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="40689-150">Cada regra é discutida com mais detalhes a seguir:</span><span class="sxs-lookup"><span data-stu-id="40689-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="40689-151">Um recurso de grupo de segurança de rede deve ser instanciadas toohold Olá regras:</span><span class="sxs-lookup"><span data-stu-id="40689-151">A Network Security Group resource must be instantiated toohold hello rules:</span></span>

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. <span data-ttu-id="40689-152">a primeira regra Olá neste exemplo permite que o tráfego DNS entre todos os servidores DNS toohello redes internas na sub-rede de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="40689-152">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="40689-153">regra de saudação tem alguns parâmetros importantes:</span><span class="sxs-lookup"><span data-stu-id="40689-153">hello rule has some important parameters:</span></span>
  * <span data-ttu-id="40689-154">"destinationAddressPrefix" - regras podem usar um tipo especial de prefixo de endereço chamado uma "marca padrão", essas marcas são identificadores fornecidos pelo sistema que permitem uma maneira fácil de tooaddress uma categoria de maior de prefixos de endereço.</span><span class="sxs-lookup"><span data-stu-id="40689-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way tooaddress a larger category of address prefixes.</span></span> <span data-ttu-id="40689-155">Esta regra usa Olá marca padrão "Internet" toosignify os endereços fora Olá VNet.</span><span class="sxs-lookup"><span data-stu-id="40689-155">This rule uses hello Default Tag “Internet” toosignify any address outside of hello VNet.</span></span> <span data-ttu-id="40689-156">VirtualNetwork e AzureLoadBalancer são outros exemplos de rótulos de prefixo.</span><span class="sxs-lookup"><span data-stu-id="40689-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="40689-157">“Direction” (Direção) indica em qual direção do fluxo de tráfego esta regra entra em vigor.</span><span class="sxs-lookup"><span data-stu-id="40689-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="40689-158">direção de saudação é da perspectiva de saudação de sub-rede hello ou máquina Virtual (dependendo de onde essa NSG está associado).</span><span class="sxs-lookup"><span data-stu-id="40689-158">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="40689-159">Portanto, se direção "Entrada" e o tráfego é entra sub-rede hello, Olá regra se aplica e tráfego deixando sub-rede Olá não é afetado por essa regra.</span><span class="sxs-lookup"><span data-stu-id="40689-159">Thus if Direction is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="40689-160">"Priority" define a ordem de saudação no qual um fluxo de tráfego é avaliado.</span><span class="sxs-lookup"><span data-stu-id="40689-160">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="40689-161">Olá inferior Olá número Olá Olá prioridade.</span><span class="sxs-lookup"><span data-stu-id="40689-161">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="40689-162">Quando uma regra se aplica o fluxo de tráfego específico tooa, nenhuma regra adicional é processada.</span><span class="sxs-lookup"><span data-stu-id="40689-162">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="40689-163">Portanto, se uma regra com prioridade 1 permite o tráfego e uma regra com prioridade 2 nega o tráfego e ambas as regras se aplicam a tootraffic então Olá tráfego será permitido tooflow (desde que a regra 1 tinha uma prioridade mais alta que levou o efeito e nenhuma regra adicional foram aplicada).</span><span class="sxs-lookup"><span data-stu-id="40689-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="40689-164">“Action” (Ação) indica se um tráfego afetado por essa regra é bloqueado (“Deny”, Negar) ou permitido (“Allow”, Permitir).</span><span class="sxs-lookup"><span data-stu-id="40689-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. <span data-ttu-id="40689-165">Essa regra permite tooflow de tráfego RDP de porta do RDP Olá internet toohello em qualquer servidor Olá associado a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="40689-165">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. <span data-ttu-id="40689-166">Essa regra permite que o servidor de web do entrada da internet tráfego toohit hello.</span><span class="sxs-lookup"><span data-stu-id="40689-166">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="40689-167">Essa regra não altera o comportamento de roteamento hello.</span><span class="sxs-lookup"><span data-stu-id="40689-167">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="40689-168">regra de saudação permite apenas o tráfego destinado a IIS01 toopass.</span><span class="sxs-lookup"><span data-stu-id="40689-168">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="40689-169">Portanto, se o tráfego de Internet de saudação tivesse servidor de web hello como seu destino essa regra deve permitir que ele e parar o processamento mais regras.</span><span class="sxs-lookup"><span data-stu-id="40689-169">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="40689-170">(Regra Olá em prioridade 140 todos os outros tráfego da internet é bloqueado).</span><span class="sxs-lookup"><span data-stu-id="40689-170">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="40689-171">Se você só estiver processando o tráfego de HTTP, essa regra pode ser mais restrito tooonly permitir destino porta 80.</span><span class="sxs-lookup"><span data-stu-id="40689-171">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. <span data-ttu-id="40689-172">Essa regra permite toopass de tráfego do servidor de IIS01 Olá toohello AppVM01 server, uma regra posterior bloqueia todos os outros tráfegos de tooBackend de front-end.</span><span class="sxs-lookup"><span data-stu-id="40689-172">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="40689-173">tooimprove esta regra, se a porta de saudação é conhecida que deve ser adicionada.</span><span class="sxs-lookup"><span data-stu-id="40689-173">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="40689-174">Por exemplo, se servidor IIS hello está atingindo somente SQL Server no AppVM01, Olá intervalo de portas de destino deverá ser alterado de "*" (qualquer) too1433 (Olá porta do SQL), permitindo uma menor superfície de ataque de entrada em AppVM01 deve aplicativo da web hello comprometido.</span><span class="sxs-lookup"><span data-stu-id="40689-174">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. <span data-ttu-id="40689-175">Esta regra nega o tráfego de servidores na rede Olá tooany da internet hello.</span><span class="sxs-lookup"><span data-stu-id="40689-175">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="40689-176">Com as regras de saudação em prioridade 110 e 120, o efeito de saudação é tooallow somente internet tráfego toohello firewall de entrada e as portas do RDP em servidores e bloqueia todo o resto.</span><span class="sxs-lookup"><span data-stu-id="40689-176">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="40689-177">Essa regra é "à prova de falhas" regra tooblock todos os fluxos inesperados.</span><span class="sxs-lookup"><span data-stu-id="40689-177">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. <span data-ttu-id="40689-178">regra final Olá nega o tráfego de sub-rede de back-end do hello front-end subrede toohello.</span><span class="sxs-lookup"><span data-stu-id="40689-178">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="40689-179">Como essa regra é uma regra de entrada única, inversa de tráfego é permitida (de back-end de saudação toohello front-end).</span><span class="sxs-lookup"><span data-stu-id="40689-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="40689-180">Cenários de tráfego</span><span class="sxs-lookup"><span data-stu-id="40689-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="40689-181">(*Permitidos*) servidor tooweb da Internet</span><span class="sxs-lookup"><span data-stu-id="40689-181">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="40689-182">Um usuário de internet solicita uma página HTTP do endereço IP público de saudação do hello que NIC associada Olá IIS01 NIC</span><span class="sxs-lookup"><span data-stu-id="40689-182">An internet user requests an HTTP page from hello public IP address of hello NIC associated with hello IIS01 NIC</span></span>
2. <span data-ttu-id="40689-183">Olá endereço IP público passa tráfego toohello VNet para IIS01 (servidor de web hello)</span><span class="sxs-lookup"><span data-stu-id="40689-183">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="40689-184">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="40689-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="40689-185">Não se aplica a regra 1 (DNS), NSG, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="40689-185">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="40689-186">2 de regra NSG (RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="40689-186">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="40689-187">Aplicar NSG regra 3 (Internet tooIIS01), o tráfego é o processamento de regras permitido, interrompa</span><span class="sxs-lookup"><span data-stu-id="40689-187">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="40689-188">Tráfego atinge o endereço IP interno do servidor de web hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="40689-188">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="40689-189">IIS01 está escutando o tráfego da web, recebe essa solicitação e inicia o processamento de solicitação de saudação</span><span class="sxs-lookup"><span data-stu-id="40689-189">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="40689-190">IIS01 solicita saudação do SQL Server em AppVM01 informações</span><span class="sxs-lookup"><span data-stu-id="40689-190">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="40689-191">Não há regras de saída na sub-rede Frontend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="40689-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="40689-192">subrede back-end Olá começa o processamento de regras de entrada:</span><span class="sxs-lookup"><span data-stu-id="40689-192">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="40689-193">Não se aplica a regra 1 (DNS), NSG, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="40689-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="40689-194">2 de regra NSG (RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="40689-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="40689-195">NSG regra 3 (tooFirewall da Internet) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="40689-195">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="40689-196">4 de regra NSG (IIS01 tooAppVM01) se aplicam, o tráfego é o processamento de regras permitido, interrompa</span><span class="sxs-lookup"><span data-stu-id="40689-196">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="40689-197">AppVM01 recebe Olá consulta SQL e responde</span><span class="sxs-lookup"><span data-stu-id="40689-197">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="40689-198">Como não há nenhuma regra de saída na sub-rede de back-end hello, resposta Olá é permitida</span><span class="sxs-lookup"><span data-stu-id="40689-198">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="40689-199">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="40689-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="40689-200">Não há nenhuma regra NSG que aplica tooInbound tráfego da sub-rede de front-end do toohello de sub-rede de back-end Olá, para que nenhuma das regras do NSG Olá aplicar</span><span class="sxs-lookup"><span data-stu-id="40689-200">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="40689-201">regra do sistema padrão Olá permitindo o tráfego entre as sub-redes permitiria que esse tráfego para que o tráfego de saudação é permitido.</span><span class="sxs-lookup"><span data-stu-id="40689-201">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="40689-202">servidor do IIS Olá recebe a resposta SQL hello e conclui a resposta HTTP hello e envia toohello solicitante</span><span class="sxs-lookup"><span data-stu-id="40689-202">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requester</span></span>
13. <span data-ttu-id="40689-203">Como não há nenhuma regra de saída na sub-rede de front-end hello, Olá resposta seja permitida e Olá Internet usuário recebe Olá web página solicitada.</span><span class="sxs-lookup"><span data-stu-id="40689-203">Since there are no outbound rules on hello Frontend subnet, hello response is allowed and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-tooiis-server"></a><span data-ttu-id="40689-204">(*Permitidos*) servidor tooIIS RDP</span><span class="sxs-lookup"><span data-stu-id="40689-204">(*Allowed*) RDP tooIIS server</span></span>
1. <span data-ttu-id="40689-205">Um administrador do servidor na internet solicita um tooIIS01 de sessão RDP no endereço IP público de saudação do hello que NIC associada Olá IIS01 NIC (esse endereço IP público pode ser encontrado por meio de saudação Portal ou o PowerShell)</span><span class="sxs-lookup"><span data-stu-id="40689-205">A Server Admin on internet requests an RDP session tooIIS01 on hello public IP address of hello NIC associated with hello IIS01 NIC (this public IP address can be found via hello Portal or PowerShell)</span></span>
2. <span data-ttu-id="40689-206">Olá endereço IP público passa tráfego toohello VNet para IIS01 (servidor de web hello)</span><span class="sxs-lookup"><span data-stu-id="40689-206">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="40689-207">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="40689-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="40689-208">Não se aplica a regra 1 (DNS), NSG, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="40689-208">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="40689-209">A regra NSG 2 (RDP) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="40689-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="40689-210">Sem regras de saída, as regras padrão serão aplicadas e o tráfego de retorno será permitido</span><span class="sxs-lookup"><span data-stu-id="40689-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="40689-211">A sessão RDP está habilitada</span><span class="sxs-lookup"><span data-stu-id="40689-211">RDP session is enabled</span></span>
6. <span data-ttu-id="40689-212">Prompts de IIS01 Olá nome de usuário e senha</span><span class="sxs-lookup"><span data-stu-id="40689-212">IIS01 prompts for hello user name and password</span></span>

>[!NOTE]
><span data-ttu-id="40689-213">servidores de back-end tooany tooRDP nesta instância, o servidor do IIS Olá é usado como uma "salto caixa".</span><span class="sxs-lookup"><span data-stu-id="40689-213">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="40689-214">Primeiro servidor IIS toohello RDP e, em seguida, do servidor de saudação RDP do servidor IIS toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="40689-214">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="40689-215">(*Permitido*) Pesquisa de DNS do servidor Web no servidor DNS</span><span class="sxs-lookup"><span data-stu-id="40689-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="40689-216">Web necessidades de servidor, IIS01, um feed de dados em www.data.gov, mas precisa tooresolve Olá endereço.</span><span class="sxs-lookup"><span data-stu-id="40689-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="40689-217">Olá configuração de rede para listas de rede virtual Olá DNS01 (10.0.2.4 na sub-rede de back-end Olá) como o servidor DNS primário de hello, IIS01 envia Olá tooDNS01 de solicitação DNS</span><span class="sxs-lookup"><span data-stu-id="40689-217">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="40689-218">Não há regras de saída na sub-rede Frontend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="40689-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="40689-219">A sub-rede Backend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="40689-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="40689-220">A regra NSG 1 (DNS) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="40689-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="40689-221">Servidor DNS recebe a solicitação de saudação</span><span class="sxs-lookup"><span data-stu-id="40689-221">DNS server receives hello request</span></span>
6. <span data-ttu-id="40689-222">Servidor DNS não tem endereço Olá armazenado em cache e solicita que um servidor DNS raiz em Olá internet</span><span class="sxs-lookup"><span data-stu-id="40689-222">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="40689-223">Nenhuma regra de saída na sub-rede Backend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="40689-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="40689-224">Resposta de saudação responde do servidor DNS da Internet, desde que esta sessão foi iniciada internamente, é permitida</span><span class="sxs-lookup"><span data-stu-id="40689-224">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="40689-225">Servidor DNS armazena em cache a resposta hello e responde toohello solicitação inicial back tooIIS01</span><span class="sxs-lookup"><span data-stu-id="40689-225">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="40689-226">Nenhuma regra de saída na sub-rede Backend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="40689-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="40689-227">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="40689-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="40689-228">Não há nenhuma regra NSG que aplica tooInbound tráfego da sub-rede de front-end do toohello de sub-rede de back-end Olá, para que nenhuma das regras do NSG Olá aplicar</span><span class="sxs-lookup"><span data-stu-id="40689-228">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="40689-229">regra do sistema padrão Olá permitindo o tráfego entre as sub-redes permitiria que esse tráfego para que Olá tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="40689-229">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="40689-230">IIS01 recebe a resposta de saudação do DNS01</span><span class="sxs-lookup"><span data-stu-id="40689-230">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="40689-231">(*Permitido*) Arquivo de acesso do servidor Web em AppVM01</span><span class="sxs-lookup"><span data-stu-id="40689-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="40689-232">IIS01 solicita um arquivo em AppVM01</span><span class="sxs-lookup"><span data-stu-id="40689-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="40689-233">Não há regras de saída na sub-rede Frontend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="40689-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="40689-234">subrede back-end Olá começa o processamento de regras de entrada:</span><span class="sxs-lookup"><span data-stu-id="40689-234">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="40689-235">Não se aplica a regra 1 (DNS), NSG, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="40689-235">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="40689-236">2 de regra NSG (RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="40689-236">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="40689-237">NSG regra 3 (tooIIS01 da Internet) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="40689-237">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="40689-238">4 de regra NSG (IIS01 tooAppVM01) se aplicam, o tráfego é o processamento de regras permitido, interrompa</span><span class="sxs-lookup"><span data-stu-id="40689-238">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="40689-239">AppVM01 recebe a solicitação de saudação e responde com o arquivo (supondo que o acesso é autorizado)</span><span class="sxs-lookup"><span data-stu-id="40689-239">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="40689-240">Como não há nenhuma regra de saída na sub-rede de back-end hello, resposta Olá é permitida</span><span class="sxs-lookup"><span data-stu-id="40689-240">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="40689-241">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="40689-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="40689-242">Não há nenhuma regra NSG que aplica tooInbound tráfego da sub-rede de front-end do toohello de sub-rede de back-end Olá, para que nenhuma das regras do NSG Olá aplicar</span><span class="sxs-lookup"><span data-stu-id="40689-242">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="40689-243">regra do sistema padrão Olá permitindo o tráfego entre as sub-redes permitiria que esse tráfego para que o tráfego de saudação é permitido.</span><span class="sxs-lookup"><span data-stu-id="40689-243">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="40689-244">servidor do IIS Olá recebe arquivo hello</span><span class="sxs-lookup"><span data-stu-id="40689-244">hello IIS server receives hello file</span></span>

#### <a name="denied-rdp-toobackend"></a><span data-ttu-id="40689-245">(*Negado*) toobackend RDP</span><span class="sxs-lookup"><span data-stu-id="40689-245">(*Denied*) RDP toobackend</span></span>
1. <span data-ttu-id="40689-246">Um usuário de internet tenta tooRDP tooserver AppVM01</span><span class="sxs-lookup"><span data-stu-id="40689-246">An internet user tries tooRDP tooserver AppVM01</span></span>
2. <span data-ttu-id="40689-247">Como não há nenhum endereço IP público associado a esta NIC de servidores, esse tráfego nunca insira Olá rede virtual e não alcançar o servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="40689-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="40689-248">Contudo, se um endereço IP público tiver sido habilitado por algum motivo, a regra NSG 2 (RDP) permitiria esse tráfego</span><span class="sxs-lookup"><span data-stu-id="40689-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
><span data-ttu-id="40689-249">servidores de back-end tooany tooRDP nesta instância, o servidor do IIS Olá é usado como uma "salto caixa".</span><span class="sxs-lookup"><span data-stu-id="40689-249">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="40689-250">Primeiro servidor IIS toohello RDP e, em seguida, do servidor de saudação RDP do servidor IIS toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="40689-250">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="40689-251">(*Negado*) servidor do Web toobackend</span><span class="sxs-lookup"><span data-stu-id="40689-251">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="40689-252">Um usuário de internet tenta tooaccess um arquivo em AppVM01</span><span class="sxs-lookup"><span data-stu-id="40689-252">An internet user tries tooaccess a file on AppVM01</span></span>
2. <span data-ttu-id="40689-253">Como não há nenhum endereço IP público associado a esta NIC de servidores, esse tráfego nunca insira Olá rede virtual e não alcançar o servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="40689-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="40689-254">Se um endereço IP público foi ativado por algum motivo, a regra NSG 5 (Internet tooVNet) bloqueia esse tráfego</span><span class="sxs-lookup"><span data-stu-id="40689-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="40689-255">(*Negado*) Pesquisa de DNS na Web no servidor DNS</span><span class="sxs-lookup"><span data-stu-id="40689-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="40689-256">Um usuário de internet tenta toolook um registro de DNS interno em DNS01</span><span class="sxs-lookup"><span data-stu-id="40689-256">An internet user tries toolook up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="40689-257">Como não há nenhum endereço IP público associado a esta NIC de servidores, esse tráfego nunca insira Olá rede virtual e não alcançar o servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="40689-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="40689-258">Se um endereço IP público foi ativado por algum motivo, a regra NSG 5 (Internet tooVNet) bloqueia esse tráfego (Observação: regra 1 (DNS) não é aplicável porque Olá solicita o endereço de origem é Olá internet e regra 1 só se aplica a toohello rede local virtual como fonte de saudação)</span><span class="sxs-lookup"><span data-stu-id="40689-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because hello requests source address is hello internet and Rule 1 only applies toohello local VNet as hello source)</span></span>

#### <a name="denied-sql-access-on-hello-web-server"></a><span data-ttu-id="40689-259">(*Negado*) acesso ao SQL no servidor de web Olá</span><span class="sxs-lookup"><span data-stu-id="40689-259">(*Denied*) SQL access on hello web server</span></span>
1. <span data-ttu-id="40689-260">Um usuário da Internet solicita dados SQL do IIS01</span><span class="sxs-lookup"><span data-stu-id="40689-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="40689-261">Como não há nenhum endereço IP público associado a esta NIC de servidores, esse tráfego nunca insira Olá rede virtual e não alcançar o servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="40689-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="40689-262">Se um endereço IP público foi ativado por algum motivo, sub-rede front-end de saudação começa o processamento de regras de entrada:</span><span class="sxs-lookup"><span data-stu-id="40689-262">If a Public IP address was enabled for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="40689-263">Não se aplica a regra 1 (DNS), NSG, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="40689-263">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="40689-264">2 de regra NSG (RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="40689-264">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="40689-265">Aplicar NSG regra 3 (Internet tooIIS01), o tráfego é o processamento de regras permitido, interrompa</span><span class="sxs-lookup"><span data-stu-id="40689-265">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="40689-266">Tráfego atinge o endereço IP interno do hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="40689-266">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="40689-267">IIS01 não está escutando na porta 1433, assim nenhuma solicitação de toohello de resposta</span><span class="sxs-lookup"><span data-stu-id="40689-267">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="40689-268">Conclusão</span><span class="sxs-lookup"><span data-stu-id="40689-268">Conclusion</span></span>
<span data-ttu-id="40689-269">Este exemplo é uma maneira relativamente simple e direta de isolamento de sub-rede de back-end de saudação do tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="40689-269">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="40689-270">Mais exemplos e uma visão geral dos limites de segurança de rede podem ser encontrados [aqui][HOME].</span><span class="sxs-lookup"><span data-stu-id="40689-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="40689-271">Referências</span><span class="sxs-lookup"><span data-stu-id="40689-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="40689-272">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="40689-272">Azure Resource Manager template</span></span>
<span data-ttu-id="40689-273">Este exemplo usa um modelo do Azure Resource Manager predefinido em um repositório GitHub mantido pela Microsoft e abra toohello comunidade.</span><span class="sxs-lookup"><span data-stu-id="40689-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="40689-274">Esse modelo pode ser implantado diretamente fora do GitHub, ou baixado e modificadas toofit suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="40689-274">This template can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> 

<span data-ttu-id="40689-275">modelo principal Hello está no arquivo hello denominado "azuredeploy.json".</span><span class="sxs-lookup"><span data-stu-id="40689-275">hello main template is in hello file named "azuredeploy.json."</span></span> <span data-ttu-id="40689-276">Esse modelo pode ser enviado por meio do PowerShell ou CLI (com o arquivo de associado "azuredeploy.parameters.json" hello) toodeploy este modelo.</span><span class="sxs-lookup"><span data-stu-id="40689-276">This template can be submitted via PowerShell or CLI (with hello associated "azuredeploy.parameters.json" file) toodeploy this template.</span></span> <span data-ttu-id="40689-277">Localizar hello mais fácil é forma toouse Olá botão "Implantar tooAzure" na página de README.md Olá no GitHub.</span><span class="sxs-lookup"><span data-stu-id="40689-277">I find hello easiest way is toouse hello "Deploy tooAzure" button on hello README.md page at GitHub.</span></span>

<span data-ttu-id="40689-278">modelo de saudação toodeploy que se baseia neste exemplo do GitHub e hello portal do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="40689-278">toodeploy hello template that builds this example from GitHub and hello Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="40689-279">Em um navegador, navegue toohello [modelo][Template]</span><span class="sxs-lookup"><span data-stu-id="40689-279">From a browser, navigate toohello [Template][Template]</span></span>
2. <span data-ttu-id="40689-280">Clique em botão de "Implantar tooAzure" hello (ou hello "Visualizar" botão toosee uma representação gráfica do modelo)</span><span class="sxs-lookup"><span data-stu-id="40689-280">Click hello "Deploy tooAzure" button (or hello "Visualize" button toosee a graphical representation of this template)</span></span>
3. <span data-ttu-id="40689-281">Digite hello conta de armazenamento, o nome de usuário e senha na folha de parâmetros de saudação, clique em **Okey**</span><span class="sxs-lookup"><span data-stu-id="40689-281">Enter hello Storage Account, User Name, and Password in hello Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="40689-282">Criar um Grupo de Recursos para essa implantação (você pode usar uma existente, mas é recomendável usar uma nova para obter melhores resultados)</span><span class="sxs-lookup"><span data-stu-id="40689-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="40689-283">Se necessário, altere as configurações de assinatura e localização de saudação para sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="40689-283">If necessary, change hello Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="40689-284">Clique em **revisar os termos legais**, leia os termos de saudação e clique em **compra** tooagree.</span><span class="sxs-lookup"><span data-stu-id="40689-284">Click **Review legal terms**, read hello terms, and click **Purchase** tooagree.</span></span>
8. <span data-ttu-id="40689-285">Clique em **criar** toobegin implantação Olá desse modelo.</span><span class="sxs-lookup"><span data-stu-id="40689-285">Click **Create** toobegin hello deployment of this template.</span></span>
9. <span data-ttu-id="40689-286">Depois que a implantação Olá concluída com êxito, navegar toohello que grupo de recursos criado para esta implantação toosee Olá os recursos configurados dentro.</span><span class="sxs-lookup"><span data-stu-id="40689-286">Once hello deployment finishes successfully, navigate toohello Resource Group created for this deployment toosee hello resources configured inside.</span></span>

>[!NOTE]
><span data-ttu-id="40689-287">Esse modelo permite que o RDP toohello IIS01 somente servidor (Olá localizar IP público para IIS01 em Olá Portal).</span><span class="sxs-lookup"><span data-stu-id="40689-287">This template enables RDP toohello IIS01 server only (find hello Public IP for IIS01 on hello Portal).</span></span> <span data-ttu-id="40689-288">servidores de back-end tooany tooRDP nesta instância, o servidor do IIS Olá é usado como uma "salto caixa".</span><span class="sxs-lookup"><span data-stu-id="40689-288">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="40689-289">Primeiro servidor IIS toohello RDP e, em seguida, do servidor de saudação RDP do servidor IIS toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="40689-289">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

<span data-ttu-id="40689-290">tooremove essa implantação, Olá excluir grupo de recursos e todos os recursos filho também serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="40689-290">tooremove this deployment, delete hello Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="40689-291">Scripts de aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="40689-291">Sample application scripts</span></span>
<span data-ttu-id="40689-292">Depois que o modelo de saudação é executado com êxito, você pode definir o servidor de web hello e servidor de aplicativos com um tooallow de aplicativo da web simples teste com essa configuração de rede de Perímetro.</span><span class="sxs-lookup"><span data-stu-id="40689-292">Once hello template runs successfully, you can set up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span> <span data-ttu-id="40689-293">tooinstall um aplicativo de exemplo para este e outros exemplos de rede de Perímetro, foi fornecido no hello link a seguir: [Script de exemplo de aplicativo][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="40689-293">tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="40689-294">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="40689-294">Next steps</span></span>

* <span data-ttu-id="40689-295">Implantar este exemplo</span><span class="sxs-lookup"><span data-stu-id="40689-295">Deploy this example</span></span>
* <span data-ttu-id="40689-296">Criar aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="40689-296">Build hello sample application</span></span>
* <span data-ttu-id="40689-297">Testar diferentes fluxos de tráfego por meio dessa DMZ</span><span class="sxs-lookup"><span data-stu-id="40689-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "DMZ de entrada com NSG"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md