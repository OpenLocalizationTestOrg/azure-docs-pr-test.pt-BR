---
title: "aaaDMZ exemplo – criar uma rede de Perímetro tooprotect aplicativos com um Firewall e NSGs | Microsoft Docs"
description: "Criar uma DMZ com um Firewall e Grupos de Segurança de Rede (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a><span data-ttu-id="7d2c2-103">Exemplo 2 – criar uma rede de Perímetro tooprotect aplicativos com um Firewall e NSGs</span><span class="sxs-lookup"><span data-stu-id="7d2c2-103">Example 2 – Build a DMZ tooprotect applications with a Firewall and NSGs</span></span>
<span data-ttu-id="7d2c2-104">[Retornar toohello página segurança limite de melhores práticas][HOME]</span><span class="sxs-lookup"><span data-stu-id="7d2c2-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="7d2c2-105">Este exemplo criará uma DMZ com um firewall, quatro servidores Windows e Grupos de Segurança de Rede.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-105">This example will create a DMZ with a firewall, four windows servers, and Network Security Groups.</span></span> <span data-ttu-id="7d2c2-106">Ele também guiará por cada Olá comandos relevantes tooprovide uma compreensão mais profunda de cada etapa.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="7d2c2-107">Também há um cenário de tráfego seção tooprovide um detalhadas passo a passo sobre como o tráfego passa as camadas de saudação de defesa Olá DMZ.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="7d2c2-108">Por fim, na seção de referências de saudação é código completo hello e instrução toobuild este ambiente tootest e experiência com vários cenários.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="7d2c2-109">![Entrada de rede de Perímetro com NVA e NSG][1]</span><span class="sxs-lookup"><span data-stu-id="7d2c2-109">![Inbound DMZ with NVA and NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="7d2c2-110">Descrição do ambiente</span><span class="sxs-lookup"><span data-stu-id="7d2c2-110">Environment Description</span></span>
<span data-ttu-id="7d2c2-111">Neste exemplo, há uma assinatura que contém Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="7d2c2-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="7d2c2-112">Dois serviços de nuvem: "FrontEnd001" e "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="7d2c2-112">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="7d2c2-113">Uma rede virtual, “CorpNetwork”, com duas sub-redes: “FrontEnd” e “BackEnd”</span><span class="sxs-lookup"><span data-stu-id="7d2c2-113">A Virtual Network “CorpNetwork”, with two subnets: “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="7d2c2-114">Um único grupo de segurança de rede que é aplicada tooboth sub-redes</span><span class="sxs-lookup"><span data-stu-id="7d2c2-114">A single Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="7d2c2-115">Um dispositivo virtual de rede, neste exemplo, um Firewall Barracuda NextGen conectado toohello front-end subrede</span><span class="sxs-lookup"><span data-stu-id="7d2c2-115">A network virtual appliance, in this example a Barracuda NextGen Firewall, connected toohello Frontend subnet</span></span>
* <span data-ttu-id="7d2c2-116">Um Windows Server que representa um servidor Web de aplicativos ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="7d2c2-116">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="7d2c2-117">Dois servidores Windows que representam servidores de back-end de aplicativos ("AppVM01", "AppVM02")</span><span class="sxs-lookup"><span data-stu-id="7d2c2-117">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="7d2c2-118">Um servidor Windows que representa um servidor DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="7d2c2-118">A Windows server that represents a DNS server (“DNS01”)</span></span>

> [!NOTE]
> <span data-ttu-id="7d2c2-119">Embora este exemplo usa um Firewall de NextGen Barracuda, muitas das Olá que diferentes dispositivos de rede Virtual pode ser usados para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-119">Although this example uses a Barracuda NextGen Firewall, many of hello different Network Virtual Appliances could be used for this example.</span></span>
> 
> 

<span data-ttu-id="7d2c2-120">Na seção de referências de saudação abaixo, há um script do PowerShell que criará a maior parte do ambiente Olá descrito acima.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-120">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="7d2c2-121">Criando Olá VMs e redes virtuais, embora são feitos pelo script de exemplo hello, não são descritas em detalhes neste documento.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="7d2c2-122">ambiente de saudação toobuild:</span><span class="sxs-lookup"><span data-stu-id="7d2c2-122">toobuild hello environment:</span></span>

1. <span data-ttu-id="7d2c2-123">Salvar arquivo hello rede config xml incluído na seção de referências de saudação (atualizada com nomes, o local e o cenário de saudação fornecido de toomatch de endereços IP)</span><span class="sxs-lookup"><span data-stu-id="7d2c2-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="7d2c2-124">Atualização Olá variáveis no script de Olá Olá script toomatch Olá ambiente é toobe executar (assinaturas, nomes de serviço, etc.)</span><span class="sxs-lookup"><span data-stu-id="7d2c2-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="7d2c2-125">Execute o script hello no PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d2c2-125">Execute hello script in PowerShell</span></span>

<span data-ttu-id="7d2c2-126">**Observação**: região Olá representado em Olá script do PowerShell deve corresponder região Olá representada no arquivo de xml de configuração de rede hello.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-126">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="7d2c2-127">Após a execução bem-sucedida do script hello Olá seguindo as etapas de pós-scripts pode ser tomada:</span><span class="sxs-lookup"><span data-stu-id="7d2c2-127">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="7d2c2-128">Configurar regras de firewall hello, isso é abordado em Olá seção intitulada: regras de Firewall.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-128">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rules.</span></span>
2. <span data-ttu-id="7d2c2-129">Opcionalmente, na seção de referências de saudação são dois tooset de scripts, o servidor de web hello e servidor de aplicativos com um tooallow de aplicativo da web simples teste com essa configuração de rede de Perímetro.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-129">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="7d2c2-130">Olá próxima seção explica a maioria das Olá scripts instruções relativo tooNetwork grupos de segurança.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-130">hello next section explains most of hello scripts statements relative tooNetwork Security Groups.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="7d2c2-131">Grupos de segurança de rede (NSG)</span><span class="sxs-lookup"><span data-stu-id="7d2c2-131">Network Security Groups (NSG)</span></span>
<span data-ttu-id="7d2c2-132">Neste exemplo, um grupo NSG é criado e então carregado com seis regras.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-132">For this example, a NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="7d2c2-133">Em geral, você deve primeiro criar suas regras específicas de "Permitir" e Olá a regras mais genéricas de "Negar" última.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-133">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="7d2c2-134">Olá prioridade determina quais regras são avaliadas primeiro.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-134">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="7d2c2-135">Depois que o tráfego for encontrado uma regra específica de tooa tooapply, nenhuma regra adicional será avaliada.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-135">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="7d2c2-136">Regras NSG podem ser aplicados em Olá direção de entrada ou saída (da perspectiva de saudação da sub-rede Olá).</span><span class="sxs-lookup"><span data-stu-id="7d2c2-136">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="7d2c2-137">Declarativamente, Olá regras a seguir está sendo compilado para o tráfego de entrada:</span><span class="sxs-lookup"><span data-stu-id="7d2c2-137">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="7d2c2-138">O tráfego interno de DNS (porta 53) é permitido</span><span class="sxs-lookup"><span data-stu-id="7d2c2-138">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="7d2c2-139">O tráfego de RDP (porta 3389) do hello Internet tooany VM é permitido</span><span class="sxs-lookup"><span data-stu-id="7d2c2-139">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="7d2c2-140">O tráfego HTTP (porta 80) de saudação Internet toohello NVA (firewall) é permitido</span><span class="sxs-lookup"><span data-stu-id="7d2c2-140">HTTP traffic (port 80) from hello Internet toohello NVA (firewall) is allowed</span></span>
4. <span data-ttu-id="7d2c2-141">Qualquer tráfego (todas as portas) do IIS01 tooAppVM1 é permitido</span><span class="sxs-lookup"><span data-stu-id="7d2c2-141">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="7d2c2-142">Qualquer tráfego (todas as portas) do hello Internet toohello VNet inteira (ambas as sub-redes) foi negado</span><span class="sxs-lookup"><span data-stu-id="7d2c2-142">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="7d2c2-143">Qualquer tráfego (todas as portas) da sub-rede de back-end do hello front-end subrede toohello foi negado</span><span class="sxs-lookup"><span data-stu-id="7d2c2-143">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="7d2c2-144">A sub-rede de tooeach associada essas regras, se uma solicitação HTTP foi entrada do servidor web do hello Internet toohello, ambos regras 3 (Permitir) e 5 (Negar) seria aplicado, mas como a regra 3 tem uma prioridade mais alta somente seria aplicada e regra 5 não seria entram em ação.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-144">With these rules bound tooeach subnet, if a HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="7d2c2-145">Assim, você seria permitido a solicitação de Olá HTTP toohello firewall.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-145">Thus hello HTTP request would be allowed toohello firewall.</span></span> <span data-ttu-id="7d2c2-146">Se o mesmo que o tráfego foi a tentativa de servidor de DNS01 tooreach hello, regra 5 (Negar) seria Olá primeiro tooapply e hello tráfego não será permitido toopass toohello server.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-146">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="7d2c2-147">Regra de 6 (Negar) blocos Olá front-end subrede contra toohello sub-rede de back-end (com exceção de tráfego permitido nas regras 1 e 4), isso protege a rede de back-end de saudação no caso de um invasor comprometer Olá aplicativo da web em Olá front-end, o invasor Olá teria acesso limitado toohello back-end "protegido" rede (somente tooresources exposto no servidor de AppVM01 Olá).</span><span class="sxs-lookup"><span data-stu-id="7d2c2-147">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="7d2c2-148">Há uma regra de saída padrão que permite que o tráfego de saída toohello internet.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-148">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="7d2c2-149">Neste exemplo, permitiremos o tráfego de saída e não modificaremos quaisquer regras de saída.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-149">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="7d2c2-150">toolock tráfego em ambas as direções, roteamento de definido pelo usuário é necessário, isso é explorado em um exemplo de diferente que pode ser encontrados no hello [documento de limite de segurança principal][HOME].</span><span class="sxs-lookup"><span data-stu-id="7d2c2-150">toolock down traffic in both directions, User Defined Routing is required, this is explored in a different example that can found in hello [main security boundary document][HOME].</span></span>

<span data-ttu-id="7d2c2-151">Olá acima discutido NSG regras são muito semelhantes toohello NSG na [exemplo 1: criar uma rede de Perímetro simples com NSGs][Example1].</span><span class="sxs-lookup"><span data-stu-id="7d2c2-151">hello above discussed NSG rules are very similar toohello NSG rules in [Example 1 - Build a Simple DMZ with NSGs][Example1].</span></span> <span data-ttu-id="7d2c2-152">Analise Olá NSG descrição nesse documento para uma visão detalhada de cada regra NSG e os atributos de TI.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-152">Please review hello NSG Description in that document for a detailed look at each NSG rule and it's attributes.</span></span>

## <a name="firewall-rules"></a><span data-ttu-id="7d2c2-153">Regras de firewall</span><span class="sxs-lookup"><span data-stu-id="7d2c2-153">Firewall Rules</span></span>
<span data-ttu-id="7d2c2-154">Um cliente de gerenciamento será necessário toobe instalado em um firewall de saudação do PC toomanage e criar configurações de saudação necessárias.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-154">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="7d2c2-155">Consulte o fornecedor de documentação do seu firewall (ou outros NVA) Olá sobre como toomanage Olá dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-155">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="7d2c2-156">restante Olá desta seção descrevem configuração Olá do firewall Olá em si, por meio do cliente de gerenciamento de fornecedores hello (ou seja, não Olá portal do Azure ou o PowerShell).</span><span class="sxs-lookup"><span data-stu-id="7d2c2-156">hello remainder of this section will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="7d2c2-157">Instruções para download do cliente e conexão toohello Barracuda usado neste exemplo podem ser encontradas aqui: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="7d2c2-157">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="7d2c2-158">No firewall hello, regras de encaminhamento precisará toobe criado.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-158">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="7d2c2-159">Como este exemplo só roteia o tráfego de entrada toohello firewall da internet e, em seguida, o servidor de web toohello, encaminhamento somente uma regra NAT é necessário.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-159">Since this example only routes internet traffic in-bound toohello firewall and then toohello web server, only one forwarding NAT rule is needed.</span></span> <span data-ttu-id="7d2c2-160">No hello Barracuda NextGen Firewall usado em Olá Este exemplo regra pode ser um destino NAT regra toopass "Horário de verão NAT (") esse tráfego.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-160">On hello Barracuda NextGen Firewall used in this example hello rule would be a Destination NAT rule (“Dst NAT”) toopass this traffic.</span></span>

