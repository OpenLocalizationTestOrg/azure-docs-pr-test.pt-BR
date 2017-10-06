---
title: aaaOverview do IPv6 para o balanceador de carga do Azure | Microsoft Docs
description: Entender o suporte a IPv6 para o Azure Load Balancer e VMs com balanceamento de carga.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "ipv6, azure load balancer, pilha dual, ip público, ipv6 nativo, móvel, iot"
ms.assetid: 6a1d583f-a305-40fd-a94b-fa42e1943bbb
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 5b203f77d86cc1ad455f4ebb297097aef46b658d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a>Visão geral do IPv6 para o Azure Load Balancer

Balanceadores de carga voltados para a Internet podem ser implantados com um endereço IPv6. Além disso tooIPv4 conectividade, isso permite Olá recursos a seguir:

* Ponta a ponta conectividade IPv6 nativa entre clientes de Internet públicos e máquinas virtuais (VMs) Azure por meio do balanceador de carga de saudação.
* Saída IPv6 nativa ponta a ponta entre VMs e clientes habilitados para IPv6 da Internet pública.

Olá a imagem a seguir ilustra a funcionalidade de saudação IPv6 para o balanceador de carga do Azure.

![Azure Load Balancer com IPv6](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

Uma vez implantado, um cliente IPv4 ou IPv6 habilitado Internet pode se comunicar Olá pública endereços IPv4 ou IPv6 (ou os nomes de host) do hello balanceador de carga para a Internet do Azure. rotas de Balanceador de carga Olá Olá pacotes toohello privada IPv6 endereços IPv6 de VMs hello usando conversão de endereços de rede (NAT). cliente de Internet IPv6 Olá não pode se comunicar diretamente com hello endereço IPv6 da saudação VMs.

## <a name="features"></a>Recursos

O suporte nativo a IPv6 para VMs implantadas por meio do Azure Resource Manager fornece:

1. Serviços de IPv6 com balanceamento de carga para clientes Olá Internet IPv6
2. Pontos de extremidade IPv4 e IPv6 nativos em VMs ("pilha dupla")
3. Conexões IPv6 nativas iniciadas por entrada e saída
4. Protocolos com suporte, como TCP, UDP e HTTP(S), permitem uma ampla gama de arquiteturas de serviço

## <a name="benefits"></a>Benefícios

Essa funcionalidade permite Olá principais vantagens a seguir:

* Atende aos regulamentos governamentais que exigem novos aplicativos ser acessíveis clientes somente tooIPv6
* Habilitar móveis e Internet das coisas (IOT) desenvolvedores toouse empilhada dual máquinas de virtuais do Azure (IPv4 com IPv6) tooaddress Olá móvel crescente & IOT mercados

## <a name="details-and-limitations"></a>Detalhes e limitações

Detalhes

* Olá serviço DNS do Azure contém um IPv4 e IPv6 AAAA registros de nome e responde com os dois registros Olá balanceador de carga. Olá cliente pode escolher quais toocommunicate de endereço (IPv4 ou IPv6) com.
* Quando uma máquina virtual inicia um dispositivo conectado à Internet IPv6 de conexão tooa pública, endereço IPv6 de origem da saudação VM é convertido de endereço de rede (NAT) toohello IPv6 endereço público saudação do balanceador de carga.
* Máquinas virtuais executando o sistema de operacional Linux Olá devem ser tooreceive configurado um endereço IP IPv6 por meio de DHCP. Muitas das imagens Linux Olá Olá Galeria do Azure já estão configuradas toosupport IPv6 sem modificação. Para saber mais, confira [Configuração de DHCPv6 em VMs do Linux](load-balancer-ipv6-for-linux.md)
* Se você escolher toouse uma integridade de teste com o balanceador de carga, criar um teste de IPv4 e usá-lo com hello IPv4 e IPv6 de pontos de extremidade. Se o serviço de saudação na sua VM falhar, Olá IPv4 e IPv6 de pontos de extremidade forem retirados da rotação.

Limitações

* Você não pode adicionar regras de balanceamento de carga do IPv6 em Olá portal do Azure. Olá regras só podem ser criadas por meio do modelo de hello, CLI, o PowerShell.
* Você não pode atualizar os endereços IPv6 de toouse de máquinas virtuais existentes. Você deve implantar novas VMs.
* Interface de rede tooa em cada VM pode ser atribuído a um único endereço IPv6.
* os endereços IPv6 públicos Olá não podem ser atribuídos tooa VM. Eles só podem ser atribuídos tooa balanceador de carga.
* Você não pode configurar a pesquisa inversa de DNS Olá para os endereços IPv6 públicos.
* Olá VMs com endereços IPv6 de saudação não pode ser membros de um serviço de nuvem do Azure. Podem ser conectado tooan rede Virtual do Azure (VNet) e se comunicar entre si através de seus endereços IPv4.
* Endereços IPv6 privados podem ser implantados em VMs individuais em um grupo de recursos, mas não podem ser implantados em um grupo de recursos por meio de Conjuntos de Escala.
* Máquinas virtuais do Azure não podem se conectar via IPv6 tooother VMs, outros serviços do Azure ou dispositivos locais. Eles podem se comunicar apenas com o balanceador de carga do Azure Olá via IPv6. No entanto, elas podem se comunicar com esses outros recursos usando IPv4.
* Há suporte para proteção de NSG (grupo de segurança de rede) para IPv4 em implantações de pilha dupla (IPv4+IPv6). Os NSGs não se aplicam a pontos de extremidade toohello IPv6.
* ponto de extremidade de saudação IPv6 em Olá VM não é diretamente exposto toohello internet. Ele fica atrás de um balanceador de carga. Somente as portas Olá especificadas nas regras de Balanceador de carga Olá são acessíveis via IPv6.
* Alterando Olá IdleTimeout parâmetro para IPv6 é **atualmente não tem suporte**. padrão de saudação é de quatro minutos.
* Alterando Olá parâmetro loadDistributionMethod para IPv6 é **atualmente não tem suporte**.
* **No momento, não há suporte** para IPs IPv6 reservados (em que IPAllocationMethod = estático).

## <a name="next-steps"></a>Próximas etapas

Saiba como toodeploy um balanceador de carga com o IPv6.

* [Disponibilidade do IPv6 por região](https://go.microsoft.com/fwlink/?linkid=828357)
* [Implantar um balanceador de carga com IPv6 usando um modelo](load-balancer-ipv6-internet-template.md)
* [Implantar um balanceador de carga com IPv6 usando o Azure PowerShell](load-balancer-ipv6-internet-ps.md)
* [Implantar um balanceador de carga com IPv6 usando CLI do Azure](load-balancer-ipv6-internet-cli.md)
