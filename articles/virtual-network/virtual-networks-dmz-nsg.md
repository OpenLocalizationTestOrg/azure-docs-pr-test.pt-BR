---
title: "Exemplo de DMZ do Azure ‑ Criar um DMZ simples com NSGs | Microsoft Docs"
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
ms.openlocfilehash: ec29e6b250f927a3a4a94ffdf83d6c7c0e325722
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="26571-103">Exemplo 1 – Criar uma DMZ simples usando NSGs com um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="26571-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="26571-104">[Voltar à página Práticas recomendadas de limite de segurança][HOME]</span><span class="sxs-lookup"><span data-stu-id="26571-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="26571-105">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="26571-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="26571-106">Clássico - PowerShell</span><span class="sxs-lookup"><span data-stu-id="26571-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="26571-107">Este exemplo criará uma DMZ simples com quatro servidores Windows e Grupos de Segurança de Rede.</span><span class="sxs-lookup"><span data-stu-id="26571-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="26571-108">Este exemplo descreve cada uma das seções relevantes do modelo para fornecer uma compreensão mais profunda de cada etapa.</span><span class="sxs-lookup"><span data-stu-id="26571-108">This example describes each of the relevant template sections to provide a deeper understanding of each step.</span></span> <span data-ttu-id="26571-109">Também há uma seção Cenário de Tráfego para fornecer um passo a passo detalhado para ver como o tráfego passa pelas camadas de defesa na DMZ.</span><span class="sxs-lookup"><span data-stu-id="26571-109">There is also a Traffic Scenario section to provide an in-depth step-by-step look at how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="26571-110">Por fim, na seção de referências, há o código do modelo e as instruções completas para criar este ambiente para testar e experimentar diversos cenários.</span><span class="sxs-lookup"><span data-stu-id="26571-110">Finally, in the references section is the complete template code and instructions to build this environment to test and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="26571-111">![DMZ de entrada com NSG][1]</span><span class="sxs-lookup"><span data-stu-id="26571-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="26571-112">Descrição do ambiente</span><span class="sxs-lookup"><span data-stu-id="26571-112">Environment description</span></span>
<span data-ttu-id="26571-113">Neste exemplo, uma assinatura contém os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="26571-113">In this example a subscription contains the following resources:</span></span>

* <span data-ttu-id="26571-114">Um único grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="26571-114">A single resource group</span></span>
* <span data-ttu-id="26571-115">Uma rede virtual com duas sub-redes: “FrontEnd” e “BackEnd”</span><span class="sxs-lookup"><span data-stu-id="26571-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="26571-116">Um grupo de segurança de rede que é aplicado a ambas as sub-redes</span><span class="sxs-lookup"><span data-stu-id="26571-116">A Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="26571-117">Um Windows Server que representa um servidor Web de aplicativos ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="26571-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="26571-118">Dois servidores Windows que representam servidores de back-end de aplicativos (“AppVM01”, “AppVM02”)</span><span class="sxs-lookup"><span data-stu-id="26571-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="26571-119">Um servidor Windows que representa um servidor DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="26571-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="26571-120">Um endereço IP público associado ao servidor Web do aplicativo</span><span class="sxs-lookup"><span data-stu-id="26571-120">A public IP address associated with the application web server</span></span>

<span data-ttu-id="26571-121">Na seção de referências, há um link para um modelo do Azure Resource Manager que cria o ambiente descrito neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="26571-121">In the references section, there is a link to an Azure Resource Manager template that builds the environment described in this example.</span></span> <span data-ttu-id="26571-122">A criação das VMs e das Redes Virtuais, embora seja realizada pelo modelo de exemplo, não será descrita em detalhes neste documento.</span><span class="sxs-lookup"><span data-stu-id="26571-122">Building the VMs and Virtual Networks, although done by the example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="26571-123">**Para criar esse ambiente** (as instruções detalhadas estão na seção de referências deste documento);</span><span class="sxs-lookup"><span data-stu-id="26571-123">**To build this environment** (detailed instructions are in the references section of this document);</span></span>

