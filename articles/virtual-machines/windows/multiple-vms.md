---
title: "aaaCreate várias máquinas virtuais | Microsoft Docs"
description: "Opções para criar várias máquinas virtuais no Windows"
services: virtual-machines-windows
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dfc1d1bb-a47d-4d7c-9fd2-f12050baacab
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: guybo
ms.openlocfilehash: 37729fabd91049744f6bd94c55221f5c1c65d527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-multiple-azure-virtual-machines"></a>Criar várias máquinas virtuais do Azure
Há muitos cenários em que você precisa toocreate um grande número de máquinas virtuais semelhantes (VMs). Alguns exemplos incluem HPC (computação de alto desempenho), análise de dados em grande escala, servidores de camada intermediária ou back-end escalonáveis e, muitas vezes, sem monitoração de estado (como servidores Web) e bancos de dados distribuídos.

Este artigo aborda Olá opções disponíveis toocreate várias VMs no Azure. Essas opções ultrapassar casos simples hello, onde você criar manualmente uma série de máquinas virtuais. toocreate várias VMs, processos de saudação que você normalmente usa não escala bem se for necessário toocreate mais de uma série de máquinas virtuais.

Unidirecional toocreate várias VMs semelhantes é construção de Gerenciador de recursos do Azure Olá toouse de *loops de recurso*.

## <a name="resource-loops"></a>loops de recursos
Os loops de recursos são um tipo de taquigrafia sintática em modelos do Azure Resource Manager. Os loops de recursos podem criar um conjunto de recursos configurados da mesma forma em um loop. Você pode usar o recurso loops toocreate várias contas de armazenamento, interfaces de rede ou máquinas virtuais. Para obter mais informações sobre loops de recursos, consulte muito[criar VMs em conjuntos de disponibilidade usando o recurso loops](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/).

## <a name="challenges-of-scale"></a>Desafios da escala
Embora os loops de recurso tornar mais fácil toobuild-out de uma infraestrutura de nuvem em escala e geram mais concisos modelos, determinados desafios permanecem. Por exemplo, se você usar um loop toocreate 100 máquinas virtuais de recursos, você precisa de controladores de interface de rede toocorrelate (NICs) com contas de armazenamento e VMs correspondentes. Como número de saudação de VMs é provavelmente toobe diferente do número de saudação de contas de armazenamento, terá muito toodeal com tamanhos de loop de recurso diferente. Estes são problemas pode ser resolvidos, mas aumenta significativamente a complexidade de saudação com escala.

Outro desafio ocorre quando você precisa de uma infraestrutura que seja dimensionada elasticamente. Por exemplo, talvez seja uma infraestrutura de dimensionamento automático que aumenta ou diminui o número de saudação de VMs em tooworkload resposta automaticamente. Máquinas virtuais não oferecem um toovary mecanismo integrado no número (expansão e escala em). Se você expandir em removendo VMs, é difícil tooguarantee alta disponibilidade, certificando-se de que as VMs são balanceadas entre domínios de atualização e falha.

Finalmente, quando você usa um loop de recursos, vários recursos de toocreate chamadas vão malha subjacente toohello. Quando várias chamadas criar recursos semelhantes, o Azure tem uma tooimprove oportunidade implícita este projeto e otimizar o desempenho e confiabilidade de implantação. É aí que entram os *conjuntos de escala de máquina virtual* .

## <a name="virtual-machine-scale-sets"></a>conjuntos de escala de máquina virtual
Conjuntos de escala de máquinas virtuais são uma toodeploy de recursos de computação do Azure e gerenciam um conjunto de VMs idênticos. Com todas as máquinas virtuais configuradas Olá mesmo, conjuntos de escala de VM são tooscale fácil no e expansão. Você simplesmente alterar número de saudação de VMs no conjunto de saudação. Você também pode configurar tooautoscale de conjuntos de escala VM com base nas demandas de saudação de carga de trabalho de saudação.

Para aplicativos que precisam de recursos de computação tooscale e em escala operações implicitamente são balanceadas entre domínios de falha e atualização.

Em vez de correlacionar vários recursos, como NICs e VMs, um conjunto de escala de VM tem propriedades de rede, armazenamento, máquina virtual e extensão que você pode configurar centralmente.

Define uma escala de tooVM de Introdução, consulte toohello [escala de máquina Virtual define a página do produto](https://azure.microsoft.com/services/virtual-machine-scale-sets/). Para obter mais informações, acesse toohello [escala de máquinas virtuais define documentação](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/).