<span data-ttu-id="7d2c2-161">a seguir Olá toocreate regra (ou verifique se as regras padrão existente), a partir do painel de cliente Barracuda NG Admin hello, navegue toohello guia de configuração, no hello configuração operacional clique Ruleset.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-161">toocreate hello following rule (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="7d2c2-162">Chamado em uma grade, "Principal regras" mostrará Olá existente regras ativadas e desativadas no firewall hello.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-162">A grid called, “Main Rules” will show hello existing active and deactivated rules on hello firewall.</span></span> <span data-ttu-id="7d2c2-163">No canto superior direito de saudação desta grade é uma pequena verde "+", clique neste toocreate uma nova regra (Observação: seu firewall pode ser "bloqueado" para que as alterações, se você vir um botão marcado "Bloqueio" e são toocreate não é possível ou editar regras, clique neste botão muito "desbloquear" hello conjunto de regras e permitir a edição).</span><span class="sxs-lookup"><span data-stu-id="7d2c2-163">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello ruleset and allow editing).</span></span> <span data-ttu-id="7d2c2-164">Se você quiser tooedit uma regra existente, selecione essa regra, clique com botão direito e selecione Editar regra.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-164">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="7d2c2-165">Crie uma nova regra e forneça um nome, como "WebTraffic".</span><span class="sxs-lookup"><span data-stu-id="7d2c2-165">Create a new rule and provide a name, such as "WebTraffic".</span></span> 

