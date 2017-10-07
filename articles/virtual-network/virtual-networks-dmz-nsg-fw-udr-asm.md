---
title: "aaaDMZ exemplo – crie uma rede de Perímetro tooProtect redes com um Firewall, UDR e NSG | Microsoft Docs"
description: "Criar uma rede de perímetro com um Firewall, o Roteamento Definido pelo Usuário (UDR) e os Grupos de Segurança de Rede (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a><span data-ttu-id="850e7-103">Exemplo 3 – crie uma rede de Perímetro tooProtect redes com um Firewall, UDR e NSG</span><span class="sxs-lookup"><span data-stu-id="850e7-103">Example 3 – Build a DMZ tooProtect Networks with a Firewall, UDR, and NSG</span></span>
<span data-ttu-id="850e7-104">[Retornar toohello página segurança limite de melhores práticas][HOME]</span><span class="sxs-lookup"><span data-stu-id="850e7-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="850e7-105">Este exemplo criará uma rede de perímetro com um firewall, quatro servidores Windows, Roteamento Definido pelo Usuário, Reencaminhamento IP e Grupos de Segurança de Rede.</span><span class="sxs-lookup"><span data-stu-id="850e7-105">This example will create a DMZ with a firewall, four windows servers, User Defined Routing, IP Forwarding, and Network Security Groups.</span></span> <span data-ttu-id="850e7-106">Ele também guiará por cada Olá comandos relevantes tooprovide uma compreensão mais profunda de cada etapa.</span><span class="sxs-lookup"><span data-stu-id="850e7-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="850e7-107">Também há um cenário de tráfego seção tooprovide um detalhadas passo a passo sobre como o tráfego passa as camadas de saudação de defesa Olá DMZ.</span><span class="sxs-lookup"><span data-stu-id="850e7-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="850e7-108">Por fim, na seção de referências de saudação é código completo hello e instrução toobuild este ambiente tootest e experiência com vários cenários.</span><span class="sxs-lookup"><span data-stu-id="850e7-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="850e7-109">![DMZ bidirecional com NVA, NSG e UDR][1]</span><span class="sxs-lookup"><span data-stu-id="850e7-109">![Bi-directional DMZ with NVA, NSG, and UDR][1]</span></span>

## <a name="environment-setup"></a><span data-ttu-id="850e7-110">Configuração do ambiente</span><span class="sxs-lookup"><span data-stu-id="850e7-110">Environment Setup</span></span>
<span data-ttu-id="850e7-111">Neste exemplo, há uma assinatura que contém Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="850e7-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="850e7-112">Três serviços de nuvem: “SecSvc001”, “FrontEnd001” e “BackEnd001”</span><span class="sxs-lookup"><span data-stu-id="850e7-112">Three cloud services: “SecSvc001”, “FrontEnd001”, and “BackEnd001”</span></span>
* <span data-ttu-id="850e7-113">Uma rede virtual, “CorpNetwork”, com três sub-redes; “SecNet”, “FrontEnd” e “BackEnd”</span><span class="sxs-lookup"><span data-stu-id="850e7-113">A Virtual Network “CorpNetwork”, with three subnets: “SecNet”, “FrontEnd”, and “BackEnd”</span></span>
* <span data-ttu-id="850e7-114">Um dispositivo virtual de rede, neste exemplo, um firewall, conectado toohello SecNet sub-rede</span><span class="sxs-lookup"><span data-stu-id="850e7-114">A network virtual appliance, in this example a firewall, connected toohello SecNet subnet</span></span>
* <span data-ttu-id="850e7-115">Um Windows Server que representa um servidor Web de aplicativos ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="850e7-115">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="850e7-116">Dois servidores Windows que representam servidores de back-end de aplicativos ("AppVM01", "AppVM02")</span><span class="sxs-lookup"><span data-stu-id="850e7-116">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="850e7-117">Um servidor Windows que representa um servidor DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="850e7-117">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="850e7-118">Na seção de referências de saudação abaixo, há um script do PowerShell que criará a maior parte do ambiente Olá descrito acima.</span><span class="sxs-lookup"><span data-stu-id="850e7-118">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="850e7-119">Criando Olá VMs e redes virtuais, embora são feitos pelo script de exemplo hello, não são descritas em detalhes neste documento.</span><span class="sxs-lookup"><span data-stu-id="850e7-119">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="850e7-120">ambiente de saudação toobuild:</span><span class="sxs-lookup"><span data-stu-id="850e7-120">toobuild hello environment:</span></span>

1. <span data-ttu-id="850e7-121">Salvar arquivo hello rede config xml incluído na seção de referências de saudação (atualizada com nomes, o local e o cenário de saudação fornecido de toomatch de endereços IP)</span><span class="sxs-lookup"><span data-stu-id="850e7-121">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="850e7-122">Atualização Olá variáveis no script de Olá Olá script toomatch Olá ambiente é toobe executar (assinaturas, nomes de serviço, etc.)</span><span class="sxs-lookup"><span data-stu-id="850e7-122">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="850e7-123">Execute o script hello no PowerShell</span><span class="sxs-lookup"><span data-stu-id="850e7-123">Execute hello script in PowerShell</span></span>

<span data-ttu-id="850e7-124">**Observação**: região Olá representado em Olá script do PowerShell deve corresponder região Olá representada no arquivo de xml de configuração de rede hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-124">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="850e7-125">Após a execução bem-sucedida do script hello Olá seguindo as etapas de pós-scripts pode ser tomada:</span><span class="sxs-lookup"><span data-stu-id="850e7-125">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="850e7-126">Configurar regras de firewall hello, isso é abordado em Olá seção intitulada: Descrição da regra de Firewall.</span><span class="sxs-lookup"><span data-stu-id="850e7-126">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rule Description.</span></span>
2. <span data-ttu-id="850e7-127">Opcionalmente, na seção de referências de saudação são dois tooset de scripts, o servidor de web hello e servidor de aplicativos com um tooallow de aplicativo da web simples teste com essa configuração de rede de Perímetro.</span><span class="sxs-lookup"><span data-stu-id="850e7-127">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="850e7-128">Depois que o script hello for executado com êxito as regras de firewall Olá precisará toobe concluída, isso é abordado na seção de saudação: regras de Firewall.</span><span class="sxs-lookup"><span data-stu-id="850e7-128">Once hello script runs successfully hello firewall rules will need toobe completed, this is covered in hello section titled: Firewall Rules.</span></span>

## <a name="user-defined-routing-udr"></a><span data-ttu-id="850e7-129">Roteamento definido pelo usuário (UDR)</span><span class="sxs-lookup"><span data-stu-id="850e7-129">User Defined Routing (UDR)</span></span>
<span data-ttu-id="850e7-130">Por padrão, a saudação rotas de sistema a seguir é definida como:</span><span class="sxs-lookup"><span data-stu-id="850e7-130">By default, hello following system routes are defined as:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

<span data-ttu-id="850e7-131">Olá VNETLocal é sempre Olá definido prefixos de endereço de saudação VNet para essa rede específico (ou seja ele será alterado de rede virtual tooVNet dependendo de como cada rede virtual específico é definida).</span><span class="sxs-lookup"><span data-stu-id="850e7-131">hello VNETLocal is always hello defined address prefix(es) of hello VNet for that specific network (ie it will change from VNet tooVNet depending on how each specific VNet is defined).</span></span> <span data-ttu-id="850e7-132">Olá restante sistema rotas padrão acima e são estáticos.</span><span class="sxs-lookup"><span data-stu-id="850e7-132">hello remaining system routes are static and default as above.</span></span>

<span data-ttu-id="850e7-133">Como prioridade, rotas são processadas por meio do método de correspondência de prefixo mais longo (LPM) hello, assim hello rota mais específica na tabela de saudação aplicaria tooa recebe o endereço de destino.</span><span class="sxs-lookup"><span data-stu-id="850e7-133">As for priority, routes are processed via hello Longest Prefix Match (LPM) method, thus hello most specific route in hello table would apply tooa given destination address.</span></span>

<span data-ttu-id="850e7-134">Portanto, o tráfego (por exemplo toohello DNS01 server, 10.0.2.4) destinado a rede local da saudação (10.0.0.0/16) será encaminhado entre o destino de tooits VNet Olá devido toohello 10.0.0.0/16 rota.</span><span class="sxs-lookup"><span data-stu-id="850e7-134">Therefore, traffic (for example toohello DNS01 server, 10.0.2.4) intended for hello local network (10.0.0.0/16) would be routed across hello VNet tooits destination due toohello 10.0.0.0/16 route.</span></span> <span data-ttu-id="850e7-135">Em outras palavras, para 10.0.2.4, rota de 10.0.0.0/16 Olá é rota mais específica de hello, embora 0.0.0.0/0 e Olá 10.0.0.0/8 também podem se aplicam, mas uma vez que são menos específicos, elas não afetam esse tráfego.</span><span class="sxs-lookup"><span data-stu-id="850e7-135">In other words, for 10.0.2.4, hello 10.0.0.0/16 route is hello most specific route, even though hello 10.0.0.0/8 and 0.0.0.0/0 also could apply, but since they are less specific they don’t affect this traffic.</span></span> <span data-ttu-id="850e7-136">Assim Olá tráfego too10.0.2.4 teria um próximo salto da Olá redes locais e simplesmente toohello destino de rota.</span><span class="sxs-lookup"><span data-stu-id="850e7-136">Thus hello traffic too10.0.2.4 would have a next hop of hello local VNet and simply route toohello destination.</span></span>

<span data-ttu-id="850e7-137">Se o tráfego foi planejado para 10.1.1.1, por exemplo, não se aplicam a rota de 10.0.0.0/16 hello, mas Olá 10.0.0.0/8 seria hello mais específico e esse tráfego Olá seria removido ("preto holed") como Olá próximo salto é Null.</span><span class="sxs-lookup"><span data-stu-id="850e7-137">If traffic was intended for 10.1.1.1 for example, hello 10.0.0.0/16 route wouldn’t apply, but hello 10.0.0.0/8 would be hello most specific, and this hello traffic would be dropped (“black holed”) since hello next hop is Null.</span></span> 

<span data-ttu-id="850e7-138">Se destino Olá não aplicou tooany de prefixos de Null hello ou prefixos de VNETLocal hello, ele seguirá Olá menos específico de rota 0.0.0.0/0 e ser roteada toohello Internet como salto seguinte hello e, portanto, fora da borda de internet do Azure.</span><span class="sxs-lookup"><span data-stu-id="850e7-138">If hello destination didn’t apply tooany of hello Null prefixes or hello VNETLocal prefixes, then it would follow hello least specific route, 0.0.0.0/0 and be routed out toohello Internet as hello next hop and thus out Azure’s internet edge.</span></span>

<span data-ttu-id="850e7-139">Há dois prefixos idênticos na tabela de rotas hello, Olá é ordem de saudação de preferência com base no atributo de "origem" de rotas hello:</span><span class="sxs-lookup"><span data-stu-id="850e7-139">If there are two identical prefixes in hello route table, hello following is hello order of preference based on hello routes “source” attribute:</span></span>

1. <span data-ttu-id="850e7-140">"VirtualAppliance" = uma tabela de rotas definidas pelo usuário toohello adicionados manualmente</span><span class="sxs-lookup"><span data-stu-id="850e7-140">"VirtualAppliance" = A User Defined Route manually added toohello table</span></span>
2. <span data-ttu-id="850e7-141">"VPNGateway" = uma rota dinâmico (BGP quando usado com redes híbridas) adicionados por um protocolo de rede dinâmica, essas rotas podem ser alterados ao longo do tempo conforme o protocolo dinâmico Olá automaticamente reflete as alterações na rede emparelhada</span><span class="sxs-lookup"><span data-stu-id="850e7-141">“VPNGateway” = A Dynamic Route (BGP when used with hybrid networks), added by a dynamic network protocol, these routes may change over time as hello dynamic protocol automatically reflects changes in peered network</span></span>
3. <span data-ttu-id="850e7-142">"Default" = Olá sistema rotas, Olá entradas estáticas locais de rede virtual e hello, conforme mostrado na tabela de rotas Olá acima.</span><span class="sxs-lookup"><span data-stu-id="850e7-142">“Default” = hello System Routes, hello local VNet and hello static entries as shown in hello route table above.</span></span>

> [!NOTE]
> <span data-ttu-id="850e7-143">Agora você pode usar o roteamento definida pelo usuário (UDR) com Gateways de VPN e rota expressa tooforce saída e o dispositivo virtual de rede roteado tooa da toobe (NVA) de tráfego de entrada entre locais.</span><span class="sxs-lookup"><span data-stu-id="850e7-143">You can now use User Defined Routing (UDR) with ExpressRoute and VPN Gateways tooforce outbound and inbound cross-premises traffic toobe routed tooa network virtual appliance (NVA).</span></span>
> 
> 

#### <a name="creating-hello-local-routes"></a><span data-ttu-id="850e7-144">Criando Olá rotas locais</span><span class="sxs-lookup"><span data-stu-id="850e7-144">Creating hello local routes</span></span>
<span data-ttu-id="850e7-145">Neste exemplo, duas tabelas de roteamento são necessários, um para as sub-redes de front-end e back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="850e7-145">In this example, two routing tables are needed, one each for hello Frontend and Backend subnets.</span></span> <span data-ttu-id="850e7-146">Cada tabela é carregada com rotas estáticas apropriadas para Olá recebe sub-rede.</span><span class="sxs-lookup"><span data-stu-id="850e7-146">Each table is loaded with static routes appropriate for hello given subnet.</span></span> <span data-ttu-id="850e7-147">Para finalidade Olá neste exemplo, cada tabela tem três rotas:</span><span class="sxs-lookup"><span data-stu-id="850e7-147">For hello purpose of this example, each table has three routes:</span></span>

1. <span data-ttu-id="850e7-148">Tráfego de sub-rede local sem próximo salto definido tooallow sub-rede local tráfego toobypass Olá firewall</span><span class="sxs-lookup"><span data-stu-id="850e7-148">Local subnet traffic with no Next Hop defined tooallow local subnet traffic toobypass hello firewall</span></span>
2. <span data-ttu-id="850e7-149">Tráfego de rede virtual com um próximo nó definido como firewall, isso substituições de regra padrão Olá que permite tooroute de tráfego de rede virtual local diretamente</span><span class="sxs-lookup"><span data-stu-id="850e7-149">Virtual Network traffic with a Next Hop defined as firewall, this overrides hello default rule that allows local VNet traffic tooroute directly</span></span>
3. <span data-ttu-id="850e7-150">Tráfego de todos os demais (0/0) com um próximo nó definido como Olá firewall</span><span class="sxs-lookup"><span data-stu-id="850e7-150">All remaining traffic (0/0) with a Next Hop defined as hello firewall</span></span>

<span data-ttu-id="850e7-151">Após a criação de tabelas de roteamento de saudação são sub-redes tootheir associado.</span><span class="sxs-lookup"><span data-stu-id="850e7-151">Once hello routing tables are created they are bound tootheir subnets.</span></span> <span data-ttu-id="850e7-152">Olá front-end subrede tabela de roteamento, tendo criado e vinculado toohello sub-rede deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="850e7-152">For hello Frontend subnet routing table, once created and bound toohello subnet should look like this:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


