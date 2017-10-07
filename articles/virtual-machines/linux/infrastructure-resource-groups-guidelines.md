---
title: grupos de aaaResource para VMs do Linux no Azure | Microsoft Docs
description: "Saiba mais sobre Olá design e implementação diretrizes importantes para a implantação de grupos de recursos nos serviços de infraestrutura do Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 93ab9d93-965a-46b9-9c87-a10d652a6422
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8809cb5eeb9a166d2bcf1946cd26b0ee748f8cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-group-guidelines-for-linux-vms"></a>Diretrizes do grupo de recursos do Azure para VMs Linux 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Este artigo se concentra em entender como toologically criar seu ambiente e todos os componentes de saudação em grupos de recursos de grupo.

## <a name="implementation-guidelines-for-resource-groups"></a>Diretrizes de implementação de Grupos de Recursos
Decisões:

* Você vai toobuild grupos de recursos por componentes básicos da infra-estrutura hello, ou pela implantação de aplicativo completo?
* Você precisa toorestrict acesso tooResource grupos usando os controles de acesso baseado em função?

Tarefas:

* Definir quais componentes principais da infraestrutura e Grupos de Recursos dedicados serão necessários.
* Examine como modelos de Gerenciador de recursos de tooimplement para implantações consistentes e reproduzíveis.
* Defina quais funções de acesso de usuário necessárias para controlar o acessam a grupos de tooResource.
* Crie conjunto de saudação de grupos de recursos usando a convenção de nomenclatura. Você pode usar o hello CLI do Azure ou no portal.

## <a name="resource-groups"></a>Grupos de recursos
No Azure, você logicamente agrupa recursos relacionados como contas de armazenamento, redes virtuais e máquinas virtuais (VMs) toodeploy, gerencia e mantê-las como uma única entidade. Essa abordagem torna mais fácil aplicativos de toodeploy enquanto manter Olá todos os recursos relacionados juntos de uma perspectiva de gerenciamento ou toogrant outros grupo toothat de acesso de recursos. Os nomes de grupo de recursos podem ter, no máximo, 90 caracteres. Para obter uma compreensão mais abrangente de grupos de recursos, você pode ler Olá [visão geral do Gerenciador de recursos do Azure](../../azure-resource-manager/resource-group-overview.md).

Um recurso importante é tooResource grupos Olá toobuild de capacidade de seu ambiente usando um arquivo JSON que declara hello, de rede de armazenamento, e os recursos de computação. Você também pode definir configurações tooapply e scripts personalizados relacionados. Usando esses modelos JSON, é possível criar implantações consistentes e reproduzíveis para seus aplicativos. Essa abordagem permite que você criar um ambiente de desenvolvimento e, em seguida, usar esse mesmo toocreate de modelo uma implantação de produção, ou vice-versa. Para melhor compreensão sobre como usar modelos, leia [Olá passo a passo do modelo](../../azure-resource-manager/resource-manager-template-walkthrough.md) que orienta você através de cada etapa da criação de um modelo JSON.

Há duas abordagens diferentes que você pode adotar ao projetar seu ambiente com Grupos de Recursos:

* Grupos de recursos para cada implantação de aplicativo que combina as contas de armazenamento hello, redes virtuais e sub-redes, máquinas virtuais, carregar balanceadores, etc.
* Grupos de Recursos centralizados que contêm suas redes virtuais e sub-redes principais ou contas de armazenamento. Os aplicativos estão, em seguida, em seus próprios Grupos de Recursos que contêm apenas VMs, balanceadores de carga, interfaces de rede, etc.

Como você expandir, criação de grupos de recursos centralizado para sua rede virtual e sub-redes torna mais fácil toobuild entre locais conexões de rede para opções de conectividade híbrida. abordagem alternativa Olá é para cada aplicativo toohave sua própria rede virtual que requer configuração e manutenção. [Controles de acesso baseado em função](../../active-directory/role-based-access-control-what-is.md) fornecer um acesso de toocontrol de forma granular tooResource grupos. Para aplicativos de produção, você pode controlar os usuários de saudação que podem acessar esses recursos ou para recursos de infraestrutura de núcleo hello, você pode limitar apenas toowork de engenheiros de infraestrutura com eles. Seus proprietários do aplicativo só têm acesso toohello componentes do aplicativo dentro de seu grupo de recursos e não core Olá infraestrutura do Azure do seu ambiente. Ao projetar seu ambiente, considere a possibilidade de usuários Olá que precisam acessar os recursos toohello e crie os grupos de recursos de maneira adequada. 

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