1. <span data-ttu-id="26571-124">Implantar o Modelo do Azure Resource Manager em: [Modelos de Início Rápido do Azure][Template]</span><span class="sxs-lookup"><span data-stu-id="26571-124">Deploy the Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="26571-125">Instalar o aplicativo de exemplo em: [Script do Aplicativo de Exemplo][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="26571-125">Install the sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
><span data-ttu-id="26571-126">Para usar o RDP em quaisquer servidores de back-end nesta instância, o servidor IIS é usado como uma “jump box”.</span><span class="sxs-lookup"><span data-stu-id="26571-126">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="26571-127">Primeiro use RDP no servidor IIS e, em seguida, do RDP do Servidor IIS para o servidor de back-end.</span><span class="sxs-lookup"><span data-stu-id="26571-127">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span> <span data-ttu-id="26571-128">Como alternativa, um IP público pode ser associado a cada servidor de NIC para realizar RDP mais facilmente.</span><span class="sxs-lookup"><span data-stu-id="26571-128">Alternately a Public IP can be associated with each server NIC for easier RDP.</span></span>
> 
>

<span data-ttu-id="26571-129">As seções a seguir fornecem uma descrição detalhada do Grupo de Segurança de Rede e como ele funciona para este exemplo, abordando as principais linhas do Modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="26571-129">The following sections provide a detailed description of the Network Security Group and how it functions for this example by walking through key lines of the Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="26571-130">Grupos de segurança de rede (NSG)</span><span class="sxs-lookup"><span data-stu-id="26571-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="26571-131">Neste exemplo, um grupo NSG é criado e então carregado com seis regras.</span><span class="sxs-lookup"><span data-stu-id="26571-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
><span data-ttu-id="26571-132">Em geral, você deve criar suas regras específicas "Permitir" primeiro e então as regras “Negar” mais genéricas por último.</span><span class="sxs-lookup"><span data-stu-id="26571-132">Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last.</span></span> <span data-ttu-id="26571-133">A prioridade atribuída ditará quais regras serão avaliadas primeiro.</span><span class="sxs-lookup"><span data-stu-id="26571-133">The assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="26571-134">Quando o tráfego se aplicar a uma regra específica, nenhuma regra adicional será avaliada.</span><span class="sxs-lookup"><span data-stu-id="26571-134">Once traffic is found to apply to a specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="26571-135">As regras NSG podem se aplicar na direção de entrada ou de saída (na perspectiva da sub-rede).</span><span class="sxs-lookup"><span data-stu-id="26571-135">NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).</span></span>
>
>

<span data-ttu-id="26571-136">Declarativamente, as regras a seguir estão sendo criadas para tráfego de entrada:</span><span class="sxs-lookup"><span data-stu-id="26571-136">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="26571-137">O tráfego interno de DNS (porta 53) é permitido</span><span class="sxs-lookup"><span data-stu-id="26571-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="26571-138">O tráfego de RDP (porta 3389) da Internet para qualquer VM é permitido</span><span class="sxs-lookup"><span data-stu-id="26571-138">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="26571-139">O tráfego HTTP (porta 80) da Internet ao servidor Web (IIS01) é permitido</span><span class="sxs-lookup"><span data-stu-id="26571-139">HTTP traffic (port 80) from the Internet to web server (IIS01) is allowed</span></span>
4. <span data-ttu-id="26571-140">Todo tráfego (todas as portas) de IIS01 para AppVM1 é permitido</span><span class="sxs-lookup"><span data-stu-id="26571-140">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="26571-141">Todo o tráfego (todas as portas) da Internet para a Rede Virtual inteira (todas as sub-redes) é Negado</span><span class="sxs-lookup"><span data-stu-id="26571-141">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="26571-142">Todo tráfego (todas as portas) da sub-rede Frontend para a sub-rede Backend é negado</span><span class="sxs-lookup"><span data-stu-id="26571-142">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="26571-143">Com essas regras associadas a cada sub-rede, se uma solicitação HTTP tiver entrado da Internet para o servidor Web, ambas as regras 3 (permitir) e 5 (negar) se aplicariam, mas já que a regra 3 tem uma prioridade maior, somente ela se aplicaria e a regra 5 não seria utilizada.</span><span class="sxs-lookup"><span data-stu-id="26571-143">With these rules bound to each subnet, if an HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="26571-144">Portanto, a solicitação HTTP seria permitida para o servidor Web.</span><span class="sxs-lookup"><span data-stu-id="26571-144">Thus the HTTP request would be allowed to the web server.</span></span> <span data-ttu-id="26571-145">Se esse mesmo tráfego estivesse tentando acessar o servidor DNS01, a regra 5 (Negar) seria a primeira a ser aplicada e o tráfego não teria permissão para passar para o servidor.</span><span class="sxs-lookup"><span data-stu-id="26571-145">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="26571-146">A regra 6 (Negar) impede que a sub-rede Frontend converse com a sub-rede Backend (exceto pelo tráfego permitido nas regras 1 e 4); esse conjunto de regras protege a rede Backend caso um invasor comprometa o aplicativo Web na rede Frontend, pois ele teria acesso limitado à rede Backend “protegida” (somente para recursos expostos no servidor AppVM01).</span><span class="sxs-lookup"><span data-stu-id="26571-146">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="26571-147">Há uma regra de saída padrão que permite o tráfego de saída para a Internet.</span><span class="sxs-lookup"><span data-stu-id="26571-147">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="26571-148">Neste exemplo, permitiremos o tráfego de saída e não modificaremos quaisquer regras de saída.</span><span class="sxs-lookup"><span data-stu-id="26571-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="26571-149">Para aplicar a política de segurança ao tráfego em ambos os sentidos, o Roteamento Definido pelo Usuário é necessário e explorado no “Exemplo 3”, na [Página de práticas recomendadas dos limites de segurança][HOME].</span><span class="sxs-lookup"><span data-stu-id="26571-149">To apply security policy to traffic in both directions, User Defined Routing is required and is explored in “Example 3” on the [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="26571-150">Cada regra é discutida com mais detalhes a seguir:</span><span class="sxs-lookup"><span data-stu-id="26571-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="26571-151">Um recurso do Grupo de Segurança de Rede deve ser instanciado para manter as regras:</span><span class="sxs-lookup"><span data-stu-id="26571-151">A Network Security Group resource must be instantiated to hold the rules:</span></span>

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

