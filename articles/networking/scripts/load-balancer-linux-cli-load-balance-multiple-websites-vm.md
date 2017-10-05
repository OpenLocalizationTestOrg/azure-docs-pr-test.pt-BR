---
title: "Exemplo de script da CLI do Azure - Balanceamento de carga de vários sites com a CLI do Azure | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Balanceamento de carga de vários sites para a mesma máquina virtual"
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
ms.openlocfilehash: c5a584b33025122033b930822ae0a0864a7ec1cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-multiple-websites"></a>Balanceamento de carga de vários sites

Este exemplo de script cria uma rede virtual com duas VMs (máquinas virtuais) que são membros de um conjunto de disponibilidade. Um balanceador de carga direciona o tráfego para dois endereços IP separados para as duas VMs. Depois de executar o script, você pode implantar software do servidor Web para as VMs e hospedar vários sites, cada um com seu próprio endereço IP.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Balancear a carga de vários sites")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa os seguintes comandos para criar um grupo de recursos, uma rede virtual, um balanceador de carga e todos os recursos relacionados. Cada comando na tabela redireciona para a documentação específica do comando.

| Command | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Cria uma sub-rede e uma rede virtual do Azure. |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Cria um endereço IP público com um endereço IP estático e um nome DNS associado. |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) | Cria um Azure Load Balancer. |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Cria uma investigação do balanceador de carga. Uma investigação do balanceador de carga é usada para monitorar cada VM no conjunto de balanceadores de carga. Se qualquer VM ficar inacessível, o tráfego não é roteado para a máquina virtual. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Cria uma regra de balanceador de carga. Neste exemplo, uma regra é criada para a porta 80. Conforme o tráfego HTTP chega ao balanceador de carga, ele é roteado para a porta 80, uma das VMs no conjunto de balanceadores de carga. |
| [az network lb frontend-ip create](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | Crie um endereço IP de front-end para o balanceador de carga. |
| [az network lb address-pool create](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | Cria um pool de endereços de back-end. |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | Cria uma placa de rede virtual e a anexa à rede virtual e à sub-rede. |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Cria um conjunto de disponibilidade. Conjuntos de disponibilidade garantem o funcionamento de aplicativos, distribuindo as máquinas virtuais em recursos físicos, de modo que, se ocorrer uma falha, todo o conjunto não é afetado. |
| [az network nic ip-config create](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | Cria uma configuração de IP. O recurso Microsoft.Network/AllowMultipleIpConfigurationsPerNic deve estar habilitado para sua assinatura. Somente uma configuração pode ser designada como a configuração de IP primário por NIC, usando o sinalizador --make-primary. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Cria a máquina virtual e a conecta a placa de rede, a rede virtual, a sub-rede e o NSG. Este comando também especifica a imagem da máquina virtual a ser usada e as credenciais administrativas.  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos adicionais de script de CLI de rede podem ser encontrados na [Documentação de visão geral da rede do Azure](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
