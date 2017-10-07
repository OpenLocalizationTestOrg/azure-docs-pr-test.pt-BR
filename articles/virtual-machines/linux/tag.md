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
ms.openlocfilehash: 456b226af4495c3b446cb79c99cf9494dde9fca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a>Como tootag uma máquina virtual do Linux no Azure
Este artigo descreve as diferentes maneiras tootag uma máquina de virtual do Linux no Azure por meio do modelo de implantação do Gerenciador de recursos de saudação. As marcas são pares de chave/valor definidos pelo usuário que podem ser colocados diretamente em um recurso ou grupo de recursos. Azure atualmente oferece suporte a marcas de too15 por grupo de recursos e recursos. Marcas podem ser colocadas em um recurso no tempo de saudação da criação ou adicionado o recurso existente tooan. Observe que as marcas que têm suporte para recursos criados por meio do modelo de implantação de Gerenciador de recursos de saudação apenas.

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a>Marcando com a CLI do Azure
toobegin, você precisa hello mais recente [2.0 de CLI do Azure (visualização)](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).

Você também pode executar essas etapas com hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Você pode exibir todas as propriedades para uma determinada máquina Virtual, incluindo marcas hello, usando este comando:

        az vm show --resource-group MyResourceGroup --name MyTestVM

tooadd uma nova marca VM por meio de saudação CLI do Azure, você pode usar o hello `azure vm update` comando junto com o parâmetro de marca hello **– defina**:

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

marcas de tooremove, você pode usar o hello **– remover** parâmetro hello `azure vm update` comando.

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


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
