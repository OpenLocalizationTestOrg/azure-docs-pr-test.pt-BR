---
title: "aaaWhat é uma lista de controle de acesso de rede do Azure?"
description: Saiba mais sobre listas de controle de acesso no Azure
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 83d66c84-8f6b-4388-8767-cd2de3e72d76
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a2681af035d162362771e6df9864bbe838f16352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-endpoint-access-control-list"></a>O que é uma lista de controle de acesso do ponto de extremidade?

> [!IMPORTANT]
> O Azure tem dois [modelos de implantação](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) diferentes para criar e trabalhar com recursos: o Gerenciador de Recursos e o Clássico. Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo de implantação do Gerenciador de recursos de saudação. 

Uma ACL (Lista de Controle de Acesso) de ponto de extremidade é uma melhoria de segurança disponível para a sua implantação do Azure. Uma ACL fornece Olá capacidade tooselectively permitir ou negar o tráfego para um ponto de extremidade de máquina virtual. Essa capacidade de filtragem de pacotes proporciona uma camada adicional de segurança. Você pode especificar ACLs de rede apenas para pontos de extremidade. Não é possível especificar uma ACL para uma rede virtual ou uma sub-rede específica contida em uma rede virtual. É recomendável toouse grupos de segurança de rede (NSGs) em vez de ACLs, sempre que possível. toolearn mais sobre os NSGs, consulte [visão geral do grupo de segurança de rede](virtual-networks-nsg.md)

