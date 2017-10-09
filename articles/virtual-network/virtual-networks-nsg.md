---
title: "grupos de segurança aaaNetwork no Azure | Microsoft Docs"
description: "Saiba como tráfego tooisolate e controle de fluxo em suas redes virtuais usando o firewall do hello distribuído no Azure usando grupos de segurança de rede."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 20e850fc-6456-4b5f-9a3f-a8379b052bc9
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 3528ce833dab17977327c3c9ae0e78316e5e6a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-network-traffic-with-network-security-groups"></a>Filtrar o tráfego de rede com grupos de segurança de rede

Um grupo de segurança de rede (NSG) contém uma lista de regras de segurança que permitem ou negam tooresources de tráfego de rede conectados a redes virtuais do tooAzure (VNet). Os NSGs podem ser associados toosubnets, VMs individuais (clássico) ou interfaces de rede individuais (NIC) anexado tooVMs (Gerenciador de recursos). Quando um NSG está associado tooa sub-rede, regras de saudação aplicam tooall recursos toohello conectado sub-rede. O tráfego pode ser restringido ainda mais associando também tooa um NSG VM ou NIC.

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md). Este artigo aborda o uso de ambos os modelos, mas a Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

## <a name="nsg-resource"></a>Recurso NSG
Os NSGs contenham Olá propriedades a seguir:

