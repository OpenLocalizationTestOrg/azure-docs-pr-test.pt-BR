---
title: aaaEnable ou desabilitar o monitoramento de VM do Azure
description: Descreve como tooEnable ou desabilitar o monitoramento de VM do Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a>Habilitar ou desabilitar o monitoramento da VM do Azure

Esta seção descreve como tooenable ou desabilite o monitoramento em Virtual máquinas em execução no Azure. Você pode habilitar ou desabilitar o monitoramento usando o portal de saudação ou Interface de linha de comando do Azure para Mac, Linux e Windows (Olá CLI do Azure).

> [!IMPORTANT]
> Este documento descreve a versão 2.3 Olá extensão de diagnóstico do Linux, que foi preterido. A versão 2.3 será suportada até 30 de junho de 2018.
>
> A versão 3.0 do hello extensão de diagnóstico do Linux pode ser habilitada em vez disso. Para obter mais informações, consulte [Olá documentação](./diagnostic-extension.md).

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a>Habilitar / desabilitar o monitoramento por meio de saudação portal do Azure

É possível habilitar o monitoramento da VM do Azure, que fornece dados sobre a sua instância em períodos de um minuto. (alterações de armazenamento se aplicam). Dados de diagnóstico detalhadas, em seguida, estão disponíveis para Olá VM gráficos portal hello ou por meio de saudação API. Por padrão, o portal do Azure permite o monitoramento baseado em host de um conjunto limitado de métricas. Você pode habilitar o monitoramento de métricas de dentro de uma máquina virtual durante a saudação que VM está em execução ou no estado parado.

* Abra hello Azure portal em [https://portal.azure.com](https://portal.azure.com).
* Na barra de navegação esquerda de Olá, clique em máquinas virtuais.
* Em máquinas virtuais da saudação lista, selecione uma instância em execução ou parada. Abre a folha de "Máquina Virtual" Hello.
* Clique em Todas as configurações.
* Clique em Diagnóstico.
* Alterar status tooOn ou desativado. Você também pode escolher neste nível de saudação de folha do monitoramento de detalhes que você deseja tooenable para sua máquina virtual.

![Habilitar / desabilitar o monitoramento por meio de saudação portal do Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a>Habilitar/desabilitar o monitoramento com a CLI do Azure

tooenable monitoramento para uma VM do Azure.

* Crie um arquivo (denominado PrivateConfig.json):

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* Habilite a extensão de saudação via CLI do Azure.

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

Para obter mais informações, consulte [de usando a extensão de diagnóstico do Linux tooMonitor Linux VM dados de desempenho e diagnósticos](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
