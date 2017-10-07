---
title: aaaAzure perguntas Frequentes de rede Virtual | Microsoft Docs
description: As respostas toohello mais perguntas frequentes sobre redes virtuais do Microsoft Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 54bee086-a8a5-4312-9866-19a1fba913d0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/18/2017
ms.author: jdial
ms.openlocfilehash: c2f9faee41b9c45e8bb196c58282d597ae732e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network-frequently-asked-questions-faq"></a>Perguntas frequentes sobre a rede virtual do Azure (FAQ)

## <a name="virtual-network-basics"></a>Noções básicas sobre redes virtuais

### <a name="what-is-an-azure-virtual-network-vnet"></a>O que é uma Rede Virtual (VNet) do Azure?
Uma rede Virtual do Azure (VNet) é uma representação de sua própria rede na nuvem hello. É uma isolamento lógico de saudação nuvem do Azure dedicado tooyour assinatura. Você pode usar VNets tooprovision e gerenciar redes virtuais privadas (VPNs) no Azure e, opcionalmente, Olá link VNets com outras VNets no Azure, ou ao seu local soluções de híbrida ou entre locais de toocreate de infraestrutura de TI. Cada rede virtual que você cria tem seu próprio bloco CIDR e pode ser vinculado tooother redes locais e VNets como blocos CIDR Olá não se sobrepõem. Você também tem controle de configurações do servidor DNS para VNets e segmentação de rede virtual do hello em sub-redes.

Use redes virtuais para:

* Crie uma VNet dedicada apenas para nuvem privada Às vezes, você não precisa de uma configuração entre locais para sua solução. Quando você cria uma rede virtual, seus serviços e VMs em sua rede virtual podem se comunicar diretamente e com segurança entre si na nuvem hello. Isso mantém o tráfego com segurança em Olá VNet, mas ainda permite que você tooconfigure conexões de ponto de extremidade para Olá VMs e serviços que exigem a comunicação com a Internet como parte de sua solução.
* Estende com segurança o seu data center com VNets, você pode criar a expansão vertical tradicionais site a site (S2S) VPNs toosecurely a capacidade do datacenter. VPNs S2S use IPSEC tooprovide uma conexão segura entre o gateway VPN corporativa e o Azure.
* Cenários de nuvem híbrida habilitar que vnets lhe Olá flexibilidade toosupport uma variedade de cenários de nuvem híbrida. Você pode se conectar com segurança tipo tooany de aplicativos baseados em nuvem do sistema local, como mainframes e sistemas Unix.

### <a name="how-do-i-know-if-i-need-a-vnet"></a>Como saber se eu preciso de uma VNet?
Olá [visão geral da rede Virtual](virtual-networks-overview.md) artigo fornece uma tabela de decisão que ajudarão você a decidir Olá melhor opção de rede design para você.