2. <span data-ttu-id="26571-152">A primeira regra neste exemplo habilita o tráfego DNS entre todas as redes internas para o servidor DNS na sub-rede de back-end.</span><span class="sxs-lookup"><span data-stu-id="26571-152">The first rule in this example allows DNS traffic between all internal networks to the DNS server on the backend subnet.</span></span> <span data-ttu-id="26571-153">A regra tem alguns parâmetros importantes:</span><span class="sxs-lookup"><span data-stu-id="26571-153">The rule has some important parameters:</span></span>
  * <span data-ttu-id="26571-154">“destinationAddressPrefix” – Regras podem usar um tipo especial de prefixo de endereço, chamado de “Marcação Padrão”, tais marcas são identificadores fornecidos pelo sistema que proporcionam uma maneira fácil de atender a uma maior categoria de prefixos de endereço.</span><span class="sxs-lookup"><span data-stu-id="26571-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way to address a larger category of address prefixes.</span></span> <span data-ttu-id="26571-155">Essa regra usa a Marcação Padrão “Internet” para significar qualquer endereço fora da VNet.</span><span class="sxs-lookup"><span data-stu-id="26571-155">This rule uses the Default Tag “Internet” to signify any address outside of the VNet.</span></span> <span data-ttu-id="26571-156">VirtualNetwork e AzureLoadBalancer são outros exemplos de rótulos de prefixo.</span><span class="sxs-lookup"><span data-stu-id="26571-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="26571-157">“Direction” (Direção) indica em qual direção do fluxo de tráfego esta regra entra em vigor.</span><span class="sxs-lookup"><span data-stu-id="26571-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="26571-158">Esta é a direção da perspectiva da sub-rede ou da máquina virtual (dependendo da associação desse NSG).</span><span class="sxs-lookup"><span data-stu-id="26571-158">The direction is from the perspective of the subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="26571-159">Portanto, se a Direção for “Inbound” (Entrada) e o tráfego estiver entrando na sub-rede, a regra se aplicará e o tráfego que sai da sub-rede não será afetado por essa regra.</span><span class="sxs-lookup"><span data-stu-id="26571-159">Thus if Direction is “Inbound” and traffic is entering the subnet, the rule would apply and traffic leaving the subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="26571-160">“Priority” (Prioridade) define a ordem na qual um fluxo de tráfego é avaliado.</span><span class="sxs-lookup"><span data-stu-id="26571-160">“Priority” sets the order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="26571-161">Quanto menor o número, maior a prioridade.</span><span class="sxs-lookup"><span data-stu-id="26571-161">The lower the number the higher the priority.</span></span> <span data-ttu-id="26571-162">Assim que uma regra se aplicar a um fluxo de tráfego específico, nenhuma regra adicional será processada.</span><span class="sxs-lookup"><span data-stu-id="26571-162">When a rule applies to a specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="26571-163">Portanto, se uma regra com prioridade 1 permite o tráfego e uma regra com prioridade 2 impede o tráfego e ambas as regras se aplicam ao tráfego, ele teria o fluxo permitido (já que a regra 1 tinha uma prioridade mais alta, ela vigorou e nenhuma regra adicional foi aplicada).</span><span class="sxs-lookup"><span data-stu-id="26571-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply to traffic then the traffic would be allowed to flow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="26571-164">“Action” (Ação) indica se um tráfego afetado por essa regra é bloqueado (“Deny”, Negar) ou permitido (“Allow”, Permitir).</span><span class="sxs-lookup"><span data-stu-id="26571-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

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

3. <span data-ttu-id="26571-165">Essa regra permite que o tráfego de RDP flua da Internet para a porta RDP em qualquer servidor na sub-rede associada.</span><span class="sxs-lookup"><span data-stu-id="26571-165">This rule allows RDP traffic to flow from the internet to the RDP port on any server on the bound subnet.</span></span> 

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