<span data-ttu-id="7d2c2-166">ícone de regra de NAT de destino Olá tem esta aparência: ![ícone de NAT de destino][2]</span><span class="sxs-lookup"><span data-stu-id="7d2c2-166">hello Destination NAT rule icon looks like this: ![Destination NAT Icon][2]</span></span>

<span data-ttu-id="7d2c2-167">regra de saudação em si deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="7d2c2-167">hello rule itself would look something like this:</span></span>

<span data-ttu-id="7d2c2-168">![Regra de firewall][3]</span><span class="sxs-lookup"><span data-stu-id="7d2c2-168">![Firewall Rule][3]</span></span>

<span data-ttu-id="7d2c2-169">Aqui qualquer endereço de entrada acertos Olá Firewall tentar tooreach HTTP (porta 80 ou 443 para HTTPS) será enviado Olá interface "DHCP1 IP Local" e o toohello redirecionado servidor Web com hello endereço IP do 10.0.1.5 do Firewall.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-169">Here any inbound address that hits hello Firewall trying tooreach HTTP (port 80 or 443 for HTTPS) will be sent out hello Firewall’s “DHCP1 Local IP” interface and redirected toohello Web Server with hello IP Address of 10.0.1.5.</span></span> <span data-ttu-id="7d2c2-170">Desde que o tráfego de saudação é recebidas na porta 80 e o servidor de web toohello contínuo na porta 80, nenhuma alteração de porta foi necessária.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-170">Since hello traffic is coming in on port 80 and going toohello web server on port 80 no port change was needed.</span></span> <span data-ttu-id="7d2c2-171">No entanto, Olá lista de destino podem ter sido 10.0.1.5:8080 se o servidor Web escutar na porta 8080, portanto, traduzindo Olá 80 em Olá firewall tooinbound porta 8080 Olá web servidor de porta de entrada.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-171">However, hello Target List could have been 10.0.1.5:8080 if our Web Server listened on port 8080 thus translating hello inbound port 80 on hello firewall tooinbound port 8080 on hello web server.</span></span>

