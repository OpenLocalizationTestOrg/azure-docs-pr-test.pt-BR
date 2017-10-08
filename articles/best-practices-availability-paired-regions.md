---
title: "BCDR (continuidade dos negócios e recuperação de desastre): regiões emparelhadas do Azure | Microsoft Docs"
description: "Saiba mais sobre Azure tooensure regional de emparelhamento, os aplicativos são resilientes durante falhas de data centers."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: c2d0a21c-2564-4d42-991a-bc31723f61a4
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 68a3a33a8e768c72fa296d42c9ab97049232d169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="business-continuity-and-disaster-recovery-bcdr-azure-paired-regions"></a>Continuidade dos negócios e recuperação de desastres (BCDR): Regiões Emparelhadas do Azure

## <a name="what-are-paired-regions"></a>O que são regiões emparelhadas?

Azure opera em várias regiões geográficas em todo o mundo de saudação. Uma região geográfica do Azure é uma área definida do Olá, mundo que contém pelo menos uma região do Azure. Uma região do Azure é uma área dentro de uma região geográfica que contém um ou mais datacenters.

Cada região do Azure é emparelhado com outra região dentro de saudação mesmo geografia, juntos, tornando um par regional. exceção de saudação é Sul do Brasil, que é associado a uma região de fora da sua região.

![AzureGeography](./media/best-practices-availability-paired-regions/GeoRegionDataCenter.png)

Figura 1 – Diagrama do par da região do Azure

| painel Geografia do app&#39;s selecionado | Regiões emparelhadas |  |
|:--- |:--- |:--- |
| Ásia |Ásia Oriental |Sudeste Asiático |
| Austrália |Leste da Austrália |Sudeste da Austrália |
| Canadá |Canadá Central |Leste do Canadá |
| China |Norte da China |Leste da China|
| Índia |Índia Central |Sul da Índia |
| Japão |Leste do Japão |Oeste do Japão |
| Coreia |Coreia Central |Sul da Coreia |
| América do Norte |Centro-Norte dos EUA |Centro-Sul dos Estados Unidos |
| América do Norte |Leste dos EUA |Oeste dos EUA |
| América do Norte |Leste dos EUA 2 |Centro dos EUA |
| América do Norte |Oeste dos EUA 2 |Centro-Oeste dos EUA |
| Europa |Norte da Europa |Europa Ocidental |
| Japão |Leste do Japão |Oeste do Japão |
| Brasil |Sul do Brasil (1) |Centro-Sul dos Estados Unidos |
| Governo dos EUA |Gov do Iowa nos EUA |Gov. dos EUA – Virgínia |
| Governo dos EUA |Gov. dos EUA – Virgínia |Governo dos EUA do Texas |
| Governo dos EUA |Governo dos EUA do Texas |Governo dos EUA do Arizona |
| Governo dos EUA |Governo dos EUA do Arizona |Governo dos EUA do Texas |
| Reino Unido |Oeste do Reino Unido |Sul do Reino Unido |
| Alemanha |Alemanha Central |Nordeste da Alemanha |

Tabela 1 – mapeamento de pares regionais do Azure

> (1) O Sul do Brasil é exclusivo porque ele está associado a uma região fora de sua própria região geográfica. A região secundária do Sul do Brasil é o Centro-Sul dos EUA. No entanto, a região secundária do Centro-Sul dos EUA não é o Sul do Brasil.


Recomendamos replicar as cargas de trabalho entre pares regionais toobenefit de políticas de isolamento e a disponibilidade do Azure. Por exemplo, atualizações do sistema do Azure planejado são implantadas em sequência (não no hello simultaneamente) entre regiões emparelhadas. Isso significa que mesmo no caso ocorra uma saudação de uma atualização com falha, ambas as regiões não serão afetadas simultaneamente. Além disso, Olá improvável de uma interrupção amplo, recuperação de pelo menos uma região de cada par é priorizada.

## <a name="an-example-of-paired-regions"></a>Um exemplo de regiões emparelhadas
Figura 2 a seguir mostra um aplicativo hipotético que usa o par regionais Olá para recuperação de desastres. Olá verde números realce as atividades entre regiões de saudação de três serviços do Azure (Azure computação, armazenamento e de banco de dados) e como eles são configurados tooreplicate entre regiões. benefícios exclusivos de saudação de implantar em regiões emparelhadas são realçados por números Olá laranja.