4. <span data-ttu-id="26571-166">Essa regra permite que o tráfego da internet alcance o servidor Web.</span><span class="sxs-lookup"><span data-stu-id="26571-166">This rule allows inbound internet traffic to hit the web server.</span></span> <span data-ttu-id="26571-167">Essa regra não altera o comportamento de roteamento.</span><span class="sxs-lookup"><span data-stu-id="26571-167">This rule does not change the routing behavior.</span></span> <span data-ttu-id="26571-168">A regra permite a passagem somente de tráfego destinado a IIS01.</span><span class="sxs-lookup"><span data-stu-id="26571-168">The rule only allows traffic destined for IIS01 to pass.</span></span> <span data-ttu-id="26571-169">Portanto, se o tráfego da Internet tinha o servidor Web como seu destino, essa regra deve permiti-lo e deve parar de processar outras regras.</span><span class="sxs-lookup"><span data-stu-id="26571-169">Thus if traffic from the Internet had the web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="26571-170">(Na regra com prioridade 140, todos os outros tráfegos de entrada da Internet estão bloqueados.)</span><span class="sxs-lookup"><span data-stu-id="26571-170">(In the rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="26571-171">Se você estiver processando somente tráfego HTTP, essa regra poderá ser mais restrita para permitir somente a porta de destino 80.</span><span class="sxs-lookup"><span data-stu-id="26571-171">If you're only processing HTTP traffic, this rule could be further restricted to only allow Destination Port 80.</span></span>

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet to [variables('VM01Name')]",
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

5. <span data-ttu-id="26571-172">Essa regra permite que o tráfego passe do servidor IIS01 para o servidor AppVM01; uma regra posterior bloqueia todo o tráfego de Frontend para Backend.</span><span class="sxs-lookup"><span data-stu-id="26571-172">This rule allows traffic to pass from the IIS01 server to the AppVM01 server, a later rule blocks all other Frontend to Backend traffic.</span></span> <span data-ttu-id="26571-173">Para melhorar essa regra, se a porta for conhecida, ela deve ser adicionada.</span><span class="sxs-lookup"><span data-stu-id="26571-173">To improve this rule, if the port is known that should be added.</span></span> <span data-ttu-id="26571-174">Por exemplo, se o servidor IIS está atingindo somente o SQL Server no AppVM01, o intervalo de porta de destino deve ser alterado de "*" (qualquer) para 1433 (a porta do SQL), permitindo uma menor superfície de ataque de entrada em AppVM01 se o aplicativo Web for comprometido.</span><span class="sxs-lookup"><span data-stu-id="26571-174">For example, if the IIS server is hitting only SQL Server on AppVM01, the Destination Port Range should be changed from “*” (Any) to 1433 (the SQL port) thus allowing a smaller inbound attack surface on AppVM01 should the web application ever be compromised.</span></span>

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] to [variables('VM02Name')]",
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

6. <span data-ttu-id="26571-175">Essa regra nega o tráfego da Internet para todos os servidores na rede.</span><span class="sxs-lookup"><span data-stu-id="26571-175">This rule denies traffic from the internet to any servers on the network.</span></span> <span data-ttu-id="26571-176">Com a regra em prioridades 110 e 120, o efeito é que ela permite somente tráfego de entrada da Internet para o firewall e portas RDP nos servidores e bloqueia todo o resto.</span><span class="sxs-lookup"><span data-stu-id="26571-176">With the rules at priority 110 and 120, the effect is to allow only inbound internet traffic to the firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="26571-177">Essa é uma regra “à prova de falhas” para bloquear todos os fluxos inesperados.</span><span class="sxs-lookup"><span data-stu-id="26571-177">This rule is a "fail-safe" rule to block all unexpected flows.</span></span>

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate the [variables('VNetName')] VNet from the Internet",
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

7. <span data-ttu-id="26571-178">A regra final nega odo o tráfego (todas as portas) da sub-rede Frontend para a sub-rede Backend.</span><span class="sxs-lookup"><span data-stu-id="26571-178">The final rule denies traffic from the Frontend subnet to the Backend subnet.</span></span> <span data-ttu-id="26571-179">Como essa é uma regra somente de Entrada, o tráfego invertido é permitido (de Backend para Frontend).</span><span class="sxs-lookup"><span data-stu-id="26571-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from the Backend to the Frontend).</span></span>

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate the [variables('Subnet1Name')] subnet from the [variables('Subnet2Name')] subnet",
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

## <a name="traffic-scenarios"></a><span data-ttu-id="26571-180">Cenários de tráfego</span><span class="sxs-lookup"><span data-stu-id="26571-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="26571-181">(*Permitido*) Internet para servidor Web</span><span class="sxs-lookup"><span data-stu-id="26571-181">(*Allowed*) Internet to web server</span></span>
1. <span data-ttu-id="26571-182">Um usuário de Internet solicita uma página HTTP do endereço IP público da NIC associada à NIC IIS01</span><span class="sxs-lookup"><span data-stu-id="26571-182">An internet user requests an HTTP page from the public IP address of the NIC associated with the IIS01 NIC</span></span>
2. <span data-ttu-id="26571-183">O endereço IP público passa tráfego para a VNet em direção a IIS01 (o servidor Web)</span><span class="sxs-lookup"><span data-stu-id="26571-183">The Public IP address passes traffic to the VNet towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="26571-184">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="26571-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="26571-185">A Regra NSG 1 (DNS) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="26571-185">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="26571-186">A Regra NSG 2 (RDP) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="26571-186">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="26571-187">A Regra NSG 3 (Internet para IIS01) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="26571-187">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="26571-188">O tráfego atinge o endereço IP interno do servidor Web IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="26571-188">Traffic hits internal IP address of the web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="26571-189">O IIS01 está escutando o tráfego da Web, recebe essa solicitação e começa a processar a solicitação</span><span class="sxs-lookup"><span data-stu-id="26571-189">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
6. <span data-ttu-id="26571-190">O IIS01 solicita informações do SQL Server na AppVM01</span><span class="sxs-lookup"><span data-stu-id="26571-190">IIS01 asks the SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="26571-191">Não há regras de saída na sub-rede Frontend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="26571-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="26571-192">A sub-rede Backend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="26571-192">The Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="26571-193">A Regra NSG 1 (DNS) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="26571-193">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="26571-194">A Regra NSG 2 (RDP) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="26571-194">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="26571-195">A Regra NSG 3 (Internet para Firewall) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="26571-195">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
  4. <span data-ttu-id="26571-196">A regra NSG 4 (IIS01 para AppVM01) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="26571-196">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="26571-197">AppVM01 recebe a consulta SQL e responde</span><span class="sxs-lookup"><span data-stu-id="26571-197">AppVM01 receives the SQL Query and responds</span></span>
