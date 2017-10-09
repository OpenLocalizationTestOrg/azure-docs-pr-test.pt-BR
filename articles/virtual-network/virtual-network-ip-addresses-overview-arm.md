---
title: "tipos de endereço aaaIP no Azure | Microsoft Docs"
description: "Saiba mais sobre endereços IP públicos e privados no Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-resource-manager
ms.assetid: 610b911c-f358-4cfe-ad82-8b61b87c3b7e
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 402d3707c00f0b3bf3ef1febd5ade66223da74bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-in-azure"></a>Tipos de endereço IP e métodos de alocação no Azure
Você pode atribuir IP endereços tooAzure recursos toocommunicate com outros recursos do Azure, sua rede local e Olá da Internet. Há dois tipos de endereços IP que você pode usar no Azure:

* **Endereços IP públicos**: usado para comunicação com hello Internet, incluindo serviços voltados ao público do Azure
* **Endereços IP privados**: usada para comunicação em uma rede virtual do Azure (VNet), e seu local de rede quando você usar um gateway VPN ou tooextend de circuito de rota expressa tooAzure sua rede.

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).  Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez da saudação [modelo de implantação clássico](virtual-network-ip-addresses-overview-classic.md).
> 

Se você estiver familiarizado com o modelo de implantação clássico Olá, verifique Olá [as diferenças entre clássico de endereçamento IP e o Gerenciador de recursos](virtual-network-ip-addresses-overview-classic.md#differences-between-resource-manager-and-classic-deployments).

## <a name="public-ip-addresses"></a>Endereços IP públicos
Endereços IP públicos permitem toocommunicate de recursos do Azure com os serviços da Internet e o Azure públicos, como [Cache Redis do Azure](https://azure.microsoft.com/services/cache/), [Hubs de eventos do Azure](https://azure.microsoft.com/services/event-hubs/), [bancos de dados do SQL](../sql-database/sql-database-technical-overview.md), e [armazenamento do Azure](../storage/common/storage-introduction.md).

No Gerenciador de recursos do Azure, um endereço [IP público](resource-groups-networking.md#public-ip-address) é um recurso com as próprias propriedades. Você pode associar um recurso de endereço IP público com qualquer Olá recursos a seguir:

* VM (máquinas virtuais)
* Balanceadores de carga para Internet
* Gateways VPN
* Application gateways

### <a name="allocation-method"></a>Método de alocação
Há dois métodos em que um endereço IP é alocado tooa *pública* recurso IP - *dinâmico* ou *estático*. método de alocação padrão Olá é *dinâmico*, onde é o endereço IP **não** alocada no tempo de saudação de sua criação. Em vez disso, o endereço IP público de saudação é alocado quando você iniciar (ou cria) recursos Olá associado (como um balanceador de carga ou de VM). endereço IP de saudação é liberado quando você interromper (ou excluir) recursos de saudação. Isso faz com que toochange de endereço IP hello quando você para e iniciar um recurso.

endereço IP tooensure Olá Olá recurso associado permanece Olá mesmo, você pode definir o método de alocação Olá explicitamente muito*estático*. Nesse caso, um endereço IP é atribuído imediatamente. Ele é liberado apenas quando você excluir o recurso de saudação ou alterar seu método de alocação muito*dinâmico*.

> [!NOTE]
> Mesmo quando você define o método de alocação Olá muito*estático*, você não pode especificar Olá real IP endereço atribuído toohello *recurso IP público*. Em vez disso, ele é alocado de um pool de endereços IP disponíveis em Olá local do Azure resource Olá é criado no.
>

Endereços IP públicos estáticos são comumente usados em Olá os seguintes cenários:

* Os usuários finais precisam tooupdate toocommunicate de regras de firewall com os recursos do Azure.
* Resolução de nome DNS, em que uma alteração no endereço IP exigiria a atualização de registros A.
* Seus recursos do Azure comunicam-se com outros aplicativos ou serviços que usam um endereço IP baseado em um modelo de segurança.
* Use o endereço IP SSL certificados tooan vinculado.

> [!NOTE]
> saudação de lista de intervalos IP do qual os endereços IP públicos (dinâmica ou estática) tooAzure os recursos são alocados é publicada na [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653).
>

### <a name="dns-hostname-resolution"></a>Resolução de nome de host DNS
Você pode especificar um rótulo de nome de domínio DNS para um recurso IP público, que cria um mapeamento para *domainnamelabel*. *local*. cloudapp.azure.com toohello endereço IP público em servidores DNS gerenciado do Azure hello. Por exemplo, se você criar um recurso IP público com **contoso** como um *domainnamelabel* em Olá **Oeste dos EUA** Azure *local*, Olá o nome de domínio totalmente qualificado (FQDN) **contoso.westus.cloudapp.azure.com** resolverá toohello de endereço IP público do recurso de saudação. Você pode usar este FQDN toocreate um registro CNAME do domínio personalizado apontando o endereço IP público de toohello no Azure.

> [!IMPORTANT]
> Cada rótulo de nome do domínio criado deve ser exclusivo dentro de seu local do Azure.  
>

### <a name="virtual-machines"></a>Máquinas virtuais
Você pode associar um endereço IP público com um [Windows](../virtual-machines/windows/overview.md) ou [Linux](../virtual-machines/virtual-machines-linux-about.md) VM atribuindo a ele tooits **interface de rede**. No caso de saudação de uma VM com várias interfaces de rede, você pode atribuí-lo toohello *primário* somente a interface de rede. Você pode atribuir um dinâmico ou um tooa de endereço IP de público estático VM.

### <a name="internet-facing-load-balancers"></a>Balanceadores de carga para Internet
Você pode associar um endereço IP público com um [balanceador de carga do Azure](../load-balancer/load-balancer-overview.md), atribuindo a ele toohello balanceador de carga **front-end** configuração. Este endereço IP público serve como um balanceamento de carga de endereço VIP (IP virtual). Você pode atribuir um dinâmico ou um estática pública IP endereço tooa balanceador de carga de front-end. Você também pode atribuir várias pública IP endereços tooa balanceador de carga de front-end, que permite [Multivip](../load-balancer/load-balancer-multivip.md) cenários como um ambiente de multilocatário com sites baseada em SSL.

### <a name="vpn-gateways"></a>Gateways VPN
[Gateway de VPN do Azure](../vpn-gateway/vpn-gateway-about-vpngateways.md) é tooconnect usado em uma rede virtual do Azure (VNet) tooother VNets do Azure ou tooan na rede local. Você precisa tooassign um tooits de endereço IP público **configuração IP** tooenable-toocommunicate com rede remota hello. No momento, você só pode atribuir um *dinâmico* pública gateway VPN de tooa para endereço IP.

### <a name="application-gateways"></a>Application gateways
Você pode associar um endereço IP público do Azure [Application Gateway](../application-gateway/application-gateway-introduction.md), atribuindo a ele do gateway toohello **front-end** configuração. Esse endereço IP público serve como um VIP com balanceamento de carga. No momento, você só pode atribuir um *dinâmico* pública tooan aplicativo gateway front-end configuração do endereço IP.

### <a name="at-a-glance"></a>Imediato
tabela de saudação abaixo mostra propriedade específica de saudação por meio do qual pode ser um endereço IP público associado tooa recurso de nível superior e Olá possíveis métodos de alocação (dinâmicos ou estáticos) que podem ser usados.

| Recurso de nível superior | Associação de Endereço IP | dinâmico | estático |
| --- | --- | --- | --- |
| Máquina virtual |interface de rede |Sim |Sim |
| Balanceador de carga |Configuração de front-end |Sim |Sim |
| Gateway de VPN |Configuração de IP do gateway |Sim |Não |
| Application Gateway |Configuração de front-end |Sim |Não |

## <a name="private-ip-addresses"></a>Endereços IP privados
Endereços IP privados permitem toocommunicate de recursos do Azure com outros recursos em um [rede virtual](virtual-networks-overview.md) ou uma rede local por meio de um gateway VPN ou um circuito de rota expressa, sem usar um endereço IP acessível da Internet.

No modelo de implantação do Azure Resource Manager hello, um endereço IP privado é associado toohello seguintes tipos de recursos do Azure:

* VMs
* ILBs (balanceadores de carga internos)
* Application gateways

### <a name="allocation-method"></a>Método de alocação
Um endereço IP privado é alocado endereço de saudação do intervalo de saudação sub-rede toowhich Olá recurso está anexado. intervalo de endereços de saudação da sub-rede de saudação em si é uma parte do intervalo de endereços da rede virtual hello.

Há dois métodos de alocar um endereço IP privado: *dinâmico* ou *estático*. método de alocação padrão Olá é *dinâmico*, onde o endereço IP de saudação é alocado automaticamente da sub-rede do recurso da saudação (usando DHCP). Esse endereço IP pode alterar quando você parar e iniciar o recurso de saudação.

Você pode definir o método de alocação hello muito*estático* tooensure Olá IP endereço permanece Olá mesmo. Nesse caso, você também precisa tooprovide um endereço IP válido que faz parte da sub-rede do recurso hello.

Os endereços IP privados estáticos costumam ser usados para:

* VMs que atuam como controladores de domínio ou servidores DNS.
* Recursos que exigem regras de firewall usando endereços IP.
* Recursos acessados por outros aplicativos/recursos por meio de um endereço IP.

### <a name="virtual-machines"></a>Máquinas virtuais
Um endereço IP privado é atribuído toohello **interface de rede** de um [Windows](../virtual-machines/windows/overview.md) ou [Linux](../virtual-machines/virtual-machines-linux-about.md) VM. No caso de uma VM com várias interfaces de rede, é atribuído um endereço IP privado a cada interface. Você pode especificar o método de alocação hello como dinâmico ou estático para uma interface de rede.

#### <a name="internal-dns-hostname-resolution-for-vms"></a>Resolução do nome do host DNS interno (para VMs)
Todas as VMs do Azure são configuradas com [servidores DNS gerenciados Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) por padrão, a menos que você explicitamente configure servidores DNS personalizados. Esses servidores DNS fornecem a resolução de nome interno para máquinas virtuais que residem dentro de saudação mesmo VNet.

Quando você cria uma máquina virtual, um mapeamento para o endereço IP privado do hello hostname tooits é adicionado toohello servidores DNS gerenciado do Azure. No caso de uma interface de multi-rede de VM, Olá hostname é mapeado toohello de endereço IP privado Olá principal da interface de rede.

Máquinas virtuais configuradas com os servidores DNS gerenciados do Azure será capaz de tooresolve Olá nomes de host de todas as VMs em seus endereços IP privados do tootheir de rede virtual.

### <a name="internal-load-balancers-ilb--application-gateways"></a>Balanceadores de carga internos (ILB) e gateways de aplicativo
Você pode atribuir um toohello de endereço IP privado **front-end** configuração de um [balanceador de carga interno do Azure](../load-balancer/load-balancer-internal-overview.md) (ILB) ou um [Azure Application Gateway](../application-gateway/application-gateway-introduction.md). Este endereço IP privado serve como um ponto de extremidade interno, acessível somente os recursos toohello dentro de sua rede virtual (VNet) e a redes remotas Olá conectados toohello VNet. Você pode atribuir a uma dinâmica ou estática privado toohello front-end configuração do endereço IP.

### <a name="at-a-glance"></a>Imediato
tabela de saudação abaixo mostra por meio do qual pode ser um endereço IP privado de propriedade específica do hello associado tooa recurso de nível superior e Olá possíveis métodos de alocação (dinâmicos ou estáticos) que podem ser usados.

| Recurso de nível superior | Associação de Endereço IP | dinâmico | estático |
| --- | --- | --- | --- |
| Máquina virtual |interface de rede |Sim |Sim |
| Balanceador de carga |Configuração de front-end |Sim |Sim |
| Application Gateway |Configuração de front-end |Sim |Sim |

## <a name="limits"></a>limites
Olá limites impostos endereçamento IP são indicados em conjunto completo de saudação de [limites de rede](../azure-subscription-service-limits.md#networking-limits) no Azure. Esses limites são por região e por assinatura. Você pode [entre em contato com o suporte](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooincrease limites de padrão de saudação a limites máximos de toohello com base em suas necessidades de negócios.

## <a name="pricing"></a>Preços
Endereços IP públicos podem ter um custo nominal. toolearn mais sobre IP endereço preços no Azure, examine Olá [preço do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página.

## <a name="next-steps"></a>Próximas etapas
* [Implantar uma VM com um IP público estático usando Olá portal do Azure](virtual-network-deploy-static-pip-arm-portal.md)
* [Implantar uma VM com um IP público estático usando um modelo](virtual-network-deploy-static-pip-arm-template.md)
* [Implantar uma VM com um endereço IP privado estático usando Olá portal do Azure](virtual-networks-static-private-ip-arm-pportal.md)