<span data-ttu-id="7d2c2-172">Um método de Conexão deve também ser sinalizado, para Olá regra de destino da saudação da Internet, "SNAT dinâmico" é mais apropriado.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-172">A Connection Method should also be signified, for hello Destination Rule from hello Internet, "Dynamic SNAT" is most appropriate.</span></span> 

<span data-ttu-id="7d2c2-173">Embora somente uma regra tenha sido criada, é importante que sua prioridade seja definida corretamente.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-173">Although only one rule has been created it's important that its priority is set correctly.</span></span> <span data-ttu-id="7d2c2-174">Se na grade de saudação de todas as regras de firewall de saudação a nova regra é na parte inferior da saudação (abaixo da regra de "BLOCKALL" hello), ele nunca será entra em jogo.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-174">If in hello grid of all rules on hello firewall this new rule is on hello bottom (below hello "BLOCKALL" rule) it will never come into play.</span></span> <span data-ttu-id="7d2c2-175">Certifique-se de regra Olá recém-criado para o tráfego da web é acima de regra BLOCKALL hello.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-175">Ensure hello newly created rule for web traffic is above hello BLOCKALL rule.</span></span>

<span data-ttu-id="7d2c2-176">Depois que Olá regra é criada, ela deve ser enviada por push toohello firewall e, em seguida, ativado, se isso não for feito regra Olá alteração não terá efeito.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-176">Once hello rule is created, it must be pushed toohello firewall and then activated, if this is not done hello rule change will not take effect.</span></span> <span data-ttu-id="7d2c2-177">processo de envio e a ativação de saudação é descrito na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-177">hello push and activation process is described in hello next section.</span></span>

## <a name="rule-activation"></a><span data-ttu-id="7d2c2-178">Ativação da regra</span><span class="sxs-lookup"><span data-stu-id="7d2c2-178">Rule Activation</span></span>
<span data-ttu-id="7d2c2-179">Com hello ruleset modificado tooadd essa regra, Olá ruleset deve ser carregado toohello firewall e ativado.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-179">With hello ruleset modified tooadd this rule, hello ruleset must be uploaded toohello firewall and activated.</span></span>

<span data-ttu-id="7d2c2-180">![Ativação de regra de firewall][4]</span><span class="sxs-lookup"><span data-stu-id="7d2c2-180">![Firewall Rule Activation][4]</span></span>

<span data-ttu-id="7d2c2-181">No canto superior direito de saudação do cliente de gerenciamento de saudação são um cluster de botões.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-181">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="7d2c2-182">Olá "enviar alterações" botão toosend Olá modificado regras toohello firewall, clique botão de "Ativar" hello.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-182">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="7d2c2-183">Com a ativação de saudação do conjunto de regras de firewall Olá esta compilação do ambiente de exemplo foi concluída.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-183">With hello activation of hello firewall ruleset this example environment build is complete.</span></span> <span data-ttu-id="7d2c2-184">Opcionalmente, Olá post compilação scripts no hello referências seção pode ser executados tooadd uma saudação de tootest aplicativo toothis ambiente abaixo cenários de tráfego.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-184">Optionally, hello post build scripts in hello References section can be run tooadd an application toothis environment tootest hello below traffic scenarios.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d2c2-185">É toorealize crítica que você não atingirá servidor da web de saudação diretamente.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-185">It is critical toorealize that you will not hit hello web server directly.</span></span> <span data-ttu-id="7d2c2-186">Quando um navegador solicita uma página HTTP do FrontEnd001.CloudApp.Net, servidor web passa de ponto de extremidade (porta 80) HTTP Olá esse tráfego toohello firewall não hello.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-186">When a browser requests an HTTP page from FrontEnd001.CloudApp.Net, hello HTTP endpoint (port 80) passes this traffic toohello firewall not hello web server.</span></span> <span data-ttu-id="7d2c2-187">Olá firewall em seguida, de acordo com regra toohello criado acima NATs que solicitam toohello servidor Web.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-187">hello firewall then, according toohello rule created above, NATs that request toohello Web Server.</span></span>
> 
> 

