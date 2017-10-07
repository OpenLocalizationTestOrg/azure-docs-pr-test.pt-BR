---
title: "aaaDesign considerações para conjuntos de escala de máquina Virtual do Azure | Microsoft Docs"
description: "Aprenda sobre considerações de design para seus conjuntos de dimensionamento de máquinas virtuais do Azure"
keywords: "máquina virtual linux, conjuntos de dimensionamento de máquina virtual"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: c27c6a59-a0ab-4117-a01b-42b049464ca1
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: f8644d36fe5903bd4b74df26dca5dc3211ee3516
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-considerations-for-scale-sets"></a>Considerações de design para conjuntos de dimensionamento
Este tópico discute considerações de design para Conjuntos de Escala de Máquina Virtual. Para obter informações sobre o que são conjuntos de escala de máquina Virtual, consulte muito[visão geral de conjuntos de escala de máquina Virtual](virtual-machine-scale-sets-overview.md).

## <a name="when-toouse-scale-sets-instead-of-virtual-machines"></a>Quando a escala toouse define, em vez de máquinas virtuais?
Em geral, os conjuntos de dimensionamento são úteis para implantar a infraestrutura altamente disponível em que um conjunto de computadores têm configuração semelhante. No entanto, alguns recursos só estão disponíveis em conjuntos de dimensionamento, enquanto outros recursos só estão disponíveis em VMs. Em ordem toomake uma decisão informada sobre quando toouse cada tecnologia, vamos primeiro deve dar uma olhada alguns dos recursos de saudação usado que estão disponíveis em conjuntos de escala, mas não as VMs:

### <a name="scale-set-specific-features"></a>Recursos específicos de conjunto de dimensionamento

