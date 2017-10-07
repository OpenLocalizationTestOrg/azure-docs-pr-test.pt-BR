---
title: "aaaHow tootag uma máquina virtual de Linux do Azure | Microsoft Docs"
description: "Saiba mais sobre a marcação de uma máquina virtual do Azure Linux criada no Azure usando o modelo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: 0e99ea66a87b7e00eb21a2f72dd2bce8673778dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a>Como tootag uma máquina virtual do Linux no Azure
Este artigo descreve as diferentes maneiras tootag uma máquina de virtual do Linux no Azure por meio do modelo de implantação do Gerenciador de recursos de saudação. As marcas são pares de chave/valor definidos pelo usuário que podem ser colocados diretamente em um recurso ou grupo de recursos. Azure atualmente oferece suporte a marcas de too15 por grupo de recursos e recursos. Marcas podem ser colocadas em um recurso no tempo de saudação da criação ou adicionado o recurso existente tooan. Observe que as marcas que têm suporte para recursos criados por meio do modelo de implantação de Gerenciador de recursos de saudação apenas.

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a>Marcando com a CLI do Azure
toobegin, [instalar e configurar Olá CLI do Azure](../../xplat-cli-azure-resource-manager.md) e verifique se você está no modo do Gerenciador de recursos (`azure config mode arm`).

Você pode exibir todas as propriedades para uma determinada máquina Virtual, incluindo marcas hello, usando este comando:

        azure vm show -g MyResourceGroup -n MyTestVM

tooadd uma nova marca VM por meio de saudação CLI do Azure, você pode usar o hello `azure vm set` comando junto com o parâmetro de marca hello **-t**:

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

tooremove todas as marcas, você pode usar o hello **– T** parâmetro hello `azure vm set` comando.

        azure vm set – g MyResourceGroup –n MyTestVM -T


Agora que estamos aplicou marcas tooour recursos CLI do Azure e Olá Portal, vamos dar uma olhada em toosee de detalhes de uso de saudação marcas Olá no portal de cobrança hello.

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Próximas etapas
* toolearn mais informações sobre a marcação de recursos do Azure, consulte [visão geral do Gerenciador de recursos do Azure] [ Azure Resource Manager Overview] e [tooorganize marcas usando os recursos do Azure] [ Using Tags tooorganize your Azure Resources].
* toosee como marcas podem ajudá-lo a gerenciar o uso de recursos do Azure, consulte [Noções básicas sobre sua conta do Azure] [ Understanding your Azure Bill] e [obter ideias sobre o consumo de recursos do Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