## <a name="traffic-scenarios"></a><span data-ttu-id="7d2c2-188">Cenários de tráfego</span><span class="sxs-lookup"><span data-stu-id="7d2c2-188">Traffic Scenarios</span></span>
#### <a name="allowed-web-tooweb-server-through-firewall"></a><span data-ttu-id="7d2c2-189">(Permitido) TooWeb Web Server através do Firewall</span><span class="sxs-lookup"><span data-stu-id="7d2c2-189">(Allowed) Web tooWeb Server through Firewall</span></span>
1. <span data-ttu-id="7d2c2-190">Usuário da Internet solicita uma página HTTP de FrontEnd001.CloudApp.Net (Internet Voltada para o Serviço de Nuvem)</span><span class="sxs-lookup"><span data-stu-id="7d2c2-190">Internet user requests HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="7d2c2-191">Tráfego passa do serviço de nuvem por meio de um ponto de extremidade aberto na porta 80 toofirewall local interface 10.0.1.4:80</span><span class="sxs-lookup"><span data-stu-id="7d2c2-191">Cloud service passes traffic through open endpoint on port 80 toofirewall local interface on 10.0.1.4:80</span></span>
3. <span data-ttu-id="7d2c2-192">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="7d2c2-192">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7d2c2-193">Não se aplica a regra 1 (DNS), NSG, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="7d2c2-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7d2c2-194">2 de regra NSG (RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="7d2c2-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="7d2c2-195">Aplicar NSG regra 3 (Internet tooFirewall), o tráfego é o processamento de regras permitido, interrompa</span><span class="sxs-lookup"><span data-stu-id="7d2c2-195">NSG Rule 3 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="7d2c2-196">Tráfego atinge o endereço IP interno do firewall hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="7d2c2-196">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="7d2c2-197">Regra de firewall encaminhamento ver isso é o tráfego na porta 80, redireciona o servidor de web toohello IIS01</span><span class="sxs-lookup"><span data-stu-id="7d2c2-197">Firewall forwarding rule see this is port 80 traffic, redirects it toohello web server IIS01</span></span>
6. <span data-ttu-id="7d2c2-198">IIS01 está escutando o tráfego da web, recebe essa solicitação e inicia o processamento de solicitação de saudação</span><span class="sxs-lookup"><span data-stu-id="7d2c2-198">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
7. <span data-ttu-id="7d2c2-199">IIS01 solicita saudação do SQL Server em AppVM01 informações</span><span class="sxs-lookup"><span data-stu-id="7d2c2-199">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
8. <span data-ttu-id="7d2c2-200">Não há regras de saída na sub-rede Frontend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="7d2c2-200">No outbound rules on Frontend subnet, traffic is allowed</span></span>
9. <span data-ttu-id="7d2c2-201">subrede back-end Olá começa o processamento de regras de entrada:</span><span class="sxs-lookup"><span data-stu-id="7d2c2-201">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7d2c2-202">Não se aplica a regra 1 (DNS), NSG, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="7d2c2-202">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7d2c2-203">2 de regra NSG (RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="7d2c2-203">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="7d2c2-204">NSG regra 3 (tooFirewall da Internet) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="7d2c2-204">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="7d2c2-205">4 de regra NSG (IIS01 tooAppVM01) se aplicam, o tráfego é o processamento de regras permitido, interrompa</span><span class="sxs-lookup"><span data-stu-id="7d2c2-205">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
10. <span data-ttu-id="7d2c2-206">AppVM01 recebe Olá consulta SQL e responde</span><span class="sxs-lookup"><span data-stu-id="7d2c2-206">AppVM01 receives hello SQL Query and responds</span></span>
11. <span data-ttu-id="7d2c2-207">Como não há nenhuma saídas regras em Olá resposta de saudação de sub-rede de back-end é permitido</span><span class="sxs-lookup"><span data-stu-id="7d2c2-207">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
12. <span data-ttu-id="7d2c2-208">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="7d2c2-208">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="7d2c2-209">Não há nenhuma regra NSG que aplica tooInbound tráfego da sub-rede de front-end do toohello de sub-rede de back-end Olá, para que nenhuma das regras do NSG Olá aplicar</span><span class="sxs-lookup"><span data-stu-id="7d2c2-209">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="7d2c2-210">regra do sistema padrão Olá permitindo o tráfego entre as sub-redes permitiria que esse tráfego para que o tráfego de saudação é permitido.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-210">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
13. <span data-ttu-id="7d2c2-211">servidor do IIS Olá recebe a resposta SQL hello e conclui a resposta HTTP hello e envia toohello solicitante</span><span class="sxs-lookup"><span data-stu-id="7d2c2-211">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
14. <span data-ttu-id="7d2c2-212">Como esta é uma sessão NAT de firewall Olá, destino de resposta da saudação (inicialmente) é para Olá Firewall</span><span class="sxs-lookup"><span data-stu-id="7d2c2-212">Since this is a NAT session from hello firewall, hello response destination (initially) is for hello Firewall</span></span>
15. <span data-ttu-id="7d2c2-213">firewall Olá recebe resposta de saudação do Olá Web Server e encaminha back toohello usuário pela Internet</span><span class="sxs-lookup"><span data-stu-id="7d2c2-213">hello firewall receives hello response from hello Web Server and forwards back toohello Internet User</span></span>
16. <span data-ttu-id="7d2c2-214">Como não há nenhum regras de saída em Olá resposta de saudação do front-end subrede é permitido e Olá usuário pela Internet recebe Olá web página solicitada.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-214">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="7d2c2-215">(Permitido) TooBackend RDP</span><span class="sxs-lookup"><span data-stu-id="7d2c2-215">(Allowed) RDP tooBackend</span></span>
1. <span data-ttu-id="7d2c2-216">Administrador do servidor na internet solicitações tooAppVM01 de sessão RDP no BackEnd001.CloudApp.Net:xxxxx onde xxxxx é o número da porta Olá atribuído aleatoriamente para RDP tooAppVM01 (porta Olá atribuído pode ser encontrada em Olá Portal do Azure ou por meio do PowerShell)</span><span class="sxs-lookup"><span data-stu-id="7d2c2-216">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure Portal or via PowerShell)</span></span>
2. <span data-ttu-id="7d2c2-217">Desde Olá que firewall está escutando apenas em Olá FrontEnd001.CloudApp.Net endereço, ele não está envolvido com esse fluxo de tráfego</span><span class="sxs-lookup"><span data-stu-id="7d2c2-217">Since hello Firewall is only listening on hello FrontEnd001.CloudApp.Net address, it is not involved with this traffic flow</span></span>
3. <span data-ttu-id="7d2c2-218">A sub-rede Backend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="7d2c2-218">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7d2c2-219">Não se aplica a regra 1 (DNS), NSG, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="7d2c2-219">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7d2c2-220">A regra NSG 2 (RDP) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="7d2c2-220">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="7d2c2-221">Sem regras de saída, as regras padrão serão aplicadas e o tráfego de retorno será permitido</span><span class="sxs-lookup"><span data-stu-id="7d2c2-221">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="7d2c2-222">A sessão RDP está habilitada</span><span class="sxs-lookup"><span data-stu-id="7d2c2-222">RDP session is enabled</span></span>
6. <span data-ttu-id="7d2c2-223">O AppVM01 solicita a senha do nome de usuário</span><span class="sxs-lookup"><span data-stu-id="7d2c2-223">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="7d2c2-224">(Permitido) Pesquisa de DNS do Servidor Web no servidor DNS</span><span class="sxs-lookup"><span data-stu-id="7d2c2-224">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="7d2c2-225">Web necessidades de servidor, IIS01, um feed de dados em www.data.gov, mas precisa tooresolve Olá endereço.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-225">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="7d2c2-226">Olá configuração de rede para listas de rede virtual Olá DNS01 (10.0.2.4 na sub-rede de back-end Olá) como o servidor DNS primário de hello, IIS01 envia Olá tooDNS01 de solicitação DNS</span><span class="sxs-lookup"><span data-stu-id="7d2c2-226">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="7d2c2-227">Não há regras de saída na sub-rede Frontend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="7d2c2-227">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="7d2c2-228">A sub-rede Backend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="7d2c2-228">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7d2c2-229">A regra NSG 1 (DNS) não se aplica; o tráfego é permitido, pare o processamento da regra</span><span class="sxs-lookup"><span data-stu-id="7d2c2-229">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="7d2c2-230">Servidor DNS recebe a solicitação de saudação</span><span class="sxs-lookup"><span data-stu-id="7d2c2-230">DNS server receives hello request</span></span>
6. <span data-ttu-id="7d2c2-231">Servidor DNS não tem endereço Olá armazenado em cache e solicita que um servidor DNS raiz em Olá internet</span><span class="sxs-lookup"><span data-stu-id="7d2c2-231">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="7d2c2-232">Nenhuma regra de saída na sub-rede Backend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="7d2c2-232">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="7d2c2-233">Resposta de saudação responde do servidor DNS da Internet, desde que esta sessão foi iniciada internamente, é permitida</span><span class="sxs-lookup"><span data-stu-id="7d2c2-233">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="7d2c2-234">Servidor DNS armazena em cache a resposta hello e responde toohello solicitação inicial back tooIIS01</span><span class="sxs-lookup"><span data-stu-id="7d2c2-234">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="7d2c2-235">Nenhuma regra de saída na sub-rede Backend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="7d2c2-235">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="7d2c2-236">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="7d2c2-236">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="7d2c2-237">Não há nenhuma regra NSG que aplica tooInbound tráfego da sub-rede de front-end do toohello de sub-rede de back-end Olá, para que nenhuma das regras do NSG Olá aplicar</span><span class="sxs-lookup"><span data-stu-id="7d2c2-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="7d2c2-238">regra do sistema padrão Olá permitindo o tráfego entre as sub-redes permitiria que esse tráfego para que Olá tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="7d2c2-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="7d2c2-239">IIS01 recebe a resposta de saudação do DNS01</span><span class="sxs-lookup"><span data-stu-id="7d2c2-239">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="7d2c2-240">(Permitido) O arquivo de acesso do Servidor Web em AppVM01</span><span class="sxs-lookup"><span data-stu-id="7d2c2-240">(Allowed) Web Server access file on AppVM01</span></span>
1. <span data-ttu-id="7d2c2-241">IIS01 solicita um arquivo em AppVM01</span><span class="sxs-lookup"><span data-stu-id="7d2c2-241">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="7d2c2-242">Não há regras de saída na sub-rede Frontend; o tráfego é permitido</span><span class="sxs-lookup"><span data-stu-id="7d2c2-242">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="7d2c2-243">subrede back-end Olá começa o processamento de regras de entrada:</span><span class="sxs-lookup"><span data-stu-id="7d2c2-243">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7d2c2-244">Não se aplica a regra 1 (DNS), NSG, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="7d2c2-244">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7d2c2-245">2 de regra NSG (RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="7d2c2-245">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="7d2c2-246">NSG regra 3 (tooFirewall da Internet) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="7d2c2-246">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="7d2c2-247">4 de regra NSG (IIS01 tooAppVM01) se aplicam, o tráfego é o processamento de regras permitido, interrompa</span><span class="sxs-lookup"><span data-stu-id="7d2c2-247">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="7d2c2-248">AppVM01 recebe a solicitação de saudação e responde com o arquivo (supondo que o acesso é autorizado)</span><span class="sxs-lookup"><span data-stu-id="7d2c2-248">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="7d2c2-249">Como não há nenhuma saídas regras em Olá resposta de saudação de sub-rede de back-end é permitido</span><span class="sxs-lookup"><span data-stu-id="7d2c2-249">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
6. <span data-ttu-id="7d2c2-250">A sub-rede Frontend inicia o processamento da regra de entrada:</span><span class="sxs-lookup"><span data-stu-id="7d2c2-250">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7d2c2-251">Não há nenhuma regra NSG que aplica tooInbound tráfego da sub-rede de front-end do toohello de sub-rede de back-end Olá, para que nenhuma das regras do NSG Olá aplicar</span><span class="sxs-lookup"><span data-stu-id="7d2c2-251">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="7d2c2-252">regra do sistema padrão Olá permitindo o tráfego entre as sub-redes permitiria que esse tráfego para que o tráfego de saudação é permitido.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-252">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="7d2c2-253">servidor do IIS Olá recebe arquivo hello</span><span class="sxs-lookup"><span data-stu-id="7d2c2-253">hello IIS server receives hello file</span></span>

#### <a name="denied-web-direct-tooweb-server"></a><span data-ttu-id="7d2c2-254">(Negado) TooWeb direta do Web Server</span><span class="sxs-lookup"><span data-stu-id="7d2c2-254">(Denied) Web direct tooWeb Server</span></span>
<span data-ttu-id="7d2c2-255">Desde Olá servidor Web, IIS01 e Olá Firewall são em Olá mesmo serviço de nuvem, eles compartilham Olá mesmo endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-255">Since hello Web Server, IIS01, and hello Firewall are in hello same Cloud Service they share hello same public facing IP address.</span></span> <span data-ttu-id="7d2c2-256">Assim, qualquer tráfego HTTP seria direcionado toohello firewall.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-256">Thus any HTTP traffic would be directed toohello firewall.</span></span> <span data-ttu-id="7d2c2-257">Enquanto a solicitação de saudação utilizarão com êxito, não pode ir diretamente toohello servidor Web, ele passado como criados, por meio de saudação do Firewall pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-257">While hello request would be successfully served, it cannot go directly toohello Web Server, it passed, as designed, through hello Firewall first.</span></span> <span data-ttu-id="7d2c2-258">Consulte Olá primeiro cenário nesta seção para fluxo de tráfego de saudação.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-258">See hello first Scenario in this section for hello traffic flow.</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="7d2c2-259">(Negado) TooBackend Web Server</span><span class="sxs-lookup"><span data-stu-id="7d2c2-259">(Denied) Web tooBackend Server</span></span>
1. <span data-ttu-id="7d2c2-260">Usuário de Internet tenta tooaccess um arquivo em AppVM01 por meio de saudação BackEnd001.CloudApp.Net serviço</span><span class="sxs-lookup"><span data-stu-id="7d2c2-260">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="7d2c2-261">Como não há nenhum ponto de extremidade aberto para compartilhamento de arquivos, isso não passaria Olá serviço de nuvem e não alcançar o servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="7d2c2-261">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="7d2c2-262">Se o ponto de extremidade de saudação estava aberto por algum motivo, a regra NSG 5 (Internet tooVNet) bloqueia esse tráfego</span><span class="sxs-lookup"><span data-stu-id="7d2c2-262">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-lookup-on-dns-server"></a><span data-ttu-id="7d2c2-263">(Negado) Pesquisa de DNS na Web no servidor DNS</span><span class="sxs-lookup"><span data-stu-id="7d2c2-263">(Denied) Web DNS lookup on DNS server</span></span>
1. <span data-ttu-id="7d2c2-264">Usuário de Internet tenta toolookup um registro DNS interno em DNS01 por meio de saudação BackEnd001.CloudApp.Net serviço</span><span class="sxs-lookup"><span data-stu-id="7d2c2-264">Internet user tries toolookup an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="7d2c2-265">Como não há nenhum ponto de extremidade aberto para DNS, isso não passaria Olá serviço de nuvem e não alcançar o servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="7d2c2-265">Since there are no endpoints open for DNS, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="7d2c2-266">Se o ponto de extremidade de saudação estava aberto por algum motivo, a regra NSG 5 (Internet tooVNet) bloqueia esse tráfego (Observação: essa regra 1 (DNS) não se aplicariam por dois motivos, primeiro endereço de origem de saudação é Olá da internet, esta regra só se aplica a toohello redes locais como saudação de origem, também Esta é uma regra de permissão, para que ele nunca seria negar o tráfego)</span><span class="sxs-lookup"><span data-stu-id="7d2c2-266">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="7d2c2-267">(Negado) Acesso via Web tooSQL através do Firewall</span><span class="sxs-lookup"><span data-stu-id="7d2c2-267">(Denied) Web tooSQL access through Firewall</span></span>
1. <span data-ttu-id="7d2c2-268">O usuário da Internet solicita dados SQL de FrontEnd001.CloudApp.Net (Serviço de Nuvem Voltado para a Internet)</span><span class="sxs-lookup"><span data-stu-id="7d2c2-268">Internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="7d2c2-269">Como não há nenhum ponto de extremidade aberto para SQL, isso não passaria Olá serviço de nuvem e não alcançar o firewall Olá</span><span class="sxs-lookup"><span data-stu-id="7d2c2-269">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="7d2c2-270">Se o ponto de extremidade estava aberto por algum motivo, sub-rede front-end de saudação começa o processamento de regras de entrada:</span><span class="sxs-lookup"><span data-stu-id="7d2c2-270">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7d2c2-271">Não se aplica a regra 1 (DNS), NSG, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="7d2c2-271">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7d2c2-272">2 de regra NSG (RDP) não se aplica, mover toonext regra</span><span class="sxs-lookup"><span data-stu-id="7d2c2-272">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="7d2c2-273">Aplicar NSG regra 2 (Internet tooFirewall), o tráfego é o processamento de regras permitido, interrompa</span><span class="sxs-lookup"><span data-stu-id="7d2c2-273">NSG Rule 2 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="7d2c2-274">Tráfego atinge o endereço IP interno do firewall hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="7d2c2-274">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="7d2c2-275">Firewall não tem nenhuma regra de encaminhamento para SQL e descarta Olá tráfego</span><span class="sxs-lookup"><span data-stu-id="7d2c2-275">Firewall has no forwarding rules for SQL and drops hello traffic</span></span>

## <a name="conclusion"></a><span data-ttu-id="7d2c2-276">Conclusão</span><span class="sxs-lookup"><span data-stu-id="7d2c2-276">Conclusion</span></span>
<span data-ttu-id="7d2c2-277">Essa é uma maneira relativamente simples de proteger seu aplicativo com um firewall e o isolamento de sub-rede de back-end de saudação do tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-277">This is a relatively straight forward way of protecting your application with a firewall and isolating hello back end subnet from inbound traffic.</span></span>

<span data-ttu-id="7d2c2-278">Mais exemplos e uma visão geral dos limites de segurança de rede podem ser encontrados [aqui][HOME].</span><span class="sxs-lookup"><span data-stu-id="7d2c2-278">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="7d2c2-279">Referências</span><span class="sxs-lookup"><span data-stu-id="7d2c2-279">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="7d2c2-280">Script principal e configuração de rede</span><span class="sxs-lookup"><span data-stu-id="7d2c2-280">Main Script and Network Config</span></span>
<span data-ttu-id="7d2c2-281">Salve Olá Script completo em um arquivo de script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-281">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="7d2c2-282">Salve Olá configuração de rede em um arquivo denominado "NetworkConf2.xml".</span><span class="sxs-lookup"><span data-stu-id="7d2c2-282">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="7d2c2-283">Modificar as variáveis definidas pelo usuário de saudação conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-283">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="7d2c2-284">Executar script hello, siga as instruções regra de configuração do Firewall Olá acima.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-284">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="7d2c2-285">Script Completo</span><span class="sxs-lookup"><span data-stu-id="7d2c2-285">Full Script</span></span>
<span data-ttu-id="7d2c2-286">Esse script vai, com base em variáveis do hello definida pelo usuário:</span><span class="sxs-lookup"><span data-stu-id="7d2c2-286">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="7d2c2-287">Conecte-se tooan assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="7d2c2-287">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="7d2c2-288">Criar uma nova conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="7d2c2-288">Create a new storage account</span></span>
3. <span data-ttu-id="7d2c2-289">Criar uma nova rede virtual e duas sub-redes, conforme definido no arquivo de configuração de rede de saudação</span><span class="sxs-lookup"><span data-stu-id="7d2c2-289">Create a new VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="7d2c2-290">Criar 4 VMs do windows server</span><span class="sxs-lookup"><span data-stu-id="7d2c2-290">Build 4 windows server VMs</span></span>
5. <span data-ttu-id="7d2c2-291">Configure o NSG, incluindo:</span><span class="sxs-lookup"><span data-stu-id="7d2c2-291">Configure NSG including:</span></span>
   * <span data-ttu-id="7d2c2-292">Criando um NSG</span><span class="sxs-lookup"><span data-stu-id="7d2c2-292">Creating a NSG</span></span>
   * <span data-ttu-id="7d2c2-293">Preenchendo-o com regras</span><span class="sxs-lookup"><span data-stu-id="7d2c2-293">Populating it with rules</span></span>
   * <span data-ttu-id="7d2c2-294">Associação de sub-redes apropriados da saudação NSG toohello</span><span class="sxs-lookup"><span data-stu-id="7d2c2-294">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="7d2c2-295">Este script do PowerShell deve ser executado localmente em um computador ou servidor conectado à Internet.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-295">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d2c2-296">Quando esse script for executado, poderá haver avisos ou outras mensagens informativas que aparecerão no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-296">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="7d2c2-297">Somente as mensagens de erro em vermelho são motivo de preocupação.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-297">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
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
       myFirewall - 10.0.1.4
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
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

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
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
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


#### <a name="network-config-file"></a><span data-ttu-id="7d2c2-298">Arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="7d2c2-298">Network Config File</span></span>
<span data-ttu-id="7d2c2-299">Salve esse arquivo xml com o local atualizado e adicione Olá link toothis arquivo toohello $NetworkConfigFile variável no script de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="7d2c2-299">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="7d2c2-300">Scripts de aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="7d2c2-300">Sample Application Scripts</span></span>
<span data-ttu-id="7d2c2-301">Se você quiser tooinstall um aplicativo de exemplo para este e outros exemplos de rede de Perímetro, foi fornecido no hello link a seguir: [Script de exemplo de aplicativo][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="7d2c2-301">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "DMZ de entrada com NSG"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Ícone de NAT de destino"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Regra de Firewall"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Ativação de regra de firewall"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
