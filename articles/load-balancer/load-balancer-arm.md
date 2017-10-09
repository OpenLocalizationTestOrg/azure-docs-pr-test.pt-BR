---
title: suporte do Gerenciador de recursos para o balanceador de carga de aaaAzure | Microsoft Docs
description: Usando o powershell do Load Balancer com o Azure Resource Manager. Usando modelos de balanceador de carga
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a>Usando o suporte do Azure Resource Manager com o Azure Load Balancer

Gerenciador de recursos do Azure é a estrutura de gerenciamento preferencial de saudação para serviços no Azure. O Azure Load Balancer pode ser gerenciado usando ferramentas e APIs baseadas no Azure Resource Manager.

## <a name="concepts"></a>Conceitos

Com o Gerenciador de recursos, o balanceador de carga do Azure contém Olá recursos filho a seguir:

* Configuração de IP front-end – um balanceador de carga pode incluir um ou mais endereços IP front-end, também conhecidos como VIPs (IPs virtuais). Esses endereços IP servem como entrada para o tráfego de saudação.
* Pool de endereços de back-end – são endereços IP associados à máquina virtual de saudação placa de rede (NIC) toowhich carga será distribuída.
* Balanceamento de carga de regras – uma propriedade de regra mapeia um IP de front-end especificado e a porta do conjunto de tooa de combinação de endereços IP de back-end e combinação de porta. Um balanceador de carga único pode ter várias regras de balanceamento de carga. Cada regra é uma combinação de um IP de front-end e IP de porta e back-end e porta associada a VMs.
* Testes – testes permitem que você tookeep faixa da integridade de saudação de instâncias de VM. Se um teste de integridade falhar, instância VM Olá será levada automaticamente da rotação.
* Regras de NAT de entrada – definir as regras de NAT Olá o tráfego de entrada que fluem através do IP de front-end hello e distribuída toohello volta terminar IP.

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a>Modelos de início rápido

Gerenciador de recursos do Azure permite que você tooprovision seus aplicativos usando um modelo declarativo. Em um modelo único, você pode implantar vários serviços, juntamente com suas dependências. Use Olá toorepeatedly do mesmo modelo implantar seu aplicativo durante cada estágio do ciclo de vida do aplicativo hello.

Modelos podem incluir definições para máquinas virtuais, redes virtuais, conjuntos de disponibilidade, NICs (Interfaces de Rede), contas de armazenamento, balanceadores de carga, grupos de segurança de rede e IPs públicos. Com os modelos, você pode criar tudo o que precisa para um aplicativo complexo. arquivo de modelo Olá pode ser inserido no sistema de gerenciamento de conteúdo para o controle de versão e a colaboração.

[Saiba mais sobre modelos](../azure-resource-manager/resource-manager-template-walkthrough.md)

[Saiba mais sobre recursos de rede](../virtual-network/resource-groups-networking.md)

Modelos de início rápido que usam o Azure Load Balancer podem ser encontrados em um [repositório GitHub](https://github.com/Azure/azure-quickstart-templates) que hospeda um conjunto de modelos gerados pela comunidade.

Exemplos de modelos:

* [2 VMs em um balanceador de carga e regras de balanceamento de carga](http://go.microsoft.com/fwlink/?LinkId=544799)
* [2 VMs em uma VNET com as regras de um balanceador de carga interno e regras do balanceador de carga](http://go.microsoft.com/fwlink/?LinkId=544800)
* [2 VMs em um balanceador de carga e configure as regras NAT em Olá LB](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a>Configurando o balanceador de carga do Azure com PowerShell ou CLI

Introdução aos cmdlets do Azure Resource Manager, ferramentas de linha de comando e APIs REST

* [Cmdlets de acesso à rede do Azure](https://msdn.microsoft.com/library/azure/mt163510.aspx) pode ser usado toocreate um balanceador de carga.
* [Como toocreate um balanceador de carga usando o Gerenciador de recursos do Azure](load-balancer-get-started-ilb-arm-ps.md)
* [Usando Olá CLI do Azure com o gerenciamento de recursos do Azure](../xplat-cli-azure-resource-manager.md)
* [APIs REST do balanceador de carga](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a>Próximas etapas

Também é possível [começar a criar um balanceador de carga para a Internet](load-balancer-get-started-internet-arm-ps.md) e configurar que tipo de [modo de distribuição](load-balancer-distribution-mode.md) para um comportamento específico de tráfego de rede do balanceador de carga.

Saiba como toomanage [ocioso configurações de tempo limite TCP para um balanceador de carga](load-balancer-tcp-idle-timeout.md). Isso é importante quando seu aplicativo precisa tookeep conexões ativo para servidores atrás de um balanceador de carga.
