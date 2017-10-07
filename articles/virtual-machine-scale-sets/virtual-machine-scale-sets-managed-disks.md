---
title: "aaaUsing gerenciados discos com o Azure escala conjuntos de máquinas virtuais | Microsoft Docs"
description: "Saiba por que e como toouse gerenciados discos com conjuntos de escala de máquinas virtuais"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a>Conjuntos de dimensionamento de VMs do Azure e discos gerenciados

Os [conjuntos de dimensionamento de máquinas virtuais](/azure/virtual-machine-scale-sets/) do Azure oferecem suporte a máquinas virtuais com discos gerenciados. O uso de discos gerenciados com conjuntos de dimensionamento tem vários benefícios, incluindo:

* Você não precisa mais toopre-criar e gerenciar os discos de armazenamento de contas toostore Olá SO para VMs do conjunto de escala de saudação.

* Você pode anexar um conjunto de escala de toohello de discos de dados gerenciados.

* Com o disco gerenciado, um conjunto de dimensionamento poderá ter a capacidade de até 1.000 VMs se for baseado em uma imagem de plataforma, ou 100 VMs se for baseado em uma imagem personalizada.

## <a name="get-started"></a>Introdução

Uma maneira simples tooget iniciado com conjuntos de escala de disco gerenciado é toodeploy de saudação portal do Azure. Para obter mais informações, consulte [este artigo](./virtual-machine-scale-sets-portal-create.md). Outra maneira simple tooget iniciado é toouse [2.0 do CLI do Azure](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy uma escala definida. Olá exemplo a seguir mostra como toocreate um Ubuntu com base em escala com 10 VMs, cada um com um disco de 50 GB e 100 GB de dados:

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

Como alternativa, você pode examinar Olá [repositório GitHub de modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates) para pastas que contêm `vmss` toosee pré-criadas exemplos de modelos que implantar conjuntos de escala. tootell quais modelos já estiver usando discos gerenciados, você pode consultar muito[essa lista](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre discos gerenciados em geral, confira [este artigo](../virtual-machines/windows/managed-disks-overview.md).

toosee como tooconvert conjuntos de uma escala de tooprovision de modelo do Gerenciador de recursos com gerenciado discos, consulte [neste artigo](./virtual-machine-scale-sets-convert-template-to-md.md). Olá, modelos de Gerenciador de recursos do mesmo modificações toohello aplicam toohello API REST do Azure.

toolearn mais sobre como usar discos de dados gerenciado com conjuntos de escala, consulte [neste artigo](./virtual-machine-scale-sets-attached-disks.md).

toobegin trabalhando com conjuntos de grande escala, consulte muito[neste artigo](./virtual-machine-scale-sets-placement-groups.md).


