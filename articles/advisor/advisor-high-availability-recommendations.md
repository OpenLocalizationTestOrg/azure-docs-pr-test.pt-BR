---
title: "Recomendações de alta disponibilidade do Azure Advisor | Microsoft Docs"
description: "Use o Azure Advisor para melhorar a alta disponibilidade das implantações do Azure."
services: advisor
documentationcenter: NA
author: KumudD
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: e1cd7948e1969cd4ddb926e428c09b559190a805
ms.sourcegitcommit: ce934aca02072bdd2ec8d01dcbdca39134436359
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/08/2017
---
# <a name="advisor-high-availability-recommendations"></a>Recomendações de alta disponibilidade do Advisor

O Assistente do Azure ajuda a garantir e melhorar a continuidade de aplicativos críticos aos negócios. Você pode obter recomendações de alta disponibilidade do Advisor na guia **Alta Disponibilidade** do painel Advisor.

## <a name="ensure-virtual-machine-fault-tolerance"></a>Assegurar tolerância a falhas de máquina virtual

Para oferecer redundância para o seu aplicativo, recomendamos que agrupe uma ou mais máquinas virtuais em um conjunto de disponibilidade. O Advisor identifica máquinas virtuais que não fazem parte de um conjunto de disponibilidade e recomenda movê-las para um conjunto de disponibilidade. Essa configuração garante que durante um evento de manutenção planejada ou não planejada, pelo menos, uma máquina virtual esteja disponível e cumpra o SLA de máquina virtual do Azure. Você pode optar por criar um conjunto de disponibilidade para a máquina virtual ou adicionar a máquina virtual a um conjunto de disponibilidade existente.

> [!NOTE]
> Se você optar por criar um conjunto de disponibilidade, será preciso adicionar pelo menos mais uma máquina virtual nele. É recomendável agrupar duas ou mais máquinas virtuais em um conjunto de disponibilidade para garantir que pelo menos uma delas esteja disponível durante uma interrupção.

## <a name="ensure-availability-set-fault-tolerance"></a>Assegure que haja tolerância a falhas de conjunto de disponibilidade 

Para oferecer redundância para o seu aplicativo, recomendamos que agrupe uma ou mais máquinas virtuais em um conjunto de disponibilidade. O Assistente identifica os conjuntos de disponibilidade que contêm uma única máquina virtual e recomenda a adição de uma ou mais máquinas virtuais a ele. Essa configuração garante que durante um evento de manutenção planejada ou não planejada, pelo menos, uma máquina virtual esteja disponível e cumpra o SLA de máquina virtual do Azure. Você pode optar por criar uma máquina virtual ou então por adicionar uma máquina virtual existente ao conjunto de disponibilidade.  

## <a name="ensure-application-gateway-fault-tolerance"></a>Garantir tolerância a falhas de Gateway de Aplicativo
Para garantir a continuidade de negócios de aplicativos críticos que são ativados pelos Gateways de Aplicativo, o Assistente identifica as instâncias de Gateway de Aplicativo que não estão configuradas para tolerância a falhas e sugere ações de correção que você pode realizar. O Assistente identifica Gateways de Aplicativo de instância única médios ou grandes e recomenda adicionar pelo menos uma instância a mais. Ele também identifica Gateways de Aplicativo de instância única ou de várias instâncias pequenos e recomenda a migração para SKUs médios ou grandes. O Assistente recomenda essas ações para garantir que suas instâncias de Gateway de Aplicativo estejam configuradas para satisfazer os requisitos de SLA atuais para esses recursos.

## <a name="improve-the-performance-and-reliability-of-virtual-machine-disks"></a>Melhorar o desempenho e a confiabilidade dos discos da máquina virtual

O Assistente identifica máquinas virtuais com discos standard e recomenda a atualização para discos premium.
 
O Armazenamento Premium do Azure dá suporte de disco de alto desempenho e baixa latência para máquinas virtuais executando cargas de trabalho com uso intensivo de E/S. Os discos da máquina virtual que usam contas de Armazenamento Premium armazenam dados em SSDs (unidades de estado sólido). Para o melhor desempenho em seu aplicativo, recomendamos migrar qualquer disco de máquina virtual que exija IOPS alta para o Armazenamento Premium. 

Se os discos não exigirem IOPS alta, você poderá limitar os custos mantendo-o em Armazenamento Standard. O Armazenamento Standard armazena dados de disco da máquina virtual em HDDs (unidades de disco rígido) em vez de SSDs. Você pode optar por migrar seus discos de máquina virtual para discos premium. Os discos premium tem suporte com a maioria dos SKUs de máquina virtual. No entanto, em alguns casos, se você quiser usar discos premium, talvez também seja preciso atualizar o SKU da máquina virtual.

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a>Proteger seus dados de máquina virtual contra exclusão acidental
Configurar o backup da máquina virtual garante a disponibilidade de seus dados críticos de negócios e oferece proteção contra corrupção ou exclusão acidental.  O Assistente identifica as máquinas virtuais em que o backup não está habilitado e recomenda habilitar o backup. 

## <a name="how-to-access-high-availability-recommendations-in-advisor"></a>Como acessar as recomendações de alta disponibilidade no Advisor

1. Entre no [Portal do Azure](https://portal.azure.com) e, em seguida, abra o [Assistente](https://aka.ms/azureadvisordashboard).

2.  No painel do Assistente, clique na guia **Alta Disponibilidade**.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre as recomendações do Assistente, consulte:
* [Introdução ao Azure Advisor](advisor-overview.md)
* [Introdução ao Advisor](advisor-get-started.md)
* [Recomendações de custo do Advisor](advisor-performance-recommendations.md)
* [Recomendações de desempenho do Advisor](advisor-performance-recommendations.md)
* [Recomendações de segurança do Advisor](advisor-security-recommendations.md)