10. <span data-ttu-id="26571-198">Como não há nenhuma regra de saída na sub-rede de Back-end, a resposta é permitida</span><span class="sxs-lookup"><span data-stu-id="26571-198">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
11. <span data-ttu-id="26571-199">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="26571-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="26571-200">Não há nenhuma regra NSG que se aplique ao tráfego de Entrada da sub-rede Backend para a sub-rede Frontend e, portanto, nenhuma das regras NSG se aplica</span><span class="sxs-lookup"><span data-stu-id="26571-200">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="26571-201">A regra do sistema padrão que permite o tráfego entre sub-redes permitiria esse tráfego e, portanto, o tráfego é permitido.</span><span class="sxs-lookup"><span data-stu-id="26571-201">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
12. <span data-ttu-id="26571-202">O servidor IIS recebe a resposta SQL, conclui a resposta HTTP e a envia ao solicitante</span><span class="sxs-lookup"><span data-stu-id="26571-202">The IIS server receives the SQL response and completes the HTTP response and sends to the requester</span></span>
13. <span data-ttu-id="26571-203">Como não há nenhuma regra de saída na sub-rede Frontend, a resposta é permitida e o Usuário da Internet recebe a página da Web solicitada.</span><span class="sxs-lookup"><span data-stu-id="26571-203">Since there are no outbound rules on the Frontend subnet, the response is allowed and the Internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-iis-server"></a><span data-ttu-id="26571-204">(*Permitido*) RDP para servidor IIS</span><span class="sxs-lookup"><span data-stu-id="26571-204">(*Allowed*) RDP to IIS server</span></span>
1. <span data-ttu-id="26571-205">Um Administrador do Servidor na Internet solicita uma sessão RDP para IIS01 no endereço IP público da NIC associada à NIC IIS01 (esse endereço IP público pode ser encontrado por meio do Portal ou do PowerShell)</span><span class="sxs-lookup"><span data-stu-id="26571-205">A Server Admin on internet requests an RDP session to IIS01 on the public IP address of the NIC associated with the IIS01 NIC (this public IP address can be found via the Portal or PowerShell)</span></span>
2. <span data-ttu-id="26571-206">O endereço IP público passa tráfego para a VNet em direção a IIS01 (o servidor Web)</span><span class="sxs-lookup"><span data-stu-id="26571-206">The Public IP address passes traffic to the VNet towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="26571-207">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="26571-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="26571-208">A Regra NSG 1 (DNS) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="26571-208">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="26571-209">A regra NSG 2 (RDP) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="26571-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="26571-210">Sem regras de saída, as regras padrão serão aplicadas e o tráfego de retorno será permitido</span><span class="sxs-lookup"><span data-stu-id="26571-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="26571-211">A sessão RDP está habilitada</span><span class="sxs-lookup"><span data-stu-id="26571-211">RDP session is enabled</span></span>
6. <span data-ttu-id="26571-212">O IIS01 solicita o nome de usuário e senha</span><span class="sxs-lookup"><span data-stu-id="26571-212">IIS01 prompts for the user name and password</span></span>