<span data-ttu-id="850e7-153">Neste exemplo, a seguir Olá comandos toobuild usado Olá a tabela de rota, adicione uma rota definida pelo usuário e, em seguida, associar a sub-rede de tooa de tabela de rota hello (Observação; todos os itens abaixo que começa com um sinal de cifrão (por exemplo: $BESubnet) são variáveis definidas pelo usuário do script hello em Olá referência seção deste documento):</span><span class="sxs-lookup"><span data-stu-id="850e7-153">For this example, hello following commands are used toobuild hello route table, add a user defined route, and then bind hello route table tooa subnet (Note; any items below beginning with a dollar sign (e.g.: $BESubnet) are user defined variables from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="850e7-154">Primeira Olá base tabela de roteamento deve ser criada.</span><span class="sxs-lookup"><span data-stu-id="850e7-154">First hello base routing table must be created.</span></span> <span data-ttu-id="850e7-155">Este trecho de código mostra a criação de saudação de tabela de saudação para a sub-rede de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="850e7-155">This snippet shows hello creation of hello table for hello Backend subnet.</span></span> <span data-ttu-id="850e7-156">No script hello, uma tabela correspondente também é criada para a sub-rede de front-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="850e7-156">In hello script, a corresponding table is also created for hello Frontend subnet.</span></span>
   
     <span data-ttu-id="850e7-157">New-AzureRouteTable -Name $BERouteTableName \`</span><span class="sxs-lookup"><span data-stu-id="850e7-157">New-AzureRouteTable -Name $BERouteTableName \`</span></span>
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. <span data-ttu-id="850e7-158">Depois de criar a tabela de rotas hello, rotas definida de usuário específicas podem ser adicionadas.</span><span class="sxs-lookup"><span data-stu-id="850e7-158">Once hello route table is created, specific user defined routes can be added.</span></span> <span data-ttu-id="850e7-159">Neste trecho, todo o tráfego (0.0.0.0/0) será encaminhado através do dispositivo virtual de saudação (uma variável, $VMIP [0], é usado toopass Olá endereço de IP atribuído ao dispositivo virtual Olá foi criado anteriormente no script hello).</span><span class="sxs-lookup"><span data-stu-id="850e7-159">In this snipped, all traffic (0.0.0.0/0) will be routed through hello virtual appliance (a variable, $VMIP[0], is used toopass in hello IP address assigned when hello virtual appliance was created earlier in hello script).</span></span> <span data-ttu-id="850e7-160">No script hello, também é criada uma regra correspondente na tabela de front-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="850e7-160">In hello script, a corresponding rule is also created in hello Frontend table.</span></span>
   
     <span data-ttu-id="850e7-161">Get-AzureRouteTable $BERouteTableName | \`</span><span class="sxs-lookup"><span data-stu-id="850e7-161">Get-AzureRouteTable $BERouteTableName | \`</span></span>
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. <span data-ttu-id="850e7-162">Olá acima rota de entrada substituirá hello "0.0.0.0/0" rota, mas 10.0.0.0/16 regra saudação padrão que ainda existente que permitiria que tráfego dentro de saudação VNet tooroute diretamente destino toohello e toohello dispositivo de rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="850e7-162">hello above route entry will override hello default "0.0.0.0/0" route, but hello default 10.0.0.0/16 rule still existing which would allow traffic within hello VNet tooroute directly toohello destination and not toohello Network Virtual Appliance.</span></span> <span data-ttu-id="850e7-163">toocorrect que deve ser adicionada a esta regra de acompanhamento de saudação comportamento.</span><span class="sxs-lookup"><span data-stu-id="850e7-163">toocorrect this behavior hello follow rule must be added.</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. <span data-ttu-id="850e7-164">Neste ponto, há um toobe da escolha feita.</span><span class="sxs-lookup"><span data-stu-id="850e7-164">At this point there is a choice toobe made.</span></span> <span data-ttu-id="850e7-165">Com hello acima duas rotas todo o tráfego roteará firewall toohello para avaliação, até mesmo tráfego dentro de uma única sub-rede.</span><span class="sxs-lookup"><span data-stu-id="850e7-165">With hello above two routes all traffic will route toohello firewall for assessment, even traffic within a single subnet.</span></span> <span data-ttu-id="850e7-166">Isso pode ser desejável, mas tooallow tráfego dentro de um tooroute sub-rede localmente sem o envolvimento do firewall Olá pode ser adicionada a uma regra de terceira, muito específica.</span><span class="sxs-lookup"><span data-stu-id="850e7-166">This may be desired, however tooallow traffic within a subnet tooroute locally without involvement from hello firewall a third, very specific rule can be added.</span></span> <span data-ttu-id="850e7-167">Essa rota estados destine de qualquer endereço de sub-rede local Olá pode simplesmente existe rota diretamente (NextHopType = VNETLocal).</span><span class="sxs-lookup"><span data-stu-id="850e7-167">This route states that any address destine for hello local subnet can just route there directly (NextHopType = VNETLocal).</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. <span data-ttu-id="850e7-168">Por fim, com hello tabela de roteamento criada e preenchida com um rotas definidas pelo usuário, tabela Olá agora deve ser sub-rede tooa associado.</span><span class="sxs-lookup"><span data-stu-id="850e7-168">Finally, with hello routing table created and populated with a user defined routes, hello table must now be bound tooa subnet.</span></span> <span data-ttu-id="850e7-169">No script hello, tabela de rotas Olá front-end também é associada toohello sub-rede front-end.</span><span class="sxs-lookup"><span data-stu-id="850e7-169">In hello script, hello front end route table is also bound toohello Frontend subnet.</span></span> <span data-ttu-id="850e7-170">Aqui está o script de associação de saudação para a sub-rede de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="850e7-170">Here is hello binding script for hello back end subnet.</span></span>
   
     <span data-ttu-id="850e7-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span><span class="sxs-lookup"><span data-stu-id="850e7-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span></span>
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a><span data-ttu-id="850e7-172">encaminhamento IP</span><span class="sxs-lookup"><span data-stu-id="850e7-172">IP Forwarding</span></span>
<span data-ttu-id="850e7-173">TooUDR um recurso complementar, é o encaminhamento IP.</span><span class="sxs-lookup"><span data-stu-id="850e7-173">A companion feature tooUDR, is IP Forwarding.</span></span> <span data-ttu-id="850e7-174">Isso é uma configuração em um dispositivo Virtual que permite o tráfego tooreceive não especificamente endereçado toohello dispositivo e, em seguida, encaminhá-los destino tráfego tooits ultimate.</span><span class="sxs-lookup"><span data-stu-id="850e7-174">This is a setting on a Virtual Appliance that allows it tooreceive traffic not specifically addressed toohello appliance and then forward that traffic tooits ultimate destination.</span></span>

<span data-ttu-id="850e7-175">Por exemplo, se o tráfego de AppVM01 faz uma solicitação toohello DNS01 ao servidor, UDR seria rotear esse firewall toohello.</span><span class="sxs-lookup"><span data-stu-id="850e7-175">As an example, if traffic from AppVM01 makes a request toohello DNS01 server, UDR would route this toohello firewall.</span></span> <span data-ttu-id="850e7-176">Com o encaminhamento IP habilitado, tráfego Olá para o destino de DNS01 hello (10.0.2.4) será aceita pelo dispositivo hello (10.0.0.4) e, em seguida, encaminhado destino final de tooits (10.0.2.4).</span><span class="sxs-lookup"><span data-stu-id="850e7-176">With IP Forwarding enabled, hello traffic for hello DNS01 destination (10.0.2.4) will be accepted by hello appliance (10.0.0.4) and then forwarded tooits ultimate destination (10.0.2.4).</span></span> <span data-ttu-id="850e7-177">Sem o encaminhamento IP ativado Olá Firewall, tráfego seria não aceito pelo dispositivo hello, embora a tabela de rotas Olá firewall hello como o próximo salto de saudação.</span><span class="sxs-lookup"><span data-stu-id="850e7-177">Without IP Forwarding enabled on hello Firewall, traffic would not be accepted by hello appliance even though hello route table has hello firewall as hello next hop.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="850e7-178">Ele é crítico tooremember tooenable encaminhamento IP em conjunto com o roteamento definida pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="850e7-178">It’s critical tooremember tooenable IP Forwarding in conjunction with User Defined Routing.</span></span>
> 
> 

<span data-ttu-id="850e7-179">A configuração do Encaminhamento IP é um único comando e pode ser feito no momento da criação da VM.</span><span class="sxs-lookup"><span data-stu-id="850e7-179">Setting up IP Forwarding is a single command and can be done at VM creation time.</span></span> <span data-ttu-id="850e7-180">Para Olá fluxo este trecho de código do exemplo hello é final de saudação do script hello e agrupado com comandos UDR hello:</span><span class="sxs-lookup"><span data-stu-id="850e7-180">For hello flow of this example hello code snippet is towards hello end of hello script and grouped with hello UDR commands:</span></span>

1. <span data-ttu-id="850e7-181">Chamar a instância de VM Olá que seu dispositivo virtual, Olá firewall nesse caso e habilitar o encaminhamento de IP (Observação; qualquer item em vermelho, começando com um sinal de cifrão (por exemplo: $VMName[0]) é uma variável definida pelo usuário do script hello na seção de referência Olá deste documento.</span><span class="sxs-lookup"><span data-stu-id="850e7-181">Call hello VM instance that is your virtual appliance, hello firewall in this case, and enable IP Forwarding (Note; any item in red beginning with a dollar sign (e.g.: $VMName[0]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="850e7-182">Olá zero entre colchetes, [0], representa Olá primeira VM na matriz de saudação de VMs, para toowork de script de exemplo hello sem modificação, firewall de Olá Olá deve ser a primeira máquina virtual (VM 0)):</span><span class="sxs-lookup"><span data-stu-id="850e7-182">hello zero in brackets, [0], represents hello first VM in hello array of VMs, for hello example script toowork without modification, hello first VM (VM 0) must be hello firewall):</span></span>
   
     <span data-ttu-id="850e7-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span><span class="sxs-lookup"><span data-stu-id="850e7-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span></span>
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a><span data-ttu-id="850e7-184">Grupos de segurança de rede (NSG)</span><span class="sxs-lookup"><span data-stu-id="850e7-184">Network Security Groups (NSG)</span></span>
<span data-ttu-id="850e7-185">Neste exemplo, um grupo NSG é criado e então carregado com uma única regra.</span><span class="sxs-lookup"><span data-stu-id="850e7-185">In this example, a NSG group is built and then loaded with a single rule.</span></span> <span data-ttu-id="850e7-186">Esse grupo, em seguida, é associado somente toohello front-end e back-end sub-redes (não Olá SecNet).</span><span class="sxs-lookup"><span data-stu-id="850e7-186">This group is then bound only toohello Frontend and Backend subnets (not hello SecNet).</span></span> <span data-ttu-id="850e7-187">Declarativamente Olá regra a seguir está sendo compilado:</span><span class="sxs-lookup"><span data-stu-id="850e7-187">Declaratively hello following rule is being built:</span></span>

1. <span data-ttu-id="850e7-188">Qualquer tráfego (todas as portas) do hello Internet toohello VNet inteiro (todas as sub-redes) foi negado</span><span class="sxs-lookup"><span data-stu-id="850e7-188">Any traffic (all ports) from hello Internet toohello entire VNet (all subnets) is Denied</span></span>

<span data-ttu-id="850e7-189">Embora NSGs sejam usados neste exemplo, seu principal objetivo será ser como uma segunda camada de defesa contra erros de configuração manual.</span><span class="sxs-lookup"><span data-stu-id="850e7-189">Although NSGs are used in this example, it’s main purpose is as a secondary layer of defense against manual misconfiguration.</span></span> <span data-ttu-id="850e7-190">Queremos tooblock todos os tráfego da saudação tooeither da internet Olá front-end ou sub-redes de back-end, o tráfego somente devem fluir através de Olá SecNet firewall de toohello de sub-rede (e, em seguida, se apropriado em toohello front-end ou back-end subredes).</span><span class="sxs-lookup"><span data-stu-id="850e7-190">We want tooblock all inbound traffic from hello internet tooeither hello Frontend or Backend subnets, traffic should only flow through hello SecNet subnet toohello firewall (and then if appropriate on toohello Frontend or Backend subnets).</span></span> <span data-ttu-id="850e7-191">Além disso, com as regras UDR Olá em vigor, qualquer tráfego torná-lo em Olá front-end ou back-end subredes seria direcionado out toohello firewall (Obrigado tooUDR).</span><span class="sxs-lookup"><span data-stu-id="850e7-191">Plus, with hello UDR rules in place, any traffic that did make it into hello Frontend or Backend subnets would be directed out toohello firewall (thanks tooUDR).</span></span> <span data-ttu-id="850e7-192">firewall Olá veria isso como um fluxo assimétrico e ficaria o tráfego de saída hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-192">hello firewall would see this as an asymmetric flow and would drop hello outbound traffic.</span></span> <span data-ttu-id="850e7-193">Assim, há três camadas de saudação de proteção de segurança front-end e back-end sub-redes; 1) sem pontos de extremidade abertos no hello FrontEnd001 e BackEnd001 serviços em nuvem, 2) NSGs negar o tráfego de Internet, firewall de 3) Olá soltar assimétrico tráfego de hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-193">Thus there are three layers of security protecting hello Frontend and Backend subnets; 1) no open endpoints on hello FrontEnd001 and BackEnd001 cloud services, 2) NSGs denying traffic from hello Internet, 3) hello firewall dropping asymmetric traffic.</span></span>

<span data-ttu-id="850e7-194">Um ponto interessante sobre Olá grupo de segurança de rede neste exemplo é que ele contém apenas uma regra, mostrada abaixo, que é toodeny internet tráfego toohello toda rede virtual que incluiria a sub-rede de segurança hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-194">One interesting point regarding hello Network Security Group in this example is that it contains only one rule, shown below, which is toodeny internet traffic toohello entire virtual network which would include hello Security subnet.</span></span> 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

<span data-ttu-id="850e7-195">No entanto, como Olá NSG só é ligado toohello front-end e back-end sub-redes, regra de saudação não é processada no tráfego de entrada toohello sub-rede de segurança.</span><span class="sxs-lookup"><span data-stu-id="850e7-195">However, since hello NSG is only bound toohello Frontend and Backend subnets, hello rule isn’t processed on traffic inbound toohello Security subnet.</span></span> <span data-ttu-id="850e7-196">Como resultado, mesmo que a regra NSG Olá não diz nenhum endereço de tooany de tráfego de Internet Olá VNet, porque Olá que NSG nunca foi associado a sub-rede de segurança toohello, o tráfego fluirá toohello sub-rede de segurança.</span><span class="sxs-lookup"><span data-stu-id="850e7-196">As a result, even though hello NSG rule says no Internet traffic tooany address on hello VNet, because hello NSG was never bound toohello Security subnet, traffic will flow toohello Security subnet.</span></span>

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a><span data-ttu-id="850e7-197">Regras de firewall</span><span class="sxs-lookup"><span data-stu-id="850e7-197">Firewall Rules</span></span>
<span data-ttu-id="850e7-198">No firewall hello, regras de encaminhamento precisará toobe criado.</span><span class="sxs-lookup"><span data-stu-id="850e7-198">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="850e7-199">Desde que o firewall hello está bloqueando ou encaminhamento todas as entrada, saído e dentro do VNet tráfego muitas regras de firewall são necessárias.</span><span class="sxs-lookup"><span data-stu-id="850e7-199">Since hello firewall is blocking or forwarding all inbound, outbound, and intra-VNet traffic many firewall rules are needed.</span></span> <span data-ttu-id="850e7-200">Além disso, todo o tráfego de entrada atingirá o endereço IP público de serviço de segurança hello (em portas diferentes), toobe processadas pelo firewall hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-200">Also, all inbound traffic will hit hello Security Service public IP address (on different ports), toobe processed by hello firewall.</span></span> <span data-ttu-id="850e7-201">Uma prática recomendada é fluxos de lógica de saudação toodiagram antes de configurar o retrabalho de tooavoid de regras de firewall e sub-redes de hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="850e7-201">A best practice is toodiagram hello logical flows before setting up hello subnets and firewall rules tooavoid rework later.</span></span> <span data-ttu-id="850e7-202">Olá figura a seguir é uma exibição lógica de regras de firewall Olá para este exemplo:</span><span class="sxs-lookup"><span data-stu-id="850e7-202">hello following figure is a logical view of hello firewall rules for this example:</span></span>

<span data-ttu-id="850e7-203">![Modo de exibição lógico de saudação regras de Firewall][2]</span><span class="sxs-lookup"><span data-stu-id="850e7-203">![Logical View of hello Firewall Rules][2]</span></span>

> [!NOTE]
> <span data-ttu-id="850e7-204">Com base em Olá que solução de virtualização de rede usada, as portas de gerenciamento Olá irão variar.</span><span class="sxs-lookup"><span data-stu-id="850e7-204">Based on hello Network Virtual Appliance used, hello management ports will vary.</span></span> <span data-ttu-id="850e7-205">Neste exemplo, um Firewall NextGen Barracuda é mencionado e usa as portas 22, 801 e 807.</span><span class="sxs-lookup"><span data-stu-id="850e7-205">In this example a Barracuda NextGen Firewall is referenced which uses ports 22, 801, and 807.</span></span> <span data-ttu-id="850e7-206">Consulte Olá appliance fornecedor documentação toofind Olá exata portas usadas para o gerenciamento de dispositivo hello está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="850e7-206">Please consult hello appliance vendor documentation toofind hello exact ports used for management of hello device being used.</span></span>
> 
> 

### <a name="logical-rule-description"></a><span data-ttu-id="850e7-207">Descrição da regra lógica</span><span class="sxs-lookup"><span data-stu-id="850e7-207">Logical Rule Description</span></span>
<span data-ttu-id="850e7-208">Olá lógico diagrama acima, sub-rede de segurança Olá não é mostrado como firewall Olá é único recurso Olá nessa sub-rede e este diagrama está mostrando as regras de firewall hello e como eles logicamente permitem ou negar fluxos de tráfego e não Olá roteados caminho real.</span><span class="sxs-lookup"><span data-stu-id="850e7-208">In hello logical diagram above, hello security subnet is not shown since hello firewall is hello only resource on that subnet, and this diagram is showing hello firewall rules and how they logically allow or deny traffic flows and not hello actual routed path.</span></span> <span data-ttu-id="850e7-209">Além disso, dois octetos do endereço IP local do Olá para facilitar a leitura mais fácil da última portas externas de saudação selecionadas para Olá tráfego RDP são portas intervalos superior (8014 – 8026) e foram selecionado toosomewhat alinhada hello (por exemplo, o endereço do servidor local 10.0.1.4 está associado porta externa 8014), no entanto, todas as portas mais alto não conflitante podem ser usadas.</span><span class="sxs-lookup"><span data-stu-id="850e7-209">Also, hello external ports selected for hello RDP traffic are higher ranged ports (8014 – 8026) and were selected toosomewhat align with hello last two octets of hello local IP address for easier readability (e.g. local server address 10.0.1.4 is associated with external port 8014), however any higher non-conflicting ports could be used.</span></span>

<span data-ttu-id="850e7-210">Neste exemplo, precisamos de sete tipos de regras, descritos abaixo:</span><span class="sxs-lookup"><span data-stu-id="850e7-210">For this example, we need 7 types of rules, these rule types are described as follows:</span></span>

* <span data-ttu-id="850e7-211">Regras externas (para o tráfego de entrada):</span><span class="sxs-lookup"><span data-stu-id="850e7-211">External Rules (for inbound traffic):</span></span>
  1. <span data-ttu-id="850e7-212">Regra de firewall de gerenciamento: Essa regra de redirecionamento do aplicativo permite que portas de gerenciamento do tráfego toopass toohello de solução de virtualização de rede hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-212">Firewall Management Rule: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance.</span></span>
  2. <span data-ttu-id="850e7-213">Regras de RDP (para cada servidor do windows): essas quatro regras (uma para cada servidor) serão permitir o gerenciamento de saudação servidores individuais via RDP.</span><span class="sxs-lookup"><span data-stu-id="850e7-213">RDP Rules (for each windows server): These four rules (one for each server) will allow management of hello individual servers via RDP.</span></span> <span data-ttu-id="850e7-214">Isso também pode ser empacotado em uma regra dependendo recursos de saudação do hello solução de virtualização de rede que está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="850e7-214">This could also be bundled into one rule depending on hello capabilities of hello Network Virtual Appliance being used.</span></span>
  3. <span data-ttu-id="850e7-215">Regras de tráfego do aplicativo: Há duas regras de tráfego do aplicativo, Olá primeiro para o tráfego de web de front-end hello e Olá segundo para o tráfego de back-end da saudação (por exemplo, servidor toodata camada da web).</span><span class="sxs-lookup"><span data-stu-id="850e7-215">Application Traffic Rules: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="850e7-216">configuração de saudação dessas regras dependerá de arquitetura de rede de saudação (em que os servidores são colocados) e fluxos de tráfego (fluxos de tráfego que Olá direção e quais portas são usadas).</span><span class="sxs-lookup"><span data-stu-id="850e7-216">hello configuration of these rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
     * <span data-ttu-id="850e7-217">primeira regra de saudação permitirá que o servidor de aplicativos do hello aplicativo real tráfego tooreach hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-217">hello first rule will allow hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="850e7-218">Enquanto hello outras regras permitirem segurança, gerenciamento, etc., regras de aplicativo são o que permite que tooaccess de usuários ou serviços externos Olá aplicativo (s).</span><span class="sxs-lookup"><span data-stu-id="850e7-218">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="850e7-219">Neste exemplo, há um único servidor web na porta 80, assim, uma regra de firewall único de aplicativo redirecionará IP externo do tráfego de entrada toohello, toohello web interno endereço IP de servidores.</span><span class="sxs-lookup"><span data-stu-id="850e7-219">For this example, there is a single web server on port 80, thus a single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span> <span data-ttu-id="850e7-220">Olá redirecionado sessão tráfego deve ser NAT tinha toohello interno do servidor.</span><span class="sxs-lookup"><span data-stu-id="850e7-220">hello redirected traffic session would be NAT’d toohello internal server.</span></span>
     * <span data-ttu-id="850e7-221">Olá segunda regra de tráfego do aplicativo é Olá back-end regra tooallow Olá Web tootalk toohello AppVM01 servidor (mas não AppVM02) por meio de qualquer porta.</span><span class="sxs-lookup"><span data-stu-id="850e7-221">hello second Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via any port.</span></span>
* <span data-ttu-id="850e7-222">Regras internas (para o tráfego interno da Rede Virtual)</span><span class="sxs-lookup"><span data-stu-id="850e7-222">Internal Rules (for intra-VNet traffic)</span></span>
  1. <span data-ttu-id="850e7-223">Regra de saída tooInternet: esta regra permitir o tráfego de qualquer rede toopass toohello selecionado redes.</span><span class="sxs-lookup"><span data-stu-id="850e7-223">Outbound tooInternet Rule: This rule will allow traffic from any network toopass toohello selected networks.</span></span> <span data-ttu-id="850e7-224">Geralmente, essa regra é uma regra padrão já está no firewall hello, mas em um estado desabilitado.</span><span class="sxs-lookup"><span data-stu-id="850e7-224">This rule is usually a default rule already on hello firewall, but in a disabled state.</span></span> <span data-ttu-id="850e7-225">Essa regra deve ser habilitada para esse exemplo.</span><span class="sxs-lookup"><span data-stu-id="850e7-225">This rule should be enabled for this example.</span></span>
  2. <span data-ttu-id="850e7-226">Regra DNS: Essa regra permite que somente o DNS (porta 53) tráfego toopass toohello servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="850e7-226">DNS Rule: This rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="850e7-227">Para esse ambiente que maior parte do tráfego de front-end de saudação toohello back-end está bloqueada, esta regra especificamente permite DNS de qualquer sub-rede local.</span><span class="sxs-lookup"><span data-stu-id="850e7-227">For this environment most traffic from hello Frontend toohello Backend is blocked, this rule specifically allows DNS from any local subnet.</span></span>
  3. <span data-ttu-id="850e7-228">Subrede tooSubnet regra: essa regra é tooallow qualquer servidor na traseira Olá finalizar o servidor de tooany tooconnect sub-rede na sub-rede de front-end de saudação (mas não Olá inversa).</span><span class="sxs-lookup"><span data-stu-id="850e7-228">Subnet tooSubnet Rule: This rule is tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet (but not hello reverse).</span></span>
* <span data-ttu-id="850e7-229">Regra à prova de falhas (para o tráfego que não atendam a qualquer Olá acima):</span><span class="sxs-lookup"><span data-stu-id="850e7-229">Fail-safe Rule (for traffic that doesn’t meet any of hello above):</span></span>
  1. <span data-ttu-id="850e7-230">Negar todas as regras de tráfego: Isso deve ser sempre a regra final hello (em termos de prioridade) e como tal, se um tráfego passa falhará toomatch qualquer Olá anteriores serão removida por esta regra de regras.</span><span class="sxs-lookup"><span data-stu-id="850e7-230">Deny All Traffic Rule: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="850e7-231">Essa é uma regra padrão e normalmente é ativada; geralmente, não é necessário fazer qualquer modificação.</span><span class="sxs-lookup"><span data-stu-id="850e7-231">This is a default rule and usually activated, no modifications are generally needed.</span></span>

> [!TIP]
> <span data-ttu-id="850e7-232">Na segunda regra de tráfego de aplicativo hello, qualquer porta é permitida para fácil deste exemplo, em uma saudação cenário real mais específicos intervalos de porta e endereço devem ser superfície de ataque de saudação tooreduce usada dessa regra.</span><span class="sxs-lookup"><span data-stu-id="850e7-232">On hello second application traffic rule, any port is allowed for easy of this example, in a real scenario hello most specific port and address ranges should be used tooreduce hello attack surface of this rule.</span></span>
> 
> 

<br />

> [!IMPORTANT]
> <span data-ttu-id="850e7-233">Depois que todos os Olá acima regras são criados, é importante tooreview prioridade de saudação do tráfego de tooensure cada regra será permitida ou negada conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="850e7-233">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="850e7-234">Neste exemplo, as regras de saudação são em ordem de prioridade.</span><span class="sxs-lookup"><span data-stu-id="850e7-234">For this example, hello rules are in priority order.</span></span> <span data-ttu-id="850e7-235">É fácil toobe bloqueada fora do firewall Olá ordenados toomis regras de conclusão.</span><span class="sxs-lookup"><span data-stu-id="850e7-235">It's easy toobe locked out of hello firewall due toomis-ordered rules.</span></span> <span data-ttu-id="850e7-236">No mínimo, certifique-se de gerenciamento Olá firewall Olá em si é sempre absoluto regra de prioridade mais alta hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-236">At a minimum, ensure hello management for hello firewall itself is always hello absolute highest priority rule.</span></span>
> 
> 

### <a name="rule-prerequisites"></a><span data-ttu-id="850e7-237">Pré-requisitos de regra</span><span class="sxs-lookup"><span data-stu-id="850e7-237">Rule Prerequisites</span></span>
<span data-ttu-id="850e7-238">Um pré-requisito para o firewall do Olá Olá Máquina Virtual em execução são pontos de extremidade públicos.</span><span class="sxs-lookup"><span data-stu-id="850e7-238">One prerequisite for hello Virtual Machine running hello firewall are public endpoints.</span></span> <span data-ttu-id="850e7-239">Para o tráfego de tooprocess firewall Olá Olá pública pontos de extremidade apropriados devem ser abertos.</span><span class="sxs-lookup"><span data-stu-id="850e7-239">For hello firewall tooprocess traffic hello appropriate public endpoints must be open.</span></span> <span data-ttu-id="850e7-240">Há três tipos de tráfego neste exemplo; 1) gerenciamento tráfego toocontrol Olá firewall e as regras de firewall, servidores com windows hello 2) RDP tráfego toocontrol e tráfego de aplicativo de 3).</span><span class="sxs-lookup"><span data-stu-id="850e7-240">There are three types of traffic in this example; 1) Management traffic toocontrol hello firewall and firewall rules, 2) RDP traffic toocontrol hello windows servers, and 3) Application Traffic.</span></span> <span data-ttu-id="850e7-241">Esses são três colunas Olá dos tipos de tráfego em Olá superior metade da exibição lógica de regras de firewall Olá acima.</span><span class="sxs-lookup"><span data-stu-id="850e7-241">These are hello three columns of traffic types in hello upper half of logical view of hello firewall rules above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="850e7-242">Uma chave takeway aqui é tooremember que **todos os** tráfego virá através do firewall do hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-242">A key takeway here is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="850e7-243">Caso toohello desktop tooremote IIS01 server, mesmo que seja no serviço de nuvem Front End de saudação e na sub-rede Front-End de hello, tooaccess neste servidor precisaremos tooRDP toohello firewall na porta 8014 e permitir a solicitação RDP Olá firewall tooroute Olá internamente toohello IIS01 a porta de RDP.</span><span class="sxs-lookup"><span data-stu-id="850e7-243">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="850e7-244">saudação "Conectar" do portal do Azure botão não funcionará porque não há nenhum tooIIS01 de caminho direto RDP (quanto portal Olá pode ver).</span><span class="sxs-lookup"><span data-stu-id="850e7-244">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="850e7-245">Isso significa que todas as conexões de saudação internet serão toohello serviço de segurança e uma porta, por exemplo, secscv001.cloudapp.net:xxxx (Olá referência acima diagrama para mapeamento de saudação de porta externa e IP interno e porta).</span><span class="sxs-lookup"><span data-stu-id="850e7-245">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx (reference hello above diagram for hello mapping of External Port and Internal IP and Port).</span></span>
> 
> 

<span data-ttu-id="850e7-246">Um ponto de extremidade pode ser aberto no momento de saudação da criação de VM ou post compilação como é feito no script de exemplo hello e mostrado abaixo neste trecho de código (Observação; todos os itens que começam com um sinal de cifrão (por exemplo: $VMName[$i]) é uma variável definida pelo usuário do script Olá Olá referen seção CE deste documento.</span><span class="sxs-lookup"><span data-stu-id="850e7-246">An endpoint can be opened either at hello time of VM creation or post build as is done in hello example script and shown below in this code snippet (Note; any item beginning with a dollar sign (e.g.: $VMName[$i]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="850e7-247">Olá "$i" entre colchetes, [$i] representa número de matriz de saudação de uma VM específica em uma matriz de máquinas virtuais):</span><span class="sxs-lookup"><span data-stu-id="850e7-247">hello “$i” in brackets, [$i], represents hello array number of a specific VM in an array of VMs):</span></span>

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

<span data-ttu-id="850e7-248">Embora não claramente mostrado aqui devido toohello uso de variáveis, mas os pontos de extremidade são **somente** aberto em Olá segurança serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="850e7-248">Although not clearly shown here due toohello use of variables, but endpoints are **only** opened on hello Security Cloud Service.</span></span> <span data-ttu-id="850e7-249">Isso é que todo o tráfego é tratado de tooensure (roteadas, NAT tinha, descartado) por firewall hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-249">This is tooensure that all inbound traffic is handled (routed, NAT'd, dropped) by hello firewall.</span></span>

<span data-ttu-id="850e7-250">Um cliente de gerenciamento será necessário toobe instalado em um firewall de saudação do PC toomanage e criar configurações de saudação necessárias.</span><span class="sxs-lookup"><span data-stu-id="850e7-250">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="850e7-251">Consulte o fornecedor de documentação do seu firewall (ou outros NVA) Olá sobre como toomanage Olá dispositivo.</span><span class="sxs-lookup"><span data-stu-id="850e7-251">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="850e7-252">restante Olá esta seção e a próxima seção hello, criação de regras de Firewall, descrevem configuração Olá do firewall Olá em si, por meio do cliente de gerenciamento de fornecedores hello (ou seja, não Olá portal do Azure ou o PowerShell).</span><span class="sxs-lookup"><span data-stu-id="850e7-252">hello remainder of this section and hello next section, Firewall Rules Creation, will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="850e7-253">Instruções para download do cliente e conexão toohello Barracuda usado neste exemplo podem ser encontradas aqui: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="850e7-253">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="850e7-254">Depois de conectado no firewall hello, mas antes de criar regras de firewall, há duas classes de objeto de pré-requisito que podem facilitar criando regras de saudação; Objetos de serviço e de rede.</span><span class="sxs-lookup"><span data-stu-id="850e7-254">Once logged onto hello firewall but before creating firewall rules, there are two prerequisite object classes that can make creating hello rules easier; Network & Service objects.</span></span>

<span data-ttu-id="850e7-255">Neste exemplo, três objetos de rede nomeada devem ser definido (um para Olá front-end subrede e sub-rede de back-end hello, também um objeto de rede para o endereço IP de saudação do servidor DNS Olá).</span><span class="sxs-lookup"><span data-stu-id="850e7-255">For this example, three named network objects should be defined (one for hello Frontend subnet and hello Backend subnet, also a network object for hello IP address of hello DNS server).</span></span> <span data-ttu-id="850e7-256">toocreate uma rede nomeada. a partir do painel de cliente Barracuda NG Admin Olá, navegue toohello guia de configuração, no hello seção de configuração operacional Ruleset, em seguida, clique em "Redes" no menu de objetos de Firewall de saudação, clique novo no menu de editar redes Olá.</span><span class="sxs-lookup"><span data-stu-id="850e7-256">toocreate a named network; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Networks” under hello Firewall Objects menu, then click New in hello Edit Networks menu.</span></span> <span data-ttu-id="850e7-257">objeto de rede Olá agora pode ser criado, adicionando o nome de saudação e um prefixo de saudação:</span><span class="sxs-lookup"><span data-stu-id="850e7-257">hello network object can now be created, by adding hello name and hello prefix:</span></span>

<span data-ttu-id="850e7-258">![Criar um objeto de rede de front-end][3]</span><span class="sxs-lookup"><span data-stu-id="850e7-258">![Create a FrontEnd Network Object][3]</span></span>

<span data-ttu-id="850e7-259">Isso criará uma rede nomeada para a sub-rede de front-end hello, um objeto semelhante deve ser criado para a sub-rede de back-end Olá também.</span><span class="sxs-lookup"><span data-stu-id="850e7-259">This will create a named network for hello FrontEnd subnet, a similar object should be created for hello BackEnd subnet as well.</span></span> <span data-ttu-id="850e7-260">Agora sub-redes Olá podem ser mais facilmente referenciadas por nome nas regras de firewall de saudação.</span><span class="sxs-lookup"><span data-stu-id="850e7-260">Now hello subnets can be more easily referenced by name in hello firewall rules.</span></span>

<span data-ttu-id="850e7-261">Para Olá objeto do servidor DNS:</span><span class="sxs-lookup"><span data-stu-id="850e7-261">For hello DNS Server Object:</span></span>

<span data-ttu-id="850e7-262">![Criar um objeto de servidor DNS][4]</span><span class="sxs-lookup"><span data-stu-id="850e7-262">![Create a DNS Server Object][4]</span></span>

<span data-ttu-id="850e7-263">Essa referência de endereço IP único será usada em uma regra DNS documento hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-263">This single IP address reference will be utilized in a DNS rule later in hello document.</span></span>

<span data-ttu-id="850e7-264">objetos de pré-requisito segundo Olá são objetos de serviços.</span><span class="sxs-lookup"><span data-stu-id="850e7-264">hello second prerequisite objects are Services objects.</span></span> <span data-ttu-id="850e7-265">Eles representarão portas de conexão de RDP Olá para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="850e7-265">These will represent hello RDP connection ports for each server.</span></span> <span data-ttu-id="850e7-266">Como o objeto de serviço RDP existente Olá é porta do RDP padrão toohello associada, 3389, novos serviços podem ser criados tooallow tráfego de portas externas de saudação (8014 8026).</span><span class="sxs-lookup"><span data-stu-id="850e7-266">Since hello existing RDP service object is bound toohello default RDP port, 3389, new Services can be created tooallow traffic from hello external ports (8014-8026).</span></span> <span data-ttu-id="850e7-267">novas portas de saudação também podem ser adicionadas toohello serviço RDP existente, mas, para facilitar a demonstração, uma regra individual para cada servidor pode ser criada.</span><span class="sxs-lookup"><span data-stu-id="850e7-267">hello new ports could also be added toohello existing RDP service, but for ease of demonstration, an individual rule for each server can be created.</span></span> <span data-ttu-id="850e7-268">toocreate uma nova regra RDP para um servidor. a partir do painel de cliente do hello Barracuda NG administrador, navegue toohello guia de configuração, no hello configuração operacional seção clique Ruleset, em seguida, clique em "Serviços" em Olá menu objetos de Firewall, role para baixo Olá lista de serviços e selecione Olá Serviço de "RDP".</span><span class="sxs-lookup"><span data-stu-id="850e7-268">toocreate a new RDP rule for a server; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Services” under hello Firewall Objects menu, scroll down hello list of services and select hello “RDP” service.</span></span> <span data-ttu-id="850e7-269">Com o botão direito do mouse e selecione copiar, então clique com botão direito do mouse e selecione Colar.</span><span class="sxs-lookup"><span data-stu-id="850e7-269">Right-click and select copy, then right-click and select Paste.</span></span> <span data-ttu-id="850e7-270">Agora há um Objeto de Serviço RDP-Copy1 que pode ser editado.</span><span class="sxs-lookup"><span data-stu-id="850e7-270">There is now a RDP-Copy1 Service Object that can be edited.</span></span> <span data-ttu-id="850e7-271">Com o botão direito Copy1 RDP e selecione Editar, Olá Editar objeto de serviço janela será exibida, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="850e7-271">Right-click RDP-Copy1 and select Edit, hello Edit Service Object window will pop up as shown here:</span></span>

<span data-ttu-id="850e7-272">![Cópia de regra RDP padrão][5]</span><span class="sxs-lookup"><span data-stu-id="850e7-272">![Copy of Default RDP Rule][5]</span></span>

<span data-ttu-id="850e7-273">valores Hello, em seguida, podem ser editado toorepresent Olá serviço RDP para um servidor específico.</span><span class="sxs-lookup"><span data-stu-id="850e7-273">hello values can then be edited toorepresent hello RDP service for a specific server.</span></span> <span data-ttu-id="850e7-274">Para AppVM01 Olá acima padrão regra RDP deve ser modificado tooreflect um novo serviço de nome, descrição, e a porta externa do RDP usado em Olá diagrama Figura 8 (Observação: Olá portas são alterados saudação padrão RDP 3389 porta externa toohello que está sendo usado para isso um servidor específico, no caso de saudação de porta externa do AppVM01 Olá é 8025) hello serviço modificado é mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="850e7-274">For AppVM01 hello above default RDP rule should be modified tooreflect a new Service Name, Description, and external RDP Port used in hello Figure 8 diagram (Note: hello ports are changed from hello RDP default of 3389 toohello external port being used for this specific server, in hello case of AppVM01 hello external Port is 8025) hello modified service is shown below:</span></span>

<span data-ttu-id="850e7-275">![Regra de AppVM01][6]</span><span class="sxs-lookup"><span data-stu-id="850e7-275">![AppVM01 Rule][6]</span></span>

<span data-ttu-id="850e7-276">Esse processo deve ser repetido toocreate serviços de RDP para Olá restantes servidores; AppVM02, DNS01 e IIS01.</span><span class="sxs-lookup"><span data-stu-id="850e7-276">This process must be repeated toocreate RDP Services for hello remaining servers; AppVM02, DNS01, and IIS01.</span></span> <span data-ttu-id="850e7-277">criação de saudação desses serviços fará a criação da regra Olá mais simples e mais óbvio na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="850e7-277">hello creation of these Services will make hello Rule creation simpler and more obvious in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="850e7-278">Um serviço RDP para Olá Firewall não é necessário por duas razões. 1) o primeiro firewall de saudação VM é uma imagem de baseadas em Linux para SSH seria usada na porta 22 para gerenciamento de VM em vez de RDP e 2) a porta 22 e duas portas de gerenciamento são permitidas na regra de gerenciamento primeiro Olá descrita abaixo tooallow para conectividade de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="850e7-278">An RDP service for hello Firewall is not needed for two reasons; 1) first hello firewall VM is a Linux based image so SSH would be used on port 22 for VM management instead of RDP, and 2) port 22, and two other management ports are allowed in hello first management rule described below tooallow for management connectivity.</span></span>
> 
> 

### <a name="firewall-rules-creation"></a><span data-ttu-id="850e7-279">Criação de regras de firewall</span><span class="sxs-lookup"><span data-stu-id="850e7-279">Firewall Rules Creation</span></span>
<span data-ttu-id="850e7-280">Há três tipos de regras de firewall usadas neste exemplo, todas elas têm ícones distintos:</span><span class="sxs-lookup"><span data-stu-id="850e7-280">There are three types of firewall rules used in this example, they all have distinct icons:</span></span>

<span data-ttu-id="850e7-281">uma regra de redirecionamento do aplicativo Hello: ![ícone de redirecionamento do aplicativo][7]</span><span class="sxs-lookup"><span data-stu-id="850e7-281">hello Application Redirect rule: ![Application Redirect Icon][7]</span></span>

<span data-ttu-id="850e7-282">regra de NAT de destino Olá: ![ícone de NAT de destino][8]</span><span class="sxs-lookup"><span data-stu-id="850e7-282">hello Destination NAT rule: ![Destination NAT Icon][8]</span></span>

<span data-ttu-id="850e7-283">regra de passagem Olá: ![passar ícone][9]</span><span class="sxs-lookup"><span data-stu-id="850e7-283">hello Pass rule: ![Pass Icon][9]</span></span>

<span data-ttu-id="850e7-284">Obter mais informações sobre essas regras podem ser encontradas no site de Barracuda hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-284">More information on these rules can be found at hello Barracuda web site.</span></span>

<span data-ttu-id="850e7-285">toocreate Olá regras a seguir (ou verifique se as regras padrão existente), a partir do painel de cliente Barracuda NG Admin hello, navegue toohello guia de configuração, no hello configuração operacional clique Ruleset.</span><span class="sxs-lookup"><span data-stu-id="850e7-285">toocreate hello following rules (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="850e7-286">Chamado em uma grade, "Principal regras" mostrará Olá existente regras ativadas e desativadas esse firewall.</span><span class="sxs-lookup"><span data-stu-id="850e7-286">A grid called, “Main Rules” will show hello existing active and deactivated rules on this firewall.</span></span> <span data-ttu-id="850e7-287">No canto superior direito de saudação desta grade é uma pequena verde "+", clique neste toocreate uma nova regra (Observação: o firewall pode ser "bloqueado" para que as alterações, se você vir um botão marcado "Bloqueio" e são toocreate não é possível ou editar regras, clique neste botão muito "desbloquear" hello se regra t e permitir a edição).</span><span class="sxs-lookup"><span data-stu-id="850e7-287">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello rule set and allow editing).</span></span> <span data-ttu-id="850e7-288">Se você quiser tooedit uma regra existente, selecione essa regra, clique com botão direito e selecione Editar regra.</span><span class="sxs-lookup"><span data-stu-id="850e7-288">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="850e7-289">Depois que as regras são criadas e/ou modificadas, eles devem ser enviados por push toohello firewall e, em seguida, ativado, se isso não for feito regra Olá alterações não entrarão em vigor.</span><span class="sxs-lookup"><span data-stu-id="850e7-289">Once your rules are created and/or modified, they must be pushed toohello firewall and then activated, if this is not done hello rule changes will not take effect.</span></span> <span data-ttu-id="850e7-290">processo de envio e a ativação de saudação é descrito abaixo as descrições de regras de detalhes de saudação.</span><span class="sxs-lookup"><span data-stu-id="850e7-290">hello push and activation process is described below hello details rule descriptions.</span></span>

<span data-ttu-id="850e7-291">especificações de saudação de cada regra necessária toocomplete neste exemplo são descritas da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="850e7-291">hello specifics of each rule required toocomplete this example are described as follows:</span></span>

* <span data-ttu-id="850e7-292">**Gerenciamento de regra de firewall**: este aplicativo de redirecionamento regra permite o tráfego toopass toohello as portas de gerenciamento do dispositivo virtual do hello rede, neste exemplo, um Firewall de NextGen Barracuda.</span><span class="sxs-lookup"><span data-stu-id="850e7-292">**Firewall Management Rule**: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance, in this example a Barracuda NextGen Firewall.</span></span> <span data-ttu-id="850e7-293">as portas de gerenciamento Olá são 801, 807 e, opcionalmente, 22.</span><span class="sxs-lookup"><span data-stu-id="850e7-293">hello management ports are 801, 807 and optionally 22.</span></span> <span data-ttu-id="850e7-294">portas de saudação internos e externos são Olá mesmo (ou seja, nenhuma conversão de porta).</span><span class="sxs-lookup"><span data-stu-id="850e7-294">hello external and internal ports are hello same (i.e. no port translation).</span></span> <span data-ttu-id="850e7-295">Essa regra, SETUP-MGMT-ACCESS, é uma regra padrão e é habilitada por padrão (no Firewall NextGen Barracuda versão 6.1).</span><span class="sxs-lookup"><span data-stu-id="850e7-295">This rule, SETUP-MGMT-ACCESS, is a default rule and enabled by default (in Barracuda NextGen Firewall version 6.1).</span></span>
  
    <span data-ttu-id="850e7-296">![Regra de gerenciamento de firewall][10]</span><span class="sxs-lookup"><span data-stu-id="850e7-296">![Firewall Management Rule][10]</span></span>

> [!TIP]
> <span data-ttu-id="850e7-297">Olá espaço de endereço de origem nesta regra é qualquer, se hello intervalos de endereços IP de gerenciamento são conhecidos, reduzindo a este escopo também reduziria Olá portas de gerenciamento de toohello superfície de ataque.</span><span class="sxs-lookup"><span data-stu-id="850e7-297">hello source address space in this rule is Any, if hello management IP address ranges are known, reducing this scope would also reduce hello attack surface toohello management ports.</span></span>
> 
> 

* <span data-ttu-id="850e7-298">**Regras de RDP**: regras de NAT de destino esses serão permitir o gerenciamento de saudação servidores individuais via RDP.</span><span class="sxs-lookup"><span data-stu-id="850e7-298">**RDP Rules**:  These Destination NAT rules will allow management of hello individual servers via RDP.</span></span>
  <span data-ttu-id="850e7-299">Há quatro toocreate de campos crítica necessário esta regra:</span><span class="sxs-lookup"><span data-stu-id="850e7-299">There are four critical fields needed toocreate this rule:</span></span>
  
  1. <span data-ttu-id="850e7-300">Origem – tooallow RDP de qualquer lugar, referência hello "Qualquer" é usado no campo de origem hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-300">Source – tooallow RDP from anywhere, hello reference “Any” is used in hello Source field.</span></span>
  2. <span data-ttu-id="850e7-301">Serviço – usar Olá objeto apropriado de serviço criado anteriormente, neste caso "AppVM01 RDP", portas externas Olá redirecionam toohello endereço IP do local de servidores e tooport 3386 (porta RDP padrão Olá).</span><span class="sxs-lookup"><span data-stu-id="850e7-301">Service – use hello appropriate Service Object created earlier, in this case “AppVM01 RDP”, hello external ports redirect toohello servers local IP address and tooport 3386 (hello default RDP port).</span></span> <span data-ttu-id="850e7-302">Essa regra específica é para tooAppVM01 de acesso RDP.</span><span class="sxs-lookup"><span data-stu-id="850e7-302">This specific rule is for RDP access tooAppVM01.</span></span>
  3. <span data-ttu-id="850e7-303">Destino – deve ser Olá *local porta no firewall Olá*, "IP Local do DHCP 1" ou eth0 se usando IPs estáticos.</span><span class="sxs-lookup"><span data-stu-id="850e7-303">Destination – should be hello *local port on hello firewall*, “DCHP 1 Local IP” or eth0 if using static IPs.</span></span> <span data-ttu-id="850e7-304">Olá um número ordinal (eth0, eth1, etc.) pode ser diferente se o dispositivo de rede tem várias interfaces de locais.</span><span class="sxs-lookup"><span data-stu-id="850e7-304">hello ordinal number (eth0, eth1, etc) may be different if your network appliance has multiple local interfaces.</span></span> <span data-ttu-id="850e7-305">Essa porta Olá é firewall Olá envia de (pode ser Olá mesmo como Olá porta de recebimento), Olá destino de roteados real é no campo de lista de destino hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-305">This is hello port hello firewall is sending out from (may be hello same as hello receiving port), hello actual routed destination is in hello Target List field.</span></span>
  4. <span data-ttu-id="850e7-306">Redirecionamento – esta seção informa o dispositivo virtual Olá onde tooultimately redirecionar esse tráfego.</span><span class="sxs-lookup"><span data-stu-id="850e7-306">Redirection – this section tells hello virtual appliance where tooultimately redirect this traffic.</span></span> <span data-ttu-id="850e7-307">redirecionamento mais simples de saudação é tooplace Olá IP e porta (opcional) no campo da lista de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="850e7-307">hello simplest redirection is tooplace hello IP and Port (optional) in hello Target List field.</span></span> <span data-ttu-id="850e7-308">Se nenhuma porta é a porta de destino de saudação usado na solicitação de entrada hello será usado (ie nenhuma tradução), se uma porta designada porta Olá também será NAT junto com IP hello tratar.</span><span class="sxs-lookup"><span data-stu-id="850e7-308">If no port is used hello destination port on hello inbound request will be used (ie no translation), if a port is designated hello port will also be NAT’d along with hello IP address.</span></span>
     
     <span data-ttu-id="850e7-309">![Regra RDP do firewall][11]</span><span class="sxs-lookup"><span data-stu-id="850e7-309">![Firewall RDP Rule][11]</span></span>
     
     <span data-ttu-id="850e7-310">Um total de quatro regras RDP precisará toobe criado:</span><span class="sxs-lookup"><span data-stu-id="850e7-310">A total of four RDP rules will need toobe created:</span></span> 
     
     | <span data-ttu-id="850e7-311">Nome da Regra</span><span class="sxs-lookup"><span data-stu-id="850e7-311">Rule Name</span></span> | <span data-ttu-id="850e7-312">Servidor</span><span class="sxs-lookup"><span data-stu-id="850e7-312">Server</span></span> | <span data-ttu-id="850e7-313">O Barramento de</span><span class="sxs-lookup"><span data-stu-id="850e7-313">Service</span></span> | <span data-ttu-id="850e7-314">Lista de destino</span><span class="sxs-lookup"><span data-stu-id="850e7-314">Target List</span></span> |
     | --- | --- | --- | --- |
     | <span data-ttu-id="850e7-315">RDP-para-IIS01</span><span class="sxs-lookup"><span data-stu-id="850e7-315">RDP-to-IIS01</span></span> |<span data-ttu-id="850e7-316">IIS01</span><span class="sxs-lookup"><span data-stu-id="850e7-316">IIS01</span></span> |<span data-ttu-id="850e7-317">RDP de IIS01</span><span class="sxs-lookup"><span data-stu-id="850e7-317">IIS01 RDP</span></span> |<span data-ttu-id="850e7-318">10.0.1.4:3389</span><span class="sxs-lookup"><span data-stu-id="850e7-318">10.0.1.4:3389</span></span> |
     | <span data-ttu-id="850e7-319">RDP-para-DNS01</span><span class="sxs-lookup"><span data-stu-id="850e7-319">RDP-to-DNS01</span></span> |<span data-ttu-id="850e7-320">DNS01</span><span class="sxs-lookup"><span data-stu-id="850e7-320">DNS01</span></span> |<span data-ttu-id="850e7-321">RDP de DNS01</span><span class="sxs-lookup"><span data-stu-id="850e7-321">DNS01 RDP</span></span> |<span data-ttu-id="850e7-322">10.0.2.4:3389</span><span class="sxs-lookup"><span data-stu-id="850e7-322">10.0.2.4:3389</span></span> |
     | <span data-ttu-id="850e7-323">RDP-para-AppVM01</span><span class="sxs-lookup"><span data-stu-id="850e7-323">RDP-to-AppVM01</span></span> |<span data-ttu-id="850e7-324">AppVM01</span><span class="sxs-lookup"><span data-stu-id="850e7-324">AppVM01</span></span> |<span data-ttu-id="850e7-325">RDP de AppVM01</span><span class="sxs-lookup"><span data-stu-id="850e7-325">AppVM01 RDP</span></span> |<span data-ttu-id="850e7-326">10.0.2.5:3389</span><span class="sxs-lookup"><span data-stu-id="850e7-326">10.0.2.5:3389</span></span> |
     | <span data-ttu-id="850e7-327">RDP-para-AppVM02</span><span class="sxs-lookup"><span data-stu-id="850e7-327">RDP-to-AppVM02</span></span> |<span data-ttu-id="850e7-328">AppVM02</span><span class="sxs-lookup"><span data-stu-id="850e7-328">AppVM02</span></span> |<span data-ttu-id="850e7-329">RDP de AppVm02</span><span class="sxs-lookup"><span data-stu-id="850e7-329">AppVm02 RDP</span></span> |<span data-ttu-id="850e7-330">10.0.2.6:3389</span><span class="sxs-lookup"><span data-stu-id="850e7-330">10.0.2.6:3389</span></span> |

> [!TIP]
> <span data-ttu-id="850e7-331">Limitar escopo Olá Olá fonte e campos de serviço pode reduzir a superfície de ataque de saudação.</span><span class="sxs-lookup"><span data-stu-id="850e7-331">Narrowing down hello scope of hello Source and Service fields will reduce hello attack surface.</span></span> <span data-ttu-id="850e7-332">escopo de Hello mais limitada que permitirá que a funcionalidade deve ser usado.</span><span class="sxs-lookup"><span data-stu-id="850e7-332">hello most limited scope that will allow functionality should be used.</span></span>
> 
> 

* <span data-ttu-id="850e7-333">**Regras de tráfego do aplicativo**: há duas regras de tráfego do aplicativo, Olá primeiro para o tráfego de web de front-end hello e Olá segundo para o tráfego de back-end da saudação (por exemplo, servidor toodata camada da web).</span><span class="sxs-lookup"><span data-stu-id="850e7-333">**Application Traffic Rules**: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="850e7-334">Essas regras dependerá da arquitetura de rede de saudação (em que os servidores são colocados) e fluxos de tráfego (fluxos de tráfego que Olá direção e quais portas são usadas).</span><span class="sxs-lookup"><span data-stu-id="850e7-334">These rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
  
    <span data-ttu-id="850e7-335">Primeiro discutido é a regra de front-end de saudação para tráfego da web:</span><span class="sxs-lookup"><span data-stu-id="850e7-335">First discussed is hello front end rule for web traffic:</span></span>
  
    <span data-ttu-id="850e7-336">![Regra Web do firewall][12]</span><span class="sxs-lookup"><span data-stu-id="850e7-336">![Firewall Web Rule][12]</span></span>
  
    <span data-ttu-id="850e7-337">Esta regra NAT de destino permite que o servidor de aplicativos do hello aplicativo real tráfego tooreach hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-337">This Destination NAT rule allows hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="850e7-338">Enquanto hello outras regras permitirem segurança, gerenciamento, etc., regras de aplicativo são o que permite que tooaccess de usuários ou serviços externos Olá aplicativo (s).</span><span class="sxs-lookup"><span data-stu-id="850e7-338">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="850e7-339">Neste exemplo, há um único servidor web na porta 80, assim, Olá única aplicativo regra de firewall será redirecionado IP externo do tráfego de entrada toohello, toohello web interno endereço IP de servidores.</span><span class="sxs-lookup"><span data-stu-id="850e7-339">For this example, there is a single web server on port 80, thus hello single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span>
  
    <span data-ttu-id="850e7-340">**Observação**: que não há nenhuma porta atribuída no campo da lista de destino de saudação, assim, hello entrada porta 80 (ou 443 para Olá serviço selecionado) será usado no redirecionamento de saudação do servidor de web hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-340">**Note**: that there is no port assigned in hello Target List field, thus hello inbound port 80 (or 443 for hello Service selected) will be used in hello redirection of hello web server.</span></span> <span data-ttu-id="850e7-341">Se o servidor de web hello está escutando em uma porta diferente, por exemplo, porta 8080; campo da lista de destino Olá pode ser tooallow too10.0.1.4:8080 atualizado para o redirecionamento de porta Olá também.</span><span class="sxs-lookup"><span data-stu-id="850e7-341">If hello web server is listening on a different port, for example port 8080, hello Target List field could be updated too10.0.1.4:8080 tooallow for hello Port redirection as well.</span></span>
  
    <span data-ttu-id="850e7-342">Olá próxima regra de tráfego do aplicativo é Olá back-end regra tooallow Olá Web tootalk toohello AppVM01 servidor (mas não AppVM02) por meio de qualquer serviço:</span><span class="sxs-lookup"><span data-stu-id="850e7-342">hello next Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via Any service:</span></span>
  
    <span data-ttu-id="850e7-343">![Regra da AppVM01 do firewall][13]</span><span class="sxs-lookup"><span data-stu-id="850e7-343">![Firewall AppVM01 Rule][13]</span></span>
  
    <span data-ttu-id="850e7-344">Essa regra de passagem permite que qualquer servidor IIS em Olá front-end subrede tooreach Olá AppVM01 (endereço IP 10.0.2.5) em qualquer porta, usando os dados de tooaccess de protocolo exigidos pelo aplicativo da web hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-344">This Pass rule allows any IIS server on hello Frontend subnet tooreach hello AppVM01 (IP Address 10.0.2.5) on Any port, using any Protocol tooaccess data needed by hello web application.</span></span>
  
    <span data-ttu-id="850e7-345">Esta captura de tela um "\<explícita dest\>" é usado em toosignify de campo de destino Olá 10.0.2.5 como destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="850e7-345">In this screen shot an "\<explicit-dest\>" is used in hello Destination field toosignify 10.0.2.5 as hello destination.</span></span> <span data-ttu-id="850e7-346">Isso pode ser chamada explícita conforme mostrado, ou um objeto de rede (como foi feito nos pré-requisitos Olá para o servidor DNS de saudação).</span><span class="sxs-lookup"><span data-stu-id="850e7-346">This could be either explicit as shown or a named Network Object (as was done in hello prerequisites for hello DNS server).</span></span> <span data-ttu-id="850e7-347">Isso é administrador toohello do firewall hello como método toowhich será usado.</span><span class="sxs-lookup"><span data-stu-id="850e7-347">This is up toohello administrator of hello firewall as toowhich method will be used.</span></span> <span data-ttu-id="850e7-348">tooadd 10.0.2.5 como um Explict Desitnation, clique duas vezes na primeira linha em branco Olá em \<explícita dest\> e insira o endereço de saudação na janela Olá pop-up.</span><span class="sxs-lookup"><span data-stu-id="850e7-348">tooadd 10.0.2.5 as an Explict Desitnation, double-click on hello first blank row under \<explicit-dest\> and enter hello address in hello window that pops up.</span></span>
  
    <span data-ttu-id="850e7-349">Com essa regra passar, nenhum NAT é necessária porque esse é o tráfego interno, portanto, Olá método de Conexão pode ser definido muito "Não SNAT".</span><span class="sxs-lookup"><span data-stu-id="850e7-349">With this Pass Rule, no NAT is needed since this is internal traffic, so hello Connection Method can be set too"No SNAT".</span></span>
  
    <span data-ttu-id="850e7-350">**Observação**: rede de origem Olá nesta regra é qualquer recurso na sub-rede de front-end hello, se haverá apenas um, ou um número específico conhecido dos servidores web, o recurso pode ser um objeto de rede criada toobe mais toothose exatos endereços IP específicos, em vez de Olá todo front-end subrede.</span><span class="sxs-lookup"><span data-stu-id="850e7-350">**Note**: hello Source network in this rule is any resource on hello FrontEnd subnet, if there will only be one, or a known specific number of web servers, a Network Object resource could be created toobe more specific toothose exact IP addresses instead of hello entire Frontend subnet.</span></span>

> [!TIP]
> <span data-ttu-id="850e7-351">Esta regra usa o serviço hello "Qualquer" toomake Olá toosetup mais fácil de aplicativo de exemplo e usar, também poderá ICMPv4 (ping) em uma única regra.</span><span class="sxs-lookup"><span data-stu-id="850e7-351">This rule uses hello service “Any” toomake hello sample application easier toosetup and use, this will also allow ICMPv4 (ping) in a single rule.</span></span> <span data-ttu-id="850e7-352">No entanto, essa não é uma prática recomendada.</span><span class="sxs-lookup"><span data-stu-id="850e7-352">However, this is not a recommended practice.</span></span> <span data-ttu-id="850e7-353">Olá protocolos e portas e ("serviços") devem ser restrita toohello possível mínimo que permite a superfície de ataque do aplicativo operação tooreduce Olá entre esse limite.</span><span class="sxs-lookup"><span data-stu-id="850e7-353">hello ports and protocols (“Services”) should be narrowed toohello minimum possible that allows application operation tooreduce hello attack surface across this boundary.</span></span>
> 
> 

<br />

> [!TIP]
> <span data-ttu-id="850e7-354">Embora essa regra mostra uma referência explícita dest que está sendo usada, uma abordagem consistente deve ser usada em toda a configuração do firewall hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-354">Although this rule shows an explicit-dest reference being used, a consistent approach should be used throughout hello firewall configuration.</span></span> <span data-ttu-id="850e7-355">É recomendável que Olá objeto de rede denominado ser usadas em toda para facilitar a legibilidade e capacidade de suporte.</span><span class="sxs-lookup"><span data-stu-id="850e7-355">It is recommended that hello named Network Object be used throughout for easier readability and supportability.</span></span> <span data-ttu-id="850e7-356">Olá dest explícito é usado aqui tooshow de apenas um método alternativo de referência e geralmente não é recomendado (especialmente para configurações complexas).</span><span class="sxs-lookup"><span data-stu-id="850e7-356">hello explicit-dest is used here only tooshow an alternative reference method and is not generally recommended (especially for complex configurations).</span></span>
> 
> 

* <span data-ttu-id="850e7-357">**Regra de saída tooInternet**: passar essa regra permitirá que o tráfego de redes de destino qualquer origem rede toopass toohello selecionado.</span><span class="sxs-lookup"><span data-stu-id="850e7-357">**Outbound tooInternet Rule**: This Pass rule will allow traffic from any Source network toopass toohello selected Destination networks.</span></span> <span data-ttu-id="850e7-358">Essa regra é uma regra padrão geralmente já firewall Barracuda NextGen de saudação, mas está em um estado desabilitado.</span><span class="sxs-lookup"><span data-stu-id="850e7-358">This rule is a default rule usually already on hello Barracuda NextGen firewall, but is in a disabled state.</span></span> <span data-ttu-id="850e7-359">Clicando duas vezes em que essa regra podem acessar o comando de ativar a regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="850e7-359">Right-clicking on this rule can access hello Activate Rule command.</span></span> <span data-ttu-id="850e7-360">regra de saudação mostrada aqui foi modificado tooadd Olá duas sub-redes locais que foram criadas como referências na seção de pré-requisitos Olá este documento toohello do atributo de origem dessa regra.</span><span class="sxs-lookup"><span data-stu-id="850e7-360">hello rule shown here has been modified tooadd hello two local subnets that were created as references in hello prerequisite section of this document toohello Source attribute of this rule.</span></span>
  
    <span data-ttu-id="850e7-361">![Regra de saída do firewall][14]</span><span class="sxs-lookup"><span data-stu-id="850e7-361">![Firewall Outbound Rule][14]</span></span>
* <span data-ttu-id="850e7-362">**Regra de DNS**: passar essa regra permite que somente o DNS (porta 53) tráfego toopass toohello servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="850e7-362">**DNS Rule**: This Pass rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="850e7-363">Para esse ambiente que maior parte do tráfego de front-end de saudação toohello back-end está bloqueada, esta regra permite especificamente DNS.</span><span class="sxs-lookup"><span data-stu-id="850e7-363">For this environment most traffic from hello FrontEnd toohello BackEnd is blocked, this rule specifically allows DNS.</span></span>
  
    <span data-ttu-id="850e7-364">![Regra DNS do firewall][15]</span><span class="sxs-lookup"><span data-stu-id="850e7-364">![Firewall DNS Rule][15]</span></span>
  
    <span data-ttu-id="850e7-365">**Observação**: nesta tela hello captura o método de Conexão está incluído.</span><span class="sxs-lookup"><span data-stu-id="850e7-365">**Note**: In this screen shot hello Connection Method is included.</span></span> <span data-ttu-id="850e7-366">Como essa regra é para o tráfego de endereços IP do interno IP toointernal, nenhum NATing é necessária, este Olá método de Conexão está definido muito "Não SNAT" para esta regra de passagem.</span><span class="sxs-lookup"><span data-stu-id="850e7-366">Because this rule is for internal IP toointernal IP address traffic, no NATing is required, this hello Connection Method is set too“No SNAT” for this Pass rule.</span></span>
* <span data-ttu-id="850e7-367">**Subrede tooSubnet regra**: passar essa regra é uma regra padrão que foi ativada e modificado tooallow qualquer servidor em volta Olá terminar server de tooany tooconnect sub-rede em Olá sub-rede front-end.</span><span class="sxs-lookup"><span data-stu-id="850e7-367">**Subnet tooSubnet Rule**: This Pass rule is a default rule that has been activated and modified tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet.</span></span> <span data-ttu-id="850e7-368">Essa regra é o tráfego interno de todos os para que Olá método de Conexão pode ser definido como tooNo SNAT.</span><span class="sxs-lookup"><span data-stu-id="850e7-368">This rule is all internal traffic so hello Connection Method can be set tooNo SNAT.</span></span>
  
    <span data-ttu-id="850e7-369">![Regra IntraVNet do firewall][16]</span><span class="sxs-lookup"><span data-stu-id="850e7-369">![Firewall Intra-VNet Rule][16]</span></span>
  
    <span data-ttu-id="850e7-370">**Observação**: Olá bidirecional de caixa de seleção não estiver marcada (nem é marcado na maioria das regras), isso é significativo para essa regra em que ele faz isso regra "única direção", que pode ser iniciada uma conexão de rede de front-end do toohello de sub-rede de back-end Olá, mas não Olá inversa.</span><span class="sxs-lookup"><span data-stu-id="850e7-370">**Note**: hello Bi-directional checkbox is not checked (nor is it checked in most rules), this is significant for this rule in that it makes this rule “one directional”, a connection can be initiated from hello back end subnet toohello front end network, but not hello reverse.</span></span> <span data-ttu-id="850e7-371">Se essa caixa de seleção tiver sido marcada, essa regra permitirá o tráfego bidirecional, o que não é desejável em nosso diagrama lógico.</span><span class="sxs-lookup"><span data-stu-id="850e7-371">If that checkbox was checked, this rule would enable bi-directional traffic, which from our logical diagram is not desired.</span></span>
* <span data-ttu-id="850e7-372">**Negar todas as regras de tráfego**: deve ser a regra final hello (em termos de prioridade) e como tal, se um tráfego que flui toomatch falhar qualquer Olá anterior regras será removido por essa regra.</span><span class="sxs-lookup"><span data-stu-id="850e7-372">**Deny All Traffic Rule**: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="850e7-373">Essa é uma regra padrão e normalmente é ativada; geralmente, não é necessário fazer qualquer modificação.</span><span class="sxs-lookup"><span data-stu-id="850e7-373">This is a default rule and usually activated, no modifications are generally needed.</span></span> 
  
    <span data-ttu-id="850e7-374">![Regra Negar do firewall][17]</span><span class="sxs-lookup"><span data-stu-id="850e7-374">![Firewall Deny Rule][17]</span></span>

> [!IMPORTANT]
> <span data-ttu-id="850e7-375">Depois que todos os Olá acima regras são criados, é importante tooreview prioridade de saudação do tráfego de tooensure cada regra será permitida ou negada conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="850e7-375">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="850e7-376">Neste exemplo, regras de saudação estão na ordem de saudação que devem ser exibidos no hello grade principal de regras em Olá Barracuda cliente de gerenciamento de encaminhamento.</span><span class="sxs-lookup"><span data-stu-id="850e7-376">For this example, hello rules are in hello order they should appear in hello Main Grid of forwarding rules in hello Barracuda Management Client.</span></span>
> 
> 

## <a name="rule-activation"></a><span data-ttu-id="850e7-377">Ativação da regra</span><span class="sxs-lookup"><span data-stu-id="850e7-377">Rule Activation</span></span>
<span data-ttu-id="850e7-378">Com a especificação de toohello Olá ruleset modificado de diagrama lógico de hello, Olá ruleset deve ser carregado toohello firewall e, em seguida, ativado.</span><span class="sxs-lookup"><span data-stu-id="850e7-378">With hello ruleset modified toohello specification of hello logic diagram, hello ruleset must be uploaded toohello firewall and then activated.</span></span>

<span data-ttu-id="850e7-379">![Ativação de regra de firewall][18]</span><span class="sxs-lookup"><span data-stu-id="850e7-379">![Firewall Rule Activation][18]</span></span>

<span data-ttu-id="850e7-380">No canto superior direito de saudação do cliente de gerenciamento de saudação são um cluster de botões.</span><span class="sxs-lookup"><span data-stu-id="850e7-380">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="850e7-381">Olá "enviar alterações" botão toosend Olá modificado regras toohello firewall, clique botão de "Ativar" hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-381">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="850e7-382">Com a ativação de saudação do conjunto de regras de firewall Olá esta compilação do ambiente de exemplo foi concluída.</span><span class="sxs-lookup"><span data-stu-id="850e7-382">With hello activation of hello firewall ruleset this example environment build is complete.</span></span>

## <a name="traffic-scenarios"></a><span data-ttu-id="850e7-383">Cenários de tráfego</span><span class="sxs-lookup"><span data-stu-id="850e7-383">Traffic Scenarios</span></span>
> [!IMPORTANT]
> <span data-ttu-id="850e7-384">Uma chave takeway é tooremember que **todos os** tráfego virá através do firewall do hello.</span><span class="sxs-lookup"><span data-stu-id="850e7-384">A key takeway is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="850e7-385">Caso toohello desktop tooremote IIS01 server, mesmo que seja no serviço de nuvem Front End de saudação e na sub-rede Front-End de hello, tooaccess neste servidor precisaremos tooRDP toohello firewall na porta 8014 e permitir a solicitação RDP Olá firewall tooroute Olá internamente toohello IIS01 a porta de RDP.</span><span class="sxs-lookup"><span data-stu-id="850e7-385">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="850e7-386">saudação "Conectar" do portal do Azure botão não funcionará porque não há nenhum tooIIS01 de caminho direto RDP (quanto portal Olá pode ver).</span><span class="sxs-lookup"><span data-stu-id="850e7-386">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="850e7-387">Isso significa que todas as conexões de saudação internet serão toohello serviço de segurança e uma porta, por exemplo, secscv001.cloudapp.net:xxxx.</span><span class="sxs-lookup"><span data-stu-id="850e7-387">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx.</span></span>
> 
> 

<span data-ttu-id="850e7-388">Para esses cenários, Olá seguindo as regras de firewall deve estar em vigor:</span><span class="sxs-lookup"><span data-stu-id="850e7-388">For these scenarios, hello following firewall rules should be in place:</span></span>

1. <span data-ttu-id="850e7-389">Gerenciamento do firewall</span><span class="sxs-lookup"><span data-stu-id="850e7-389">Firewall Management</span></span>
2. <span data-ttu-id="850e7-390">TooIIS01 RDP</span><span class="sxs-lookup"><span data-stu-id="850e7-390">RDP tooIIS01</span></span>
3. <span data-ttu-id="850e7-391">TooDNS01 RDP</span><span class="sxs-lookup"><span data-stu-id="850e7-391">RDP tooDNS01</span></span>
4. <span data-ttu-id="850e7-392">TooAppVM01 RDP</span><span class="sxs-lookup"><span data-stu-id="850e7-392">RDP tooAppVM01</span></span>
5. <span data-ttu-id="850e7-393">TooAppVM02 RDP</span><span class="sxs-lookup"><span data-stu-id="850e7-393">RDP tooAppVM02</span></span>
6. <span data-ttu-id="850e7-394">Toohello de tráfego de aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="850e7-394">App Traffic toohello Web</span></span>
7. <span data-ttu-id="850e7-395">TooAppVM01 de tráfego do aplicativo</span><span class="sxs-lookup"><span data-stu-id="850e7-395">App Traffic tooAppVM01</span></span>
8. <span data-ttu-id="850e7-396">Saída toohello da Internet</span><span class="sxs-lookup"><span data-stu-id="850e7-396">Outbound toohello Internet</span></span>
9. <span data-ttu-id="850e7-397">TooDNS01 de front-end</span><span class="sxs-lookup"><span data-stu-id="850e7-397">Frontend tooDNS01</span></span>
10. <span data-ttu-id="850e7-398">Tráfego de dentro da sub-rede (end toofront back-end apenas)</span><span class="sxs-lookup"><span data-stu-id="850e7-398">Intra-Subnet Traffic (back end toofront end only)</span></span>
11. <span data-ttu-id="850e7-399">Negar Tudo</span><span class="sxs-lookup"><span data-stu-id="850e7-399">Deny All</span></span>

<span data-ttu-id="850e7-400">conjunto de regras de firewall real Hello, provavelmente terão muitas outras regras toothese adição, regras de saudação em qualquer determinado firewall também terá números de prioridade diferentes Olá aqueles listados aqui.</span><span class="sxs-lookup"><span data-stu-id="850e7-400">hello actual firewall ruleset will most likely have many other rules in addition toothese, hello rules on any given firewall will also have different priority numbers than hello ones listed here.</span></span> <span data-ttu-id="850e7-401">Esta lista e números associados são de relevância de tooprovide entre apenas essas onze regras e a prioridade relativa de saudação entre eles.</span><span class="sxs-lookup"><span data-stu-id="850e7-401">This list and associated numbers are tooprovide relevance between just these eleven rules and hello relative priority amongst them.</span></span> <span data-ttu-id="850e7-402">Em outras palavras; no firewall do hello real, Olá "RDP tooIIS01" pode ser regra número 5, mas como está abaixo da regra de "Gerenciamento de Firewall" hello e acima de regra de "RDP tooDNS01" hello que ele seria alinhar com intenção de saudação desta lista.</span><span class="sxs-lookup"><span data-stu-id="850e7-402">In other words; on hello actual firewall, hello “RDP tooIIS01” may be rule number 5, but as long as it’s below hello “Firewall Management” rule and above hello “RDP tooDNS01” rule it would align with hello intention of this list.</span></span> <span data-ttu-id="850e7-403">lista de saudação também ajudará a saudação abaixo cenários permitindo brevidade; Por exemplo "Regra de FW 9 (DNS)".</span><span class="sxs-lookup"><span data-stu-id="850e7-403">hello list will also aid in hello below scenarios allowing brevity; e.g. “FW Rule 9 (DNS)”.</span></span> <span data-ttu-id="850e7-404">Também por questão de brevidade, Olá quatro regras RDP será coletivamente chamado, "hello regras RDP" quando o cenário de tráfego de saudação é tooRDP não relacionado.</span><span class="sxs-lookup"><span data-stu-id="850e7-404">Also for brevity, hello four RDP rules will be collectively called, “hello RDP rules” when hello traffic scenario is unrelated tooRDP.</span></span>

<span data-ttu-id="850e7-405">Lembre-se também de que os grupos de segurança de rede estão no local para o tráfego da internet em Olá front-end e back-end subredes.</span><span class="sxs-lookup"><span data-stu-id="850e7-405">Also recall that Network Security Groups are in-place for inbound internet traffic on hello Frontend and Backend subnets.</span></span>

#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="850e7-406">(Permitido) Internet tooWeb Server</span><span class="sxs-lookup"><span data-stu-id="850e7-406">(Allowed) Internet tooWeb Server</span></span>
1. <span data-ttu-id="850e7-407">O usuário da Internet solicita uma página HTTP de SecSvc001.CloudApp.Net (Internet Voltada para o Serviço de Nuvem)</span><span class="sxs-lookup"><span data-stu-id="850e7-407">Internet user requests HTTP page from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="850e7-408">Tráfego passa do serviço de nuvem por meio de um ponto de extremidade aberto na interface toofirewall porta 80 10.0.0.4:80</span><span class="sxs-lookup"><span data-stu-id="850e7-408">Cloud service passes traffic through open endpoint on port 80 toofirewall interface on 10.0.0.4:80</span></span>
3. <span data-ttu-id="850e7-409">Nenhum NSG atribuído tooSecurity sub-rede, para que as regras do sistema NSG permitem tráfego toofirewall</span><span class="sxs-lookup"><span data-stu-id="850e7-409">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="850e7-410">Tráfego atinge o endereço IP interno do firewall hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="850e7-410">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="850e7-411">O firewall inicia o processamento de regras:</span><span class="sxs-lookup"><span data-stu-id="850e7-411">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="850e7-412">FW regra 1 (FW Mgmt) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-412">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="850e7-413">Regras 2 a 5 (regras de RDP) não se aplicam, mova a regra toonext</span><span class="sxs-lookup"><span data-stu-id="850e7-413">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="850e7-414">FW regra 6 (aplicativo: Web) se aplicam, o tráfego é permitido, o firewall NAT-too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="850e7-414">FW Rule 6 (App: Web) does apply, traffic is allowed, firewall NATs it too10.0.1.4 (IIS01)</span></span>
6. <span data-ttu-id="850e7-415">subrede front-end Olá começa o processamento de regras de entrada:</span><span class="sxs-lookup"><span data-stu-id="850e7-415">hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="850e7-416">NSG regra 1 (bloco de Internet) não se aplica (esse tráfego foi NAT seria pelo firewall hello, portanto, o endereço de origem de saudação agora é firewall Olá na sub-rede de segurança hello e vistos por sub-rede front-end de saudação o tráfego do NSG toobe "local" e, portanto, é permitido), mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-416">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Frontend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="850e7-417">As regras NSG padrão permitir o tráfego de toosubnet de sub-rede, o tráfego é permitido, pare o processamento de regras NSG</span><span class="sxs-lookup"><span data-stu-id="850e7-417">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="850e7-418">IIS01 está escutando o tráfego da web, recebe essa solicitação e inicia o processamento de solicitação de saudação</span><span class="sxs-lookup"><span data-stu-id="850e7-418">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
8. <span data-ttu-id="850e7-419">Tentativas de IIS01 tooinitiates um tooAppVM01 de sessão FTP na sub-rede back-end</span><span class="sxs-lookup"><span data-stu-id="850e7-419">IIS01 attempts tooinitiates an FTP session tooAppVM01 on Backend subnet</span></span>
9. <span data-ttu-id="850e7-420">rota UDR Olá na sub-rede front-end torna o próximo salto do hello firewall Olá</span><span class="sxs-lookup"><span data-stu-id="850e7-420">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
10. <span data-ttu-id="850e7-421">Não há regras de saída na sub-rede Frontend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="850e7-421">No outbound rules on Frontend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="850e7-422">O firewall inicia o processamento de regras:</span><span class="sxs-lookup"><span data-stu-id="850e7-422">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="850e7-423">FW regra 1 (FW Mgmt) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-423">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="850e7-424">Regra de firmware 2 a 5 (regras de RDP) não se aplicam, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-424">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="850e7-425">6 de regra FW (aplicativo: Web) não se aplicam, mova a regra toonext</span><span class="sxs-lookup"><span data-stu-id="850e7-425">FW Rule 6 (App: Web) doesn’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="850e7-426">7 de regra FW (aplicativo: back-end) se aplicam, o tráfego é permitido, firewall encaminha o tráfego too10.0.2.5 (AppVM01)</span><span class="sxs-lookup"><span data-stu-id="850e7-426">FW Rule 7 (App: Backend) does apply, traffic is allowed, firewall forwards traffic too10.0.2.5 (AppVM01)</span></span>
12. <span data-ttu-id="850e7-427">subrede back-end Olá começa o processamento de regras de entrada:</span><span class="sxs-lookup"><span data-stu-id="850e7-427">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="850e7-428">NSG regra 1 (bloco de Internet) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-428">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="850e7-429">As regras NSG padrão permitir o tráfego de toosubnet de sub-rede, o tráfego é permitido, pare o processamento de regras NSG</span><span class="sxs-lookup"><span data-stu-id="850e7-429">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
13. <span data-ttu-id="850e7-430">AppVM01 recebe a solicitação de saudação e inicia a sessão de saudação e responde</span><span class="sxs-lookup"><span data-stu-id="850e7-430">AppVM01 receives hello request and initiates hello session and responds</span></span>
14. <span data-ttu-id="850e7-431">rota UDR Olá na sub-rede back-end torna o próximo salto do hello firewall Olá</span><span class="sxs-lookup"><span data-stu-id="850e7-431">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
15. <span data-ttu-id="850e7-432">Como não há nenhuma regra NSG saída em Olá resposta de saudação de sub-rede de back-end é permitido</span><span class="sxs-lookup"><span data-stu-id="850e7-432">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
16. <span data-ttu-id="850e7-433">Porque isso está retornando o tráfego em uma sessão estabelecida Olá de firewall passa o servidor de web hello resposta toohello back (IIS01)</span><span class="sxs-lookup"><span data-stu-id="850e7-433">Because this is returning traffic on an established session hello firewall passes hello response back toohello web server (IIS01)</span></span>
17. <span data-ttu-id="850e7-434">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="850e7-434">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="850e7-435">NSG regra 1 (bloco de Internet) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-435">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="850e7-436">As regras NSG padrão permitir o tráfego de toosubnet de sub-rede, o tráfego é permitido, pare o processamento de regras NSG</span><span class="sxs-lookup"><span data-stu-id="850e7-436">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
18. <span data-ttu-id="850e7-437">servidor do IIS Olá recebe a resposta hello, conclui a transação Olá com AppVM01 e conclui construção Olá resposta HTTP, essa resposta HTTP é enviada toohello solicitante</span><span class="sxs-lookup"><span data-stu-id="850e7-437">hello IIS server receives hello response, completes hello transaction with AppVM01, and then completes building hello HTTP response, this HTTP response is sent toohello requestor</span></span>
19. <span data-ttu-id="850e7-438">Como não há nenhuma regra NSG saída em Olá resposta de saudação de sub-rede front-end é permitido</span><span class="sxs-lookup"><span data-stu-id="850e7-438">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
20. <span data-ttu-id="850e7-439">Olá firewall de saudação de acertos de resposta HTTP e como isso é Olá resposta tooan estabelecida sessão NAT é aceito pelo firewall Olá</span><span class="sxs-lookup"><span data-stu-id="850e7-439">hello HTTP response hits hello firewall, and because this is hello response tooan established NAT session is accepted by hello firewall</span></span>
21. <span data-ttu-id="850e7-440">Olá firewall, em seguida, redireciona Olá resposta back toohello usuário pela Internet</span><span class="sxs-lookup"><span data-stu-id="850e7-440">hello firewall then redirects hello response back toohello Internet User</span></span>
22. <span data-ttu-id="850e7-441">Desde que não existem regras NSG saída ou saltos UDR na sub-rede de front-end Olá resposta Olá é permitida e Olá Internet usuário recebe Olá web página solicitada.</span><span class="sxs-lookup"><span data-stu-id="850e7-441">Since there are no outbound NSG rules or UDR hops on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-internet-rdp-toobackend"></a><span data-ttu-id="850e7-442">(Permitido) TooBackend RDP de Internet</span><span class="sxs-lookup"><span data-stu-id="850e7-442">(Allowed) Internet RDP tooBackend</span></span>
1. <span data-ttu-id="850e7-443">Administrador do servidor na internet solicitações tooAppVM01 de sessão RDP via SecSvc001.CloudApp.Net:8025, onde o 8025 é o número da porta do hello atribuídos pelo usuário para a regra de firewall "RDP tooAppVM01" hello</span><span class="sxs-lookup"><span data-stu-id="850e7-443">Server Admin on internet requests RDP session tooAppVM01 via SecSvc001.CloudApp.Net:8025, where 8025 is hello user assigned port number for hello “RDP tooAppVM01” firewall rule</span></span>
2. <span data-ttu-id="850e7-444">serviço de nuvem Olá passa o tráfego por meio do ponto de extremidade aberto Olá na interface de toofirewall porta 8025 em 10.0.0.4:8025</span><span class="sxs-lookup"><span data-stu-id="850e7-444">hello cloud service passes traffic through hello open endpoint on port 8025 toofirewall interface on 10.0.0.4:8025</span></span>
3. <span data-ttu-id="850e7-445">Nenhum NSG atribuído tooSecurity sub-rede, para que as regras do sistema NSG permitem tráfego toofirewall</span><span class="sxs-lookup"><span data-stu-id="850e7-445">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="850e7-446">O firewall inicia o processamento de regras:</span><span class="sxs-lookup"><span data-stu-id="850e7-446">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="850e7-447">FW regra 1 (FW Mgmt) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-447">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="850e7-448">FW regra 2 (RDP IIS) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-448">FW Rule 2 (RDP IIS) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="850e7-449">FW regra 3 (DNS01 RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-449">FW Rule 3 (RDP DNS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="850e7-450">Aplicar FW regra 4 (RDP AppVM01), o tráfego é permitido, o firewall NAT-too10.0.2.5:3386 (porta RDP em AppVM01)</span><span class="sxs-lookup"><span data-stu-id="850e7-450">FW Rule 4 (RDP AppVM01) does apply, traffic is allowed, firewall NATs it too10.0.2.5:3386 (RDP port on AppVM01)</span></span>
5. <span data-ttu-id="850e7-451">subrede back-end Olá começa o processamento de regras de entrada:</span><span class="sxs-lookup"><span data-stu-id="850e7-451">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="850e7-452">NSG regra 1 (bloco de Internet) não se aplica (esse tráfego foi NAT seria pelo firewall hello, portanto, o endereço de origem de saudação agora é firewall Olá na sub-rede de segurança hello e vistos por sub-rede de back-end Olá o tráfego do NSG toobe "local" e, portanto, é permitido), mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-452">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Backend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="850e7-453">As regras NSG padrão permitir o tráfego de toosubnet de sub-rede, o tráfego é permitido, pare o processamento de regras NSG</span><span class="sxs-lookup"><span data-stu-id="850e7-453">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="850e7-454">O AppVM01 está ouvindo o tráfego RDP e responde</span><span class="sxs-lookup"><span data-stu-id="850e7-454">AppVM01 is listening for RDP traffic and responds</span></span>
7. <span data-ttu-id="850e7-455">Sem regras de saída, as regras NSG padrão serão aplicadas e o tráfego de retorno será permitido</span><span class="sxs-lookup"><span data-stu-id="850e7-455">With no outbound NSG rules, default rules apply and return traffic is allowed</span></span>
8. <span data-ttu-id="850e7-456">UDR roteia o tráfego de saída toohello firewall como próximo salto de saudação</span><span class="sxs-lookup"><span data-stu-id="850e7-456">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
9. <span data-ttu-id="850e7-457">Porque isso está retornando o tráfego em uma sessão estabelecida Olá de firewall passa o usuário da internet Olá resposta toohello back</span><span class="sxs-lookup"><span data-stu-id="850e7-457">Because this is returning traffic on an established session hello firewall passes hello response back toohello internet user</span></span>
10. <span data-ttu-id="850e7-458">A sessão RDP está habilitada</span><span class="sxs-lookup"><span data-stu-id="850e7-458">RDP session is enabled</span></span>
11. <span data-ttu-id="850e7-459">O AppVM01 solicita a senha do nome de usuário</span><span class="sxs-lookup"><span data-stu-id="850e7-459">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="850e7-460">(Permitido) Pesquisa de DNS do Servidor Web no servidor DNS</span><span class="sxs-lookup"><span data-stu-id="850e7-460">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="850e7-461">Web necessidades de servidor, IIS01, um feed de dados em www.data.gov, mas precisa tooresolve Olá endereço.</span><span class="sxs-lookup"><span data-stu-id="850e7-461">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="850e7-462">Olá configuração de rede para listas de rede virtual Olá DNS01 (10.0.2.4 na sub-rede de back-end Olá) como o servidor DNS primário de hello, IIS01 envia Olá tooDNS01 de solicitação DNS</span><span class="sxs-lookup"><span data-stu-id="850e7-462">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="850e7-463">UDR roteia o tráfego de saída toohello firewall como próximo salto de saudação</span><span class="sxs-lookup"><span data-stu-id="850e7-463">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
4. <span data-ttu-id="850e7-464">Nenhuma regra NSG saída é associados toohello front-end subrede, o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="850e7-464">No outbound NSG rules are bound toohello Frontend subnet, traffic is allowed</span></span>
5. <span data-ttu-id="850e7-465">O firewall inicia o processamento de regras:</span><span class="sxs-lookup"><span data-stu-id="850e7-465">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="850e7-466">FW regra 1 (FW Mgmt) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-466">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="850e7-467">Regra de firmware 2 a 5 (regras de RDP) não se aplicam, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-467">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="850e7-468">FW regras 6 e 7 (regras de aplicativo) não se aplicam, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-468">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="850e7-469">Regra de FW 8 (tooInternet) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-469">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="850e7-470">Aplicar a regra de FW 9 (DNS), o tráfego é permitido, firewall encaminha o tráfego too10.0.2.4 (DNS01)</span><span class="sxs-lookup"><span data-stu-id="850e7-470">FW Rule 9 (DNS) does apply, traffic is allowed, firewall forwards traffic too10.0.2.4 (DNS01)</span></span>
6. <span data-ttu-id="850e7-471">subrede back-end Olá começa o processamento de regras de entrada:</span><span class="sxs-lookup"><span data-stu-id="850e7-471">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="850e7-472">NSG regra 1 (bloco de Internet) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-472">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="850e7-473">As regras NSG padrão permitir o tráfego de toosubnet de sub-rede, o tráfego é permitido, pare o processamento de regras NSG</span><span class="sxs-lookup"><span data-stu-id="850e7-473">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="850e7-474">Servidor DNS recebe a solicitação de saudação</span><span class="sxs-lookup"><span data-stu-id="850e7-474">DNS server receives hello request</span></span>
8. <span data-ttu-id="850e7-475">Servidor DNS não tem endereço Olá armazenado em cache e solicita que um servidor DNS raiz em Olá internet</span><span class="sxs-lookup"><span data-stu-id="850e7-475">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
9. <span data-ttu-id="850e7-476">UDR roteia o tráfego de saída toohello firewall como próximo salto de saudação</span><span class="sxs-lookup"><span data-stu-id="850e7-476">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
10. <span data-ttu-id="850e7-477">Nenhuma regra NSG de saída na sub-rede Backend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="850e7-477">No outbound NSG rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="850e7-478">O firewall inicia o processamento de regras:</span><span class="sxs-lookup"><span data-stu-id="850e7-478">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="850e7-479">FW regra 1 (FW Mgmt) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-479">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="850e7-480">Regra de firmware 2 a 5 (regras de RDP) não se aplicam, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-480">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="850e7-481">FW regras 6 e 7 (regras de aplicativo) não se aplicam, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-481">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="850e7-482">Aplicar FW regra 8 (tooInternet), o tráfego é permitido, sessão é SNAT tooroot Server de DNS na Internet de saudação</span><span class="sxs-lookup"><span data-stu-id="850e7-482">FW Rule 8 (tooInternet) does apply, traffic is allowed, session is SNAT out tooroot DNS server on hello Internet</span></span>
12. <span data-ttu-id="850e7-483">Servidor DNS da Internet responde, desde que esta sessão foi iniciada no firewall hello, resposta Olá é aceito pelo firewall Olá</span><span class="sxs-lookup"><span data-stu-id="850e7-483">Internet DNS server responds, since this session was initiated from hello firewall, hello response is accepted by hello firewall</span></span>
13. <span data-ttu-id="850e7-484">Como esta é uma sessão estabelecida, o firewall Olá encaminha Olá resposta toohello Iniciar servidor, DNS01</span><span class="sxs-lookup"><span data-stu-id="850e7-484">As this is an established session, hello firewall forwards hello response toohello initiating server, DNS01</span></span>
14. <span data-ttu-id="850e7-485">subrede back-end Olá começa o processamento de regras de entrada:</span><span class="sxs-lookup"><span data-stu-id="850e7-485">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="850e7-486">NSG regra 1 (bloco de Internet) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-486">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="850e7-487">As regras NSG padrão permitir o tráfego de toosubnet de sub-rede, o tráfego é permitido, pare o processamento de regras NSG</span><span class="sxs-lookup"><span data-stu-id="850e7-487">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
15. <span data-ttu-id="850e7-488">servidor DNS Olá recebe e armazena em cache a resposta de saudação e, em seguida, responde toohello solicitação inicial back tooIIS01</span><span class="sxs-lookup"><span data-stu-id="850e7-488">hello DNS server receives and caches hello response, and then responds toohello initial request back tooIIS01</span></span>
16. <span data-ttu-id="850e7-489">rota UDR Olá na sub-rede back-end torna o próximo salto do hello firewall Olá</span><span class="sxs-lookup"><span data-stu-id="850e7-489">hello UDR route on backend subnet makes hello firewall hello next hop</span></span>
17. <span data-ttu-id="850e7-490">Nenhuma regra NSG saída existe na sub-rede de back-end hello, o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="850e7-490">No outbound NSG rules exist on hello Backend subnet, traffic is allowed</span></span>
18. <span data-ttu-id="850e7-491">Esta é uma sessão estabelecida no firewall hello, resposta Olá é encaminhada pelo servidor de IIS Olá firewall back toohello</span><span class="sxs-lookup"><span data-stu-id="850e7-491">This is an established session on hello firewall, hello response is forwarded by hello firewall back toohello IIS server</span></span>
19. <span data-ttu-id="850e7-492">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="850e7-492">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="850e7-493">Não há nenhuma regra NSG que aplica tooInbound tráfego da sub-rede de front-end do toohello de sub-rede de back-end Olá, para que nenhuma das regras do NSG Olá aplicar</span><span class="sxs-lookup"><span data-stu-id="850e7-493">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="850e7-494">regra do sistema padrão Olá permitindo o tráfego entre as sub-redes permitiria que esse tráfego para que Olá tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="850e7-494">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
20. <span data-ttu-id="850e7-495">IIS01 recebe a resposta de saudação do DNS01</span><span class="sxs-lookup"><span data-stu-id="850e7-495">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-backend-server-toofrontend-server"></a><span data-ttu-id="850e7-496">(Permitido) Servidor de tooFrontend do servidor de back-end</span><span class="sxs-lookup"><span data-stu-id="850e7-496">(Allowed) Backend server tooFrontend server</span></span>
1. <span data-ttu-id="850e7-497">Um administrador conectado tooAppVM02 via RDP solicita um arquivo diretamente do servidor de IIS01 Olá por meio do Explorador de arquivos do windows</span><span class="sxs-lookup"><span data-stu-id="850e7-497">An administrator logged on tooAppVM02 via RDP requests a file directly from hello IIS01 server via windows file explorer</span></span>
2. <span data-ttu-id="850e7-498">rota UDR Olá na sub-rede back-end torna o próximo salto do hello firewall Olá</span><span class="sxs-lookup"><span data-stu-id="850e7-498">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
3. <span data-ttu-id="850e7-499">Como não há nenhuma regra NSG saída em Olá resposta de saudação de sub-rede de back-end é permitido</span><span class="sxs-lookup"><span data-stu-id="850e7-499">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
4. <span data-ttu-id="850e7-500">O firewall inicia o processamento de regras:</span><span class="sxs-lookup"><span data-stu-id="850e7-500">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="850e7-501">FW regra 1 (FW Mgmt) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-501">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="850e7-502">Regra de firmware 2 a 5 (regras de RDP) não se aplicam, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-502">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="850e7-503">FW regras 6 e 7 (regras de aplicativo) não se aplicam, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-503">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="850e7-504">Regra de FW 8 (tooInternet) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-504">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="850e7-505">Não se aplica a regra de FW 9 (DNS), mova a regra toonext</span><span class="sxs-lookup"><span data-stu-id="850e7-505">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="850e7-506">Aplicar FW regra 10 (dentro da sub-rede), o tráfego é permitido, firewall passa tráfego too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="850e7-506">FW Rule 10 (Intra-Subnet) does apply, traffic is allowed, firewall passes traffic too10.0.1.4 (IIS01)</span></span>
5. <span data-ttu-id="850e7-507">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="850e7-507">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="850e7-508">NSG regra 1 (bloco de Internet) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-508">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="850e7-509">As regras NSG padrão permitir o tráfego de toosubnet de sub-rede, o tráfego é permitido, pare o processamento de regras NSG</span><span class="sxs-lookup"><span data-stu-id="850e7-509">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="850e7-510">Supondo que a autorização e autenticação adequada, IIS01 aceita a solicitação de saudação e responde</span><span class="sxs-lookup"><span data-stu-id="850e7-510">Assuming proper authentication and authorization, IIS01 accepts hello request and responds</span></span>
7. <span data-ttu-id="850e7-511">rota UDR Olá na sub-rede front-end torna o próximo salto do hello firewall Olá</span><span class="sxs-lookup"><span data-stu-id="850e7-511">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
8. <span data-ttu-id="850e7-512">Como não há nenhuma regra NSG saída em Olá resposta de saudação de sub-rede front-end é permitido</span><span class="sxs-lookup"><span data-stu-id="850e7-512">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
9. <span data-ttu-id="850e7-513">Pois esta é uma sessão existente no firewall Olá esta resposta é permitida e firewall Olá retorna Olá resposta tooAppVM02</span><span class="sxs-lookup"><span data-stu-id="850e7-513">As this is an existing session on hello firewall this response is allowed and hello firewall returns hello response tooAppVM02</span></span>
10. <span data-ttu-id="850e7-514">A sub-rede Backend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="850e7-514">Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="850e7-515">NSG regra 1 (bloco de Internet) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-515">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="850e7-516">As regras NSG padrão permitir o tráfego de toosubnet de sub-rede, o tráfego é permitido, pare o processamento de regras NSG</span><span class="sxs-lookup"><span data-stu-id="850e7-516">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
11. <span data-ttu-id="850e7-517">AppVM02 recebe a resposta de saudação</span><span class="sxs-lookup"><span data-stu-id="850e7-517">AppVM02 receives hello response</span></span>

#### <a name="denied-internet-direct-tooweb-server"></a><span data-ttu-id="850e7-518">(Negado) Internet direto tooWeb Server</span><span class="sxs-lookup"><span data-stu-id="850e7-518">(Denied) Internet direct tooWeb Server</span></span>
1. <span data-ttu-id="850e7-519">Usuário de Internet tenta tooaccess Olá servidor web, IIS01, por meio de saudação FrontEnd001.CloudApp.Net serviço</span><span class="sxs-lookup"><span data-stu-id="850e7-519">Internet user tries tooaccess hello web server, IIS01, through hello FrontEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="850e7-520">Como não há nenhum ponto de extremidade aberto para o tráfego de HTTP, isso não seria passar Olá serviço de nuvem e não alcançar o servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="850e7-520">Since there are no endpoints open for HTTP traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="850e7-521">Se o ponto de extremidade de saudação estava aberto por algum motivo, Olá NSG (bloco de Internet) na sub-rede de front-end Olá bloqueia esse tráfego</span><span class="sxs-lookup"><span data-stu-id="850e7-521">If hello endpoints were open for some reason, hello NSG (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="850e7-522">Finalmente, rota do hello front-end subrede UDR poderia enviar qualquer tráfego de saída de IIS01 toohello firewall como salto seguinte hello e firewall Olá teria visto como tráfego assimétrico e descartar a resposta de saída dessa forma, há pelo menos três camadas independentes de saudação de defesa entre hello IIS01 e internet por meio de seu serviço de nuvem impedindo o acesso não autorizado/inadequados.</span><span class="sxs-lookup"><span data-stu-id="850e7-522">Finally, hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and IIS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toobackend-server"></a><span data-ttu-id="850e7-523">(Negado) Internet tooBackend Server</span><span class="sxs-lookup"><span data-stu-id="850e7-523">(Denied) Internet tooBackend Server</span></span>
1. <span data-ttu-id="850e7-524">Usuário de Internet tenta tooaccess um arquivo em AppVM01 por meio de saudação BackEnd001.CloudApp.Net serviço</span><span class="sxs-lookup"><span data-stu-id="850e7-524">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="850e7-525">Como não há nenhum ponto de extremidade aberto para compartilhamento de arquivos, isso não passaria Olá serviço de nuvem e não alcançar o servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="850e7-525">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="850e7-526">Se o ponto de extremidade de saudação estava aberto por algum motivo, Olá NSG (bloco de Internet) bloqueia esse tráfego</span><span class="sxs-lookup"><span data-stu-id="850e7-526">If hello endpoints were open for some reason, hello NSG (Block Internet) would block this traffic</span></span>
4. <span data-ttu-id="850e7-527">Finalmente, rota UDR Olá poderia enviar qualquer tráfego de saída de AppVM01 toohello firewall como salto seguinte hello e firewall Olá teria visto como tráfego assimétrico e descartar a resposta de saída Olá dessa forma, há pelo menos três camadas independentes de defesa entre Olá AppVM01 e internet por meio de seu serviço de nuvem impedindo o acesso não autorizado/inadequados.</span><span class="sxs-lookup"><span data-stu-id="850e7-527">Finally, hello UDR route would send any outbound traffic from AppVM01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and AppVM01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-frontend-server-toobackend-server"></a><span data-ttu-id="850e7-528">(Negado) Servidor de front-end tooBackend Server</span><span class="sxs-lookup"><span data-stu-id="850e7-528">(Denied) Frontend server tooBackend Server</span></span>
1. <span data-ttu-id="850e7-529">Suponha que IIS01 foi comprometido e está executando código mal-intencionado tentar servidores de sub-rede tooscan Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="850e7-529">Assume IIS01 was compromised and is running malicious code trying tooscan hello Backend subnet servers.</span></span>
2. <span data-ttu-id="850e7-530">rota UDR Olá front-end subrede poderia enviar qualquer tráfego de saída de IIS01 toohello firewall como próximo salto de saudação.</span><span class="sxs-lookup"><span data-stu-id="850e7-530">hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop.</span></span> <span data-ttu-id="850e7-531">Isso não é algo que pode ser alterada por Olá comprometido VM.</span><span class="sxs-lookup"><span data-stu-id="850e7-531">This is not something that can be altered by hello compromised VM.</span></span>
3. <span data-ttu-id="850e7-532">firewall Olá processaria tráfego hello, se a solicitação Olá foi tooAppVM01 ou servidor DNS toohello para pesquisas DNS tráfego potencialmente pode ser permitido pelo firewall da saudação (vencimento tooFW regras 7 e 9).</span><span class="sxs-lookup"><span data-stu-id="850e7-532">hello firewall would process hello traffic, if hello request was tooAppVM01, or toohello DNS server for DNS lookups that traffic could potentially be allowed by hello firewall (due tooFW Rules 7 and 9).</span></span> <span data-ttu-id="850e7-533">Todo o outro tráfego seria bloqueado pela Regra FW 11 (Negar Tudo).</span><span class="sxs-lookup"><span data-stu-id="850e7-533">All other traffic would be blocked by FW Rule 11 (Deny All).</span></span>
4. <span data-ttu-id="850e7-534">Se avançada detecção de ameaças foi habilitada no firewall da saudação (que não é abordado neste documento, consulte a documentação do fornecedor Olá para seu dispositivo de rede específico ameaça recursos avançados), até mesmo o tráfego será permitido pelo Olá básico de regras de encaminhamento abordadas neste documento pode ser impedido se tráfego Olá contido assinaturas conhecidas ou padrões de sinalizar uma regra avançada.</span><span class="sxs-lookup"><span data-stu-id="850e7-534">If advanced threat detection was enabled on hello firewall (which is not covered in this document, see hello vendor documentation for your specific network appliance advanced threat capabilities), even traffic that would be allowed by hello basic forwarding rules discussed in this document could be prevented if hello traffic contained known signatures or patterns that flag an advanced threat rule.</span></span>

#### <a name="denied-internet-dns-lookup-on-dns-server"></a><span data-ttu-id="850e7-535">(Negado) Pesquisa DNS da Internet no servidor DNS</span><span class="sxs-lookup"><span data-stu-id="850e7-535">(Denied) Internet DNS lookup on DNS server</span></span>
1. <span data-ttu-id="850e7-536">Usuário de Internet tenta toolookup um registro DNS interno em DNS01 por meio do serviço BackEnd001.CloudApp.Net</span><span class="sxs-lookup"><span data-stu-id="850e7-536">Internet user tries toolookup an internal DNS record on DNS01 through BackEnd001.CloudApp.Net service</span></span> 
2. <span data-ttu-id="850e7-537">Como não há nenhum ponto de extremidade aberto para o tráfego de DNS, isso não seria passar Olá serviço de nuvem e não alcançar o servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="850e7-537">Since there are no endpoints open for DNS traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="850e7-538">Se o ponto de extremidade de saudação estava aberto por algum motivo, Olá NSG regra (bloco de Internet) na sub-rede de front-end Olá a bloquear esse tráfego</span><span class="sxs-lookup"><span data-stu-id="850e7-538">If hello endpoints were open for some reason, hello NSG rule (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="850e7-539">Finalmente, rota UDR de sub-rede de back-end Olá poderia enviar qualquer tráfego de saída de DNS01 toohello firewall como salto seguinte hello e firewall Olá teria visto como tráfego assimétrico e descartar a resposta de saída dessa forma, há pelo menos três camadas independentes de saudação de defesa entre hello DNS01 e internet por meio de seu serviço de nuvem impedindo o acesso não autorizado/inadequados.</span><span class="sxs-lookup"><span data-stu-id="850e7-539">Finally, hello Backend subnet UDR route would send any outbound traffic from DNS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and DNS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toosql-access-through-firewall"></a><span data-ttu-id="850e7-540">(Negado) Acesso à Internet tooSQL através do Firewall</span><span class="sxs-lookup"><span data-stu-id="850e7-540">(Denied) Internet tooSQL access through Firewall</span></span>
1. <span data-ttu-id="850e7-541">O usuário da Internet solicita dados SQL de SecSvc001.CloudApp.Net (Serviço de Nuvem Voltado para a Internet)</span><span class="sxs-lookup"><span data-stu-id="850e7-541">Internet user requests SQL data from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="850e7-542">Como não há nenhum ponto de extremidade aberto para SQL, isso não passaria Olá serviço de nuvem e não alcançar o firewall Olá</span><span class="sxs-lookup"><span data-stu-id="850e7-542">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="850e7-543">Se o ponto de extremidade do SQL estava aberto por algum motivo, o firewall Olá começaria processamento da regra:</span><span class="sxs-lookup"><span data-stu-id="850e7-543">If SQL endpoints were open for some reason, hello firewall would begin rule processing:</span></span>
   1. <span data-ttu-id="850e7-544">FW regra 1 (FW Mgmt) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-544">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="850e7-545">Regras 2 a 5 (regras de RDP) não se aplicam, mova a regra toonext</span><span class="sxs-lookup"><span data-stu-id="850e7-545">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="850e7-546">FW regra 6 e 7 (regras de aplicativo) não se aplicam, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-546">FW Rule 6 & 7 (Application Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="850e7-547">Regra de FW 8 (tooInternet) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-547">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="850e7-548">Não se aplica a regra de FW 9 (DNS), mova a regra toonext</span><span class="sxs-lookup"><span data-stu-id="850e7-548">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="850e7-549">Regra de FW 10 (dentro da sub-rede) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="850e7-549">FW Rule 10 (Intra-Subnet) doesn’t apply, move toonext rule</span></span>
   7. <span data-ttu-id="850e7-550">A Regra FW 11 (Negar Tudo) se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="850e7-550">FW Rule 11 (Deny All) does apply, traffic is blocked, stop rule processing</span></span>

## <a name="references"></a><span data-ttu-id="850e7-551">Referências</span><span class="sxs-lookup"><span data-stu-id="850e7-551">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="850e7-552">Script principal e configuração de rede</span><span class="sxs-lookup"><span data-stu-id="850e7-552">Main Script and Network Config</span></span>
<span data-ttu-id="850e7-553">Salve Olá Script completo em um arquivo de script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="850e7-553">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="850e7-554">Salve Olá configuração de rede em um arquivo denominado "NetworkConf2.xml".</span><span class="sxs-lookup"><span data-stu-id="850e7-554">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="850e7-555">Modificar as variáveis definidas pelo usuário de saudação conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="850e7-555">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="850e7-556">Executar script hello, siga as instruções regra de configuração do Firewall Olá acima.</span><span class="sxs-lookup"><span data-stu-id="850e7-556">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="850e7-557">Script Completo</span><span class="sxs-lookup"><span data-stu-id="850e7-557">Full Script</span></span>
<span data-ttu-id="850e7-558">Esse script vai, com base em variáveis do hello definida pelo usuário:</span><span class="sxs-lookup"><span data-stu-id="850e7-558">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="850e7-559">Conecte-se tooan assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="850e7-559">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="850e7-560">Criar uma nova conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="850e7-560">Create a new storage account</span></span>
3. <span data-ttu-id="850e7-561">Criar uma nova rede virtual e três sub-redes conforme definido no arquivo de configuração de rede de saudação</span><span class="sxs-lookup"><span data-stu-id="850e7-561">Create a new VNet and three subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="850e7-562">Criar cinco máquinas virtuais; um firewall e quatro VMs do Windows Server</span><span class="sxs-lookup"><span data-stu-id="850e7-562">Build five virtual machines; 1 firewall and 4 windows server VMs</span></span>
5. <span data-ttu-id="850e7-563">Configurar o UDR, incluindo:</span><span class="sxs-lookup"><span data-stu-id="850e7-563">Configure UDR including:</span></span>
   1. <span data-ttu-id="850e7-564">Criar duas novas tabelas de rotas</span><span class="sxs-lookup"><span data-stu-id="850e7-564">Creating two new route tables</span></span>
   2. <span data-ttu-id="850e7-565">Adicionar rotas toohello tabelas</span><span class="sxs-lookup"><span data-stu-id="850e7-565">Add routes toohello tables</span></span>
   3. <span data-ttu-id="850e7-566">Associar sub-redes de tooappropriate de tabelas</span><span class="sxs-lookup"><span data-stu-id="850e7-566">Bind tables tooappropriate subnets</span></span>
6. <span data-ttu-id="850e7-567">Ativar o encaminhamento IP hello NVA</span><span class="sxs-lookup"><span data-stu-id="850e7-567">Enable IP Forwarding on hello NVA</span></span>
7. <span data-ttu-id="850e7-568">Configure o NSG, incluindo:</span><span class="sxs-lookup"><span data-stu-id="850e7-568">Configure NSG including:</span></span>
   1. <span data-ttu-id="850e7-569">Criando um NSG</span><span class="sxs-lookup"><span data-stu-id="850e7-569">Creating a NSG</span></span>
   2. <span data-ttu-id="850e7-570">Adicionando uma regra</span><span class="sxs-lookup"><span data-stu-id="850e7-570">Adding a rule</span></span>
   3. <span data-ttu-id="850e7-571">Associação de sub-redes apropriados da saudação NSG toohello</span><span class="sxs-lookup"><span data-stu-id="850e7-571">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="850e7-572">Este script do PowerShell deve ser executado localmente em um computador ou servidor conectado à Internet.</span><span class="sxs-lookup"><span data-stu-id="850e7-572">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="850e7-573">Quando esse script for executado, poderá haver avisos ou outras mensagens informativas que aparecerão no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="850e7-573">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="850e7-574">Somente as mensagens de erro em vermelho são motivo de preocupação.</span><span class="sxs-lookup"><span data-stu-id="850e7-574">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

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

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
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

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="850e7-575">Arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="850e7-575">Network Config File</span></span>
<span data-ttu-id="850e7-576">Salve esse arquivo xml com o local atualizado e adicione Olá link toothis arquivo toohello $NetworkConfigFile variável no script de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="850e7-576">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

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
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
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

#### <a name="sample-application-scripts"></a><span data-ttu-id="850e7-577">Scripts de aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="850e7-577">Sample Application Scripts</span></span>
<span data-ttu-id="850e7-578">Se você quiser tooinstall um aplicativo de exemplo para este e outros exemplos de rede de Perímetro, foi fornecido no hello link a seguir: [Script de exemplo de aplicativo][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="850e7-578">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "DMZ bidirecional com NVA, NSG e UDR"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Modo de exibição lógico de saudação regras de Firewall"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Criar um objeto de rede de front-end"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Criar um objeto de servidor DNS"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Cópia da regra RDP padrão"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "Regra de AppVM01"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Ícone de redirecionamento do aplicativo"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Ícone de NAT de destino"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Ícone de passagem"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Regra de Gerenciamento de Firewall"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Regra RDP do firewall"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Regra Web do firewall"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Regra de AppVM01 do firewall"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Regra de saída do firewall"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Regra de DNS do firewall"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Regra entre VNets do firewall"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Regra Negar do firewall"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Ativação de regra de firewall"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
