---
title: "aaaRedeploy máquinas virtuais Linux no Azure | Microsoft Docs"
description: "Como máquinas de virtuais de Linux tooredeploy na conexão de SSH toomitigate do Azure emite."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a>Reimplantar toonew de máquina virtual Linux nó do Azure
Se você enfrentar problemas SSH de solução de problemas ou aplicativo acessar a máquina virtual do Linux tooa (VM) no Azure, reimplantar Olá VM pode ajudar. Quando você reimplanta uma VM, ele move Olá VM tooa novo nó no hello infraestrutura do Azure e liga novamente. Todos os recursos associados e opções de configuração são mantidos. Este artigo mostra como tooredeploy uma VM usando a CLI do Azure ou hello portal do Azure.

> [!NOTE]
> Depois que você reimplanta uma VM, disco temporário Olá é perdido e endereços IP dinâmicos associados à interface de rede virtual são atualizados. 

Você pode reimplantar uma VM usando um Olá as opções a seguir. Você só precisa toochoose uma opção tooredeploy sua VM:

- [CLI 2.0 do Azure](#azure-cli-20)
- [CLI 1.0 do Azure](#azure-cli-10)
- [Portal do Azure](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a>Use Olá 2.0 do CLI do Azure
Saudação de instalação mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e fazer logon na conta do Azure usando o tooan [logon az](/cli/azure/#login).

Reimplante a VM com [az vm redeploy](/cli/azure/vm#redeploy). Olá reimplanta de exemplo a seguir Olá VM denominada *myVM* no grupo de recursos de saudação denominado *myResourceGroup*:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a>Use Olá 1.0 da CLI do Azure
Instalar Olá [mais recente do Azure CLI 1.0](../../cli-install-nodejs.md), faça logon no tooan conta do Azure e certifique-se de que você está no modo do Gerenciador de recursos (`azure config mode arm`).

Olá reimplanta de exemplo a seguir Olá VM denominada *myVM* no grupo de recursos de saudação denominado *myResourceGroup*:

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Próximas etapas
Se você estiver tendo problemas para se conectar tooyour VM, você pode encontrar ajuda específica na [Solucionando problemas de conexões SSH](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [detalhadas etapas de solução de problemas de SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Você também pode ler [problemas com a solução de problemas de aplicativo](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se não conseguir acessar um aplicativo em execução em sua VM.