### <a name="how-do-i-get-started"></a>Como começar?
Visite Olá [documentação de rede Virtual](https://docs.microsoft.com/azure/virtual-network/) tooget iniciado. Este conteúdo fornece informações de visão geral e implantação para todos os recursos de rede virtual hello.

### <a name="can-i-use-vnets-without-cross-premises-connectivity"></a>Posso usar redes virtuais sem conectividade entre locais?
Sim. É possível usar uma rede virtual sem usar conectividade híbrida. Isso é particularmente útil se você desejar controladores de domínio do Active Directory do Microsoft Windows Server toorun e farms do SharePoint no Azure.

### <a name="can-i-perform-wan-optimization-between-vnets-or-a-vnet-and-my-on-premises-data-center"></a>Posso realizar uma otimização de WAN entre redes virtuais ou entre uma rede virtual e meu data center local?

Sim. Você pode implantar um [solução de virtualização de rede WAN otimização](https://azure.microsoft.com/marketplace/?term=wan+optimization) de vários fornecedores por meio de saudação do Azure Marketplace.

## <a name="configuration"></a>Configuração

### <a name="what-tools-do-i-use-toocreate-a-vnet"></a>Ferramentas fazem uso toocreate uma rede virtual?
Você pode usar o hello toocreate ferramentas a seguir ou configurar uma rede virtual:

* Portal do Azure (para Redes Virtuais clássicas e do Gerenciador de Recursos).
* Um arquivo de configuração de rede (netcfg - somente para Redes Virtuais clássicas). Consulte Olá [configurar uma rede virtual usando um arquivo de configuração de rede](virtual-networks-using-network-configuration-file.md) artigo.
* PowerShell (para Redes Virtuais clássicas e do Gerenciador de Recursos).
* CLI do Azure (para Redes Virtuais clássicas e do Gerenciador de Recursos).

### <a name="what-address-ranges-can-i-use-in-my-vnets"></a>Quais intervalos de endereço posso usar em minhas redes virtuais?
Qualquer intervalo de endereços IP definido na [RFC 1918](http://tools.ietf.org/html/rfc1918). Por exemplo, 10.0.0.0/16.

### <a name="can-i-have-public-ip-addresses-in-my-vnets"></a>Posso ter endereços IP públicos em minhas redes virtuais?
Sim. Para obter mais informações sobre intervalos de endereços IP públicos, consulte Olá [espaço de endereço IP público em uma rede virtual](virtual-networks-public-ip-within-vnet.md) artigo. Os endereços IP públicos não será diretamente acessíveis pela Internet da saudação.

### <a name="is-there-a-limit-toohello-number-of-subnets-in-my-vnet"></a>Há um número de toohello limite de sub-redes na minha rede virtual?
Sim. Saudação de leitura [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo para obter detalhes. Espaços de endereço de sub-rede não podem se sobrepor.

### <a name="are-there-any-restrictions-on-using-ip-addresses-within-these-subnets"></a>Existem restrições quanto ao uso de endereços IP dentro dessas sub-redes?
Sim. O Azure reserva alguns endereços IP em cada sub-rede. Olá primeiro e últimos endereços IP das sub-redes Olá são reservados para conformidade de protocolo, juntamente com 3 endereços mais usados para serviços do Azure.

### <a name="how-small-and-how-large-can-vnets-and-subnets-be"></a>Que tamanho, máximo e mínimo, as redes virtuais e sub-redes podem ter?
menor sub-rede Olá com que suporte é/29 e Olá maior é/8 (usando definições de subrede CIDR).

### <a name="can-i-bring-my-vlans-tooazure-using-vnets"></a>Posso trazer minha tooAzure VLANs usando VNets?
Não. As v são sobreposições da Camada 3. O Azure não oferece suporte a nenhuma semântica da Camada 2.

### <a name="can-i-specify-custom-routing-policies-on-my-vnets-and-subnets"></a>Posso especificar políticas de roteamento personalizadas nas minhas redes virtuais e sub-redes?
Sim. Você pode usar o UDR (Roteamento Definido pelo Usuário). Para saber mais sobre UDR, visite [Rotas definidas pelo usuário e Encaminhamento IP](virtual-networks-udr-overview.md).

### <a name="do-vnets-support-multicast-or-broadcast"></a>As redes virtuais oferecem suporte ao multicast ou à difusão?
Não. Não há suporte para nenhum dos dois.

### <a name="what-protocols-can-i-use-within-vnets"></a>Quais protocolos posso usar nas redes virtuais?
Você pode usar protocolos TCP, UDP e ICMP TCP/IP em redes virtuais. Pacotes encapsulados de IP em IP, multicast, difusão e pacotes de Encapsulamento de Roteamento Genérico (GRE) são bloqueados nas redes virtuais. 

### <a name="can-i-ping-my-default-routers-within-a-vnet"></a>Posso executar ping em meus roteadores padrão em uma rede virtual?
Não.

### <a name="can-i-use-tracert-toodiagnose-connectivity"></a>Posso usar o tracert toodiagnose conectividade?
Não.

### <a name="can-i-add-subnets-after-hello-vnet-is-created"></a>Pode adicionar sub-redes depois Olá que vnet é criada?
Sim. Subredes podem ser adicionados tooVNets a qualquer momento desde que o endereço de sub-rede Olá não é parte de outra sub-rede na Olá VNet.

### <a name="can-i-modify-hello-size-of-my-subnet-after-i-create-it"></a>Pode modificar o tamanho de saudação do meu sub-rede depois de criá-lo?
Sim. Você poderá adicionar, remover, expandir ou reduzir uma sub-rede se não houver VMs ou serviços implantados nela.

### <a name="can-i-modify-subnets-after-i-created-them"></a>Posso modificar sub-redes depois de criá-las?
Sim. Você pode adicionar, remover e modificar os blocos CIDR Olá usados por uma rede virtual.

### <a name="can-i-connect-toohello-internet-if-i-am-running-my-services-in-a-vnet"></a>Posso conectar toohello internet se estiver executando meus serviços em uma rede virtual?
Sim. Todos os serviços implantados em uma rede virtual podem se conectar a toohello internet. Cada serviço de nuvem implantado no Azure tem um VIP publicamente endereçável atribuído tooit. Você terá pontos de extremidade de entrada de toodefine para funções de PaaS e pontos de extremidade para máquinas virtuais tooenable esses serviços tooaccept conexões de saudação à internet.

### <a name="do-vnets-support-ipv6"></a>As redes virtuais oferecem suporte ao IPv6?
Não. Não é possível usar o IPv6 com redes virtuais neste momento.

### <a name="can-a-vnet-span-regions"></a>Uma rede virtual pode abranger regiões?
Não. Uma rede virtual é limitado tooa única região.

### <a name="can-i-connect-a-vnet-tooanother-vnet-in-azure"></a>Posso conectar uma rede virtual tooanother VNet no Azure?
Sim. Você pode se conectar a uma rede virtual tooanother VNet usando:
- um Gateway de VPN do Azure. Saudação de leitura [configurar uma conexão de rede virtual a rede](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artigo para obter detalhes. 
- Emparelhamento VNet. Saudação de leitura [visão geral de emparelhamento VNet](virtual-network-peering-overview.md) artigo para obter detalhes.

## <a name="name-resolution-dns"></a>Resolução de nomes (DNS)

### <a name="what-are-my-dns-options-for-vnets"></a>Quais são minhas opções DNS para redes virtuais?
Tabela de decisões Olá use em Olá [resolução de nomes para VMs e instâncias de função](virtual-networks-name-resolution-for-vms-and-role-instances.md) tooguide de página em todas as Olá DNS opções disponíveis.

### <a name="can-i-specify-dns-servers-for-a-vnet"></a>Posso especificar servidores DNS para uma rede virtual?
Sim. Você pode especificar endereços IP do servidor DNS nas configurações de rede virtual hello. Isso será aplicado como servidores DNS a saudação padrão para todas as VMs em redes de saudação.

### <a name="how-many-dns-servers-can-i-specify"></a>Quantos servidores DNS posso especificar?
Saudação de referência [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo para obter detalhes.

### <a name="can-i-modify-my-dns-servers-after-i-have-created-hello-network"></a>Posso modificar meus servidores DNS depois de ter criado rede Olá?
Sim. Você pode alterar a lista de servidores DNS Olá para sua rede virtual a qualquer momento. Se você alterar sua lista de servidores DNS, será necessário toorestart Olá VMs na sua rede virtual para que eles toopick o novo servidor DNS hello.

### <a name="what-is-azure-provided-dns-and-does-it-work-with-vnets"></a>O que é o DNS fornecido pelo Azure? Ele funciona com redes virtuais?
O DNS fornecido pelo Azure é um serviço DNS multilocatário oferecido pela Microsoft. O Azure registra todas as VMs e instâncias de função do serviço de nuvem nesse serviço. Esse serviço fornece a resolução de nomes por nome de host para VMs e instâncias de função contidas Olá mesmo serviço de nuvem e pelo FQDN para VMs e instâncias de função em Olá mesma rede virtual. Saudação de leitura [resolução de nomes para VMs e instâncias de função](virtual-networks-name-resolution-for-vms-and-role-instances.md) artigo toolearn mais sobre o DNS.

> [!NOTE]
> Há uma limitação no toohello tempo primeiros 100 serviços de nuvem em uma rede virtual para resolução de nome entre locatários usando o DNS fornecido pelo Azure. Se você estiver usando seu próprio servidor DNS, essa limitação não se aplicará.
> 
> 

### <a name="can-i-override-my-dns-settings-on-a-per-vm--service-basis"></a>Posso substituir minhas configurações DNS por VM/serviço?
Sim. Você pode definir servidores DNS por nuvem serviço base toooverride saudação padrão as configurações de rede. No entanto, é recomendável usar DNS para toda a rede, tanto quanto possível.

### <a name="can-i-bring-my-own-dns-suffix"></a>Posso colocar meu próprio sufixo DNS?
Não. Você não pode especificar um sufixo DNS personalizado para suas redes virtuais.

## <a name="connecting-virtual-machines"></a>Conexão de máquinas virtuais

### <a name="can-i-deploy-vms-tooa-vnet"></a>Posso implantar VMs tooa VNet?
Sim. Todos os tooa de interfaces (NIC) anexados de rede VM implantada por meio do modelo de implantação do Gerenciador de recursos de saudação deve ser conectado tooa VNet. As VMs implantadas por meio do modelo de implantação clássico Olá podem ser conectado tooa VNet.

### <a name="what-are-hello-different-types-of-ip-addresses-i-can-assign-toovms"></a>Quais são os tipos diferentes de saudação tooVMs pode atribuir endereços IP?
* **Particular:** atribuído tooeach NIC dentro de cada VM. endereço de saudação é atribuído usando um método estático ou dinâmico de saudação. São atribuídos endereços IP privados de intervalo de saudação especificado nas configurações de sub-rede de saudação da sua rede virtual. Os recursos implantados por meio do modelo de implantação clássico Olá recebem endereços IP privados, mesmo se eles não estão conectados tooa VNet. Um endereço IP privado atribuído permanece de método dinâmico Olá atribuído tooa recurso até que o recurso de saudação é excluído (máquinas virtuais ou serviço de nuvem slots de implantação). Um endereço IP privado atribuído com método dinâmico Olá pode mudar quando uma VM for reiniciada depois de ter sido Olá interrompido estado (desalocado). Um endereço IP privado atribuído com hello método estático permanece atribuído tooa recurso até que o recurso de saudação é excluído. Se você precisar tooensure esse endereço IP privado de saudação para um recurso nunca é alterado até que o recurso de saudação é excluído, atribua um endereço IP privado com o método estático hello.
* **Público:** tooNICs opcionalmente atribuído anexado tooVMs implantadas por meio do modelo de implantação do Azure Resource Manager hello. endereço de saudação pode ser atribuído com o método de alocação estática ou dinâmica hello. Todas as VMs e serviços de nuvem instâncias de função implantadas por meio do modelo de implantação clássico Olá existem em um serviço de nuvem, que é atribuído um *dinâmico*, público endereço IP virtual (VIP). Um endereço IP público e *estático*, chamado de [endereço IP Reservado](virtual-networks-reserved-public-ip.md), pode ser atribuído como VIP. Você pode atribuir tooindividual de endereços IP público VMs ou serviços de nuvem instâncias de função implantadas por meio do modelo de implantação clássico hello. Eles são chamados de [endereços IP públicos em nível de instância (ILPIP)](virtual-networks-instance-level-public-ip.md) e podem ser atribuídos dinamicamente.

### <a name="can-i-reserve-a-private-ip-address-for-a-vm-that-i-will-create-at-a-later-time"></a>Posso reservar um endereço IP privado para uma VM que vou criar mais tarde?
Não. Não é possível reservar um endereço IP privado. Se houver um endereço IP privado ele será atribuído tooa VM ou instância de função servidor DHCP de saudação. Essa VM pode ou não pode ser Olá que você deseja Olá privada IP endereço toobe atribuído ao. No entanto, você pode alterar o endereço IP privado de saudação de um já criada VM tooany disponível endereço IP privado.

### <a name="do-private-ip-addresses-change-for-vms-in-a-vnet"></a>Os endereços IP privado mudam para VMs em uma rede virtual?
Isso depende. Endereços IP privados dinâmicos permanecem com uma máquina virtual que ela seja interrompida (desalocada) ou excluída. Endereços IP privados estáticos só são liberados de uma VM quando esta é excluída.

### <a name="can-i-manually-assign-ip-addresses-toonics-within-hello-vm-operating-system"></a>Posso manualmente atribuir tooNICs de endereços IP no sistema operacional da VM Olá?
Sim, mas não é recomendável. Alterar manualmente o endereço IP de saudação para uma NIC no sistema operacional da VM pode levar toolosing conectividade toohello VM se o endereço IP de saudação atribuído tooa NIC dentro Olá VM do Azure foram toochange.

### <a name="what-happens-toomy-ip-addresses-if-i-stop-a-cloud-service-deployment-slot-or-shutdown-a-vm-from-within-hello-operating-system"></a>O que acontece toomy endereços IP se eu parar um slot de implantação do serviço de nuvem ou desligar uma VM de dentro do sistema operacional de saudação?
Nada. endereços IP de saudação (VIP público, público e privado) permanecem toohello atribuído slot de implantação de serviço de nuvem ou máquina virtual. Os endereços dinâmicos só são liberados se uma VM for interrompida (desalocada) ou excluída ou se um slot de implantação do serviço de nuvem for excluído. Olá clicando em **parar** botão para uma VM em Olá portal do Azure define seu tooStopped estado (desalocado). Nesse caso, a saudação VM perderá seus endereços IP.

### <a name="can-i-move-vms-from-one-subnet-tooanother-subnet-in-a-vnet-without-re-deploying"></a>Posso mover máquinas virtuais de uma sub-rede tooanother de sub-rede em uma rede virtual sem reimplantação?
Sim. Você pode encontrar mais informações no hello [como toomove uma VM ou uma função de instância tooa outra sub-rede](virtual-networks-move-vm-role-to-subnet.md) artigo.

### <a name="can-i-configure-a-static-mac-address-for-my-vm"></a>Posso configurar um endereço MAC estático para minha VM?
Não. Um endereço MAC não pode ser configurado estaticamente.

### <a name="will-hello-mac-address-remain-hello-same-for-my-vm-once-it-has-been-created"></a>Olá endereço MAC permanecerá Olá mesmo para minha VM depois de ele ter sido criado?
Sim, Olá endereço MAC permanecerá Olá que mesmo para uma VM implantados por meio de saudação Gerenciador de recursos e modelos de implantação clássico até serem excluídas. Anteriormente, Olá endereço MAC foi liberada se hello VM foi parada (desalocada), mas agora endereço MAC de saudação é mantido mesmo quando Olá VM está em Olá desalocada estado.

### <a name="can-i-connect-toohello-internet-from-a-vm-in-a-vnet"></a>Posso conectar toohello internet por meio de uma VM em uma rede virtual?
Sim. Instâncias de função de todas as VMs e serviços de nuvem implantadas em uma rede virtual podem se conectar a toohello da Internet.

## <a name="azure-services-that-connect-toovnets"></a>Serviços do Azure que se conectam tooVNets

### <a name="can-i-use-azure-app-service-web-apps-with-a-vnet"></a>Posso usar os Aplicativos Web do Serviço de Aplicativo do Azure em uma rede virtual?
Sim. Você pode implantar Aplicativos Web em uma rede virtual usando o ASE (Ambiente do Serviço de Aplicativo). Todos os Aplicativos Web poderão se conectar e acessar os recursos na Rede Virtual do Azure se você tiver configurado uma conexão ponto a site para sua rede virtual. Para obter mais informações, consulte Olá artigos a seguir:

* [Criando Aplicativos Web em um Ambiente do Serviço de Aplicativo](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Integrar seu aplicativo a uma Rede Virtual do Azure](../app-service-web/web-sites-integrate-with-vnet.md)
* [Usando conexões híbridas e integração de rede virtual com Aplicativos Web](../app-service-web/web-sites-integrate-with-vnet.md#hybrid-connections-and-app-service-environments)

### <a name="can-i-deploy-cloud-services-with-web-and-worker-roles-paas-in-a-vnet"></a>Posso implantar Serviços de Nuvem com funções web e de trabalho (PaaS) em uma rede virtual?
Sim. Você pode implantar instâncias de função de Serviços de Nuvem em redes virtuais. toodo assim, você pode especificar nome de rede virtual hello e mapeamentos de função/sub-rede Olá na seção de configuração de rede de saudação da sua configuração de serviço. Não é necessário tooupdate nenhum de seus binários.

### <a name="can-i-connect-a-virtual-machine-scale-set-vmss-tooa-vnet"></a>Posso conectar uma rede virtual de tooa do conjunto de escala de máquina Virtual (VMSS)?
Sim. Você deve se conectar a um tooa VMSS VNet.

### <a name="can-i-move-my-services-in-and-out-of-vnets"></a>Posso mover meus serviços para dentro e fora das redes virtuais?
Não. Não é possível mover serviços para dentro e fora das redes virtuais. Você terá toodelete e reimplantar Olá serviço toomove-tooanother VNet.

## <a name="security"></a>Segurança

### <a name="what-is-hello-security-model-for-vnets"></a>O que é o modelo de segurança Olá para VNets?
VNets são completamente isoladas uma da outra, e outros serviços hospedados em Olá infraestrutura do Azure. Uma rede virtual é um limite de confiança.

### <a name="can-i-restrict-inbound-or-outbound-traffic-flow-toovnet-connected-resources"></a>Pode restringir o recursos de conectado tooVNet de fluxo de tráfego de entrada ou saída?
Sim. Você pode aplicar [grupos de segurança de rede](virtual-networks-nsg.md) tooindividual sub-redes dentro de uma rede virtual NICs conectados tooa VNet, ou ambos.

### <a name="can-i-implement-a-firewall-between-vnet-connected-resources"></a>Posso implementar um firewall entre os recursos conectados à rede virtual?
Sim. Você pode implantar um [solução de virtualização de rede do firewall](https://azure.microsoft.com/en-us/marketplace/?term=firewall) de vários fornecedores por meio de saudação do Azure Marketplace.

### <a name="is-there-information-available-about-securing-vnets"></a>Existem informações disponíveis sobre como proteger redes virtuais?
Sim. Consulte Olá [visão geral de segurança de rede do Azure](../security/security-network-overview.md) artigo para obter detalhes.

## <a name="apis-schemas-and-tools"></a>APIs, esquemas e ferramentas

### <a name="can-i-manage-vnets-from-code"></a>Posso gerenciar redes virtuais usando código?
Sim. Você pode usar APIs REST para VNets em Olá [do Azure Resource Manager](https://msdn.microsoft.com/library/mt163658.aspx) e [clássico (gerenciamento de serviço)](http://go.microsoft.com/fwlink/?LinkId=296833)) modelos de implantação.

### <a name="is-there-tooling-support-for-vnets"></a>Há suporte a ferramentas para redes virtuais?
Sim. Saiba mais sobre como usar:
- Olá VNets toodeploy portal do Azure por meio de saudação [do Azure Resource Manager](virtual-networks-create-vnet-arm-pportal.md) e [clássico](virtual-networks-create-vnet-classic-pportal.md) modelos de implantação.
- PowerShell toomanage VNets implantados por meio de saudação [Gerenciador de recursos de](/powershell/resourcemanager/azurerm.network/v3.1.0/azurerm.network.md) e [clássico](/powershell/module/azure/?view=azuresmps-3.7.0) modelos de implantação.
- Olá [interface de linha de comando (CLI) do Azure](../virtual-machines/azure-cli-arm-commands.md#azure-network-commands-to-manage-network-resources) toomanage VNets implantados por meio de ambos os modelos de implantação.  
