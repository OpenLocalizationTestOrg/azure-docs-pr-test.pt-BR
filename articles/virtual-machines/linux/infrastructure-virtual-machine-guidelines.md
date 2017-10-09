---
title: "aaaAzure diretrizes de máquinas virtuais do Linux | Microsoft Docs"
description: "Saiba mais sobre Olá design e implementação diretrizes importantes para a implantação de máquinas virtuais Linux no Azure"
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 740767d7-9a40-407b-93e7-c29dd976ffd7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.openlocfilehash: 0f779f791005441b6b16e106a3dc5a095bb33034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-guidelines-for-linux"></a>Diretrizes de máquinas virtuais do Azure para Linux
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Este artigo enfoca a compreensão Olá necessárias etapas de planejamento para criar e gerenciar máquinas virtuais (VMs) em seu ambiente do Azure.

## <a name="implementation-guidelines-for-vms"></a>Diretrizes de implementação de VMs
Decisões:

* Quantas VMs são necessárias para suas várias camadas de aplicativos e componentes de sua infraestrutura?
* Quais recursos de CPU e memória cada VM precisa e quais são os requisitos de armazenamento Olá?

Tarefas:

* Defina as cargas de trabalho de saudação para seu aplicativo e hello Olá de recursos que VMs exigem.
* Alinhe Olá demandas de recursos para cada VM com o tipo de saudação apropriado VM armazenamento e tamanho.
* Defina os grupos de recursos para diferentes camadas de saudação e componentes de sua infraestrutura.
* Definir sua convenção de nomenclatura de VM.
* Crie suas VMs usando Olá CLI do Azure, web portal, ou com modelos do Gerenciador de recursos.

## <a name="virtual-machines"></a>Máquinas virtuais
Um dos principais recursos hello dentro de seu ambiente do Azure é provavelmente VMs. Esse recurso é o local em que você executa seus aplicativos bancos de dados, serviços de autenticação, etc.

É importante toounderstand Olá [diferentes tamanhos de VM](sizes.md) toocorrectly dimensionar seu ambiente de uma perspectiva de desempenho e custo. Se as VMs não tiverem núcleos de CPU ou memória suficiente, o desempenho do aplicativo será afetado, independentemente de como ele for projetado e desenvolvido. Saudação de revisão sugerido cargas de trabalho para cada série VM como um ponto de partida como decidir qual toouse VM de tamanho para cada componente em sua infraestrutura. Você pode [alterar o tamanho de saudação de uma VM](change-vm-size.md) após a implantação.

O armazenamento desempenha um papel fundamental no desempenho da VM. Você pode usar o armazenamento Standard que use discos giratórios regulares ou o armazenamento Premium para altas cargas de trabalho de E/S e o desempenho de pico que usam os discos SSD. Como com hello tamanho da VM, não há são custo médio de armazenamento considerações tooselecting hello. Você pode ler Olá [artigo de diretrizes de infraestrutura de armazenamento](infrastructure-storage-solutions-guidelines.md) toounderstand como toodesign apropriado armazenamento para desempenho ideal das suas máquinas virtuais.

## <a name="resource-groups"></a>Grupos de recursos
Componentes como VMs são agrupados logicamente para facilidade de gerenciamento e manutenção usando os [Grupos de Recursos do Azure](../../azure-resource-manager/resource-group-overview.md). Usando grupos de recursos, você pode criar, gerenciar e monitorar todos os recursos de saudação que compõem um determinado aplicativo. Você também pode implementar [controles de acesso baseado em função](../../active-directory/role-based-access-control-what-is.md) toogrant acesso tooothers dentro de seus recursos de saudação tooonly equipe precisam. Levar tempo tooplan seus grupos de recursos e as atribuições de função. Há diferentes abordagens tooactually projetar e implementar grupos de recursos, portanto, se tooread Olá [artigo de diretrizes de grupos de recursos](infrastructure-resource-groups-guidelines.md) toounderstand toobuild a melhor maneira de suas VMs.

## <a name="templates"></a>Modelos
Você pode criar modelos, definidos por arquivos JSON declarativos, toocreate suas VMs. Modelos normalmente também criar Olá necessário armazenamento, rede, interfaces de rede, endereçamento IP, etc., juntamente com as próprias VMs hello. Você pode usar modelos toocreate consistente e reproduzível ambientes de desenvolvimento e teste tooeasily de fins replicam os ambientes de produção e vice-versa. Você pode ler mais sobre [criando e usando modelos](../../azure-resource-manager/resource-group-overview.md#template-deployment) toounderstand como você pode usá-los para criar e implantar suas VMs.

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

