---
title: "balanceamento de carga de aaaAzure exemplo de Script CLI - vários sites com hello CLI do Azure | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - toohello de vários sites o balanceamento de carga mesma máquina virtual"
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
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a>Balanceamento de carga de vários sites

Este exemplo de script cria uma rede virtual com duas VMs (máquinas virtuais) que são membros de um conjunto de disponibilidade. Um balanceador de carga direcione o tráfego para separar duas toohello duas VMs de endereços IP. Após o script hello em execução, você pode implantar web server software toohello VMs e hospedar vários sites, cada qual com seu próprio endereço IP.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos toocreate um grupo de recursos de rede virtual, o balanceador de carga e relacionados com todos os recursos a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Cria uma sub-rede e uma rede virtual do Azure. |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Cria um endereço IP público com um endereço IP estático e um nome DNS associado. |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) | Cria um Azure Load Balancer. |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Cria uma investigação do balanceador de carga. Uma investigação do balanceador de carga é usado toomonitor cada VM no conjunto de Balanceador de carga de saudação. Se qualquer VM ficar inacessível, o tráfego não é roteado toohello VM. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Cria uma regra de balanceador de carga. Neste exemplo, uma regra é criada para a porta 80. Como o tráfego HTTP chega ao balanceador de carga Olá, é roteado tooport 80 uma saudação VMs no conjunto de Balanceador de carga de saudação. |
| [az network lb frontend-ip create](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | Crie um endereço IP de front-end para Olá balanceador de carga. |
| [az network lb address-pool create](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | Cria um pool de endereços de back-end. |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | Cria uma placa de rede virtual e anexa-rede virtual toohello e sub-rede. |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Cria um conjunto de disponibilidade. Conjuntos de disponibilidade garantem o funcionamento do aplicativo distribuindo as máquinas virtuais de saudação em recursos físicos, de modo que se ocorrer falha, todo o conjunto de saudação não é afetado. |
| [az network nic ip-config create](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | Cria uma configuração de IP. Você deve ter o recurso de Microsoft.Network/AllowMultipleIpConfigurationsPerNic Olá habilitado para sua assinatura. Somente uma configuração pode ser designada como a configuração de IP primário Olá por NIC, usando hello – sinalizador tornar primário. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e NSG. Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI rede adicionais podem ser encontrados no hello [documentação de visão geral da rede do Azure](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
