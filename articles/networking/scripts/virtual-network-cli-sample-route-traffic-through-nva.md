---
title: "exemplo de script CLI aaaAzure - rotear o tráfego por meio de um dispositivo de rede virtual | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Rotear o tráfego por meio de uma solução de virtualização de rede de firewall.solução de virtualização."
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a>Rotear o tráfego por meio de uma solução de virtualização de rede

Este exemplo de script cria uma rede virtual com sub-redes de front-end e back-end. Ele também cria uma VM com tráfego tooroute habilitado entre duas sub-redes de saudação de encaminhamento IP. Depois de executar o script hello, você pode implantar o software de rede, como um aplicativo de firewall, toohello VM.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>Script de exemplo


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá toocreate comandos a seguir, um grupo de recursos, a rede virtual e grupos de segurança de rede. Cada comando na tabela Olá vincula a documentação específica do toocommand.

| Command | Observações |
|---|---|
| [az group create](/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az network vnet create](/cli/azure/network/vnet#create) | Cria uma rede virtual do Azure e uma sub-rede front-end. |
| [az network subnet create](/cli/azure/network/vnet/subnet#create) | Cria as sub-redes back-end e DMZ. |
| [az network public-ip create](/cli/azure/network/public-ip#create) | Cria um tooaccess endereço IP público Olá VM de saudação à Internet. |
| [az network nic create](/cli/azure/network/nic#create) | Cria uma interface de rede virtual e habilita o encaminhamento IP nela. |
| [az network nsg create](/cli/azure/network/nsg#create) | Cria um grupo de segurança de rede (NSG). |
| [az network nsg rule create](/cli/azure/network/nsg/rule#create) | Cria regras NSG que permitem que as portas HTTP e HTTPS de entrada toohello VM. |
| [az network vnet subnet update](/cli/azure/network/vnet/subnet#update)| Associa Olá NSGs e toosubnets de tabelas de rota. |
| [az network route-table create](/cli/azure/network/route-table#create)| Cria uma tabela de rotas com todas as rotas. |
| [az network route-table route create](/cli/azure/network/route-table/route#create)| Cria rotas tooroute tráfego entre as sub-redes e saudação da Internet por meio de saudação VM. |
| [az vm create](/cli/azure/vm#create) | Cria uma máquina virtual e anexa Olá NIC tooit. Esse comando também especifica Olá toouse de imagem de máquina virtual e as credenciais administrativas. |
| [az group delete](/cli/azure/group#delete) | Exclui um grupo de recursos e todos os seus recursos contidos nele. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](/cli/azure/overview).

Exemplos de script CLI rede adicionais podem ser encontrados no hello [documentação de visão geral da rede do Azure](../cli-samples.md)
