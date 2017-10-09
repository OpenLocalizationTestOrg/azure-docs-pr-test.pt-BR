---
title: "aaaAzure e visão geral de rede de VM do Linux | Microsoft Docs"
description: "Uma visão geral da rede de VM do Azure e do Linux."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: b5420e35-0463-4456-9803-6142db150f2e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: c3de2dc583c62160e10c0e97e96fef49b9eaffbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-network-overview"></a>Visão geral de rede de VM do Azure e do Linux
## <a name="virtual-networks"></a>Redes Virtuais
Uma rede virtual do Azure (VNet) é uma representação de sua própria rede na nuvem hello. É uma isolamento lógico de saudação nuvem do Azure dedicado tooyour assinatura. Você pode controlar totalmente blocos de endereços IP hello, configurações de DNS, políticas de segurança e tabelas de rotas dentro dessa rede. Você também pode segmentar a VNet em sub-redes e iniciar as máquinas virtuais (VMs) de IaaS do Azure e/ou os Serviços de nuvem (instâncias de função de PaaS). Além disso, você pode conectar a rede Olá rede virtual tooyour local usando uma das opções de conectividade de saudação disponíveis no Azure. Em essência, você pode expandir tooAzure sua rede, com controle total em blocos de endereços IP com o benefício de saudação de escala corporativa que Azure fornece.

* [Visão geral da Rede Virtual](../../virtual-network/virtual-networks-overview.md)

uma rede virtual por meio de toocreate Olá CLI do Azure, vá toofollow aqui Olá passo a passo.

* [Como toocreate usando uma rede virtual Olá CLI do Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

## <a name="network-security-groups"></a>Grupos de segurança de rede
O grupo de segurança de rede (NSG) contém uma lista de regras de lista de controle de acesso (ACL) que permitem ou negam o tráfego de rede tooyour instâncias VM em uma rede Virtual. Os NSGs podem ser associados a sub-redes ou instâncias de VM individuais dentro dessa sub-rede. Quando um NSG está associado uma sub-rede, regras de ACL de saudação se aplicam a instâncias de VM Olá tooall nessa sub-rede. Além disso, o tráfego tooan VM individual pode ser restrito adicional associando um NSG toothat VM diretamente.

* [O que é um NSG (grupo de segurança de rede)?](../../virtual-network/virtual-networks-nsg.md)
* [Como NSGs toocreate em Olá CLI do Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

## <a name="user-defined-routes"></a>Rotas definidas pelo usuário
Quando você adiciona máquinas virtuais (VMs) tooa VPN (rede virtual) no Azure, você observará que Olá VMs são capaz de toocommunicate entre si pela rede hello, automaticamente. Não é necessário toospecify um gateway, embora Olá VMs estiverem em sub-redes diferentes. Olá mesmo é verdadeiro para comunicação de saudação VMs toohello Internet pública e rede de local tooyour mesmo quando uma conexão híbrida do Azure tooyour possui datacenter estiver presente.

* [O que são Rotas Definidas pelo Usuário e Encaminhamento de IP?](../../virtual-network/virtual-networks-udr-overview.md)
* [Criar um UDR no hello CLI do Azure](../../virtual-network/virtual-network-create-udr-arm-cli.md)

## <a name="associating-a-fqdn-tooyour-linux-vm"></a>Associando um tooyour FQDN VM do Linux
Quando você cria uma máquina virtual (VM) no portal do Azure de saudação recursos para a máquina virtual de saudação usando o modelo de implantação do Gerenciador de recursos hello, um IP público é criado automaticamente. Você usa essa saudação de acesso de tooremotely do endereço IP VM. Embora o portal de saudação não cria um nome de domínio totalmente qualificado, ou FQDN, por padrão, você pode adicionar um depois Olá VM é criada.

* [Criar um nome de domínio totalmente qualificado no hello portal do Azure](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="network-interfaces"></a>Interfaces de rede
Uma interface de rede (NIC) é a interconexão Olá entre uma máquina Virtual (VM) e Olá subjacente de rede de software. Este artigo explica quais uma interface de rede é e como ele é usado no modelo de implantação do Azure Resource Manager hello.

* [Interfaces de Rede Virtual](../../virtual-network/virtual-network-network-interface.md)

## <a name="virtual-nics-and-dns-labeling"></a>NICs virtuais o rotulação de DNS
Se você tiver um servidor que você precisa toobe persistentes, mas esse servidor é tratado como cattle e é subdividido e implantada com frequência, você desejará toouse rotulagem de DNS em seu nome NIC toopersist Olá Olá VNET.  Com hello após passo a passo, você irá configurar uma NIC de maneira persistente nomeada com um endereço IP estático.

* [Criar um ambiente completo do Linux usando Olá CLI do Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="virtual-network-gateways"></a>Gateways de Rede Virtual
Um gateway de rede virtual é usado toosend tráfego de rede entre redes virtuais do Azure e locais de local e também entre redes virtuais no Azure (VNet para VNet). Quando você configura um gateway de VPN, é necessário criar e configurar um gateway de rede virtual e uma conexão de gateway de rede virtual.

* [Sobre o Gateway de VPN](../../vpn-gateway/vpn-gateway-about-vpngateways.md)

## <a name="internal-load-balancing"></a>Balanceamento de carga interno
Um Azure Load Balancer é um balanceador de carga de Camada 4 (TCP, UDP). o balanceador de carga Olá fornece alta disponibilidade através da distribuição de tráfego de entrada entre instâncias do serviço de integridade em serviços de nuvem ou máquinas virtuais em um conjunto de Balanceador de carga. O Azure Load Balancer também pode apresentar esses serviços em várias portas, vários endereços IP ou ambos.

* [Criando um balanceador de carga interno usando Olá CLI do Azure](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)