![Visão geral dos benefícios das regiões emparelhadas](./media/best-practices-availability-paired-regions/PairedRegionsOverview2.png)

Figura 2 – par da região do Azure hipotético

## <a name="cross-region-activities"></a>Atividades entre regiões
Como tooin chamado Figura 2.

![PaaS](./media/best-practices-availability-paired-regions/1Green.png) **de computação do Azure (PaaS)** – você deve provisionar recursos de computação adicionais com antecedência tooensure recursos estão disponíveis em outra região durante um desastre. Para saber mais, confira as [Orientação técnica de resiliência do Azure](resiliency/resiliency-technical-guidance.md).

![Armazenamento](./media/best-practices-availability-paired-regions/2Green.png) **Armazenamento do Azure** – O GRS (armazenamento com redundância geográfica) é configurado por padrão quando uma conta de armazenamento do Azure é criada. Com o GRS, seus dados são replicados automaticamente três vezes dentro de região primária hello e três vezes na região emparelhada hello. Para saber mais, consulte [Opções de redundância do Armazenamento do Azure](storage/common/storage-redundancy.md).

![SQL Azure](./media/best-practices-availability-paired-regions/3Green.png) **bancos de dados do SQL Azure** – com o Azure SQL replicação geográfica padrão, você pode configurar a replicação assíncrona de região emparelhada de tooa de transações. Com a replicação geográfica do premium, você pode configurar região tooany de replicação Olá, mundo; No entanto, recomendamos que você implantar esses recursos em uma região emparelhada na maioria dos cenários de recuperação de desastres. Para saber mais, confira [Replicação geográfica no Banco de Dados SQL do Azure](sql-database/sql-database-geo-replication-overview.md).

![Resource Manager](./media/best-practices-availability-paired-regions/4Green.png) **Azure Resource Manager** – O Resource Manager fornece de maneira inerente isolamento lógico dos componentes do gerenciamento de serviço entre as regiões. Isso significa que falhas lógicas em uma região são menos provável tooimpact outro.

## <a name="benefits-of-paired-regions"></a>Benefícios de uma região emparelhada
Como tooin chamado Figura 2.  

![Isolamento](./media/best-practices-availability-paired-regions/5Orange.png)
**Isolamento físico** – Sempre que possível, o Azure prefere pelo menos 300 milhas de separação entre os datacenters em um par regional, embora isso não seja possível nem conveniente em todas as áreas geográficas. Separação de data center físico reduz a probabilidade de saudação de desastres naturais, tumultos civis, quedas de energia ou interrupções de rede física que afetam as duas regiões de uma vez. O isolamento é restrições de toohello assunto em geografia hello (tamanho de geografia, disponibilidade da infraestrutura de rede/power, regulamentos, etc.).  

![Replicação](./media/best-practices-availability-paired-regions/6Orange.png)
**replicação fornecida pela plataforma** -alguns serviços, como o armazenamento com redundância geográfica fornecer região emparelhada de toohello de replicação automática.

![Recuperação](./media/best-practices-availability-paired-regions/7Orange.png)
**ordem de recuperação de região** – no evento de saudação de uma interrupção amplo, recuperação de uma região é priorizada fora de cada par. Os aplicativos que são implantados em regiões emparelhadas têm a garantia toohave uma das regiões Olá recuperada com prioridade. Se um aplicativo é implantado em várias regiões que não são combinados, recuperação pode ser atrasada – Olá pior regiões escolhido caso Olá Olá a duas últimas toobe recuperado.

![Atualizações](./media/best-practices-availability-paired-regions/8Orange.png)
**atualizações sequenciais** – Azure planejado atualizações do sistema são distribuídas toopaired regiões sequencialmente (não no hello simultaneamente) toominimize de tempo de inatividade, efeito de saudação de bugs e falhas lógicas no evento raro Olá uma atualização inválida.

![Dados](./media/best-practices-availability-paired-regions/9Orange.png)
**residência dados** – uma região reside em Olá mesmo geography como seu par (com exceção de saudação do Sul do Brasil) nos requisitos de residência do pedido toomeet dados para fins de jurisdição de imposição de imposto e lei.