- Depois que você especificar a configuração do conjunto de escala hello, você pode simplesmente atualizar hello "capacidade" propriedade toodeploy mais VMs em paralelo. Isso é muito mais simples do que escrever um tooorchestrate script Implantando várias VMs individuais em paralelo.
- Você pode [uso do Azure AutoEscala tooautomatically dimensionar um conjunto de escala](./virtual-machine-scale-sets-autoscale-overview.md) mas VMs não individuais.
- Você pode [refazer a imagem de VMs de conjunto de dimensionamento](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-a-vm), mas [não de VMs individuais](https://docs.microsoft.com/rest/api/compute/virtualmachines).
- Você pode [superprovisionar](./virtual-machine-scale-sets-design-overview.md) VMs de conjunto de dimensionamento maior confiabilidade e tempos de implantação mais rápidos. Você não pode fazer isso com VMs individuais, a menos que você escrever código personalizado toodo isso.
- Você pode especificar um [atualizar política](./virtual-machine-scale-sets-upgrade-scale-set.md) toomake-tooroll fácil atualizações entre VMs em seu conjunto de escala. Com VMs individuais, você mesmo deve organizar as atualizações.

### <a name="vm-specific-features"></a>Recursos específicos de VM

Em Olá outro lado, alguns recursos só estão disponíveis em máquinas virtuais (pelo menos do que está sendo Olá tempo):

- Você pode anexar dados discos toospecific VMs individuais, mas os discos de dados anexados são configurados para todas as VMs em um conjunto de escala.
- Você pode anexar discos de dados não vazio tooindividual VMs, mas não as VMs em um conjunto de escala.
- Você pode fazer um instantâneo de uma VM individual, mas não de uma VM em um conjunto de dimensionamento.
- Você pode capturar uma imagem de uma VM individual, mas não de uma VM em um conjunto de dimensionamento.
- Você pode migrar uma VM individual de discos de toomanaged discos nativos, mas você não pode fazer isso para VMs em um conjunto de escala.
- Você pode atribuir endereços IP públicos de IPv6 tooindividual nics VM, mas não é possível fazer isso para VMs em um conjunto de escala. Observe que você pode atribuir endereços IP públicos de IPv6 balanceadores tooload na frente de qualquer VMs individuais ou conjunto de escala de máquinas virtuais.

## <a name="storage"></a>Armazenamento

### <a name="scale-sets-with-azure-managed-disks"></a>Conjuntos de dimensionamento com Azure Managed Disks
Conjuntos de dimensionamento podem ser criados com [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md), em vez de contas de armazenamento do Azure tradicionais. Discos gerenciados fornecem Olá benefícios a seguir:
- Você não tem toopre-criar um conjunto de contas de armazenamento do Azure para VMs do conjunto de escala de saudação.
- Você pode definir [discos de dados conectados](virtual-machine-scale-sets-attached-disks.md) para Olá VMs em sua escala definida.
- Conjuntos de escala podem ser configurados de maneira muito[oferecem suporte a too1, 000 VMs em um conjunto de](virtual-machine-scale-sets-placement-groups.md). 

Se você tiver um modelo existente, você também pode [atualizar Olá modelo toouse discos gerenciado](virtual-machine-scale-sets-convert-template-to-md.md).

### <a name="user-managed-storage"></a>Armazenamento gerenciado pelo usuário
Um conjunto de escala que não está definido com discos gerenciado do Azure depende de discos de SO armazenamento criado pelo usuário contas toostore Olá Olá VMs no conjunto de saudação. Uma proporção de 20 VMs por conta de armazenamento ou menos é recomendada e/s máxima de tooachieve e também tirar proveito do _superprovisionamento_ (veja abaixo). Também é recomendável que você espalhados caracteres iniciais de saudação de nomes de conta de armazenamento Olá alfabeto hello. Isso ajuda a distribuir a carga entre diferentes sistemas internos. 


## <a name="overprovisioning"></a>Provisionamento em excesso
Escala define atualmente padrão muito "excesso de provisionamento" VMs. Com excesso de provisionamento ativado, escala de saudação definido realmente gira mais máquinas virtuais que você solicitou, exclui Olá VMs adicionais depois de saudação solicitou o número de VMs com êxito são provisionadas. O provisionamento em excesso melhora as taxas de sucesso do provisionamento e reduz o tempo de implantação. Você não será cobrado para hello VMs adicionais e eles não são contadas seus limites de cota.

Excesso de provisionamento de melhorar as taxas de sucesso de provisionamento, ele pode causar confusão no comportamento de um aplicativo que é projetado não toohandle VMs adicionais que aparece e, em seguida, desaparece. tooturn excesso de provisionamento, certifique-se de ter Olá cadeia de caracteres no modelo a seguir: `"overprovision": "false"`. Mais detalhes podem ser encontrados no hello [documentação da API de REST de conjunto de escala](/rest/api/virtualmachinescalesets/create-or-update-a-set).

Se seu conjunto de escala usa armazenamento gerenciada pelo usuário, e você desativar excesso de provisionamento, você pode ter mais de 20 VMs por conta de armazenamento, mas não é recomendável toogo acima 40 por motivos de desempenho de e/s. 

## <a name="limits"></a>limites
Um conjunto de escala criada em uma imagem do Marketplace (também conhecido como uma imagem de plataforma) e configurada toouse discos gerenciado do Azure oferece suporte a uma capacidade de backup too1, 000 VMs. Se você configurar sua toosupport de conjunto de escala mais de 100 VMs, não todo o trabalho de cenários Olá mesmo (por exemplo balanceamento de carga). Para obter mais informações, confira [Como trabalhar com conjuntos de dimensionamento grandes de máquinas virtuais](virtual-machine-scale-sets-placement-groups.md). 

Escala de um conjunto configurada com contas de armazenamento gerenciada pelo usuário é atualmente limitada too100 VMs (e 5 contas de armazenamento são recomendadas para essa escala).

Um conjunto de escala criado em uma imagem personalizada (um criado por você) pode ter a capacidade de máquinas virtuais de too100 quando configurado com discos gerenciado do Azure. Se o conjunto de escala hello está configurado com contas de armazenamento gerenciada pelo usuário, ele deve criar todos os VHDs de disco do sistema operacional em uma conta de armazenamento. Como resultado, o máximo Olá número recomendado de VMs em um conjunto de escala criado em uma imagem personalizada e armazenamento gerenciada pelo usuário é 20. Se você desativar o excesso de provisionamento, você pode subir too40.

Para mais de VMs de permitir que esses limites, você precisa toodeploy escala vários define como mostrado na [este modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/301-custom-images-at-scale).