>[!NOTE]
><span data-ttu-id="26571-213">Para usar o RDP em quaisquer servidores de back-end nesta instância, o servidor IIS é usado como uma “jump box”.</span><span class="sxs-lookup"><span data-stu-id="26571-213">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="26571-214">Primeiro use RDP no servidor IIS e, em seguida, do RDP do Servidor IIS para o servidor de back-end.</span><span class="sxs-lookup"><span data-stu-id="26571-214">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span>
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="26571-215">(*Permitido*) Pesquisa de DNS do servidor Web no servidor DNS</span><span class="sxs-lookup"><span data-stu-id="26571-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="26571-216">O Servidor Web, IIS01, necessita de um feed de dados em www.data.gov, mas precisa resolver o endereço.</span><span class="sxs-lookup"><span data-stu-id="26571-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="26571-217">A configuração de rede para a Rede Virtual lista DNS01 (10.0.2.4 na sub-rede Backend), já que o servidor DNS primário, IIS01, envia a solicitação DNS para DNS01</span><span class="sxs-lookup"><span data-stu-id="26571-217">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="26571-218">Não há regras de saída na sub-rede Frontend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="26571-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="26571-219">A sub-rede Backend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="26571-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="26571-220">A regra NSG 1 (DNS) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="26571-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="26571-221">O servidor DNS recebe a solicitação</span><span class="sxs-lookup"><span data-stu-id="26571-221">DNS server receives the request</span></span>
6. <span data-ttu-id="26571-222">O servidor DNS não tem o endereço armazenado em cache e consulta um servidor DNS raiz na Internet</span><span class="sxs-lookup"><span data-stu-id="26571-222">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="26571-223">Nenhuma regra de saída na sub-rede Backend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="26571-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="26571-224">O servidor DNS da Internet responde e, desde que esta sessão tenha sido iniciada internamente, a resposta será permitida</span><span class="sxs-lookup"><span data-stu-id="26571-224">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="26571-225">O servidor DNS armazena em cache a resposta e responde à solicitação inicial para IIS01</span><span class="sxs-lookup"><span data-stu-id="26571-225">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="26571-226">Nenhuma regra de saída na sub-rede Backend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="26571-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="26571-227">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="26571-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="26571-228">Não há nenhuma regra NSG que se aplique ao tráfego de Entrada da sub-rede Backend para a sub-rede Frontend e, portanto, nenhuma das regras NSG se aplica</span><span class="sxs-lookup"><span data-stu-id="26571-228">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="26571-229">A regra do sistema padrão que permite o tráfego entre sub-redes permitiria esse tráfego e, portanto, o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="26571-229">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="26571-230">O IIS01 recebe a resposta do DNS01</span><span class="sxs-lookup"><span data-stu-id="26571-230">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="26571-231">(*Permitido*) Arquivo de acesso do servidor Web em AppVM01</span><span class="sxs-lookup"><span data-stu-id="26571-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="26571-232">IIS01 solicita um arquivo em AppVM01</span><span class="sxs-lookup"><span data-stu-id="26571-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="26571-233">Não há regras de saída na sub-rede Frontend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="26571-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="26571-234">A sub-rede Backend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="26571-234">The Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="26571-235">A Regra NSG 1 (DNS) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="26571-235">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="26571-236">A Regra NSG 2 (RDP) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="26571-236">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="26571-237">A Regra NSG 3 (Internet para IIS01) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="26571-237">NSG Rule 3 (Internet to IIS01) doesn’t apply, move to next rule</span></span>
  4. <span data-ttu-id="26571-238">A regra NSG 4 (IIS01 para AppVM01) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="26571-238">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="26571-239">AppVM01 recebe a solicitação e responde com o arquivo (supondo que o acesso é autorizado)</span><span class="sxs-lookup"><span data-stu-id="26571-239">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="26571-240">Como não há nenhuma regra de saída na sub-rede de Back-end, a resposta é permitida</span><span class="sxs-lookup"><span data-stu-id="26571-240">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
6. <span data-ttu-id="26571-241">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="26571-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="26571-242">Não há nenhuma regra NSG que se aplique ao tráfego de Entrada da sub-rede Backend para a sub-rede Frontend e, portanto, nenhuma das regras NSG se aplica</span><span class="sxs-lookup"><span data-stu-id="26571-242">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="26571-243">A regra do sistema padrão que permite o tráfego entre sub-redes permitiria esse tráfego e, portanto, o tráfego é permitido.</span><span class="sxs-lookup"><span data-stu-id="26571-243">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="26571-244">O servidor IIS recebe o arquivo</span><span class="sxs-lookup"><span data-stu-id="26571-244">The IIS server receives the file</span></span>

