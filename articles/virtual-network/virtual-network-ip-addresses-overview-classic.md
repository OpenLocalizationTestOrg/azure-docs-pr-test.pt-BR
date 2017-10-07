---
title: "tipos de endereço aaaIP no Azure (clássica) | Microsoft Docs"
description: "Saiba mais sobre endereços IP (clássicos) públicos e privados no Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 2f8664ab-2daf-43fa-bbeb-be9773efc978
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 7e09a5ad5b5f2d55329152b5d843de3c4455d1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-classic-in-azure"></a>Tipos de endereço IP e métodos de alocação (clássico) no Azure
Você pode atribuir IP endereços tooAzure recursos toocommunicate com outros recursos do Azure, sua rede local e Olá da Internet. Há dois tipos de endereços IP que você pode usar no Azure: público e privado.

Endereços IP públicos são usados para comunicação com hello Internet, incluindo serviços voltados ao público do Azure.

Endereços IP privados são usados para comunicação em uma rede virtual do Azure (VNet), um serviço de nuvem e sua rede local quando você usar um gateway VPN ou tooextend de circuito de rota expressa tooAzure sua rede.

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).  Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que a maioria das implantações novas use o Gerenciador de Recursos. Saiba mais sobre endereços IP no Gerenciador de recursos por leitura Olá [endereços IP](virtual-network-ip-addresses-overview-arm.md) artigo.