ACLs podem ser configuradas usando o PowerShell ou Olá portal do Azure. tooconfigure uma ACL de rede usando o PowerShell, consulte [listas de controle de acesso de gerenciamento para pontos de extremidade usando o PowerShell](virtual-networks-acl-powershell.md). uma ACL de rede por meio de tooconfigure hello Azure portal, consulte [como tooset máquina de virtual pontos de extremidade tooa](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Usando as ACLs de rede, você pode fazer a seguir hello:

* Seletivamente permitir ou negar o tráfego de entrada com base em IPv4 endereço intervalo tooa máquina virtual entrada ponto de extremidade de sub-rede remota.
* Inserir endereços IP em uma lista negra
* Criar várias regras por ponto de extremidade de máquina virtual
* Use a regra de ordenação tooensure Olá correto de conjunto de regras são aplicadas em um ponto de extremidade da máquina virtual fornecida (toohighest mais baixo)
* Especificar uma ACL para um endereço IPv4 de sub-rede remota específica.

Consulte Olá [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) artigo para limites ACL.

## <a name="how-acls-work"></a>Como funcionam as ACLs
Uma ACL é um objeto que contém uma lista de regras. Quando você cria uma ACL e aplique-o ponto de extremidade de máquina virtual tooa, filtragem de pacote ocorre no nó de host de saudação da VM. Isso significa que o tráfego de saudação de endereços IP remotos é filtrado pelo nó de host Olá regras de ACL correspondência em vez de na sua VM. Isso impede que a VM gaste os preciosos ciclos de CPU Olá na filtragem de pacotes.

Quando uma máquina virtual é criada, uma ACL padrão é colocada no local tooblock todo o tráfego de entrada. No entanto, se um ponto de extremidade é criado para (porta 3389), em seguida, padrão Olá que ACL é modificada tooallow todo o tráfego de entrada para esse ponto de extremidade. O tráfego de entrada de qualquer sub-rede remota é então permitido toothat de ponto de extremidade e nenhum provisionamento de firewall é necessária. Todas as outras portas são bloqueadas para tráfego de entrada, a menos que os pontos de extremidade sejam criados para essas portas. O tráfego de saída é permitido por padrão.

**Exemplo de tabela ACL padrão**

| **Nº da regra** | **Sub-rede remota** | **Ponto de extremidade** | **Permitir/Negar** |
| --- | --- | --- | --- |
| 100 |0.0.0.0/0 |3389 |Permitir |

## <a name="permit-and-deny"></a>Permitir e negar
Você pode permitir ou negar seletivamente o tráfego de rede para um ponto de extremidade de entrada de máquina virtual criando regras que especificam "permitir" ou "negar". É importante toonote que por padrão, quando um ponto de extremidade é criado, todo o tráfego é permitido toohello de ponto de extremidade. Por esse motivo, é importante toounderstand como toocreate regras de Permitir/Negar e colocá-los na ordem de precedência Olá apropriada se você quiser um controle granular sobre rede Olá tráfego que você escolher o ponto de extremidade da máquina virtual Olá tooallow tooreach.

Tooconsider pontos:

1. **Nenhum ACL –** por padrão quando um ponto de extremidade é criado, permitimos tudo para o ponto de extremidade de saudação.
2. **Permitir -** quando você adiciona um ou mais intervalos de "permissão", está negando todos os outros intervalos por padrão. Somente os pacotes de saudação permitido intervalo IP será capaz de toocommunicate com ponto de extremidade de máquina virtual de saudação.
3. **Negar -** quando você adiciona um ou mais intervalos de "negação", está permitindo, por padrão, todos os outros intervalos do tráfego.
4. **Combinação de permitir e negar -** você pode usar uma combinação de "Permitir" e "Negar" quando você deseja toocarve-out de um IP específico intervalo toobe permitido ou negado.

## <a name="rules-and-rule-precedence"></a>Regras e precedência de regras
As ACLs de rede podem ser configuradas em pontos de extremidade de máquina virtual específicos. Por exemplo, você pode especificar uma ACL de rede para um ponto de extremidade RDP criado em uma máquina virtual que bloqueia o acesso de determinados endereços IP. Olá, tabela a seguir mostra um toopublic de acesso do modo toogrant IPs virtuais (VIPs) de um determinado intervalo toopermit acesso RDP. Todos os outros IPs remotos são negados. Seguimos uma ordem de regras em que a *mais baixa tem precedência* .

### <a name="multiple-rules"></a>Várias regras
O exemplo hello abaixo, se você quiser que o ponto de extremidade do tooallow acesso toohello RDP apenas de dois públicos intervalos de endereços IPv4 (65.0.0.0/8 e 159.0.0.0/8), você pode obter isso especificando duas *permitir* regras. Nesse caso, já que o RDP é criado por padrão para uma máquina virtual, convém toolock para baixo de porta do RDP toohello acesso com base em uma sub-rede remota. Olá, exemplo a seguir mostra um toopublic de acesso do modo toogrant IPs virtuais (VIPs) de um determinado intervalo toopermit acesso RDP. Todos os outros IPs remotos são negados. Isso funciona porque as ACLs de rede podem ser configuradas para um ponto de extremidade específico de máquina virtual e o acesso é negado por padrão.

**Exemplo – Várias regras**

| **Nº da regra** | **Sub-rede remota** | **Ponto de extremidade** | **Permitir/Negar** |
| --- | --- | --- | --- |
| 100 |65.0.0.0/8 |3389 |Permitir |
| 200 |159.0.0.0/8 |3389 |Permitir |

### <a name="rule-order"></a>Ordem das regras
Como várias regras podem ser especificadas para um ponto de extremidade, deve haver regras tooorganize de maneira em ordem toodetermine quais regras têm precedência. Especifica a ordem da regra Olá precedência. As ACLs de rede seguem uma ordem de regras em que a *mais baixa tem precedência* . O exemplo hello abaixo, ponto de extremidade de saudação na porta 80 é concedido seletivamente o acesso tooonly determinados intervalos de endereços IP. tooconfigure isso, temos uma regra de negação (regra \# 100) para endereços no espaço de 175.1.0.1/24 hello. Uma segunda regra é especificada com a precedência de 200 que permite acessar tooall outros endereços em 175.0.0.0/8.

**Exemplo – Precedência de regra**

| **Nº da regra** | **Sub-rede remota** | **Ponto de extremidade** | **Permitir/Negar** |
| --- | --- | --- | --- |
| 100 |175.1.0.1/24 |80 |Negar |
| 200 |175.0.0.0/8 |80 |Permitir |

## <a name="network-acls-and-load-balanced-sets"></a>ACLs de rede e conjuntos de cargas balanceadas
As ACLs de rede podem ser especificadas em um ponto de extremidade com conjunto de balanceamento de carga. Se for especificada uma ACL para um conjunto com balanceamento de carga, o ACL de rede Olá é máquinas virtuais de tooall aplicada em conjunto com balanceamento de carga. Por exemplo, se um conjunto com balanceamento de carga é criado com a "Porta 80" e Olá conjunto de balanceamento de carga contiver 3 máquinas virtuais, rede Olá ACL criada no ponto de extremidade "Porta 80" de uma que VM será automaticamente aplica toohello outras VMs.

![ACLs de rede e conjuntos de cargas balanceadas](./media/virtual-networks-acl/IC674733.png)

## <a name="next-steps"></a>Próximas etapas
[Gerenciar listas de controle de acesso para pontos de extremidade usando o PowerShell](virtual-networks-acl-powershell.md)