#### <a name="denied-rdp-to-backend"></a><span data-ttu-id="26571-245">(*Negado*) RDP para back-end</span><span class="sxs-lookup"><span data-stu-id="26571-245">(*Denied*) RDP to backend</span></span>
1. <span data-ttu-id="26571-246">Um usuário da Internet tenta realizar RDP para o servidor AppVM01</span><span class="sxs-lookup"><span data-stu-id="26571-246">An internet user tries to RDP to server AppVM01</span></span>
2. <span data-ttu-id="26571-247">Como não há nenhum endereço IP público associado a esta NIC dos servidores, esse tráfego nunca entraria na VNet e não alcançaria o servidor</span><span class="sxs-lookup"><span data-stu-id="26571-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="26571-248">Contudo, se um endereço IP público tiver sido habilitado por algum motivo, a regra NSG 2 (RDP) permitiria esse tráfego</span><span class="sxs-lookup"><span data-stu-id="26571-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
><span data-ttu-id="26571-249">Para usar o RDP em quaisquer servidores de back-end nesta instância, o servidor IIS é usado como uma “jump box”.</span><span class="sxs-lookup"><span data-stu-id="26571-249">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="26571-250">Primeiro use RDP no servidor IIS e, em seguida, do RDP do Servidor IIS para o servidor de back-end.</span><span class="sxs-lookup"><span data-stu-id="26571-250">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span>
>
>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="26571-251">(*Negado*) Web para o servidor de back-end</span><span class="sxs-lookup"><span data-stu-id="26571-251">(*Denied*) Web to backend server</span></span>
1. <span data-ttu-id="26571-252">Um usuário da Internet tenta acessar um arquivo no AppVM01</span><span class="sxs-lookup"><span data-stu-id="26571-252">An internet user tries to access a file on AppVM01</span></span>
2. <span data-ttu-id="26571-253">Como não há nenhum endereço IP público associado a esta NIC dos servidores, esse tráfego nunca entraria na VNet e não alcançaria o servidor</span><span class="sxs-lookup"><span data-stu-id="26571-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="26571-254">Se um endereço IP público tiver sido habilitado por algum motivo, a regra NSG 5 (Internet para VNet) bloquearia esse tráfego</span><span class="sxs-lookup"><span data-stu-id="26571-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="26571-255">(*Negado*) Pesquisa de DNS na Web no servidor DNS</span><span class="sxs-lookup"><span data-stu-id="26571-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="26571-256">Um usuário da Internet tenta pesquisar um registro DNS interno no DNS01</span><span class="sxs-lookup"><span data-stu-id="26571-256">An internet user tries to look up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="26571-257">Como não há nenhum endereço IP público associado a esta NIC dos servidores, esse tráfego nunca entraria na VNet e não alcançaria o servidor</span><span class="sxs-lookup"><span data-stu-id="26571-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="26571-258">Se um endereço IP público tiver sido habilitado por algum motivo, a regra NSG 5 (Internet para VNet) bloquearia esse tráfego (Observação: aquela Regra 1 (DNS) não se aplicaria, pois as solicitações de endereço de origem estão na Internet e a Regra 1 se aplica apenas à VNet local como a origem)</span><span class="sxs-lookup"><span data-stu-id="26571-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because the requests source address is the internet and Rule 1 only applies to the local VNet as the source)</span></span>

#### <a name="denied-sql-access-on-the-web-server"></a><span data-ttu-id="26571-259">(*Negado*) Acesso a SQL no servidor Web</span><span class="sxs-lookup"><span data-stu-id="26571-259">(*Denied*) SQL access on the web server</span></span>
1. <span data-ttu-id="26571-260">Um usuário da Internet solicita dados SQL do IIS01</span><span class="sxs-lookup"><span data-stu-id="26571-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="26571-261">Como não há nenhum endereço IP público associado a esta NIC dos servidores, esse tráfego nunca entraria na VNet e não alcançaria o servidor</span><span class="sxs-lookup"><span data-stu-id="26571-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="26571-262">Se um endereço IP Público tiver sido habilitado por algum motivo, a sub-rede Frontend iniciará o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="26571-262">If a Public IP address was enabled for some reason, the Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="26571-263">A Regra NSG 1 (DNS) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="26571-263">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="26571-264">A Regra NSG 2 (RDP) não se aplica; vá para a próxima regra</span><span class="sxs-lookup"><span data-stu-id="26571-264">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="26571-265">A Regra NSG 3 (Internet para IIS01) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="26571-265">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="26571-266">O tráfego atinge o endereço IP interno do IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="26571-266">Traffic hits internal IP address of the IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="26571-267">O IIS01 não está escutando na porta 1433; portanto, não há resposta para a solicitação</span><span class="sxs-lookup"><span data-stu-id="26571-267">IIS01 isn't listening on port 1433, so no response to the request</span></span>

## <a name="conclusion"></a><span data-ttu-id="26571-268">Conclusão</span><span class="sxs-lookup"><span data-stu-id="26571-268">Conclusion</span></span>
<span data-ttu-id="26571-269">Esse exemplo representa uma maneira relativamente simples e direta de isolar a sub-rede de back-end do tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="26571-269">This example is a relatively simple and straight forward way of isolating the back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="26571-270">Mais exemplos e uma visão geral dos limites de segurança de rede podem ser encontrados [aqui][HOME].</span><span class="sxs-lookup"><span data-stu-id="26571-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="26571-271">Referências</span><span class="sxs-lookup"><span data-stu-id="26571-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="26571-272">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="26571-272">Azure Resource Manager template</span></span>
<span data-ttu-id="26571-273">Esse exemplo usa um modelo do Azure Resource Manager predefinido em um repositório GitHub mantido pela Microsoft e aberto para a comunidade.</span><span class="sxs-lookup"><span data-stu-id="26571-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open to the community.</span></span> <span data-ttu-id="26571-274">Esse modelo pode ser implantado diretamente do GitHub ou baixados e modificados para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="26571-274">This template can be deployed straight out of GitHub, or downloaded and modified to fit your needs.</span></span> 