## <a name="public-ip-addresses"></a>Endereços IP públicos
Endereços IP públicos permitem toocommunicate de recursos do Azure com os serviços da Internet e o Azure públicos, como [Cache Redis do Azure](https://azure.microsoft.com/services/cache/), [Hubs de eventos do Azure](https://azure.microsoft.com/services/event-hubs/), [bancos de dados do SQL](../sql-database/sql-database-technical-overview.md), e [armazenamento do Azure](../storage/common/storage-introduction.md).

Um endereço IP público está associado com hello tipos de recursos a seguir:

* Serviços de Nuvem
* VMs (Máquinas Virtuais) de IaaS
* Instâncias de função de PaaS
* Gateways VPN
* Application gateways

### <a name="allocation-method"></a>Método de alocação
Quando precisa de um endereço IP público toobe atribuído tooan recursos do Azure, é *dinamicamente* alocado de um pool de IP público disponível endereço no recurso de Olá Olá local é criado. Esse endereço IP é liberado quando o recurso de saudação é interrompido. No caso de um serviço de nuvem, isso ocorre quando todas as instâncias de função hello forem interrompidas, que pode ser evitado usando um *estático* endereço IP (reservado) (consulte [serviços de nuvem](#Cloud-services)).

> [!NOTE]
> saudação de lista de intervalos IP do qual os endereços IP públicos tooAzure os recursos são alocados é publicada na [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

### <a name="dns-hostname-resolution"></a>Resolução de nome de host DNS
Quando você criar um serviço de nuvem ou em uma VM de IaaS, é necessário tooprovide um nome DNS do serviço de nuvem que é exclusivo em todos os recursos no Azure. Isso cria um mapeamento no hello servidores DNS gerenciados do Azure para *dnsname*. cloudapp.net toohello endereço IP público do recurso de saudação. Por exemplo, quando você criar um serviço de nuvem com um nome DNS do serviço de nuvem do **contoso**, nome de domínio totalmente qualificado (FQDN) do hello **contoso.cloudapp.net** resolverá o endereço IP público (VIP) tooa do serviço de nuvem Hello. Você pode usar este FQDN toocreate um registro CNAME do domínio personalizado apontando o endereço IP público de toohello no Azure.

### <a name="cloud-services"></a>Serviços de Nuvem
Um serviço de nuvem sempre tem um IP público referidos tooas um endereço IP virtual (VIP) de endereços. Você pode criar pontos de extremidade em uma nuvem serviço tooassociate diferentes portas em portas de toointernal Olá VIP em máquinas virtuais e instâncias de função no serviço de nuvem hello. 

Um serviço de nuvem pode conter várias VMs de IaaS ou instâncias de função de PaaS, todos os exposto por meio de Olá mesmo VIP de serviço de nuvem. Você também pode atribuir [serviço em nuvem vários VIPs tooa](../load-balancer/load-balancer-multivip.md), que permite cenários de multi-VIP como ambiente de multilocatário com sites baseada em SSL.

Você pode garantir o endereço IP público de saudação de um serviço de nuvem permanece Olá mesmo, mesmo quando todas as instâncias de função de Olá forem interrompidos, usando um *estático* endereço IP público, chamado tooas [IP reservado](virtual-networks-reserved-public-ip.md). Você pode criar um recurso IP estático (reservado) em um local específico e atribua-o serviço de nuvem tooany nesse local. Não é possível especificar o endereço IP real de saudação para IP reservado de Olá, é alocado do pool de endereços IP disponíveis no local de saudação que é criado. Esse endereço IP não é liberado até você explicitamente excluí-lo.

Estáticos endereços IP públicos (reservados) são usados em cenários de saudação onde um serviço de nuvem:

* requer a instalação de toobe de regras de firewall por usuários finais.
* depende da resolução de nome DNS externa, e um IP dinâmico exigiria atualizar registros A.
* consome serviços Web externos que usam o modelo de segurança com base em IP.
* usa o endereço IP SSL certificados tooan vinculado.

> [!NOTE]
> Quando você cria uma VM clássica, um contêiner *serviço de nuvem* é criado pelo Azure, que tem um endereço IP virtual (VIP). Quando a criação de saudação é feita por meio do portal, um padrão RDP ou SSH *ponto de extremidade* é configurado pelo portal Olá para toohello VM possa se conectar por meio de saudação VIP de serviço de nuvem. Este VIP de serviço de nuvem pode ser reservada, que fornece efetivamente uma tooconnect endereço IP reservado toohello VM. Você pode abrir portas adicionais configurando mais pontos de extremidade.
> 
> 

### <a name="iaas-vms-and-paas-role-instances"></a>VMs de IaaS e instâncias de função PaaS
Você pode atribuir um público endereço IP diretamente tooan IaaS [VM](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou instância de função de PaaS dentro de um serviço de nuvem. Isso é chamado tooas um endereço IP público de nível de instância ([ILPIP](virtual-networks-instance-level-public-ip.md)). Esse endereço IP público pode ser apenas dinâmico.

> [!NOTE]
> Isso é diferente de saudação VIP saudação do serviço de nuvem, que é um contêiner para as VMs de IaaS ou PaaS instâncias de função, como um serviço de nuvem pode conter várias VMs de IaaS, ou instâncias de função de PaaS, todos os exposto por meio de saudação mesmo VIP de serviço na nuvem.
> 
> 

### <a name="vpn-gateways"></a>Gateways VPN
Um [gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) pode ser usado tooconnect tooother uma rede virtual do Azure redes VNets do Azure ou no local. Um gateway de VPN é atribuído um endereço IP público *dinamicamente*, que permite a comunicação com a rede remota hello.

### <a name="application-gateways"></a>Application gateways
Um Azure [Application gateway](../application-gateway/application-gateway-introduction.md) pode ser usado para Layer7 balanceamento de carga de tráfego de rede tooroute com base em HTTP. Gateway de aplicativo é atribuído um endereço IP público *dinamicamente*, que serve como Olá VIP com balanceamento de carga.

### <a name="at-a-glance"></a>Visão rápida
Olá tabela a seguir mostra cada tipo de recurso com métodos de alocação possíveis hello (dinâmica ou estática) e capacidade tooassign vários endereços IP públicos.

| Recurso | Dinâmico | estático | Vários endereços IP |
| --- | --- | --- | --- |
| serviço de nuvem |Sim |Sim |Sim |
| Instância de função de PaaS ou VM de IaaS |Sim |Não |Não |
| gateway de VPN |Sim |Não |Não |
| Application Gateway |Sim |Não |Não |

## <a name="private-ip-addresses"></a>Endereços IP privados
Endereços IP privados permitem toocommunicate de recursos do Azure com outros recursos em um serviço de nuvem ou um [rede virtual](virtual-networks-overview.md)(VNet), ou de rede local tooon (por meio de um gateway de VPN ou circuito de rota expressa), sem usar um Endereço IP acessível da Internet.

No modelo de implantação clássico do Azure, um endereço IP privado pode ser atribuído toohello recursos do Azure a seguir:

* VMs de IaaS e instâncias de função PaaS
* Balanceador de carga interno
* Application Gateway

### <a name="iaas-vms-and-paas-role-instances"></a>VMs de IaaS e instâncias de função PaaS
Máquinas virtuais (VMs) criadas com o modelo de implantação clássico Olá sempre são colocadas em um serviço de nuvem, instâncias de função tooPaaS semelhante. comportamento de saudação de endereços IP privados, portanto, são semelhantes para esses recursos.

É importante toonote que um serviço de nuvem pode ser implantados de duas maneiras:

* Como um serviço de nuvem *autônomo* , em que ele não está dentro de uma rede virtual.
* Como parte de uma rede virtual.

#### <a name="allocation-method"></a>Método de alocação
No caso de um *autônomo* serviço em nuvem, obtenha recursos alocado de um endereço IP privado *dinamicamente* intervalo de endereços de IP privado do hello datacenter do Azure. Ele pode ser usado apenas para comunicação com outras máquinas virtuais dentro de saudação mesmo serviço de nuvem. Esse endereço IP pode alterar quando o recurso de saudação é interrompido e iniciado.

No caso de um serviço de nuvem implantado em uma rede virtual, recursos obter privados endereços IP alocados do intervalo de endereços de saudação do hello associados sub-redes (conforme especificado em sua configuração de rede). Este endereço IP particular pode ser usado para comunicação entre todas as VMs em redes de saudação.

Além disso, no caso de serviços de nuvem em uma rede virtual, um endereço IP privado é alocado *dinamicamente* (usando DHCP) por padrão. Ele pode alterar quando o recurso de saudação é interrompido e iniciado. tooensure Olá IP endereço permanece Olá mesmo, você precisa de método de alocação de saudação tooset muito*estático*e forneça um endereço IP válido dentro do intervalo de endereços correspondente hello.

Os endereços IP privados estáticos costumam ser usados para:

* VMs que atuam como controladores de domínio ou servidores DNS.
* VMs que exigem regras de firewall usando endereços IP.
* VMs executando serviços acessados por outros aplicativos por meio de um endereço IP.

#### <a name="internal-dns-hostname-resolution"></a>Resolução do nome do host DNS interno
Todas as VMs do Azure e instâncias de função de PaaS são configuradas com [servidores DNS gerenciados pelo Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) por padrão, a menos que você explicitamente configure servidores DNS personalizados. Esses servidores DNS fornecem a resolução de nome interno para VMs e instâncias de função que residem dentro de Olá mesmo serviço de nuvem ou rede virtual.

Quando você cria uma máquina virtual, um mapeamento para o endereço IP privado do hello hostname tooits é adicionado toohello servidores DNS gerenciado do Azure. No caso de uma VM multi-NIC, Olá hostname é mapeado toohello endereço IP privado primário NIC de saudação. No entanto, essas informações de mapeamento serão restrito tooresources dentro Olá mesmo serviço de nuvem ou rede virtual.

No caso de um *autônomo* serviço em nuvem, você será capaz de tooresolve nomes de host de todas as instâncias de VMs/função dentro de saudação mesmo serviço somente na nuvem. No caso de um serviço de nuvem dentro de uma rede virtual será tooresolve capaz de nomes de host de todas as instâncias de VMs/função hello dentro Olá VNet.

### <a name="internal-load-balancers-ilb--application-gateways"></a>Balanceadores de carga internos (ILB) e gateways de aplicativo
Você pode atribuir um toohello de endereço IP privado **front-end** configuração de um [balanceador de carga interno do Azure](../load-balancer/load-balancer-internal-overview.md) (ILB) ou um [Azure Application Gateway](../application-gateway/application-gateway-introduction.md). Este endereço IP privado serve como um ponto de extremidade interno, acessível somente os recursos toohello dentro de sua rede virtual (VNet) e a redes remotas Olá conectados toohello VNet. Você pode atribuir a uma dinâmica ou estática privado toohello front-end configuração do endereço IP. Você também pode atribuir várias privada IP endereços tooenable vip vários cenários.

### <a name="at-a-glance"></a>Visão rápida
Olá tabela a seguir mostra cada tipo de recurso com métodos de alocação possíveis hello (dinâmica ou estática) e capacidade tooassign vários endereços IP privados.

| Recurso | Dinâmico | estático | Vários endereços IP |
| --- | --- | --- | --- |
| VM (em um serviço de nuvem *autônomo* ) |Sim |Sim |Sim |
| Instância de função de PaaS (em um serviço de nuvem *autônomo* ) |Sim |Não |Sim |
| Instância de função VM ou PaaS (em uma rede virtual) |Sim |Sim |Sim |
| Front-end do balanceador de carga interno |Sim |Sim |Sim |
| Front-end do Application Gateway |Sim |Sim |Sim |

## <a name="limits"></a>limites
tabela de saudação abaixo mostra limites Olá impostos IP endereçamento no Azure por assinatura. Você pode [entre em contato com o suporte](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooincrease limites de padrão de saudação a limites máximos de toohello com base em suas necessidades de negócios.

|  | Limite padrão | Limite máximo |
| --- | --- | --- |
| Endereços IP públicos (dinâmicos) |5 |entrar em contato com o suporte |
| Endereços IP públicos reservados |20 |entrar em contato com o suporte |
| VIP público por implantação (serviço de nuvem) |5 |entrar em contato com o suporte |
| VIP privado (ILB) por implantação (serviço de nuvem) |1 |1 |

Certifique-se de ler o conjunto completo de saudação de [limites de rede](../azure-subscription-service-limits.md#networking-limits) no Azure.

## <a name="pricing"></a>Preços
Na maioria dos casos, endereços IP públicos são gratuitos. Há uma taxa nominal toouse adicionais e/ou estáticos endereços IP públicos. Certifique-se de entender Olá [estrutura de preços para IPs públicos](https://azure.microsoft.com/pricing/details/ip-addresses/).

## <a name="differences-between-resource-manager-and-classic-deployments"></a>Diferenças entre as implantações do Gerenciador de recursos e clássica
Abaixo está uma comparação dos recursos de endereçamento de IP no Gerenciador de recursos e o modelo de implantação clássico hello.

|  | Recurso | Clássico | Gerenciador de Recursos |
| --- | --- | --- | --- |
| **Endereço IP público** |***VM*** |Chamado tooas um ILPIP (dinâmico) |Chamado tooas um IP público (dinâmico ou estático) |
|  ||Tooan atribuído IaaS VM ou uma instância de função de PaaS |NIC toohello associado da VM | |
|  |***Balanceador de carga para a Internet*** |Chamado tooas VIP (dinâmico) ou IP reservado (estático) |Chamado tooas um IP público (dinâmico ou estático) | |
|  ||Serviço de nuvem tooa atribuído |Configuração de front-end do balanceador de carga toohello associado | |
|  | | | |
| **Endereço IP privado** |***VM*** |Tooas chamado um DIP |Chamado tooas um endereço IP privado |
|  ||Tooan atribuído IaaS VM ou uma instância de função de PaaS |NIC toohello atribuído da VM | |
|  |***Balanceador de carga interno (ILB)*** |Atribuído toohello ILB (dinâmico ou estático) |Configuração de front-end do ILB toohello atribuído (dinâmica ou estática) | |

## <a name="next-steps"></a>Próximas etapas
* [Implantar uma VM com um endereço IP privado estático](virtual-networks-static-private-ip-classic-pportal.md) usando Olá portal do Azure.

