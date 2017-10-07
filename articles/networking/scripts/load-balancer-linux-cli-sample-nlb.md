---
title: "Exemplo de Script CLI - tooVMs de tráfego de balanceamento de carga para alta disponibilidade de aaaAzure | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - tooVMs de tráfego de balanceamento de carga para alta disponibilidade"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 0954b5c261512724dfb9c6e7be123c9d45624f4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a>Carregar tooVMs de tráfego de balanceamento para alta disponibilidade

Este exemplo de script cria todo o necessário toorun várias máquinas virtuais de Ubuntu configurado em uma alta disponibilidade e de carga balanceada configuração. Após o script hello em execução, você terá três máquinas virtuais, tooan ingressado no conjunto de disponibilidade do Azure e acessível por meio de um balanceador de carga do Azure. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos toocreate um grupo de recursos, máquina virtual, o conjunto de disponibilidade, balanceador de carga e todos os recursos relacionados a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Cria uma sub-rede e uma rede virtual do Azure. |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Cria um endereço IP público com um endereço IP estático e um nome DNS associado. |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) | Cria um Azure Load Balancer. |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Cria uma investigação do balanceador de carga. Uma investigação do balanceador de carga é usado toomonitor cada VM no conjunto de Balanceador de carga de saudação. Se qualquer VM ficar inacessível, o tráfego não é roteado toohello VM. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Cria uma regra de balanceador de carga. Neste exemplo, uma regra é criada para a porta 80. Como o tráfego HTTP chega ao balanceador de carga Olá, é roteado tooport 80 uma saudação VMs no conjunto de balanceamento de carga de saudação. |
| [az network lb inbound-nat-rule create](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | Cria uma regra de NAT (conversão de endereços de rede) do balanceador de carga.  Regras NAT mapeiam uma porta de porta tooa do balanceador de carga Olá em uma máquina virtual. Neste exemplo, uma regra NAT é criada para o SSH tráfego tooeach VM no conjunto de Balanceador de carga de saudação.  |
| [az network nsg create](https://docs.microsoft.com/cli/azure/network/nsg#create) | Cria um grupo de segurança de rede (NSG), que é um limite de segurança entre a máquina de virtual de internet e Olá Olá. |
| [az network nsg rule create](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Cria um tooallow de regra NSG o tráfego de entrada. Neste exemplo, a porta 22 é aberta para o tráfego SSH. |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | Cria uma placa de rede virtual e anexa-rede virtual toohello, sub-rede e NSG. |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Cria um conjunto de disponibilidade. Conjuntos de disponibilidade garantem o funcionamento do aplicativo distribuindo as máquinas virtuais de saudação em recursos físicos, de modo que se ocorrer falha, todo o conjunto de saudação não é afetado. |
| [az vm create](/cli/azure/vm#create) | Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e NSG. Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI de rede do Azure adicionais podem ser encontrados no hello [documentação de rede do Azure](../cli-samples.md).