<span data-ttu-id="26571-275">O modelo principal está no arquivo chamado “azuredeploy.json”.</span><span class="sxs-lookup"><span data-stu-id="26571-275">The main template is in the file named "azuredeploy.json."</span></span> <span data-ttu-id="26571-276">Esse modelo pode ser enviado por meio do PowerShell ou da CLI (com o arquivo associado “azuredeploy.parameters.json”) para implantar esse modelo.</span><span class="sxs-lookup"><span data-stu-id="26571-276">This template can be submitted via PowerShell or CLI (with the associated "azuredeploy.parameters.json" file) to deploy this template.</span></span> <span data-ttu-id="26571-277">Creio que a maneira mais fácil é usar o botão “Implantar no Azure” na página README.md no GitHub.</span><span class="sxs-lookup"><span data-stu-id="26571-277">I find the easiest way is to use the "Deploy to Azure" button on the README.md page at GitHub.</span></span>

<span data-ttu-id="26571-278">Para implantar o modelo que cria esse exemplo do GitHub e do Portal do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="26571-278">To deploy the template that builds this example from GitHub and the Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="26571-279">Em um navegador, navegue para o [Modelo][Template]</span><span class="sxs-lookup"><span data-stu-id="26571-279">From a browser, navigate to the [Template][Template]</span></span>
2. <span data-ttu-id="26571-280">Clique no botão “Implantar no Azure” (ou no botão “Visualizar” para ver uma representação gráfica deste modelo)</span><span class="sxs-lookup"><span data-stu-id="26571-280">Click the "Deploy to Azure" button (or the "Visualize" button to see a graphical representation of this template)</span></span>
3. <span data-ttu-id="26571-281">Digite a Conta de Armazenamento, o Nome de Usuário e a Senha na folha Parâmetros e clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="26571-281">Enter the Storage Account, User Name, and Password in the Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="26571-282">Criar um Grupo de Recursos para essa implantação (você pode usar uma existente, mas é recomendável usar uma nova para obter melhores resultados)</span><span class="sxs-lookup"><span data-stu-id="26571-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="26571-283">Se necessário, altere as configurações de Assinatura e Local da sua VNet.</span><span class="sxs-lookup"><span data-stu-id="26571-283">If necessary, change the Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="26571-284">Clique em **Ler os termos legais**, leia-os e clique em **Comprar** para concordar.</span><span class="sxs-lookup"><span data-stu-id="26571-284">Click **Review legal terms**, read the terms, and click **Purchase** to agree.</span></span>
8. <span data-ttu-id="26571-285">Clique em **Criar** para iniciar a implantação deste modelo.</span><span class="sxs-lookup"><span data-stu-id="26571-285">Click **Create** to begin the deployment of this template.</span></span>
9. <span data-ttu-id="26571-286">Depois que a implantação for concluída com êxito, navegue até o Grupo de Recursos criado para essa implantação para ver os recursos configurados dentro.</span><span class="sxs-lookup"><span data-stu-id="26571-286">Once the deployment finishes successfully, navigate to the Resource Group created for this deployment to see the resources configured inside.</span></span>

>[!NOTE]
><span data-ttu-id="26571-287">Este modelo permite realizar RDP somente no servidor IIS01 (encontre o IP público para IIS01 no Portal).</span><span class="sxs-lookup"><span data-stu-id="26571-287">This template enables RDP to the IIS01 server only (find the Public IP for IIS01 on the Portal).</span></span> <span data-ttu-id="26571-288">Para usar o RDP em quaisquer servidores de back-end nesta instância, o servidor IIS é usado como uma “jump box”.</span><span class="sxs-lookup"><span data-stu-id="26571-288">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="26571-289">Primeiro use RDP no servidor IIS e, em seguida, do RDP do Servidor IIS para o servidor de back-end.</span><span class="sxs-lookup"><span data-stu-id="26571-289">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span>
>
>

<span data-ttu-id="26571-290">Para remover essa implantação, exclua o Grupo de Recursos e todos os recursos filho também serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="26571-290">To remove this deployment, delete the Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="26571-291">Scripts de aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="26571-291">Sample application scripts</span></span>
<span data-ttu-id="26571-292">Depois que o modelo for executado com êxito, você poderá configurar o servidor Web e o servidor de aplicativos com um aplicativo Web simples para testar a configuração desta DMZ.</span><span class="sxs-lookup"><span data-stu-id="26571-292">Once the template runs successfully, you can set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span> <span data-ttu-id="26571-293">Se você desejar instalar um aplicativo de exemplo para esse e outros Exemplos de DMZ, um é fornecido no seguinte link: [Script de aplicativo de exemplo][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="26571-293">To install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="26571-294">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="26571-294">Next steps</span></span>

* <span data-ttu-id="26571-295">Implantar este exemplo</span><span class="sxs-lookup"><span data-stu-id="26571-295">Deploy this example</span></span>
* <span data-ttu-id="26571-296">Compilar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="26571-296">Build the sample application</span></span>
* <span data-ttu-id="26571-297">Testar diferentes fluxos de tráfego por meio dessa DMZ</span><span class="sxs-lookup"><span data-stu-id="26571-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
<span data-ttu-id="26571-298">[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "DMZ de entrada com NSG"</span><span class="sxs-lookup"><span data-stu-id="26571-298">[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Inbound DMZ with NSG"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md