| Propriedade | Descrição | Restrições | Considerações |
| --- | --- | --- | --- |
| Nome |Nome para Olá NSG |Deve ser exclusivo dentro da região de saudação.<br/>Pode conter letras, números, sublinhados, pontos e hifens.<br/>Deve começar com uma letra ou número.<br/>Deve terminar com uma letra, número ou sublinhado.<br/>Não pode exceder 80 caracteres. |Como talvez seja necessário toocreate NSGs vários, verifique se que você tem uma convenção de nomenclatura que torna mais fácil tooidentify função de saudação de seus NSGs. |
| Região |Azure [região](https://azure.microsoft.com/regions) onde hello NSG é criado. |Os NSGs só podem ser associado tooresources dentro Olá Olá NSG mesma região. |toolearn sobre quantas NSGs que você pode ter por região, ler Olá [Azure limita](../azure-subscription-service-limits.md#virtual-networking-limits-classic) artigo.|
| Grupo de recursos |Olá [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups) Olá NSG existe. |Embora um NSG existe em um grupo de recursos, pode ser associado tooresources em qualquer grupo de recursos, como recursos Olá faz parte da saudação mesma região do Azure Olá NSG. |Grupos de recursos é toomanage usado juntos, como uma unidade de implantação de vários recursos.<br/>Você pode considerar o agrupamento Olá NSG com recursos que ela está associada. |
| Regras |Regras de entrada ou saída que definem o tráfego que é permitido ou negado. | |Consulte Olá [regras NSG](#Nsg-rules) deste artigo. |

> [!NOTE]
> ACLs baseadas em ponto de extremidade e segurança de rede grupos não têm suporte em Olá a mesma instância VM. Se você quiser toouse um NSG e já tiver um ponto de extremidade ACL em vigor, primeiro remova o ponto de extremidade de saudação ACL. toolearn como tooremove uma ACL, ler Olá [Gerenciando controle listas de acesso (ACLs) para pontos de extremidade usando o PowerShell](virtual-networks-acl-powershell.md) artigo.
> 

### <a name="nsg-rules"></a>Regras NSG
Regras NSG contenham Olá propriedades a seguir:

| Propriedade | Descrição | Restrições | Considerações |
| --- | --- | --- | --- |
| **Nome** |Nome de regra de saudação. |Deve ser exclusivo dentro da região de saudação.<br/>Pode conter letras, números, sublinhados, pontos e hifens.<br/>Deve começar com uma letra ou número.<br/>Deve terminar com uma letra, número ou sublinhado.<br/>Não pode exceder 80 caracteres. |Você pode ter várias regras dentro de um NSG, então certifique-se de que seguir uma convenção de nomenclatura que permite que você tooidentify função de saudação da sua regra. |
| **Protocolo** |Toomatch de protocolo para a regra de saudação. |TCP, UDP ou * |Usando * como um protocolo inclui ICMP (somente o tráfego Leste e Oeste), como TCP e UDP e pode reduzir o número de saudação de regras que você precisa.<br/>AT Olá mesmo tempo, usando * pode ser uma abordagem muito ampla, portanto, é recomendável que você use * somente quando necessário. |
| **Intervalo de portas de origem** |Toomatch de intervalo de porta de fonte para regra de saudação. |Um único número de porta de 1 too65535, intervalo de portas (exemplo: 1-65535), ou * (para todas as portas). |As portas de origem pode ser efêmeras. A menos que seu programa cliente esteja usando uma porta específica, use * na maioria dos casos.<br/>Tente intervalos de porta toouse conforme a necessidade de saudação tooavoid possíveis para várias regras.<br/>Várias portas ou intervalos de portas não podem ser agrupados por uma vírgula. |
| **Intervalo de portas de destino** |Toomatch de intervalo de porta de destino para a regra de saudação. |Um único número de porta de 1 too65535, intervalo de portas (exemplo: 1-65535), ou \* (para todas as portas). |Tente intervalos de porta toouse conforme a necessidade de saudação tooavoid possíveis para várias regras.<br/>Várias portas ou intervalos de portas não podem ser agrupados por uma vírgula. |
| **Prefixo de endereço de origem** |Origem endereço prefixo ou marca toomatch para regra de saudação. |Um único endereço IP (exemplo: 10.10.10.10), sub-rede de IP (exemplo: 192.168.1.0/24), [marca padrão](#default-tags) ou * (para todos os endereços). |Considere o uso de intervalos, marcas de formatação padrão, e * número de saudação tooreduce de regras. |
| **Prefixo de endereço de destino** |Destino endereço prefixo ou marca toomatch para regra de saudação. | Um único endereço IP (exemplo: 10.10.10.10), sub-rede de IP (exemplo: 192.168.1.0/24), [marca padrão](#default-tags) ou * (para todos os endereços). |Considere o uso de intervalos, marcas de formatação padrão, e * número de saudação tooreduce de regras. |
| **Direção** |Direção do tráfego toomatch para regra de saudação. |Entrada ou saída. |Regras de entrada e saída são processadas separadamente, com base na direção. |
| **Prioridade** |As regras são verificadas em ordem de saudação de prioridade. Depois que uma regra se aplica, outras regras não são testadas quanto à correspondência. | Número entre 100 e 4096. | Considere a criação de regras saltando prioridades por 100 para cada espaço de tooleave regra para as novas regras que você pode criar no hello futuras. |
| **Access** |Tipo de acesso tooapply se Olá regra corresponde. | Permitir ou negar. | Tenha em mente que, se uma regra de permissão não for encontrada para um pacote, pacote de saudação é descartado. |

Os NSGs contêm dois conjuntos de regras: entrada e saída. prioridade de saudação para uma regra deve ser exclusiva em cada conjunto. 

![Processamento de regras do NSG](./media/virtual-network-nsg-overview/figure3.png) 

imagem anterior Olá mostra como as regras NSG são processadas.

### <a name="default-tags"></a>Marcas padrão
Marcas padrão são identificadores fornecidos pelo sistema tooaddress uma categoria de endereços IP. Você pode usar marcas de formatação padrão na Olá **prefixo de endereço de origem** e **prefixo de endereço de destino** propriedades de qualquer regra. Há três marcas padrão que você pode usar:

* **VirtualNetwork** (Gerenciador de recursos) (**VIRTUAL_NETWORK** para clássico): essa marca inclui o espaço de endereço de rede virtual hello (intervalos CIDR definidos no Azure), todas conectadas espaços de endereço local e conectam VNets do Azure (redes locais).
* **AzureLoadBalancer** (Resource Manager) (**AZURE_LOADBALANCER** para clássico): essa marca denota o balanceador de carga de infraestrutura do Azure. marca de saudação converte tooan proveniente de IP de datacenter do Azure onde sondas de integridade do Azure.
* **Internet** (Gerenciador de recursos) (**INTERNET** para clássico): esta marca denota o espaço de endereço IP de saudação que está fora da rede virtual hello e acessível pela Internet pública. intervalo de saudação inclui Olá [Azure espaço IP próprio público](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="default-rules"></a>Regras padrão
Todos os NSGs contêm um conjunto de regras padrão. as regras de saudação padrão não podem ser excluídas, mas porque eles recebem a prioridade mais baixa hello, elas podem ser substituídas pelas regras de saudação que você criar. 

as regras padrão Olá permitem e impedir que o tráfego da seguinte maneira:
- **Rede virtual:** o tráfego que começa e termina em uma rede virtual é permitido nas direções de entrada e saída.
- **Internet:** o tráfego de saída é permitido, mas o tráfego de entrada é bloqueado.
- **Balanceador de carga:** integridade do Azure carga balanceador tooprobe Olá permitir de suas máquinas virtuais e instâncias de função. Se não estiver usando um conjunto de balanceamento de carga, você poderá substituir essa regra.

**Regras de entrada padrão**

| Nome | Prioridade | IP de origem | Porta de origem | IP de destino | Porta de destino | Protocolo | Access |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVNetInBound |65000 | VirtualNetwork | * | VirtualNetwork | * | * | PERMITIR |
| AllowAzureLoadBalancerInBound | 65001 | AzureLoadBalancer | * | * | * | * | PERMITIR |
| DenyAllInBound |65500 | * | * | * | * | * | NEGAR |

**Regras de saída padrão**

| Nome | Prioridade | IP de origem | Porta de origem | IP de destino | Porta de destino | Protocolo | Access |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVnetOutBound | 65000 | VirtualNetwork | * | VirtualNetwork | * | * | PERMITIR |
| AllowInternetOutBound | 65001 | * | * | Internet | * | * | PERMITIR |
| DenyAllOutBound | 65500 | * | * | * | * | * | NEGAR |

## <a name="associating-nsgs"></a>Associando NSGs
Você pode associar um NSG tooVMs, NICs e sub-redes, dependendo do modelo de implantação de saudação que você está usando, da seguinte maneira:

* **VM (clássico):** regras de segurança são aplicadas tooall tráfego na Olá VM. 
* **NIC (somente no Gerenciador de recursos):** regras de segurança são aplicadas tooall tráfego na Olá Olá NIC NSG está associado. Em uma VM multi-NIC, você pode aplicar diferentes (ou Olá mesmo) NSG tooeach NIC individualmente. 
* **Subrede (Gerenciador de recursos e clássico):** regras de segurança são aplicadas tooany tráfego para/de todos os recursos conectados toohello VNet.

Você pode associar diferentes NSGs tooa VM (ou NIC, dependendo do modelo de implantação de saudação) e Olá uma VM ou NIC conectado à sub-rede. As regras de segurança de tráfego toohello aplicadas, por prioridade, em cada NSG, em Olá a seguir ordem:

- **Tráfego de entrada**

  1. **Toosubnet NSG aplicado:** se uma sub-rede NSG tiver um tráfego de toodeny regra de correspondência, o pacote de saudação é descartado.

  2. **NSG aplicada tooNIC** (Gerenciador de recursos) ou VM (clássico): NSG de VM\NIC se tem uma regra de correspondência que nega o tráfego, os pacotes são descartados em Olá VM\NIC, mesmo se uma sub-rede NSG tem uma regra de correspondência que permita o tráfego.

- **Tráfego de saída**

  1. **NSG aplicada tooNIC** (Gerenciador de recursos) ou VM (clássico): se um NSG VM\NIC tem uma regra de correspondência que nega o tráfego, os pacotes são descartados.

  2. **Toosubnet NSG aplicado:** se uma sub-rede NSG tem uma regra de correspondência que nega o tráfego, pacotes sejam descartados, mesmo se um NSG VM\NIC tem uma regra de correspondência que permita o tráfego.

> [!NOTE]
> Embora você só pode associar uma única NSG tooa sub-rede, VM ou NIC; Você pode associar Olá mesmo tooas NSG muitos recursos que você desejar.
>

## <a name="implementation"></a>Implementação
Você pode implementar NSGs em Olá Gerenciador de recursos ou modelos de implantação clássico usando Olá ferramentas a seguir:

| Ferramenta de implantação | Clássico | Gerenciador de Recursos |
| --- | --- | --- |
| Portal do Azure   | Sim | [Sim](virtual-networks-create-nsg-arm-pportal.md) |
| PowerShell     | [Sim](virtual-networks-create-nsg-classic-ps.md) | [Sim](virtual-networks-create-nsg-arm-ps.md) |
| CLI do Azure **V1**   | [Sim](virtual-networks-create-nsg-classic-cli.md) | [Sim](virtual-networks-create-nsg-cli-nodejs.md) |
| CLI do Azure **V2**   | Não | [Sim](virtual-networks-create-nsg-arm-cli.md) |
| Modelo do Azure Resource Manager   | Não  | [Sim](virtual-networks-create-nsg-arm-template.md) |

## <a name="planning"></a>Planejamento
Antes de implementar os NSGs, é necessário tooanswer Olá perguntas a seguir:

1. Os tipos de recursos você deseja toofilter tooor de tráfego de? Você pode se conectar a recursos, como NICs (Resource Manager), máquinas virtuais (clássico), serviços de nuvem, ambientes de serviço de aplicativos e Conjuntos de Dimensionamento de VMs. 
2. São Olá recursos você deseja que o tráfego de toofilter de toosubnets conectado em VNets existentes?

Para obter mais informações sobre planejamento de segurança de rede no Azure, leia Olá [serviços de nuvem e segurança de rede](../best-practices-network-security.md) artigo. 

## <a name="design-considerations"></a>Considerações sobre o design
Depois que você souber respostas Olá perguntas toohello Olá [planejamento](#Planning) seção, examine Olá seções a seguir antes de definir seus NSGs:

### <a name="limits"></a>limites
Há limites de número de toohello de NSGs que em uma assinatura e o número de regras por NSG. mais sobre os limites de Olá Olá de leitura de toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.

### <a name="vnet-and-subnet-design"></a>Design da rede virtual e da sub-rede
Como os NSGs podem ser aplicadas toosubnets, você pode minimizar o número de saudação do NSGs agrupando os recursos de sub-rede e aplicando os NSGs toosubnets.  Se você decidir tooapply NSGs toosubnets, você pode achar que VNets existentes e sub-redes que não foram definidas com os NSGs em mente. Você pode precisar toodefine novas VNets e sub-redes toosupport seu design NSG e implantar novas sub-redes de tooyour seus recursos novos. Em seguida, você pode definir um toomove de estratégia de migração existente novas sub-redes de toohello de recursos. 

### <a name="special-rules"></a>Regras especiais
Se você bloquear o tráfego permitido pelo Olá regras a seguir, sua infraestrutura não pode se comunicar com os serviços do Azure essenciais:

* **IP virtual do nó de host Olá:** serviços de infraestrutura básica como DHCP, DNS e monitoramento de integridade são fornecidos por meio de host virtualizado Olá endereço IP 168.63.129.16. Este endereço IP público pertence tooMicrosoft e é Olá único endereço IP virtualizado usado em todas as regiões para essa finalidade. Esse endereço IP mapeia toohello endereço IP físico da máquina do servidor de saudação (nó de host) hospeda Olá VM. nó de host Olá atua como retransmissão DHCP hello, resolvedor de DNS recursivo hello e fonte investigação Olá Olá carga sonda do balanceador de integridade e investigação de integridade do computador hello. Endereço IP de toothis de comunicação não é um ataque.
* **Licenciamento (serviço de gerenciamento de chaves):** imagens do Windows em execução em VMs devem ser licenciadas. tooensure licenciamento, uma solicitação é enviada toohello servidores de host de serviço de gerenciamento de chaves que lidam com essas consultas. solicitação de saudação é feita saída pela porta 1688.

### <a name="icmp-traffic"></a>Tráfego ICMP
as regras NSG atuais Olá permitem apenas protocolos *TCP* ou *UDP*. Não há uma marca específica para o *ICMP*. No entanto, o tráfego ICMP é permitido dentro de uma rede virtual por regra padrão AllowVNetInBound hello, que permite tooand de tráfego de qualquer porta e protocolo dentro Olá VNet.

### <a name="subnets"></a>Sub-redes
* Considere o número de saudação de camadas que requer sua carga de trabalho. Cada camada pode ser isolada por meio de uma sub-rede, com uma sub-rede de toohello NSG aplicado. 
* Se você precisar tooimplement uma sub-rede de gateway de VPN ou circuito de rota expressa, **não** se aplicam a uma sub-rede de toothat NSG. Se você fizer isso, a conectividade entre VNet ou entre locais poderá falhar. 
* Se você precisar tooimplement um dispositivo de rede virtual NVA (), conecte-se Olá NVA tooits próprio subrede e criar rotas definidas pelo usuário (UDR) tooand de saudação NVA. Você pode implementar um nível de sub-rede tráfego de toofilter NSG dentro e fora nesta sub-rede. toolearn mais sobre UDRs, ler Olá [rotas definidas pelo usuário](virtual-networks-udr-overview.md) artigo.

### <a name="load-balancers"></a>Balanceadores de carga
* Considere o endereço de rede e balanceamento de carga de saudação regras NAT (conversão) para cada balanceador de carga usada por cada uma das suas cargas de trabalho. Regras NAT são associados tooa pool de back-end que contém instâncias de função de serviços de nuvem/VMs (clássico) ou NICs (Gerenciador de recursos). Considere a criação de um NSG para cada pool de back-end, permitindo que somente o tráfego mapeado por meio de regras de saudação implementadas em balanceadores de carga de saudação. Criar um NSG para cada pool de back-end, você garante que o tráfego proveniente de pool de back-end toohello diretamente (em vez de por meio do balanceador de carga de saudação), também é filtrada.
* Em implantações clássicas, você deve criar pontos de extremidade que mapeiam portas em um tooports do balanceador de carga em suas VMs ou instâncias de função. Você também pode criar seu próprio balanceador de carga público individual por meio do Resource Manager. porta de destino Olá para tráfego de entrada é porta real Olá Olá VM ou instância de função, não porta Olá exposta por um balanceador de carga. porta de origem Hello e o endereço de saudação conexão toohello em que VM é uma porta e endereço Olá Olá Internet computador remoto, não porta hello e o endereço de expostos pelo Balanceador de carga de saudação.
* Quando você cria os NSGs toofilter tráfego recebidas por meio de um balanceador de carga interno (ILB), produtos de intervalo de porta e endereço de origem Olá aplicado são de saudação computador, não o balanceador de carga Olá de origem. intervalo de porta e endereço de destino de saudação são aqueles do computador de destino hello, não o balanceador de carga hello.

### <a name="other"></a>outro
* Listas de controle de acesso baseado em ponto de extremidade (ACL) e os NSGs não têm suporte em Olá mesma instância VM. Se você quiser toouse um NSG e já tiver um ponto de extremidade ACL em vigor, primeiro remova o ponto de extremidade de saudação ACL. Para obter informações sobre como tooremove um ponto de extremidade ACL, consulte Olá [gerenciar ACLs de ponto de extremidade](virtual-networks-acl-powershell.md) artigo.
* No Gerenciador de recursos, você pode usar um tooa NSG associado NIC para VMs com o gerenciamento de tooenable várias NICs (acesso remoto) em uma base por NIC. Associar exclusivo NSGs tooeach NIC permite a separação dos tipos de tráfego entre NICs.
* Use toohello semelhante de balanceadores de carga, ao filtrar o tráfego de outras VNets, você deve usar o intervalo de endereço de origem de saudação do computador remoto hello, não gateway Olá conectando Olá VNets.
* Muitos serviços do Azure não podem ser tooVNets conectado. Se um recurso do Azure não estiver conectado tooa VNet, você não pode usar um recurso de toohello NSG toofilter tráfego.  Leia a documentação Olá para serviços Olá você usar toodetermine se serviço Olá pode ser conectado tooa VNet.

## <a name="sample-deployment"></a>Exemplo de implantação
aplicativo de hello tooillustrate de informações de saudação neste artigo, considere um cenário comum de um aplicativo de duas camadas mostrado na figura abaixo de saudação:

![NSGs](./media/virtual-network-nsg-overview/figure1.png)

Conforme mostrado no diagrama hello, Olá *Web1* e *Web2* as VMs são conectado toohello *front-end* sub-rede e hello *DB1* e *DB2* as VMs são conectado toohello *back-end* sub-rede.  Ambas as sub-redes são parte da saudação *TestVNet* VNet. Olá componentes de aplicativos cada executado em tooa uma VM do Azure conectado VNet. cenário de saudação tem Olá requisitos a seguir:

1. Separação do tráfego entre Olá WEB e servidores de banco de dados.
2. Encaminhar o tráfego de servidores de web hello carga balanceador tooall na porta 80 regras de balanceamento de carga.
3. Carregar balanceador NAT regras encaminhar o tráfego entra no balanceador de carga de saudação em tooport 50001 porta 3389 no hello WEB1 VM.
4. Nenhum acesso toohello VMs front-end ou back-end de saudação da Internet, exceto os requisitos de 2 e 3.
5. Nenhum acesso de saída da Internet dos servidores WEB ou de banco de dados de saudação.
6. Acesso de sub-rede de front-end de saudação é permitido tooport 3389 de qualquer servidor web.
7. Acesso de sub-rede de front-end de saudação é permitido tooport 3389 de qualquer servidor de banco de dados.
8. Acesso de sub-rede de front-end de saudação é permitido tooport 1433 de todos os servidores de banco de dados.
9. Separação do tráfego de gerenciamento (porta 3389) e do tráfego de banco de dados (1433) nas diferentes NICs de servidores DB.

Requisitos de 1 a 6 (exceto requisitos 3 e 4) são todos os espaços de toosubnet restrita. Olá NSGs seguintes requisitos Olá anterior, minimizando o número de saudação de NSGs necessário:

### <a name="frontend"></a>FrontEnd
**Regras de entrada**

| Regra | Access | Prioridade | Intervalo de endereços de origem | Porta de origem | Intervalo de endereços de destino | Porta de destino | Protocolo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-HTTP-Internet | PERMITIR | 100 | Internet | * | * | 80 | TCP |
| Allow-Inbound-RDP-Internet | PERMITIR | 200 | Internet | * | * | 3389 | TCP |
| Deny-Inbound-All | NEGAR | 300 | Internet | * | * | * | TCP |

**Regras de saída**

| Regra | Access | Prioridade | Intervalo de endereços de origem | Porta de origem | Intervalo de endereços de destino | Porta de destino | Protocolo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All |NEGAR |100 | * | * | Internet | * | * |

### <a name="backend"></a>BackEnd
**Regras de entrada**

| Regra | Access | Prioridade | Intervalo de endereços de origem | Porta de origem | Intervalo de endereços de destino | Porta de destino | Protocolo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All | NEGAR | 100 | Internet | * | * | * | * |

**Regras de saída**

| Regra | Access | Prioridade | Intervalo de endereços de origem | Porta de origem | Intervalo de endereços de destino | Porta de destino | Protocolo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All | NEGAR | 100 | * | * | Internet | * | * |

Olá NSGs seguintes são criados e associadas tooNICs em Olá máquinas virtuais a seguir:

### <a name="web1"></a>WEB1
**Regras de entrada**

| Regra | Access | Prioridade | Intervalo de endereços de origem | Porta de origem | Intervalo de endereços de destino | Porta de destino | Protocolo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Internet | PERMITIR | 100 | Internet | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet | PERMITIR | 200 | Internet | * | * | 80 | TCP |

> [!NOTE]
> intervalo de endereço de origem Olá para regras anteriores Olá é **Internet**, Olá não o endereço IP virtual da saudação balanceador de carga. porta de origem Olá é *, não 500001. Regras NAT para balanceadores de carga não são Olá mesmo que as regras de segurança do NSG. Regras de segurança do NSG são sempre toohello relacionados de origem e destino final de tráfego, **não** balanceador de carga de saudação entre hello dois. 
> 
> 

### <a name="web2"></a>WEB2
**Regras de entrada**

| Regra | Access | Prioridade | Intervalo de endereços de origem | Porta de origem | Intervalo de endereços de destino | Porta de destino | Protocolo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Inbound-RDP-Internet | NEGAR | 100 | Internet | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet | PERMITIR | 200 | Internet | * | * | 80 | TCP |

### <a name="db-servers-management-nic"></a>Servidores DB (NIC de gerenciamento)
**Regras de entrada**

| Regra | Access | Prioridade | Intervalo de endereços de origem | Porta de origem | Intervalo de endereços de destino | Porta de destino | Protocolo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Front-end | PERMITIR | 100 | 192.168.1.0/24 | * | * | 3389 | TCP |

### <a name="db-servers-database-traffic-nic"></a>Servidores DB (tráfego NIC do banco de dados)
**Regras de entrada**

| Regra | Access | Prioridade | Intervalo de endereços de origem | Porta de origem | Intervalo de endereços de destino | Porta de destino | Protocolo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-SQL-Front-end | PERMITIR | 100 | 192.168.1.0/24 | * | * | 1433 | TCP |

Como algumas Olá NSGs são associado tooindividual NICs, regras de saudação são para os recursos implantados por meio do Gerenciador de recursos. As regras são combinadas para sub-rede e NIC, dependendo de como estão associados. 

## <a name="next-steps"></a>Próximas etapas
* [Implantar NSGs (Gerenciador de Recursos)](virtual-networks-create-nsg-arm-pportal.md).
* [Implantar NSGs (clássico)](virtual-networks-create-nsg-classic-ps.md).
* [Gerenciar logs do NSG](virtual-network-nsg-manage-log.md).
* [Solucionar problemas de NSGs] (virtual-network-nsg-troubleshoot-portal.md)
